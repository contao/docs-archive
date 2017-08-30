# Contao 4 Cookbook
This part of the cookbook contains several technical articles about the
Contao 4 ecosystem for administrators and developers. The topics are in no way
intended to be exhaustive. However, please feel free to add your own article to
help this become a valuable resource over time.


## Various topics

* Installation & Setup
    * [Cron job vs. periodic command scheduler](setup/cron-job.md)
    * Symlinks under Windows
    * Deployment / Asset Management / Backup


* Customization
    * Overwriting resources
    * [Handling custom routes](customization/custom-routes.md)    
    * [Modifying dca entries](customization/data-container.md)
    
        

## Bundle development tutorial

Contao 4 builds on Symfony. So if you are somewhat familiar with the Symfony 
ecosystem, you should have a look at the developer documentation on extending
Contao 4. And if you want to get more familiar with Symfony (which on a long
term you should do), check out their great and extensive documentation. 

→ [Extending Contao 4][ExtendingContao4]  
→ [Symfony Bundle Development][SymfonyBundleDev]


**What to expect**  

Hopefully lot's of practical code examples and guides that not only focus on
Contao but may also include things that are also valid for Symfony itself. 
This is an attempt for a more guided approach than the developer reference. 

### Let's go

1) [Overview and structure](bundle-dev/overview.md)
2) [Set up your local dev environment](bundle-dev/local-dev-environment.md)
3) Use new features
    * About semantic configuration
    * [About Services and Dependency Injection](bundle-dev/services-di.md)
    * Use Twig for templates
4) Add a Manager Plugin
5) [Publish your reusable bundle](bundle-dev/publish.md)


### Other references

* TODO



[ExtendingContao4]: ../../extending-contao4/README.md
[SymfonyBundleDev]: https://symfony.com/doc/current/bundles.html