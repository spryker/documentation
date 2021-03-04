This page describes the Microsoft Azure Active Directory and how to integrate it into a Spryker project.

## Partner Information

Microsoft Corporation is an American multinational technology company with headquarters in Redmond, Washington. It develops, manufactures, licenses supports, and sells computer software, consumer electronics, personal computers, and related services.

Azure Active Directory is Microsoft’s multi-tenant, cloud-based directory and identity management service. For an organization, Azure AD helps employees sign up to multiple services and access them anywhere over the cloud with a single set of login credentials.

## General information

The [SprykerEco.Oauth-Azure](https://github.com/spryker-eco/oauth-azure) enables OAuth 2.0 authentication via Microsoft Azure Active Directory.

## Integrating Azure Active Directory

Follow the steps below to integrate Azure Active Directory.

### Prerequisites

To start the feature integration:

1. Overview and install the necessary features:


| Name | Version | Integration guide |
| --- | --- | --- |
| Spryker Core Back Office | master | [Spryker Core Back Office feature integration](https://documentation.spryker.com/upcoming-release/docs/spryker-core-back-office-feature-integration) |


2. [Register an application with the Microsoft identity platform](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app).

### 1) Install the required modules using Composer

Run the following command(s) to install the required modules:
```bash
composer require spryker-eco/oauth-azure:"^1.0.0" --update-with-dependencies
```
:::(Warning) (Verification)
 

Ensure that the following modules have been installed:


| Module | Expected directory |
| --- | --- |
| OauthAzure | /vendor/spryker-eco/oauth-azure |


:::

### 2) Set up the configuration

Using the data from your Microsoft Azure Active Directory account, configure OAuth Azure credentials:

**config/Shared/config_default.php**
```php
$config[KernelConstants::DOMAIN_WHITELIST][] = 'https://login.microsoftonline.com/';	

// Oauth Azure	
$config[OauthAzureConstants::CLIENT_ID] = 'YOUR CLIENT ID';	
$config[OauthAzureConstants::CLIENT_SECRET] = 'YOUR CLIENT SECRET';	
$config[OauthAzureConstants::REDIRECT_URI] = sprintf(	
    'https://%s/security-oauth-user/login',	
    getenv('SPRYKER_BE_HOST')	
);	
$config[OauthAzureConstants::PATH_AUTHORIZE] = '/oauth2/v2.0/authorize';	
$config[OauthAzureConstants::PATH_TOKEN] = '/oauth2/v2.0/token';
```

### 3) Set up transfer objects

Generate transfer changes:
```bash
console transfer:generate
```

:::(Warning) (Verification)

Make sure that the following changes have been applied in the transfer objects:

| Transfer | Type | Event | Path |
| --- | --- | --- | --- |
| OauthAuthenticationLinkTransfer | class | created | src/Generated/Shared/Transfer/OauthAuthenticationLinkTransfer |
|ResourceOwnerTransfer| class| created| src/Generated/Shared/Transfer/ResourceOwner|
| ResourceOwnerRequestTransfer |class| created| src/Generated/Shared/Transfer/ResourceOwnerRequestTransfer|
| ResourceOwnerResponseTransfer |class| created| src/Generated/Shared/Transfer/ResourceOwnerResponseTransfer|
:::

### 4) Set up behavior

Activate the following plugins:

| Plugin | Specification | Prerequisites | Namespace |
| --- | --- | --- | --- |
| AzureOauthUserClientStrategyPlugin| Requests a resource owner using a specified option set. |None |SprykerEco\Zed\OauthAzure\Communication\Plugin\SecurityOauthUser|
| AzureAuthenticationLinkPlugin| Prepares an OAuth Azure authentication link. |None| SprykerEco\Zed\OauthAzure\Communication\Plugin\SecurityGui|

**src/Pyz/Zed/SecurityGui/SecurityGuiDependencyProvider.php**
```php
<?php

namespace Pyz\Zed\SecurityGui;
	
use Spryker\Zed\SecurityGui\SecurityGuiDependencyProvider as SprykerSecurityGuiDependencyProvider;
use SprykerEco\Zed\OauthAzure\Communication\Plugin\SecurityGui\AzureAuthenticationLinkPlugin;

class SecurityGuiDependencyProvider extends SprykerSecurityGuiDependencyProvider
{	
    /**	
     * @return \Spryker\Zed\SecurityGuiExtension\Dependency\Plugin\AuthenticationLinkPluginInterface[]	
     */	
    protected function SecurityGuiDependencyProvider(): array	
    {	
        return [	
            new AzureAuthenticationLinkPlugin(),	
        ];	
    }	
}
```
:::(Warning) (Verification)
Make sure you’ve activated `AzureAuthenticationLinkPlugin` by checking the **Login with Microsoft Azure** button on the Back Office login page.
:::

**src/Pyz/Zed/SecurityOauthUser/SecurityOauthUserDependencyProvider.php**

```php
<?php

namespace Pyz\Zed\SecurityOauthUser;
	
use Spryker\Zed\SecurityOauthUser\SecurityOauthUserDependencyProvider as SprykerSecurityOauthUserDependencyProvider;
use SprykerEco\Zed\OauthAzure\Communication\Plugin\SecurityOauthUser\AzureOauthUserClientStrategyPlugin;

class SecurityOauthUserDependencyProvider extends SprykerSecurityOauthUserDependencyProvider
{	
    /**	
     * @return \Spryker\Zed\SecurityOauthUserExtension\Dependency\Plugin\OauthUserClientStrategyPluginInterface[]	
     */	
    protected function getOauthUserClientStrategyPlugins(): array	
    {	
        return [	
            new AzureOauthUserClientStrategyPlugin(),	
        ];	
    }
}	
```

:::(Warning) (Verification)

Make sure you’ve activated `AzureOauthUserClientStrategyPlugin`:

1. On the Back Office login page, select **Login with Microsoft Azure**.

2. Check that you are redirected to the Microsoft Azure authentication page.

3. Check that, after authenticating with Microsoft Azure, you are redirected back and authenticated with the Back Office as a Microsoft Azure Active Directory user.
:::