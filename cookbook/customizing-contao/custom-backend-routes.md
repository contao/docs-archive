## Adding custom backend routes

You can use the Contao backend to display content generated in your own custom Controllers.
This way you can develop custom extensions without the need to use DCA configuration.
The following example can be changed according to your own setup. For example you're
not obliged to use the annotation configuration for your routes you could use
XML or YAML interchangeably.

### Create your Controller and Template

The first step is to create your own Controller. A more detailed explanation
on how Symfony Controller work can be found in the [Symfony documentation](https://symfony.com/doc/current/controller.html).
The Controller class is placed inside the `Controller` directory in your `AppBundle`
and is configured through annotations.

```php

<?php

// src/AppBundle/Controller/BackendController.php

declare(strict_types=1);

namespace AppBundle\Controller;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Template;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;

/**
 * @Route("/contao", defaults={
 *     "_scope" = "backend",
 *     "_token_check" = true,
 *     "_backend_module" = "my-modules"
 * })
 */
class BackendController extends AbstractController
{
    /**
     * @Route("/my-backend-route", name="app.backend-route")
     * @Template("AppBundle::my_backend_route.html.twig")
     */
    public function backendRouteAction()
    {
        return [];
    }
}

```

We need three different route parameters.

* `_scope`: This forces the scope of this route to be `backend`. That way you're
telling Contao, that this route belongs to the backend and should be handled accordingly.
* `_token_check`: If you're using Contao forms with the RequestToken integration
you need to set this to true, in order to get it to work.
* `_backend_module`: This attribute is not mandatory but will be used to match
the current route in order to highlight the currently active node in the backend menu.
More on this later.

Be sure to have imported your bundles Controllers in your `routing.yml` *before* 
the `ContaoCoreBundle` routes. 

```yaml
# app/config/routing.yml

app:
    resource: '@AppBundle/Controller/'
    type:     annotation
```

Our route `backendRouteAction` will render the template `AppBuundle::my_backend_route.html.twig`
which must be placed into `src/AppBundle/Resources/views`.

```twig
{% extends "@ContaoCore/Backend/be_page.html.twig" %}

{% block headline %}
    Not only the content of the `title`-tag but also the title of the content section.
{% endblock %}

{% block error %}
    Will be placed within the error block.
{% endblock %}

{% block main %}
    <div class="tl_listing_container">
        Main Content.
    </div>
{% endblock %}
```

As we extend from `@ContaoCore/Backend/be_page.html.twig` it is worth noting 
that there are three different block you can currently use:

* `headline`: This block renders the headline of the document.
* `error`: In case of an error, place your message here, it will be placed prominently
on the top of the page
* `main`: This is the content area for output.

This exampe renders like this:

![](images/custom-backend-routes.png)

### Extend the backend menu

Most of the time you probably want to add a menu entry for your backend module.
Since the backend menu can be extended with an `EventListener` we can easily
create one that listens for the menu event to be dispatched.

```php
<?php
// src/AppBundle/EventListener/BackendMenuListener.php

declare(strict_types=1);

namespace AppBundle\EventListener;

use Contao\CoreBundle\Event\MenuEvent;
use Symfony\Component\HttpFoundation\RequestStack;
use Symfony\Component\Routing\RouterInterface;

class BackendMenuListener
{
    protected $router;
    protected $requestStack;

    public function __construct(RouterInterface $router, RequestStack $requestStack)
    {
        $this->router = $router;
        $this->requestStack = $requestStack;
    }

    public function onBuild(MenuEvent $event): void
    {
        $factory = $event->getFactory();
        $tree = $event->getTree();

        $contentNode = $tree->getChild('content');

        $node = $factory->createItem(
            'my-modules',
            [
                'label' => 'My Modules',
                'attributes' => [
                    'title' => 'Title',
                    'href' => $this->router->generate('app.backend-route'),
                    'class' => 'my-modules'
                ],
            ]
        );

        $node->setCurrent($this->requestStack->getCurrentRequest()->get('_backend_module') === 'my-modules');

        $contentNode->addChild($node);
    }
}

```

This EventListener creates a new menu node and handles its own `currentState` by
reading and matching the previously mentioned request attribute `_backend_module`.

The only thing left to do is to register the EventListener in the service container.
For this to work, we add the following lines to our service configuration in `app/config/services.yml`.

```yaml
services:

    contao.listener.user_backend_menu_listener:
        class: AppBundle\EventListener\BackendMenuListener
        arguments:
            - "@router"
            - "@request_stack"
        tags:
            - { name: kernel.event_listener, event: contao.backend_menu_build, method: onBuild, priority: -255 }
```

We purposely assign it a low priority, so that we can be sure to be loaded after
the Contao Core EventListeners. Otherwise the `content` node we assign ourself to
will not be available yet.