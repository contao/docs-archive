# About services and dependency injection

Symfony comes with the powerful concept of *services* that live in a so called
*service container*. Have a look into the Symfony docs to get the idea behind
it:

 → [Service Container Introduction][SymfonyServiceContainer]  

Also make sure you are somewhat familiar with the idea of a dependency
injection (D.I.) container in general:

→ [Video explaining the basics of D.I. and Services (KnpUniversity)]
  [DependencyInjection101]   
→ [The DependencyInjection Component (Symfony docs)]
  [SymfonyDependencyInjection]


There are a lot of resources about the concept of services, and why and how to
make use of the concept. Here we only focus on some aspects that are special to
Contao. Feel free to read more in the Symfony docs - everything from best
practices to the endless options of configuring applies for your Contao bundle
as well. Beauty!  


## Hooks? Service! 
Developers familiar with Contao 3 most likely have seen something like this - 
registering a *hook*, a callback, e.g. to do some custom stuff on each page
generation: 

```php
// config.php

$GLOBALS['TL_HOOKS']['generatePage'][] = 
[
   'Maybe\Some\Namespace\SomeClass',
   'doSomething'
];
```

With Contao 4 this operation easily can become a service. The nice thing is:
You can directly replace the expression above with the service's id and the
method to call.

```php
$GLOBALS['TL_HOOKS']['generatePage'][] = 
[
   'my_service.something',
   'onPageGeneration'
];
``` 

This is how the respective service declaration in your bundle could look like:
 
```yml
services:
  my_service.something:
    class: 'Maybe\Some\Namespace\SomeClass'
```

> #### info:: Info
> This also works at other places with analogous callbacks. For example for
> contao's cron job array, when defining a custom action for your dca and so
> on …  



## Injecting the Symfony container / Contao framework
Symfony provides a convenient way to inject the *container* into your classes.
Contao follows this practice to allow injecting the Contao *framework*. See how
it's done in both cases.

By adding the following declaration to your bundle's service configuration you
can instruct Symfony to call a certain class function after initialization
if the class implements a certain interface (see ``_instanceof:``) - the method
to call must of course be part of the interface declaration:

```yml
services:
  _instanceof:
    Symfony\Component\DependencyInjection\ContainerAwareInterface:
      calls:
        - ["setContainer", ["@service_container"]]

    Contao\CoreBundle\Framework\FrameworkAwareInterface:
      calls:
        - ["setFramework", ["@contao.framework"]]
```

So in this case ``setContainer()`` gets called for all classes implementing the
``ContainerAwareInterface`` with the container being injected as a parameter.
Same goes for ``setFramework()`` with the ``FrameworkAwareInterface``.
  
To avoid duplicate code and make things even more convenient there exist two
respective traits that already contain all needed setter logic. So to use
the Symfony *container* in your class all you have to write is: 

```php
use Symfony\Component\DependencyInjection\ContainerAwareInterface;
use Symfony\Component\DependencyInjection\ContainerAwareTrait;

class MyClass implements ContainerAwareInterface
{
    use ContainerAwareTrait;
    
    // 'protected $container' now part of your class
    //  -> container (ContainerInterface) available via $this->container
}
```

Same goes for the Contao *framework* object (and of course you could use both
at the same time):

```php
use Contao\CoreBundle\Framework\FrameworkAwareInterface;
use Contao\CoreBundle\Framework\FrameworkAwareTrait;

class MyClass implements FrameworkAwareInterface
{
    use FrameworkAwareTrait;
    
    // 'private $framework' now part of your class
    //  -> framework (ContaoFrameworkInterface) available via $this->framework
}
```

Have a look at the implementation of the [ContainerAwareTrait]
[ContainerAwareTrait] and the [FrameworkAwareTrait][FrameworkAwareTrait] to 
fully understand how things are working (no magic involved).


[SymfonyServiceContainer]: https://symfony.com/doc/current/service_container.html
[SymfonyDependencyInjection]: https://symfony.com/doc/current/components/dependency_injection.html
[DependencyInjection101]: https://www.youtube.com/watch?v=DcNtg4_i-2w
[ContainerAwareTrait]: https://github.com/symfony/symfony/blob/v3.3.8/src/Symfony/Component/DependencyInjection/ContainerAwareTrait.php 
[FrameworkAwareTrait]: https://github.com/contao/core-bundle/blob/4.4.3/src/Framework/FrameworkAwareTrait.php