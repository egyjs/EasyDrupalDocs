---
title: Middleware in Drupal
---
# Middleware in Drupal

Routing is a fundamental concept in Drupal that maps incoming requests to the appropriate code that handles them. It defines the paths, URLs, and associated callback functions or controllers for different pages or actions in your Drupal site. Understanding routing is crucial for developing custom modules, creating new pages, and extending Drupal's functionality.

## Route Definitions

In Drupal, route definitions are stored in a routing YAML file within a module. The routing YAML file follows a specific naming convention: `<module_name>.routing.yml`. Here's an example of a simple route definition:

```yaml
mymodule.example_route:
  path: '/example'
  defaults:
    _controller: '\Drupal\mymodule\Controller\ExampleController::content'
    _title: 'Example Page'
  requirements:
    _permission: 'access content'
```

In this example:

- **mymodule.example_route** is the unique machine name for the route. It's important to use a unique name to avoid conflicts with other modules.
- **path** defines the URL path for the route. In this case, the route will match the `/example` path.
- **defaults** specify the default values for the route. The `_controller` key identifies the controller class and method responsible for generating the content. The `_title` key sets the title of the page.
- **requirements** define additional requirements for the route. In this case, the route requires the user to have the 'access content' permission.

## Route Parameters

Routes can include parameters that allow for dynamic and variable paths. Parameters are defined within curly braces `{}` in the route's path. Here's an example:

```yaml
mymodule.dynamic_route:
  path: '/example/{param}'
  defaults:
    _controller: '\Drupal\mymodule\Controller\ExampleController::content'
    _title: 'Dynamic Example Page'
  requirements:
    _permission: 'access content'
```

In this example, the `{param}` parameter is included in the route's path. When a request is made to a URL matching this route, the value of `{param}` will be passed as an argument to the controller method.

## Access Control

Access control for routes can be specified using permissions or custom access checks. By default, Drupal provides a set of core permissions that can be used to restrict access to routes. You can specify the required permission in the `requirements` section of the route definition. Additionally, custom access checks can be implemented by creating a class that implements the `AccessInterface` and defining it in the `requirements` section.

## Altering Existing Routes

Drupal allows you to alter existing routes provided by modules or Drupal core. This enables you to modify the behavior, permissions, or other attributes of routes without directly modifying the original module's code. Route alterations are implemented using hook system in Drupal. The `hook_route_alter()` hook allows modules to alter the definition of routes provided by other modules.

## Route Callbacks vs. Controllers

In Drupal, routes can be associated with either callback functions or controllers. Callback functions are standalone PHP functions that handle the logic for generating the content of a page. Controllers, on the other hand, are classes that follow the Controller pattern and contain methods responsible for generating the page content.

While both approaches can be used, it's generally recommended to use controllers for handling route callbacks in modern Drupal development. Controllers provide a structured and object-oriented approach, allowing for better code organization and separation of concerns.

## Conclusion

Routing is a fundamental part of Drupal's architecture, allowing you to map URLs to code that generates the content for different pages or actions. By defining routes, you can create custom pages, specify access control, and handle dynamic paths. Understanding routing is crucial for developing custom modules and extending Drupal's

 functionality to meet your specific requirements.
