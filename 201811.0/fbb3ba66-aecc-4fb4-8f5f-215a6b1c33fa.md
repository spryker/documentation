## Upgrading from Version 3.0.* Version to 4.0.0

In this new version of the **ShipmentDiscountConnector** module, we have added support of split delivery. You can find more details about the changes on the [ShipmentDiscountConnector module release page](https://github.com/spryker/shipment-discount-connector/releases).
    
@(Error)()(This release is a part of the **Split delivery** concept migration. When you upgrade this module version, you should also update all other installed modules in your project to use the same concept as well as to avoid inconsistent behavior. For more information, see [Split Delivery Migration Concept](https://documentation.spryker.com/v4/docs/split-delivery-concept).)
    
**To upgrade to the new version of the module, do the following:**

1. Upgrade the `ShipmentDiscountConnector` module to the new version:
    
```bash
composer require spryker/shipment-discount-connector: "^4.0.0" --update-with-dependencies
```
    
2. Generate the transfer objects:
    
```bash
console transfer:generate
```
    
*Estimated migration time: 5 min*

## Upgrading from Version 1.* to Version 3.0.0

@(Info)()(To dismantle the Horizontal Barrier and enable partial module updates on projects, a Technical Release took place. Public API of source and target major versions are equal. No migration efforts are required. Please [contact us](https://support.spryker.com/hc/en-us) if you have any questions.)

<!-- Last review date: Sep 18, 2019 by Denys Sokolov, Yuliia Boiko -->