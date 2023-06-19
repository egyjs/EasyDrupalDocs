---
title: Controllers in Drupal
---
# Controllers in Drupal

Controllers play a central role in handling and processing requests in Drupal. They are responsible for generating the content and managing the business logic for different pages and actions within your Drupal application. Understanding controllers is essential for developing custom modules and extending Drupal's functionality. This page will guide you through the concepts and best practices of working with controllers in Drupal.

## Introduction to Controllers

In Drupal, controllers are PHP classes that encapsulate the logic for generating the content of a page or handling a specific action. Controllers follow the Controller pattern, where each controller class represents a specific page or action in your application.

## Creating a Controller

To create a controller in Drupal, you need to define a class that extends the base controller class provided by Drupal. Here's an example of a simple controller class:

```php
namespace Drupal\my_module\Controller;

use Drupal\Core\Controller\ControllerBase;

class MyController extends ControllerBase {

  public function content() {
    // Generate and return the content for the page.
    return [
      '#markup' => $this->t('Hello, Drupal!'),
    ];
  }

}
```

In this example, the `MyController` class extends the `ControllerBase` class. The `content()` method generates and returns the content for the page. In this case, it simply displays the "Hello, Drupal!" message.

## Defining Routes for Controllers

To associate a controller with a specific URL or route, you need to define a route in your module's routing YAML file. Here's an example:

```yaml
my_module.route:
  path: '/my-route'
  defaults:
    _controller: '\Drupal\my_module\Controller\MyController::content'
    _title: 'My Page'
  requirements:
    _permission: 'access content'
```

In this example, the `my_module.route` route is associated with the `MyController` class and its `content()` method. The `_title` key sets the title of the page. The `_permission` key specifies the required permission to access the page.

## Dependency Injection in Controllers

Controllers in Drupal can leverage dependency injection to access various services and resources provided by the Drupal core or other modules. By type-hinting the required dependencies in the controller's constructor or methods, Drupal's dependency injection container will automatically provide the corresponding instances. Here's an example:

```php
namespace Drupal\my_module\Controller;

use Drupal\Core\Controller\ControllerBase;
use Drupal\Core\Database\Connection;
use Drupal\Core\Entity\EntityTypeManagerInterface;

class MyController extends ControllerBase {

  protected $database;
  protected $entityTypeManager;

  public function __construct(Connection $database, EntityTypeManagerInterface $entityTypeManager) {
    $this->database = $database;
    $this->entityTypeManager = $entityTypeManager;
  }

  public function content() {
    // Access the services and resources.
    // ...
  }

}
```

In this example, the `Connection` and `EntityTypeManagerInterface` services are injected into the controller's constructor. They can then be accessed within the controller's methods.

## Returning a Response

Controllers in Drupal typically return a render array or a response object that represents the generated content. Here's an example:

```php
public function content() {
  // Generate and return the content for the page.
  return [
    '#markup' => $this->t('Hello, Drupal!'),
  ];
}
```

In this example, the `content()` method returns a render array with a `#markup` key, which contains the "Hello, Drupal!" message.

## Conclusion

Controllers are an integral part of handling requests and generating content in Drupal. By creating controller classes, defining routes, and leveraging dependency injection, you can build custom pages and actions within your Drupal modules. Controllers

 provide a structured and object-oriented approach, allowing for better code organization and separation of concerns. Understanding and utilizing controllers will empower you to develop custom modules and extend Drupal's functionality to meet your specific requirements.