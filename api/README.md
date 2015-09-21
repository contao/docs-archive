# Contao API Reference

Contao development has started back in 2005. Over the years, a lot of features
were added to the framework.

> **Info** Be aware that this reference guide always describes the latest Contao version.
> The differences are described in the respective sections of the reference guide.

The Contao API (Application Programming Interface) Reference is split into different sections.

 1. #### [Data Configuration Array](dca/README.md)
    The DCA is one of the most important features in Contao. The backend CRUD functinality
    is described in a PHP array structure. The DCA is responsible for a unified look in
    the backend, and one of the first points where you can customize the system.

 2. #### [Extending Contao](extensions/README.md)
    This section describes how to add functionality like *content elements*,
    *frontend modules* or custom *form fields* to the system. Another important
     parts are *hooks*, Contao's own event system to extend core functionality.

 3. #### [Frontend Output](frontend/README.md)
    Detailed information how to inject custom code to the frontend output, without
    modifying the `fe_page` template.

 4. #### [Advanced Configuration](advanced/README.md)
    In-depth list of configuration options for the advanced framework users.

 5. #### [Constants](constants/README.md)
    Contao 3 uses a lot of PHP constants to represent state.

 6. #### [Functions and static methods](functions/README.md)
    Descriptions of the available functions and static methods.

 7. #### [Classes and Singletons](classes/README.md)
    A reference guide to the framework classes.



{% include "../LICENSE.md" %}


