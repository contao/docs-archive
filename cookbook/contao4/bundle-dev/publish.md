# Publish your bundle

Got your bundle working? Congratulations! Now it's time to publish it. This
short guide focuses on bundles that should be available publicly and should be
able to get installed directly via composer.

## Open up a git repository

A simple way to make your files accessible is to create a new repository on
[GitHub](https://github.com). If you are using git for version control, simply
define this repository as a remote and then ``git push`` your code up there. If
not, you should start to do so now. :-)

Consider the following things:
 * Add a ``LICENSE`` file to inform users under which license your code is
   published.
 * Add a ``README.md`` and give some short information how to 
   install/config/use your bundle.
 * Tag your code with a version like 0.1 / 1.0.0 and use
   [*semantic versioning*][SemanticVersioning].
   
  

## Submit your package on Packagist

To allow composer to find your package, go to [packagist.org][Packagist] and
submit it by specifying your git url. It's a good idea to install a *GitHub
Service Hook* so that your files get updated as soon you push something to your
repository. It's easy to do so - for more detail follow the steps listed in the 
[Packagist docs](https://packagist.org/about#how-to-update-packages). 

Now you should be able to install your package via composer:  
> composer require my-name/contao-something


## A word on Open Source

You already developed a *reusable* bundle. So it most likely could be
beneficial for other projects like other bundles could be for yours. Beside
these fair use ethics more people using your bundle also means more testers,
more ideas and therefore in the end probably a better product. Furthermore,
many companies let open source projects use their tools (IDE's, code analysis,
continuous integration, translation platforms and so on) for free. Together
with the concept of pull requests this can pay off quickly.   

And this is how Contao has grown! With Symfony and Composer we now have a good
component architecture to make the system getting more and more powerful and
feature-rich over time. So wouldn't it be awesome to have **your** piece of
software being part of the big puzzle? :-) 


[Packagist]: https://packagist.org/packages/submit
[SemanticVersioning]: http://semver.org/