## Install Feature API
### Prerequisites
To start feature integration, review and install the necessary features:
|Name|Version|
|---|---|
|Spryker Core|201903.0|
|Navigation|201903.0|
### 1) Install the Required Modules Using Composer

Run the following command to install the required modules:
```yaml
composer require spryker/navigations-rest-api:"^1.0.0" --update-with-dependencies
```

@(Info)(Verification)(Make sure that the following module is installed:)
|Module|Expected Directory|
|---|---|
|`NavigationsRestApi`|`vendor/spryker/navigations-rest-api`|
### 2) Set up Transfer Objects

Run the following commands to generate transfer changes:
```yaml
console transfer:generate
```
@(Info)(Verification)(Make sure that the following changes are present in the transfer objects:)
|Transfer|Type|Event|Path|
|---|---|---|---|
|`RestNavigationAttributesTransfer`|class|created|`src/Generated/Shared/Transfer/RestNavigationAttributesTransfer`|
|`RestNavigationNodeTransfer`|class|created|`src/Generated/Shared/Transfer/RestNavigationNodeTransfer`|
		
### 3) Set up Configuration
Configure mapping to specify source field from which resourceId field should be filled depends on navigation node type.
**`src/Pyz/Glue/GlueApplication/GlueApplicationDependencyProvider.php`**
```php
<?php
 
namespace Pyz\Glue\NavigationsRestApi;
 
use Spryker\Glue\NavigationsRestApi\NavigationsRestApiConfig as SprykerNavigationsRestApiConfigi;
 
class NavigationsRestApiConfig extends SprykerNavigationsRestApiConfig
{
    /**
     * @return array
     */
    public function getNavigationTypeToUrlResourceIdFieldMapping(): array
    {
        return [
            'category' =&gt; 'fkResourceCategorynode',
            'cms_page' =&gt; 'fkResourcePage',
        ];
    }
}
```
### 4) Set up Behavior

#### Enable Resources and Relationships
Activate the following plugin:
|Plugin|Specification|Prerequisites|Namespace|
|---|---|---|---|
|`NavigationsResourceRoutePlugin`|Registers the navigations resource.|None|`Spryker\Glue\NavigationsRestApi\Plugin\ResourceRoute`|
**`src/Pyz/Glue/GlueApplication/GlueApplicationDependencyProvider.php`**
```php
<;?php
 
namespace Pyz\Glue\GlueApplication;
 
use Spryker\Glue\CategoriesRestApi\Plugin\CategoriesResourceRoutePlugin;
use Spryker\Glue\CategoriesRestApi\Plugin\CategoryResourceRoutePlugin;
use Spryker\Glue\GlueApplication\GlueApplicationDependencyProvider as SprykerGlueApplicationDependencyProvider;
 
class GlueApplicationDependencyProvider extends SprykerGlueApplicationDependencyProvider
{
    /**
     * @return \Spryker\Glue\GlueApplicationExtension\Dependency\Plugin\ResourceRoutePluginInterface[]
     */
    protected function getResourceRoutePlugins(): array
    {
        return [
            new NavigationsResourceRoutePlugin(),
        ];
    }
}
```

@(Info)(Verification)(Make sure that the following endpoint is available:</br>http://example.org/navigations/`{navigationId}`)
 
**See also:**
[Navigation API](https://documentation.spryker.com/glue_rest_api/glue_api_storefront_guides/retrieving-navigation-trees-201903.htm)
 
 *Last review date: Mar. 14th, 2019* <!-- by Volodymyr Volkov  -->