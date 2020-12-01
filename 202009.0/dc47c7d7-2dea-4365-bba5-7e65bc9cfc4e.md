This endpoint allows authenticating as a company user.

## Authenticate as a company user

To authenticate as a company user, send the request:

***
`POST` **/company-user-access-tokens**
***

| Header key | Required | Description |
| --- | --- | --- |
| Authorization | v | An alphanumeric string that authorizes the customer to send requests to protected resources. Get it by [authenticating as a customer](https://documentation.spryker.com/authenticating-as-a-customer).  |

### Request

Request sample: 

`POST https://glue.mysprykershop.com/company-user-access-tokens`
```json
{
    "data": {
        "type": "company-user-access-tokens",
        "attributes": {
            "idCompanyUser": "5daf27b3-eddf-5b81-98cb-899f140f97e5"
        }
    }
}
```


| Attribute | Type | Description |
| --- | --- | --- |
| idCompanyUser | String | Unique identifier of a company user to authenticate as. To get it, [Retrieve available company users](https://documentation.spryker.com/docs/searching-by-company-users#retrieve-available-company-users).  |
    


### Response


<details>
    <summary>Response sample</summary>
    
```json
{
    "data": {
        "type": "company-user-access-tokens",
        "id": null,
        "attributes": {
            "tokenType": "Bearer",
            "expiresIn": 28800,
            "accessToken": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUz",
            "refreshToken": "def50200d7338763c798a0600f18e"
        },
        "links": {
            "self": "https://glue.mysprykershop.com/company-user-access-tokens"
        }
    }
}
```
    
</details>

| Attribute | Type | Description |
| --- | --- | --- |
| tokenType | String | Token type. The default value is `Bearer`. |
| accessToken | String | Authentication token used to send requests to the protected resources available for the company user. |
| expiresIn | Integer | The time in seconds in which the token expires. The default value is `28800`. |
| refreshToken | String | Token used to [refresh](https://documentation.spryker.com/docs/managing-company-user-authentication-tokens#refresh-a-company-user-authentication-token) the `accessToken`. |




## Possible errors

| Code | Reason |
| --- | --- |
| 401 | Failed to authenticate a user. This can happen due to the following reasons:<ul><li>The current authenticated customer cannot authenticate as the specified company user;</li><li>The specified Company User does not exist;</li><li>The authentication token provided in the request is incorrect.</li></ul> |
| 403 | The authentication token is missing in the request. |
| 422 | The Company User Id format is incorrect. |



 
##  Next steps

* [Manage company user authentication tokens](https://documentation.spryker.com/docs/managing-company-user-authentication-tokens)