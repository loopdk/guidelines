Code standards
==========

This document is a guideline for writing good standarized and readable code when working with a Drupal project.

These are *guidelines*, and if you think it's necessary to deviate feel free to do so, **but** please be sensible and only do this when necessary and make sure you don't break it for everyone else. And if you do, be sure to leave a comment with your reason so it won't stay inside your head only.

The guidelines should help achieve:

* A stable, secure and high quality foundation for building and maintaining websites
* Consistency across multiple developers participating in the project
* The best possible conditions for sharing modules between sites
* The best possible conditions for the individual website to customize configuration and appearance

**When working with a open source community project like Ding**
Contributions to the core project will be reviewed by members of the core team. These guidelines should inform contributors about what to expect in such a review. If a review comment cannot be traced back to one of these guidelines it indicates that the guidelines should be updated to ensure transparency.

### Be familiar with

* Drupal Coding Standards](https://drupal.org/coding-standards)
* and [PHP codesniffer](http://pear.php.net/manual/en/package.php.php-codesniffer.php)

Content
----------

1. [Coding Standards](#coding_standards)
2. [Naming](#naming)
3. [Code Structure](#code_structure)
4. [Updating core modules](#update_core)
5. [Altering existing modules](#altering_modules)

<a name="coding_standards"></a>
1. Coding Standards
----------

### PHP

Code must be compatible with PHP 5.3. Compatability can be checked using PHP_Codesniffer.

Code must conform to the [Drupal Coding Standards](https://drupal.org/coding-standards). In effect this means that the code must pass through an automated review by the [Coder module](https://drupal.org/project/coder) without any notices expect known false negatives. The review must include all severities and all reviews except upgrade7x.

Code must not generate notices without erroneous conditions when running in E_STRICT error mode .

### JavaScript

It is recommended that JavaScript code is checked by JSHint with options:

* debug
* forin
* qnull
* noarg
* noempty
* eqeqeq
* boss
* loopfunc
* evil
* laxbreak
* bitwise
* strict
* undef
* nonew
* browser
* jquery

If the web-version is used this equals to checking all warnings and assuming jQuery and Browser environment.

### CSS

See [CSS guidelines](css-guidelines.md)

### Documentation

**README:** All modules must contain a README.md file containing the following where applicable:

* A brief description of the module - preferably with a screenshot
* Configuration options
* Installation procedure
* Hidden variables
* Other requirements and how to obtain these such as API urls, versions, keys, library system and trimmings
* Any code which does not comply with these guidelines and a brief argument why

**LICENSE.txt:** All repositories must contain a LICENSE.txt file containing the license for project: GPL2.

<a name="naming"></a>
2. Naming
----------


### General

All names must be in English.

### Modules

All modules written specifically for *projectname* must be prefixed with *projectname* e.g. projectname_your_module. Use a sharthand name whe working on a project with a long name.

The prefix are not required for modules which provides functionality deemed relevant outside the *projectname* sphere e.g. generic modules that have relevance on other projects as well.

### Files

Files provide by modules must be placed in the following folders and have the extensions defined here.

* General
 * MODULENAME.info
 * MODULENAME.module
 * MODULENAME.install
 * includes/*.inc
 * templates/*.tpl.php
 * *.theme.inc
* CSS
 * CSS files must use the BAT (Base/Admin/Theme) naming schema as described here.
 * /css/*.(base|admin|theme).css
 * /sass/*.(base|admin|theme).scss
 * /sass/libs/*
* JavaScript
 * Files must include the module name to easily find their origin during debugging
 * /js/*.MODULENAME.js
* Images
 * Image resources must be placed in a folder named images and have the following extensions.
 * images/*.(png|jpeg|gif|svg)
* External resources (PHP and JavaScript libraries) must be included using [Libraries API](https://drupal.org/project/libraries)

### Module elements

Programmatic elements such as variables, content types, views and panel pages, defined in modules must comply to a set of common guidelines.

* Machine names should be prefixed with the name of the module that defines them.
* Administrative titles, human readable names and descriptions should contain the purpose.
* If a programmatic element supports tagging e.g. rules and views one of the tags must be the name of the module that defines them.
* As there is no finite set of programmatic elements for a site these apply to all types except if explicitly specified below.

**Guidelines for specific elements:**

* Panel variants (handlers) must not use auto generated names as this increases the risk of different modules implementing variants for the same pages overwriting each other. Instead use module_name_page_name_variant_name e.g. projectname_blog_node_view_blog NB: Auto generated names is the default behavior when using features!

### Repositories

Repositories should be named after the module/project contained within. The repository for the module projectname_event should be called projectname_event.


<a name="code_structure"></a>
3. Code Structure
----------

* Each module/project should be placed within its own repository. Each repository should only contain one module/project.
* If a module/project has dependencies these should be declared within a .make file included with the module so that they are downloaded automatically during a build. Dependencies can be projects on Drupal.org or external resources. It is recommended that dependencies specify a specific version.
* A module/project should provide all required code and resources for it to work on its own or through dependencies. This includes all configuration, theming, CSS, images and JavaScript libraries.
* All default configuration required for a module/project to function should be implemented in code. The preferred way of doing this is using the [Features module](https://drupal.org/project/features) or hooks provided by the module itself. Modules/projects where configuration cannot be handled using features should maintain configuration using hook_install() and hook_update_N().
* If a module/project require configuration for which there is no sensible default the module must implement hook_install_tasks() so users can perform the necessary configuration during installation.
* All default text content in modules must be in English. Localization of content must be handled using the Drupal translation modules.


<a name="update_core"></a>
4. Updating project core modules
----------

* If a project core module is expanded with updates to current functionality the default behavior must be the same as previous versions or as close to this as possible. This also includes new modules which replaces current modules.
* If an update does not provide a way to reuse existing content and/or configuration then the decision on whether to include the change resides with the Project owner.

<a name="altering_modules"></a>
5. Altering existing modules
----------

* Modules which alter or extend functionality provided by the project core modules should use appropriate alter hooks to override these instead of forking these modules.
* In cases where modules provide layered configuration, modules should implement new layers with a higher priority than default configuration. This instead of altering the default configuration. This is often handled through lower weights. To support multiple modules providing separate layers of configuration without conflicts identifiers must be unique to the module as opposed to auto-generated. This may require altering auto-generated code manually. The recommended way to generate unique identifiers would be to prefix the existing identifier with the module name. Example: Panel variants.
* It is preferable to add a new layer to layered configuration instead of altering an existing layer provided by the core modules. This ensures that alterations and extensions work as expected even when the core modules are updated. This means that sites which use alterations may not reflect the latest changes to core. It is deemed preferable instead of potentially breaking the site.


