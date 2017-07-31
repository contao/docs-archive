> TODO: rewrite

# Publish your bundle

Got your bundle working? Now it's time to publish it. This short guide focuses on bundles that should be available
publicly and should be able to get installed directly via composer.

## Open up a git repository

A simple way to make your files accessible is to create a new repository on [GitHub](https://github.com). If you are
using git for version control, simply define this repository as a remote and then ``git push`` your code up there. If
not, you should start to do so now. :-)

Consider the following things:
 * Add a ``LICENSE`` file to inform users under which license your code is published.
 * Add a ``README.md`` and give some short information how to install/config/use your bundle.
 * Tag your code with a version like 0.1 / 1.0.0.
   
  

## Submit your package on Packagist

To allow composer to find your package, go to [packagist.org](https://packagist.org/packages/submit) and submit it by
specifying your git url. It's a good idea to install a *GitHub Service Hook* so that your files get updated as soon you 
push something to your repository. It's easy to do so - for more detail follow the steps listed in the 
[Packagist docs](https://packagist.org/about#how-to-update-packages).  

Now you should be able to install your package via composer:  
``composer require my-name/contao-something``


