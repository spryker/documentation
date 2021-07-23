This document describes how to integrate the Cart Glue API feature into a Spryker project.

## Install feature core

Follow the steps below to install the Cart Glue API feature core.

### Prerequisites

To start feature integration, integrate the required features:

| NAME | VERSION | INTEGRATION GUIDE |
|-|-|-|
| Spryker Core | 202009.0 | [Spryker Core feature integration](https://documentation.spryker.com/docs/spryker-core-feature-integration)| Spryker  |
| Cart | 202009.0 | [Cart feature integration](https://documentation.spryker.com/docs/cart-feature-integration) |

### 1) Install the required modules using Composer

Install the required modules:

```bash
composer require spryker/carts-rest-api:"^5.14.0" --update-with-dependencies
```
Ensure the following modules have been installed:

| MODULE | EXPECTED DIRECTORY |
|-|-|
| CartsRestApi | vendor/spryker/carts-rest-api |

### 2) Set up behavior

Set up the following behaviors.

#### Enable product-concrete resource expanding plugin

Activate the following plugin:

| PLUGIN | SPECIFICATION | PREREQUISITES | NAMESPACE |
|-|-|-|-|
| CustomerCartsResourceRoutePlugin | Configuration for resource routing, how HTTP methods map to controller actions, and if actions are protected. |   | 	
Spryker\Glue\CartsRestApi\Plugin\ResourceRoute\CustomerCartsResourceRoutePlugin |

**src/Pyz/Glue/GlueApplication/GlueApplicationDependencyProvider.php**

```php
<?php

namespace Pyz\Glue\GlueApplication;

use Spryker\Glue\CartsRestApi\Plugin\ResourceRoute\CustomerCartsResourceRoutePlugin;
use Spryker\Glue\GlueApplication\GlueApplicationDependencyProvider as SprykerGlueApplicationDependencyProvider;

class GlueApplicationDependencyProvider extends SprykerGlueApplicationDependencyProvider
{
    /**
     * {@inheritDoc}
     *
     * @return \Spryker\Glue\GlueApplicationExtension\Dependency\Plugin\ResourceRoutePluginInterface[]
     */
    protected function getResourceRoutePlugins(): array
    {
        return [
            new CustomerCartsResourceRoutePlugin()
        ]
    }
}
```

:::(Warning) (Verification)
Make sure that the `https://glue.mysprykershop.com/customers/{{customerId}}/carts` endpoint is available.
:::