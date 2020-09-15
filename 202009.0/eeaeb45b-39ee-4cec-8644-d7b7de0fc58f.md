## Install Feature Core

### Prerequisites
To start feature integration, overview and install the necessary features:

| Feature | Version |
| --- | --- |
| Configurable Bundle | master |
| Order Management | master |
| Spryker Core | master |

### 1) Set up Behaviour

| Plugin | Specification | Prerequisites | Namespace |
| --- | --- | --- | --- |
| `ConfiguredBundleOrderItemExpanderPlugin` | Expands order items with sales order configured bundles. | None | `Spryker\Zed\SalesConfigurableBundle\Communication\Plugin\Sales` |

**src/Pyz/Zed/Sales/SalesDependencyProvider.php**
```php
<?php

namespace Pyz\Zed\Sales;

use Spryker\Zed\SalesConfigurableBundle\Communication\Plugin\Sales\ConfiguredBundleOrderItemExpanderPlugin;
use Spryker\Zed\Sales\SalesDependencyProvider as SprykerSalesDependencyProvider;

class SalesDependencyProvider extends SprykerSalesDependencyProvider
{
    /**
     * @return \Spryker\Zed\SalesExtension\Dependency\Plugin\OrderItemExpanderPluginInterface[]
     */
    protected function getOrderItemExpanderPlugins(): array
    {
        return [
            new ConfiguredBundleOrderItemExpanderPlugin(),
        ];
    }
}
```
:::(Warning) (Verification)
Make sure that every order item from `SalesFacade::getOrderItems()` results, contains sales order configured bundles data if the order contains configurable bundle.
:::

