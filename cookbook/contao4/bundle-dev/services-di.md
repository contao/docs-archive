# About services and dependency injection

// TODO

* short introduction
* writing a service vs. hooks



## Injecting the symfony container / contao framework
There is a convenient way to inject the symfony container and contao framework into your classes. By adding the
following declaration to your bundle's service configuration you can instruct symfony to call a certain class function
after initialization whenever the class implements a certain interface.

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

In this case ``setContainer()`` gets called for all classes implementing the ``ContainerAwareInterface`` with the
container being injected as a parameter. Same goes for ``setFramework()`` with the ``FrameworkAwareInterface``.
  
To avoid duplicate code and make things even more convenient there exist two respective traits that already contain the
setter being called. So to use the symfony container in your class all you have to write is: 

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

Same goes for the framework object (of course you can use both at once):
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

Have a look at the implementation of the traits
([ContainerAwareTrait](https://github.com/symfony/symfony/blob/master/src/Symfony/Component/DependencyInjection/ContainerAwareTrait.php), 
[FrameworkAwareTrait](https://github.com/contao/core-bundle/blob/master/src/Framework/FrameworkAwareTrait.php))
to fully understand how its working (no magic involved).


## ...