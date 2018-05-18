# Magento Architecture and Customization Techniques

----------------------------------------------------
## 1.1 Describe Magento’s module-based architecture
Describe module limitations.

#### How do different modules interact with each other? 
* Sequences in module.xml file
* "Service contracts" - APi and Data API
* Dependency injections in di.xml (preferences and plugins)
* Layouts - one extension can extend and other via layout
* Require JS - overrides and mixins

#### What side effects can come from this interaction?
* If modules use Dependency injection, they can load in the wrong order or try to redefine the already redefined functionality of the module. To solve this problem, you should use sequence in module.xml.
* If the modules use other modules’ logic and the module, whose logic is used, is disabled, dependencies will not be used and an error will occur when executing the code.
* Modules circular dependency - in `sequence` section

#### References:
* [Service Contracts](https://devdocs.magento.com/guides/v2.2/extension-dev-guide/service-contracts/service-contracts.html)
* [Api Concepts](https://devdocs.magento.com/guides/v2.2/extension-dev-guide/api-concepts.html)
* [Design Patterns](https://devdocs.magento.com/guides/v2.2/extension-dev-guide/service-contracts/design-patterns.html)
* [Event and Observers](https://devdocs.magento.com/guides/v2.2/extension-dev-guide/events-and-observers.html)
* [Module dependencies](https://devdocs.magento.com/guides/v2.2/architecture/archi_perspectives/components/modules/mod_depend.html)
----------------------------------------------------
## 1.2 Describe Magento’s directory structure
Determine how to locate different types of files in Magento.

#### Where are the files containing JavaScript, HTML, and PHP located?
#####Story:
    * {area} - |base|adminhtml|frontend|
    * {vendor} - |ISM|Amasty| and others
    * {module-name} - |Magento_Catalog|ISM_BugFixes| and others
    * {theme-name} - |luma|melano| and others
 

* JavaScript:
    * [Module] - app/code/{vendor}/{module-name}/view/{area}/web/js/
    * [Theme] - design/{area}/{vendor}/{theme-name}/{module-name}/web/js/
* HTML:
    * [Module] - app/code/{vendor}/{module-name}/view/{area}/web/template/
    * [Theme] - design/{area}/{vendor}/{theme-name}/{module-name}/web/template/
* PHP:
    * vendor
    * app/code
    * lib
* PHTML:
    * [Module] - app/code/{vendor}/{module-name}/view/{area}/templates
    * [Theme] - design/{area}/{vendor}/{theme-name}/{module-name}/templates/    
    
#### How do you find the files responsible for certain functionality?
Based on module example.
* API - the module’s interfaces for models and classes.
* BLOCK - PHP files utilized for information processing for viewing needs.
* CONSOLE - PHP files that are responsible for console programs execution.
* CONTROLLER - controller files that process requests sent to the server.
* CRON - tore the files, which are later executed on the Cron launching.
* CUSTOMERDATA - PHP files responsible for processing information for sections.  (private content)
* ETC - the main configuration files of the module.
    - frontend - frontend scope
    - adminhtml - adminhtml scope
    - webapi_rest - REST API scope
    - webapi_soap - SOAP API scope
* HELPER - PHP helper files that include some aggregated functionality, which can be utilized in different module’s parts.
* i18n - translations.
* MODEL - files that work with the database tables and contains business logic of data processing.
* OBSERVER - PHP files responsible for executing commands from the listener.
* PLUGIN - contains plugins.
* SETUP - installation and upgrade scripts of your extension, scripts interacting with the database.
* TEST - unit tests.
* UI - UI components. This UI directory contains files for data generation, which later receive, process and show the components on a display.
* VIEW - In this directory you can find all the visual files: .js, .css, .html, .phtml, .xml, or, simply, all the files we see on the frontend. The files are divided into three categories relying on the area of the operation.   

----------------------------------------------------
## 1.3 Utilize configuration XML and variables scope
#### Which configuration files correspond to different features and functionality?
- acl.xml - resource access configurations
- catalog_attributes.xml - declare attributes to be loaded in collection for specific entities
- config.xml - default Adminhtml config settings
- crontab.xml - cron settings
- di.xml - Dependency Injections declaration
- eav_attributes.xml - properties for EAV attributes (need to be checked)
- events.xml - observer events configuration
- extension_attributes.xml - declaring extension configurations
- indexer.xml - indexes configuration
- module.xml - module declaration
- mview.xml - mView settings (partial reindex, see framework/Mview)
- product_options.xml - product options configurations
- product_types.xml - product types configurations
- view.xml - view configuration (theme view setting. See thene/etc/view.xml)
- webapi.xml - API configuration settings
- widget.xml - widget settings
- frontend
    - sections.xml - private data sections invalidation settings
    - routes.xml - routing settings (router, frontname)
    - page_types.xml - provide page types (for widgets injections)
- adminhtml
    - menu.xml - configurations for adminhtml menu
    - routes.xml - adminhtml routing
    - system.xml - configurations for Stores -> Config
    
#### References
[Config PHP](https://devdocs.magento.com/guides/v2.2/config-guide/config/config-php.html)
[Config Files](https://devdocs.magento.com/guides/v2.2/config-guide/config/config-files.html)
[Create your own config type](https://devdocs.magento.com/guides/v2.2/config-guide/config/config-create.htm)