:::(Error) (Prerequisites)
This migration guide is a part of the [Search migration effort](https://documentation.spryker.com/v4/docs/search-migration-concept). Prior to upgarding this module, make sure you have completed all the steps from the [Search Migration Guide](https://documentation.spryker.com/v4/docs/migration-guide-search). 
:::
To upgrade the module, do the following:
1. Update the module with composer:
```Bash
composer update spryker/cms-page-search
```
2. Remove all deprecated query expander plugins coming from the Search module (if any) from `Pyz\Client\CmsPageSearch\CmsPageSearchDependencyProvider`:
```PHP
Spryker\Client\Search\Plugin\Elasticsearch\QueryExpander\IsActiveInDateRangeQueryExpanderPlugin
Spryker\Client\Search\Plugin\Elasticsearch\QueryExpander\IsActiveQueryExpanderPlugin
Spryker\Client\Search\Plugin\Elasticsearch\QueryExpander\LocalizedQueryExpanderPlugin
Spryker\Client\Search\Plugin\Elasticsearch\QueryExpander\StoreQueryExpanderPlugin
```
3. Enable the replacement plugins:

<details open>
<summary>Pyz\Client\CmsPageSearch</summary>
   
```PHP
<?php

namespace Pyz\Client\CmsPageSearch;

...
use Spryker\Client\CmsPageSearch\CmsPageSearchDependencyProvider as SprykerCmsPageSearchDependencyProvider;
use Spryker\Client\SearchElasticsearch\Plugin\QueryExpander\IsActiveInDateRangeQueryExpanderPlugin;
use Spryker\Client\SearchElasticsearch\Plugin\QueryExpander\IsActiveQueryExpanderPlugin;
use Spryker\Client\SearchElasticsearch\Plugin\QueryExpander\LocalizedQueryExpanderPlugin;
use Spryker\Client\SearchElasticsearch\Plugin\QueryExpander\StoreQueryExpanderPlugin;

class CmsPageSearchDependencyProvider extends SprykerCmsPageSearchDependencyProvider
{
    ...
    
    /**
     * @return \Spryker\Client\SearchExtension\Dependency\Plugin\QueryExpanderPluginInterface[]
     */
    protected function createCmsPageSearchQueryExpanderPlugins(): array
    {
        return [
            ...
            new StoreQueryExpanderPlugin(),
            new LocalizedQueryExpanderPlugin(),
            new IsActiveQueryExpanderPlugin(),
            new IsActiveInDateRangeQueryExpanderPlugin(),
        ];
    }

    /**
     * @return \Spryker\Client\SearchExtension\Dependency\Plugin\QueryExpanderPluginInterface[]
     */
    protected function createCmsPageSearchCountQueryExpanderPlugins(): array
    {
        return [
            new StoreQueryExpanderPlugin(),
            new LocalizedQueryExpanderPlugin(),
            new IsActiveQueryExpanderPlugin(),
            new IsActiveInDateRangeQueryExpanderPlugin(),
        ];
    }
}  
```
 <br>
</details>


4. Remove the deprecated plugin usages listed below from `Pyz\Zed\Search\SearchDependencyProvider`:
```PHP
Spryker\Zed\CmsPageSearch\Communication\Plugin\Search\CmsDataPageMapBuilder
```

