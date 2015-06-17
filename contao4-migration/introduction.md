# Introduction

As a Contao 3 developer you are used to the fact that Contao provides its own
components for the whole application. It has been a standalone application
providing all the dependencies it needed ever since.

This was due to the fact that sharing PHP libraries was not easy in the early
days of Contao (or TypoLight back then). But a lot has changed since then. PHP
itself has become a lot more mature in terms of the programming language itself
but particularly in terms of the whole ecosystem:

* The [PHP FIG](http://www.php-fig.org/) has been formed, trying to enable
interoperability between different PHP projects and libraries.
* The package manager [Composer](https://getcomposer.org/) has become the
de-facto standard to define and load dependencies based on the standards the
PHP FIG has defined (see PSR-0 and PSR-4).
* Continuous Integration has become easier thanks to Open Source-friendly
services such as [Travis CI](https://travis-ci.org/),
[Scruitinizer](https://scrutinizer-ci.com/) and many more!
* etc.

Thanks to the PHP and the whole Open Source community we have a lot of
excellent tools and libraries available that we can reuse in our projects which
allows us to invest more time in creating new, awesome software instead of
doing the same work others already did again.

One of the basic concepts of Contao 4 is to take advantage of these libraries.
We stop reinventing the wheel over and over again - right now! That's why we
have decided to reuse the awesome components of
[Symfony 2](http://symfony.com/). In fact, we not only use the components but
rather use the whole full stack framework it provides and thus, Contao
**is a Symfony 2 Bundle** now!

Composer loads all the Symfony components and their respective dependencies
when we install Symfony and the Contao Core Bundle.

So the best thing you can do when you want to understand how Contao 4+ works,
is to understand how a Symfony application works. The
[Symfony documentation](http://symfony.com/doc/current/index.html) is excellent
and will give you a lot more insight of why it is awesome and probably also
give you an idea of why we chose it as our new foundation for Contao.
Did you notice that we just reused something that is not PHP code? Knowing
Symfony means understanding a big part of Contao 4+ which in turn means we can
also reuse their documentation and the rest of the ecosystem such as training
lessons, e-learning courses etc. This automatically spreads the efforts on many
shoulders which is a great thing for any project!

So before you start reading how to make your Contao 3 extensions compatible to
Contao 4+ and thus actually building Symfony bundles, you probably somehow have
to change your mindset a bit.
Stop thinking about developing for Contao but rather start thinking about
building for the PHP community! As we now use Composer there is a whole new
world of PHP code you can reuse in your bundles
(note: we now call them bundles!) and you are probably about to build libraries
that could be interesting for anybody. Split your code into a library that can
be reused by anybody and write an additional bundle providing glue code that
integrates your library into Symfony and/or Contao!
