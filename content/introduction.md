# Zops Saas API
Version: 0.0.1

## Table of Contents

* [LoginResource](#loginresource)

* [User Logout and Invalidate All Tokens](#user-logout-and-invalidate-all-tokens)

* [Forgot Password Resource](#forgot-password-resource)

* [Reset Password Resource](#reset-password-resource)

* [Account Get & Update & Delete](#account-get--update--delete)

* [Account Create](#account-create)

* [Account Update with Approve Code](#account-update-with-approve-code)

* [Approve Code Resend](#approve-code-resend)

* [Admin User Create & List](#admin-user-create--list)

* [Admin Retrieve & Update & Delete](#admin-retrieve--update--delete)

* [Billing User Create & List](#billing-user-create--list)

* [Billing User Retrieve & Update & Delete](#billing-user-retrieve--update--delete)

* [Developer User Create & List](#developer-user-create--list)

* [Developer User Retrieve & Update & Delete](#developer-user-retrieve--update--delete)

* [Get User Information](#get-user-information)

* [Project Create & List](#project-create--list)

* [Project Retrieve & Update](#project-retrieve--update)

* [Google Server API Key, Google Project Number, Apns IOS Push Certification Retrieve & Update](#google-server-api-key-google-project-number-apns-ios-push-certification-retrieve--update)

* [Service Catalog Create and List](#service-catalog-create-and-list)

* [Service Create](#service-create)

* [Service Delete](#service-delete)

* [Consumer Create & List](#consumer-create--list)

* [Project Consumer Delete](#project-consumer-delete)

* [Project Consumer Create](#project-consumer-create)

* [Consumer Token Create](#consumer-token-create)

* [Consumer Token Delete](#consumer-token-delete)


## LoginResource

* __path:__ /api/v1/session
* __methods:__ ['POST', 'OPTIONS']
* __type:__ list

Login Resource.

#### Code Example:

### POST
Login System with Email and Password.
Return User_Id, Role and Token(Token used until logout )

#### Request

    ```bash
        #bash
        curl \
             --request POST                             \
             --header "Content-Type: application/json"  \
             --body "{                                                             \
                     "email": "zops_test_eneoooeeN@example.com",               \
                     "password": "123"                                         \
             }"                                                                    \
             https://api_baseurl/api/v1/session
    ```

    ```python
        #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json"
                  }

        body = {
                "email": "zops_test_eneoooeeN@example.com",
                "password": "123",
                }

        req = requests.post("https://api_baseurl/api/v1/session",
                                        header=header, data=json.dumps(body))
    ```
    #### Response:
    ```json
        {
        "meta": {
                "params": {
                            "indent": 0
                            }
                },
        "content": {
                    "token": "asdljfsl394whefsudfo9sdfysdf"
                    }
        }
    ```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| token | string | False |  True |  Access token. |  None | None |
| email | string | True |  False |  Email for user.Max length 70 Character |  None | None |
| password | string | True |  False |  Password for user.Max length 128 Character |  None | None |




## User Logout and Invalidate All Tokens

* __path:__ /api/v1/session/logout
* __methods:__ ['DELETE', 'OPTIONS']
* __type:__ object

Logout resource.
User logout and used token invalidated.(token is disposable)
If "others" parameters is true then users all token deleted except that used this request

#### Code Example:

#### DELETE
Logout User Account and Invalidate user token.
#### Request:

    ```bash
        #bash
        curl \
             --request DELETE                                                        \
             --header "Content-Type: application/json"                               \
             --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"   \
             https://api_baseurl/api/v1/session/logout
    ```

    ```python
        #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
                  }
        req = requests.GET("https://api_baseurl/api/v1/session/logout,
                                        header=header)
    ```
    ##### Response:
    202 OK.
    ```json
        {
          "meta": {
            "params": {
              "indent": 0
            }
          },
          "content": null
        }
    ```
#### DELETE
If "others" parameters is true then users all token deleted except that used this request
#### Request:

    ```bash
        #bash
        curl \
             --request DELETE                                                       \
             --header "Content-Type: application/json"                              \
             --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"  \
             https://api_baseurl/api/v1/session/logout?others=True
    ```

    ```python
        #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
                  }
        req = requests.GET("https://api_baseurl/api/v1/session/logout?others=True,
                                        header=header)
    ```
    ##### Response:
    202 OK.
    ```json
        {
          "meta": {
            "params": {
              "indent": 0
            }
          },
          "content": null
        }
    ```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |
| others | bool | False |  False |  This parameter is user delete token parameter. If it is true users all token deleted |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| token | string | False |  True |  Access token |  None | None |




## Forgot Password Resource

* __path:__ /api/v1/forgot-password
* __methods:__ ['POST', 'OPTIONS']
* __type:__ list

Forgot Password Resource

### Code Examples:

    #### POST:
    Send reset password email. We send to reset link your email address. You can reset your password using these
    link in 5 hours
    #### Request:

    ```bash
        #bash
        curl \
             --request POST                                                             \
             --header "Content-Type: application/json"                                  \
             --header "AUTHORIZATION: eyJ0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"   \
             --body "{                                                              \
                     "email": "zops_test_eneoooeeN@example.com",                \
             }"                                                                     \
             https://api_baseurl/api/v1/forgot-password
    ```

    ```python
        #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
                  }

        body = {
                "email": "zops_test_eneoooeeN@example.com"
                }

        req = requests.post("https://api_baseurl/api/v1/forgot-password",
                                        header=header, data=json.dumps(body))
    ```

    #### Response:
    201 Accepted:
    ```json
        {
        "meta": {
                "params": {
                            "indent": 0
                            }
                },
        }
    ```
    #### Possible Errors
    - __Not Found__
    - __Unauthorized__
    - __Failed Dependency__ :An Error occur on 3rd part service. Please retry after a few minutes.

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| email | string | True |  False |  Email for user.Max length 70 Character |  None | None |




## Reset Password Resource

* __path:__ /api/v1/reset-password
* __methods:__ ['PUT', 'OPTIONS']
* __type:__ object

Reset Password Resource

### Code Examples:

    #### PUT:
    Reset Password with reset_token and new password
    #### Request:
    ```bash
        #bash
        curl \
             --request PUT                                                              \
             --header "Content-Type: application/json"                                  \
             --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"      \
             --body "{                                                             \
                     "password": "123",                                        \
                     "resetToken": "sdfsdfsdf23423dasdasdasd"                  \
             }" \
             https://api_baseurl/api/v1/reset-password
    ```

    ```python
        #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
                  }
        body = {
                "password": "123",
                "resetToken": "asdfsdfsdfsdfsdf234234"
                }
        req = requests.put("https://api_baseurl/api/v1/reset-password",
                                        header=header, data=json.dumps(body))
    ```
    ##### Response:
    202 Accepted.
    ```json{
          "meta": {
            "params": {
              "indent": 0
            }
          }
        }
    ```
    #### Possible Error
    - __Not Found_
    - __Invalid Params__

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| resetToken | string | True |  False |  Forgot Password Token |  None | None |
| password | string | True |  False |  New password for user. Max length 128 Character |  None | None |




## Account Get & Update & Delete

* __path:__ /api/v1/account
* __methods:__ ['GET', 'PUT', 'DELETE', 'OPTIONS']
* __type:__ object

Account get, update and delete resource

### Code Example:

#### PUT:
Update account field
### Request:

```bash
    #bash
    curl \
         --request PUT                                                          \
         --header "Content-Type: application/json"                              \
         --header "AUTHORIZATION: sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"   \
             --body "{                                                              \
              "organizationName": "Updated Example Organization",               \
              "address": "Updated_Example Address, A Street No 5.",             \
              "phone": "12345670001",                                           \
              "email": "Updated_zops_test_eneoooeeN@example.com"                \
         }"                                                                         \
         https://api_baseurl/api/v1/account
```

```python
    #python
    import requests
    import json
        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
                  }
        body = {
                "organizationName": "Updated_Example Organization",
                "address": "Updated_Example Address, A Street No 5.",
                "phone": "12345678901",
                "email": "Updated_zops_test_eneoooeeN@example.com"
        }

    req = requests.put("https://api_baseurl/api/v1/account",
                                    header=header, data=json.dumps(body))
```

#### Response:
202 Accepted.
```json
    {
    "meta":{
            "params": {
                    "indent": 0
                    }
           },
    "content": {
                 "organizationName": "Updated_Example Organization",
                 "address": "Updated_Example Address, A Street No 5.",
                 "phone": "12345670001",
                 "email": "Updated_zops_test_eneoooeeN@example.com",
                 }
    }
```
#### Possible Errors
- __Conflict__: Email address already used


#### DELETE
Delete account (all connected field deleted (users, services, consumers, projects)
### Request:

```bash
    #bash
    curl \
         --request DELETE                                                       \
         --header "Content-Type: application/json"                              \
         --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"  \
         https://api_baseurl/api/v1/account
```

```python
    #python
    import requests
    import json
        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
                  }
    req = requests.delete("https://api_baseurl/api/v1/account",
                                    header=header)
```
#### Response:
202 Accepted.

#### GET
Get account information
### Request:

```bash
    #bash
    curl \
         --request GET                                                          \
         --header "Content-Type: application/json"                              \
         --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"  \
         https://api_baseurl/api/v1/account
```

```python
    #python
    import requests
    import json
        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
                  }
    req = requests.get("https://api_baseurl/api/v1/account",
                                    header=header)
```
#### Response:
200 Accepted.
```json
    {
    "meta":{
            "params": {
                    "indent": 0
                    }
           },
    "content": {
                 "organizationName": "Example Organization",
                 "address": "Example Address, A Street No 5.",
                 "phone": "12345670001",
                 "email": "zops_test_eneoooeeN@example.com",
                 }
    }
```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| organizationName | string | False |  False |  Organization Name.Max Organization Name length 100 Character |  None | None |
| address | string | False |  False |  Address. Max Address length 200 Character |  None | None |
| phone | string | False |  False |  Phone Number, length must be 11 character. |  None | None |
| email | string | False |  False |  Email for Account.Max Email length 70 Character |  None | None |




## Account Create

* __path:__ /api/v1/register
* __methods:__ ['POST', 'OPTIONS']
* __type:__ list

Allows to Post Register New Account

####### Code Example:

### POST:
Create a new account
### Request:

```bash
    #bash
    curl \
         --request POST                             \
         --header "Content-Type: application/json"  \
         --body "{                                                          \
              "organizationName": "Example Organization",               \
              "email": "zops_test_eneoooeeN@example.com"                \
         }"                                                                 \
         https://api_baseurl/api/v1/register
```

```python
    #python
    import requests
    import json

    header = {'Content-Type': 'application/json'}

    body = {
            "organizationName": "Example Organization",
            "email": "zops_test_eneoooeeN@example.com"
    }

    req = requests.post("https://api_baseurl/api/v1/register",
                                    header=header, data=json.dumps(body))
```

#### Response:
201 Created.
```json
    {
    "meta":{
            "params": {
                    "indent": 0
                    }
           },
    "content": {
                 "organizationName": "Example Organization",
                 "email": "zops_test_eneoooeeN@example.com",
                 "registrationId": "f200baccded4413a81f9a381063c435c",
                 }
    }
```
#### Possible Errors
- __Conflict__: Email address already used
- __Failed Dependency__ :An Error occur on 3rd part service. Please retry after a few minutes.

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |
| testing | bool | False |  False |  Testing mode parameter. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| organizationName | string | False |  False |  Organization name.Max length 100 Character |  None | None |
| email | string | False |  False |  Email for account.Max length 70 Character |  None | None |
| registrationId | string | False |  True |  Registered account id. |  None | None |




## Account Update with Approve Code

* __path:__ /api/v1/register/{registration_id}
* __methods:__ ['PUT', 'OPTIONS']
* __type:__ object

Allows to update with Approve Code and Password

####### Code Example:

#### PUT
Update account with approve code and password. Create User with admin role
### Request:

```bash
    #bash
    curl \
         --request PUT                             \
         --header "Content-Type: application/json" \
         --body "{                                                                                      \
               "approveCode": "595819dca81e3ae6f81f4a39bd0470103044f936f6dd971803a23",              \
               "email": "zops_test_eneoooeeN@example.com",                                          \
               "password": "123",                                                                   \
               "firstName": "emre",                                                                 \
               "lastName": "dönmesz"                                                                \
         }"                                                                                             \
         https://api_baseurl/api/v1/register/{registration_id}

```

```python
    #python
    import requests
    import json

    header = {'Content-Type': 'application/json'}

    body = {
               "approveCode": "22f2a019590595819dca81e3ae6f81f4a39bd0470103044f936f6dd971803a23",
               "email": "zops_test_eneoooeeN@example.com",
               "password": "123",
               "firstName": "emre",
               "lastName": "dönmezs"
    }

    req = requests.put("https://api_baseurl/api/v1/register/{registration_id}",
                                    header=header, data=json.dumps(body))
```
#### Response:
202 Accepted:
```json

    {
    "meta": {
            "params": {
                        "indent": 0
                        }
            },
    "content": {
                "id": "90c4cc8b11ab49a58ecb4b799faa8979",
                "token": asdaskdh2uhehdasdhaksd,
                "email": "zops_test_eneoooeeN@example.com",
                "firstName": "emre",
                "lastName": "dönmezs"
                }
    }
```
> Warning
>
> In order to obtain the token, after approving the account it is necessary to be logged in. The
> response of the login request will include the token.

#### Possible Errors
- __Not Found__: Request invalid registration id.
- __Not Found__: Request invalid approve code

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| id | string | False |  True |  ID |  None | None |
| email | string | False |  False |  Email for user.Max length 70 Character |  None | None |
| password | string | True |  False |  Password for user.Max length 128 Character |  None | None |
| approveCode | string | True |  False |  Approve code to activate the account. |  None | None |
| firstName | string | False |  False |  Name of user.Max length 32 Character |  None | None |
| lastName | string | False |  False |  Last Name of user.Max length 32 Character |  None | None |
| token | string | False |  True |  User token |  None | None |




## Approve Code Resend

* __path:__ /api/v1/register/approve-code
* __methods:__ ['POST', 'OPTIONS']
* __type:__ list

Allows to resend approve code

####### Code Example:

#### POST
Resend account approve code
### Request:

```bash
    #bash
    curl \
         --request POST                             \
         --header "Content-Type: application/json" \
         --body "{                                                                                      \
               "email": "zops_test_eneoooeeN@example.com",                                          \
         }"                                                                                             \
         https://api_baseurl/api/v1/register/approve-code

```

```python
    #python
    import requests
    import json

    header = {'Content-Type': 'application/json'}

    body = {
               "email": "zops_test_eneoooeeN@example.com",
    }

    req = requests.post("https://api_baseurl/api/v1/register/approve-code",
                                    header=header, data=json.dumps(body))
```
#### Response:
202 Accepted:
```json

    {
    "meta": {
            "params": {
                        "indent": 0
                        }
            }
    }
```

#### Possible Errors
- __Not Found__: These email address does not exist
- __Failed Dependency__ :An Error occur on 3rd part service. Please retry after a few minutes.

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |
| testing | bool | False |  False |  Testing mode parameter. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| email | string | True |  False |  Email for account.Max length 70 Character |  None | None |




## Admin User Create & List

* __path:__ /api/v1/admins
* __methods:__ ['GET', 'POST', 'OPTIONS']
* __type:__ list

Allows to list and create admin

### Code Examples:
#### POST:
Create a new user with admin role
#### Request:

```bash
    #bash
    curl \
         --request POST                                                             \
         --header "Content-Type: application/json"                                  \
         --header "AUTHORIZATION: eyJ0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"   \
         --body "{                                                              \
                 "email": "zops_test_eneoooeeN@example.com",                \
                 "password": "123",                                         \
                 "firstName": "emre",                                       \
                 "lastName": "dönmesz"                                      \
         }"                                                                     \
         https://api_baseurl/api/v1/admins
```

```python
    #python
    import requests
    import json

    header = {
                "Content-Type": "application/json",
                "AUTHORIZATION": "sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
              }

    body = {
            "email": "zops_test_eneoooeeN@example.com",
            "password": "123",
            "firstName": "emre",
            "lastName": "dönmezs"
            }

    req = requests.post("https://api_baseurl/api/v1/admins",
                                    header=header, data=json.dumps(body))
```

#### Response:
201 Accepted:
```json
    {
    "meta": {
            "params": {
                        "indent": 0
                        }
            },
    "content": {
                "id": "3a033bb9d86443c4a82a98a575c6a461",
                "token": "ExlQUMQ8YNyLfUdYf7rmldGI79KQcIz8nwX1NcFC5o",
                "email": "zops_test_eoNeeoeNnn@example.com",
                "role": "admin",
                "firstName": "emre",
                "lastName": "dönmez"
                }
    }
```
#### Possible Errors
- __Conflict__
- __Unauthorized__


#### GET
Retrieve account admins.
#### Request:

```bash
    #bash
    curl \
         --request GET                                                          \
         --header "Content-Type: application/json"                              \
         --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"  \
         https://api_baseurl/api/v1/admins
```

```python
    #pyhon
    import requests
    import json

    header = {
                "Content-Type": "application/json",
                "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
              }
    req = requests.post("https://api_baseurl/api/v1/admins",
                                    header=header)
```

#### Response:
200 OK.
```json
    {
    "meta": {
            "params": {
                        "indent": 0
                        }
            },
    "content": [
                {
                 "id": "fc236ae7e97f4afbb638f2f3075eee1c",
                 "email": "zops_test_NnNNnoneoo@example.com",
                 "firstName": "emre",
                 "lastName": "dönmez"
                 "role": "admin",
                 "token": null,

                 },
                {
                 "id": "b0cbdd61cff843fdaf5a8c62cbbe460e",
                 "email": "zops_test_oNNnNneoeN@example.com",
                 "firstName": "emre2",
                 "lastName": "dönmez2"
                 "role": "admin",
                 "token": null,
                 },
                {
                 "id": "d31703ec133246f8ab6ee62176aa16f1",
                 "email": "zops_test_oNNenNoo@example.com",
                 "firstName": "emre3",
                 "lastName": "dönmez3"
                 "role": "admin",
                 "token": null,
                 }
               ]
    }
```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| id | string | False |  True |  ID |  None | None |
| token | string | False |  True |  Access token |  None | None |
| email | string | False |  False |  Email for user.Max length 70 Character |  None | None |
| password | string | True |  False |  Password for user.Max length 128 Character |  None | None |
| role | string | False |  True |  Role of user. |  None | None |
| firstName | string | False |  False |  Name of user.Max length 32 Character |  None | None |
| lastName | string | False |  False |  Last Name of user.Max length 32 Character |  None | None |




## Admin Retrieve & Update & Delete

* __path:__ /api/v1/admins/{admin_id}
* __methods:__ ['GET', 'PUT', 'DELETE', 'OPTIONS']
* __type:__ object

Allows to get and update admin with id.

### Code Examples
#### GET:
Retrieve admin user with id.
#### Request:
```bash
    #bash
    curl \
         --request GET                                                          \
         --header "Content-Type: application/json"                              \
         --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"  \
         https://api_baseurl/api/v1/admins/{admin_id}
```

```python
    #python
    import requests
    import json

    header = {
                "Content-Type": "application/json",
                "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
              }
    req = requests.get("https://api_baseurl/api/v1/admins/{admin_id}",
                                    header=header)
```

##### Response:
200 OK.
```json
    {
      "meta": {
        "params": {
          "indent": 0
        }
      },
      "content": {
        "email": "zops_test_oenNeNen@example.com",
        "role": "admin",
        "firstName": "ahmet",
        "lastName": "mehmet"
      }
    }
```


#### PUT:
Update admin user with id.
#### Request:
```bash
    #bash
    curl \
         --request PUT                                                              \
         --header "Content-Type: application/json"                                  \
         --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"      \
         --body "{                                                             \
                 "email": "zops_test_eneoooeeN@example.com",               \
                 "password": "123",                                        \
                 "firstName": "mehmet",                                    \
                 "lastName": "ahmet"                                       \
         }" \
         https://api_baseurl/api/v1/admins/{admin_id}
```

```python
    #python
    import requests
    import json

    header = {
                "Content-Type": "application/json",
                "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
              }
    body = {
            "email": "zops_test_eneoooeeN@example.com",
            "password": "123",
            "firstName": "mehmet",
            "lastName": "ahmet"
            }
    req = requests.put("https://api_baseurl/api/v1/admins/{admin_id}",
                                    header=header, data=json.dumps(body))
```
##### Response:
202 Accepted.
```json{
      "meta": {
        "params": {
          "indent": 0
        }
      },
      "content": {
        "email": "zops_test_nNnoeeee@example.com",
        "role": "admin",
        "firstName": "mehmet",
        "lastName": "ahmet"
      }
    }
```
#### Possible Error
- __Conflict_
- __Bad Request__

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| email | string | False |  False |  Email for user.Max length 70 Character |  None | None |
| password | string | True |  False |  Password for user.Max length 128 Character |  None | None |
| role | string | False |  True |  Role of user. |  None | None |
| firstName | string | False |  False |  Name of user.Max length 32 Character |  None | None |
| lastName | string | False |  False |  Last Name of user.Max length 32 Character |  None | None |
| token | string | False |  True |  Access token. |  None | None |




## Billing User Create & List

* __path:__ /api/v1/billings
* __methods:__ ['GET', 'POST', 'OPTIONS']
* __type:__ list

Allows to list and create billing

### Code Examples:

#### POST:
Create a new user with  billing role
#### Request:

```bash
    #bash
    curl \
         --request POST                                                             \
         --header "Content-Type: application/json"                                  \
         --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"      \
         --body "{                                                             \
                 "email": "zops_test_eneoooeeN@example.com",               \
                 "password": "123",                                        \
                 "firstName": "emre",                                      \
                 "lastName": "dönmesz"                                     \
         }"                                                                    \
         https://api_baseurl/api/v1/billings
```

```python
    #python
    import requests
    import json

    header = {
                "Content-Type": "application/json",
                "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
              }

    body = {
            "email": "zops_test_eneoooeeN@example.com",
            "password": "123",
            "firstName": "emre",
            "lastName": "dönmezs"
            }

    req = requests.post("https://api_baseurl/api/v1/billings",
                                    header=header, data=json.dumps(body))
```

#### Response:
201 Accepted:
```json
    {
    "meta": {
            "params": {
                        "indent": 0
                        }
            },
    "content": {
                "id": "3a033bb9d86443c4a82a98a575c6a461",
                "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MTA4MTkyNTQsImlhdCI6MTUxMDIxNDQ1NCwic3ViIjoiM2EwMzNiYjlkODY0NDNjNGE4MmE5OGE1NzVjNmE0NjEiLCJyb2wiOjIsInRlbmFudF9pZCI6bnVsbCwiYWNjb3VudF9pZCI6ImYyMDBiYWNjZGVkNDQxM2E4MWY5YTM4MTA2M2M0MzVjIn0.pExlQUMQ8YNyLfUdYf7rmldGI79KQcIz8nwX1NcFC5o",
                "email": "zops_test_eoNeeoeNnn@example.com",
                "role": "billing",
                "firstName": "emre",
                "lastName": "dönmez"
                }
    }
```
#### Possible Errors
- __Conflict__
- __Unauthorized__


#### GET
Retrieve user billing
#### Request:

```bash
    #bash
    curl \
         --request GET                                                          \
         --header "Content-Type: application/json"                              \
         --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"  \
         https://api_baseurl/api/v1/billings
```

```python
    #python
    import requests
    import json

    header = {
                "Content-Type": "application/json",
                "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
              }
    req = requests.get("https://api_baseurl/api/v1/billings",
                                    header=header)
```

#### Response:
200 OK.
```json
    {
    "meta": {
            "params": {
                        "indent": 0
                        }
            },
    "content": [
                {
                 "id": "fc236ae7e97f4afbb638f2f3075eee1c",
                 "email": "zops_test_NnNNnoneoo@example.com",
                 "firstName": "emre",
                 "lastName": "dönmez"
                 "role": "billing",
                 "token": null,

                 },
                {
                 "id": "b0cbdd61cff843fdaf5a8c62cbbe460e",
                 "email": "zops_test_oNNnNneoeN@example.com",
                 "firstName": "emre2",
                 "lastName": "dönmez2"
                 "role": "billing",
                 "token": null,
                 },
                {
                 "id": "d31703ec133246f8ab6ee62176aa16f1",
                 "email": "zops_test_oNNenNoo@example.com",
                 "firstName": "emre3",
                 "lastName": "dönmez3"
                 "role": "billing",
                 "token": null,
                 }
               ]
    }
```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| id | string | False |  True |  ID |  None | None |
| token | string | False |  True |  Access token |  None | None |
| email | string | False |  False |  Email for user.Max length 70 Character |  None | None |
| password | string | True |  False |  Password for user.Max length 128 Character |  None | None |
| role | string | False |  True |  Role of user. |  None | None |
| firstName | string | False |  False |  Name of user.Max length 32 Character |  None | None |
| lastName | string | False |  False |  Last Name of user.Max length 32 Character |  None | None |




## Billing User Retrieve & Update & Delete

* __path:__ /api/v1/billings/{billing_id}
* __methods:__ ['GET', 'PUT', 'DELETE', 'OPTIONS']
* __type:__ object

Allows to get and update billing with id.

### Code Examples

#### GET:
Retrieve billing user with id.
#### Request:

```bash
    #bash
    curl \
         --request GET                                                            \
         --header "Content-Type: application/json"                                \
         --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"    \
         https://api_baseurl/api/v1/billings/{billing_id}
```

```python
    #python
    import requests
    import json

    header = {
                "Content-Type": "application/json",
                "AUTHORIZATION": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MTA4MTkyNTQsImlhdCI6MTUxMDIxNDQ1NCwic3ViIjoiOTBjNGNjOGIxMWFiNDlhNThlY2I0Yjc5OWZhYTg5NzkiLCJyb2wiOjIsInRlbmFudF9pZCI6bnVsbCwiYWNjb3VudF9pZCI6ImYyMDBiYWNjZGVkNDQxM2E4MWY5YTM4MTA2M2M0MzVjIn0.0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
              }
    req = requests.post("https://api_baseurl/api/v1/billings/hsdkfsd8f7sdf7s6df6rewyr",
                                    header=header)
```
##### Response:
200 OK.
```json
    {
      "meta": {
        "params": {
          "indent": 0
        }
      },
      "content": {
        "email": "zops_test_oenNeNen@example.com",
        "role": "billing",
        "firstName": "ahmet",
        "lastName": "mehmet"
      }
    }
```


#### PUT:
Update billing user with id.
#### Request:

```bash
    #bash
    curl \
         --request PUT                                                              \
         --header "Content-Type: application/json"                                  \
         --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"      \
         --body "{                                                             \
                 "email": "zops_test_eneoooeeN@example.com",               \
                 "password": "123",                                        \
                 "firstName": "mehmet",                                    \
                 "lastName": "ahmet"                                       \
         }" \
         https://api_baseurl/api/v1/billings/{billing_id}
```

```python
    #python
    import requests
    import json

    header = {
                "Content-Type": "application/json",
                "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
              }
    body = {
            "email": "zops_test_eneoooeeN@example.com",
            "password": "123",
            "firstName": "mehmet",
            "lastName": "ahmet"
            }
    req = requests.put("https://api_baseurl/api/v1/billings/{billing_id}",
                                    header=header, data=json.dumps(body))
```

##### Response:
202 Accepted.
```json{
      "meta": {
        "params": {
          "indent": 0
        }
      },
      "content": {
        "email": "zops_test_nNnoeeee@example.com",
        "role": "billing",
        "firstName": "mehmet",
        "lastName": "ahmet"
      }
    }
```
#### Possible Error
- __Conflict_
- __Bad Request__

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| email | string | False |  False |  Email for user.Max length 70 Character |  None | None |
| password | string | True |  False |  Password for user.Max length 128 Character |  None | None |
| role | string | False |  True |  Role of user. |  None | None |
| firstName | string | False |  False |  Name of user.Max length 32 Character |  None | None |
| lastName | string | False |  False |  Last Name of user.Max length 32 Character |  None | None |
| token | string | False |  True |  Access token. |  None | None |




## Developer User Create & List

* __path:__ /api/v1/developers
* __methods:__ ['GET', 'POST', 'OPTIONS']
* __type:__ list

Allows to list and create developer

### Code Examples:

#### POST:
Create a new user with developer role
#### Request:

```bash
    #bash
    curl \
         --request POST                                                          \
         --header "Content-Type: application/json"                               \
         --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"   \
         --body "{                                                             \
                 "email": "zops_test_eneoooeeN@example.com",               \
                 "password": "123",                                        \
                 "firstName": "emre",                                      \
                 "lastName": "dönmesz"                                     \
         }" \
         https://api_baseurl/api/v1/developers
```

```python
    #python
    import requests
    import json

    header = {
                "Content-Type": "application/json",
                "AUTHORIZATION": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MTA4MTkyNTQsImlhdCI6MTUxMDIxNDQ1NCwic3ViIjoiOTBjNGNjOGIxMWFiNDlhNThlY2I0Yjc5OWZhYTg5NzkiLCJyb2wiOjIsInRlbmFudF9pZCI6bnVsbCwiYWNjb3VudF9pZCI6ImYyMDBiYWNjZGVkNDQxM2E4MWY5YTM4MTA2M2M0MzVjIn0.0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
              }

    body = {
            "email": "zops_test_eneoooeeN@example.com",
            "password": "123",
            "firstName": "emre",
            "lastName": "dönmezs"
            }

    req = requests.post("https://api_baseurl/api/v1/developers",
                                    header=header, data=json.dumps(body))
```

#### Response:
201 Accepted:

```json
    {
    "meta": {
            "params": {
                        "indent": 0
                        }
            },
    "content": {
                "id": "3a033bb9d86443c4a82a98a575c6a461",
                "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MTA4MTkyNTQsImlhdCI6MTUxMDIxNDQ1NCwic3ViIjoiM2EwMzNiYjlkODY0NDNjNGE4MmE5OGE1NzVjNmE0NjEiLCJyb2wiOjIsInRlbmFudF9pZCI6bnVsbCwiYWNjb3VudF9pZCI6ImYyMDBiYWNjZGVkNDQxM2E4MWY5YTM4MTA2M2M0MzVjIn0.pExlQUMQ8YNyLfUdYf7rmldGI79KQcIz8nwX1NcFC5o",
                "email": "zops_test_eoNeeoeNnn@example.com",
                "role": "developer",
                "firstName": "emre",
                "lastName": "dönmez"
                }
    }
```

#### Possible Errors
- __Conflict__
- __Unauthorized__


#### GET
Retrieve account developers.
#### Request:

```bash
    #bash
    curl \
         --request GET                                                          \
         --header "Content-Type: application/json"                              \
         --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"  \
         https://api_baseurl/api/v1/developers
```

```python
    #python
    import requests
    import json

    header = {
                "Content-Type": "application/json",
                "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
              }
    req = requests.get("https://api_baseurl/api/v1/developers",
                                    header=header)
```

#### Response:
200 OK.
```json
    {
    "meta": {
            "params": {
                        "indent": 0
                        }
            },
    "content": [
                {
                 "id": "fc236ae7e97f4afbb638f2f3075eee1c",
                 "email": "zops_test_NnNNnoneoo@example.com",
                 "firstName": "emre",
                 "lastName": "dönmez"
                 "role": "developer",
                 "token": null,

                 },
                {
                 "id": "b0cbdd61cff843fdaf5a8c62cbbe460e",
                 "email": "zops_test_oNNnNneoeN@example.com",
                 "firstName": "emre2",
                 "lastName": "dönmez2"
                 "role": "developer",
                 "token": null,
                 },
                {
                 "id": "d31703ec133246f8ab6ee62176aa16f1",
                 "email": "zops_test_oNNenNoo@example.com",
                 "firstName": "emre3",
                 "lastName": "dönmez3"
                 "role": "developer",
                 "token": null,
                 }
               ]
    }
```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| id | string | False |  True |  ID |  None | None |
| token | string | False |  True |  Access token |  None | None |
| email | string | False |  False |  Email for user.Max length 70 Character |  None | None |
| password | string | True |  False |  Password for user.Max length 128 Character |  None | None |
| role | string | False |  True |  Role of user. |  None | None |
| firstName | string | False |  False |  Name of user.Max length 32 Character |  None | None |
| lastName | string | False |  False |  Last Name of user.Max length 32 Character |  None | None |




## Developer User Retrieve & Update & Delete

* __path:__ /api/v1/developers/{developer_id}
* __methods:__ ['GET', 'PUT', 'DELETE', 'OPTIONS']
* __type:__ object

Allows to get and update developer with id.

### Code Examples

#### GET:
Retrieve developer user with id.
#### Request:

```bash
    #bash
    curl \
         --request GET                                                          \
         --header "Content-Type: application/json"                              \
         --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"  \
         https://api_baseurl/api/v1/developers/{developer_id}
```

```python
    #python
    import requests
    import json

    header = {
                "Content-Type": "application/json",
                "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
              }
    req = requests.get("https://api_baseurl/api/v1/developers/{developer_id}",
                                    header=header)
```

##### Response:
200 OK.
```json
    {
      "meta": {
        "params": {
          "indent": 0
        }
      },
      "content": {
        "email": "zops_test_oenNeNen@example.com",
        "role": "developer",
        "firstName": "ahmet",
        "lastName": "mehmet"
      }
    }
```


#### PUT:
Update developer user with id.
#### Request:

```bash
    #bash
    curl \
         --request PUT                                                              \
         --header "Content-Type: application/json"                                  \
         --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"      \
         --body "{                                                             \
                 "email": "zops_test_eneoooeeN@example.com",               \
                 "password": "123",                                        \
                 "firstName": "mehmet",                                    \
                 "lastName": "ahmet"                                       \
         }" \
         https://api_baseurl/api/v1/developers/{developer_id}
```

```python
    #python
    import requests
    import json

    header = {
                "Content-Type": "application/json",
                "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
              }
    body = {
            "email": "zops_test_eneoooeeN@example.com",
            "password": "123",
            "firstName": "mehmet",
            "lastName": "ahmet"
            }
    req = requests.post("https://api_baseurl/api/v1/developers/{developer_id}",
                                    header=header, data=json.dumps(body))
```

##### Response:
202 Accepted.
```json{
      "meta": {
        "params": {
          "indent": 0
        }
      },
      "content": {
        "email": "zops_test_nNnoeeee@example.com",
        "role": "developers",
        "firstName": "mehmet",
        "lastName": "ahmet"
      }
    }
```

#### Possible Error
- __Conflict_
- __Bad Request__

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| email | string | False |  False |  Email for user.Max length 70 Character |  None | None |
| password | string | True |  False |  Password for user.Max length 128 Character |  None | None |
| role | string | False |  True |  Role of user. |  None | None |
| firstName | string | False |  False |  Name of user.Max length 32 Character |  None | None |
| lastName | string | False |  False |  Last Name of user.Max length 32 Character |  None | None |
| token | string | False |  True |  Access token. |  None | None |




## Get User Information

* __path:__ /api/v1/me
* __methods:__ ['GET', 'OPTIONS']
* __type:__ object

Allow to get user information

    ### Code Examples
    #### GET:
    Retrieve user information with token.
    #### Request:
    ```bash
        #bash
        curl \
             --request GET                                                          \
             --header "Content-Type: application/json"                              \
             --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"  \
             https://api_baseurl/api/v1/me
    ```

    ```python
        #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
                  }
        req = requests.get("https://api_baseurl/api/v1/me",
                                        header=header)
    ```

    ##### Response:
    200 OK.
    ```json
        {
          "meta": {
            "params": {
              "indent": 0
            }
          },
          "content": {
            "email": "zops_test_oenNeNen@example.com",
            "role": "admin",
            "id": 123123123123,
            "firstName": "ahmet",
            "lastName": "mehmet"
          }
        }
    ```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| id | string | False |  True |  ID |  None | None |
| email | string | False |  True |  Email for user.Max length 70 Character |  None | None |
| role | string | False |  True |  Role of user. |  None | None |
| firstName | string | False |  True |  Name of user.Max length 32 Character |  None | None |
| lastName | string | False |  True |  Last Name of user.Max length 32 Character |  None | None |




## Project Create & List

* __path:__ /api/v1/projects
* __methods:__ ['GET', 'POST', 'OPTIONS']
* __type:__ list

Allows to create and list project

####### Code Example:

#### POST:
  Create a new project
 ### Request:

   ```bash
       #bash
          curl \
                --request POST                                                                   \
                --header "Content-Type: application/json"                                        \
                --header "AUTHORIZATION : sdkjfhskjfk32kjh42kj2h342kh34h2k3h4kkhjsdhjkhwr"       \
                --body "{                                                   \
                          "name": "Aka Project",                        \
                          "description": "Super top secret project!"    \
                        }"                                                  \
                 https://api_baseurl/api/v1/projects
   ```

   ```python
       #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "sdkjfhskjfk32kjh42kj2h342kh34h2k3h4kkhjsdhjkhwr"
                  }

        body = {
                "name": "Aka Project",
                "description": "Super top secret project!"
                }

        req = requests.post("https://api_baseurl/api/v1/projects",
                                        header=header, data=json.dumps(body))
   ```
 ### Response:
  201 Created.
  ```json
        {
          "meta": {
            "params": {
              "indent": 0
            }
          },
          "content": {
            "name": "Aka Project",
            "description": "Super top secret project!",
            "id": "1aa36f61f9c14156a900921abb04af56",
            "userLimit": null,
            "userUsed": null
          }
        }
  ```


#### GET:
  List projects
 ### Request:

   ```bash
       #bash
          curl \
                --request GET                                                               \
                --header "Content-Type: application/json"                                   \
                --header "AUTHORIZATION: sdkjfhskjfk32kjh42kj2h342kh34h2k3h4kkhjsdhjkhwr"   \
                 https://api_baseurl/api/v1/projects
   ```

   ```python
       #python
        import requests
        import json

            header = {
                        "Content-Type": "application/json",
                        "AUTHORIZATION": "sdkjfhskjfk32kjh42kj2h342kh34h2k3h4kkhjsdhjkhwr"
                      }

        req = requests.get("https://api_baseurl/api/v1/projects",
                                        header=header)
   ```

 ### Response:
  200 OK.
  ```json

    {
      "meta": {
        "params": {
          "indent": 0
        }
      },
      "content": [
        {
          "name": "Aka Project",
          "description": "Super top secret project!",
          "id": "1aa36f61f9c14156a900921abb04af56",
          "userLimit": 10,
          "userUsed": 0
        },
        {
          "name": "Zetaops Project",
          "description": "secret project!",
          "id": "asdasd1aa36f61f9c14156a900921abb04af56",
          "userLimit": 10,
          "userUsed": 0
        }
      ]
    }

  ```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| name | string | False |  False |  Project name.Max length 70 Character |  None | None |
| description | string | False |  False |  Project description.Max length 200 Character |  None | None |
| id | string | False |  True |  ID |  None | None |
| userLimit | int | False |  True |  User limit of service. |  None | None |
| userUsed | int | False |  True |  User used of service. |  None | None |
| services | None | False |  True |  Project's active services |  None | None |




## Project Retrieve & Update

* __path:__ /api/v1/projects/{project_id}
* __methods:__ ['GET', 'PUT', 'OPTIONS']
* __type:__ object

Allows to update and retrieve project with project id

####### Code Example:

#### PUT:
  Update project with project id
 ### Request:

   ```bash
       #bash
          curl \
                --request PUT                                                                       \
                --header "Content-Type: application/json"                                           \
                --header "AUTHORIZATION": sdkjfhskjfk32kjh42kj2h342kh34h2k3h4kkhjsdhjkhwr"          \
                --body "{                                                         \
                            "name": "Aka Project!..",                         \
                            "description": "Super top secret project!",       \
                        }"                                                        \
                 https://api_baseurl/api/v1/projects/{projectId}

   ```

   ```python
       #python
        import requests
        import json

            header = {
                        "Content-Type": "application/json",
                        "AUTHORIZATION": "sdkjfhskjfk32kjh42kj2h342kh34h2k3h4kkhjsdhjkhwr"
                      }
            body = {
                    "name": "Aka Project!..",
                    "description": "Super top secret project!"
                    }

        req = requests.put("https://api_baseurl/api/v1/projects/{projectId}",
                                        header=header, data=json.dumps(body))
   ```
 ### Response:
  202 Accepted.
  ```json
    {
      "meta": {
        "params": {
          "indent": 0
        }
      },
      "content": {
        "name": "Aka Project!..",
        "description": "Super top secret project!",
        "id": "1aa36f61f9c14156a900921abb04af56",
        "userLimit": 10,
        "userUsed": 0
      }
    }
  ```

#### GET:
  Retrieve project with id
 ### Request:

   ```bash
       #bash
          curl \
                --request GET                                                                       \
                --header "Content-Type: application/json"                                           \
                --header "AUTHORIZATION": Token sdkjfhskjfk32kjh42kj2h342kh34h2k3h4kkhjsdhjkhwr"    \
                 https://api_baseurl/api/v1/projects/{projectId}
   ```

   ```python
       #python
        import requests
        import json

            header = {
                        "Content-Type": "application/json",
                        "AUTHORIZATION": "sdkjfhskjfk32kjh42kj2h342kh34h2k3h4kkhjsdhjkhwr"
                      }

        req = requests.get("https://api_baseurl/api/v1/projects/{projectId}",
                                        header=header)
   ```
 ### Response:
  200 OK.
  ```json
        {
          "meta": {
            "params": {
              "indent": 0
            }
          },
          "content": {
            "name": "Aka Project",
            "description": "Super top secret project!",
            "id": "1aa36f61f9c14156a900921abb04af56",
            "services": ["roc", "push"]
            "userLimit": 10,
            "userUsed": 0
          }
        }
  ```
  ## Possible Error
   - __Not Found___

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| name | string | False |  False |  Project name.Max length 70 Character |  None | None |
| description | string | False |  False |  Project description.Max length 200 Character |  None | None |
| id | string | False |  True |  ID |  None | None |
| userLimit | int | False |  True |  User limit of service. |  None | None |
| userUsed | int | False |  True |  User used of service. |  None | None |
| services | None | False |  True |  Project's active services |  None | None |




## Google Server API Key, Google Project Number, Apns IOS Push Certification Retrieve & Update

* __path:__ /api/v1/projects/{project_id}/api
* __methods:__ ['GET', 'PUT', 'OPTIONS']
* __type:__ object

Project Google Server API Key, Google Project Number, Apns IOS Push Certification Resource. You can get and update using this resource.

    ### Code Examples

    #### GET:
    Get Google Server API Key, Google Project Number, Apns IOS Push Certification
    #### Request:

    ```bash
        #bash
        curl \
             --request GET                                                          \
             --header "Content-Type: application/json"                              \
             --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"  \
             https://api_baseurl/api/v1/projects/{project_id}/api
    ```

    ```python
        #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
                  }
        req = requests.get("https://api_baseurl/api/v1/projects/{project_id}/api",
                                        header=header)
    ```

    ##### Response:
    200 OK.
    ```json
        {
          "meta": {
            "params": {
              "indent": 0
            }
          },
          "content": {
            "fcmApiKeys": "asdasdasdas123123",
            "fcmProjectNumber": "12312312qweqweq213",
            "apnsCert": "Yga25vd2xlZGdlLCBleGNlZWRzIHRoZSBzaG9ydCB2ZWhlbWVuY2Ugb2YgYW55IGNhcm5hbCBwbGVhc3VyZS4=",
            "id": "c3c0a4864a054b6da3c642588c594fc3"
          }
        }
    ```


    #### PUT:
    Update Google Server API Key, Google Project Number, Apns IOS Push Certification
    #### Request:

    ```bash
        #bash
        curl \
             --request PUT                                                              \
             --header "Content-Type: application/json"                                  \
             --header "AUTHORIZATION: 0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"      \
             --body "{                                                                                  \
                    "fcmApiKeys": "asdasdasdas123123",                                              \
                    "fcmProjectNumber": "12312312qweqweq213",                                       \
                    "apnsCert": "ZWRzIHRoZSBzaG9ydCB2ZWhlbWVuY2Ugb2YgYW55IGNhcm5hbCBwbGVhc3VyZS4="  \
             }" \
             https://api_baseurl/api/v1/projects/{project_id}/api
    ```

    ```python
        #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "0sOEQfyptM0ZG7kJYkNxmswp_p5y9iX5t61KI1qH83w"
                  }
        body = {
                "fcmApiKeys": "asdasdasdas123123",
                "fcmProjectNumber": "12312312qweqweq213",
                "apnsCert": "asd2342j3423942342343VyZS4="
                }
        req = requests.put("https://api_baseurl/api/v1/projects/{project_id}/api",
                                        header=header, data=json.dumps(body))
    ```
    ##### Response:
    202 Accepted.
    ```json{
          "meta": {
            "params": {
              "indent": 0
            }
          },
          "content": {
            "fcmApiKeys": "asdasdasdas123123",
            "fcmProjectNumber": "12312312qweqweq213",
            "apnsCert": "HRoZSBzaG9ydCB2ZWhlbWVuY2Ugb2YgYW55IGNhcm5hbCBwbGVhc3VyZS4=",
            "id": "c3c0a4864a054b6da3c642588c594fc3"
          }
        }
    ```
    #### Possible Error
    - __Bad Request__

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| fcmApiKeys | string | False |  False |  Fcm API Key |  None | None |
| fcmProjectNumber | string | False |  False |  Fcm Project Number |  None | None |
| apnsCert | string | False |  False |  Apns Cert |  None | None |
| id | string | False |  True |  ID |  None | None |




## Service Catalog Create and List

* __path:__ /api/v1/services
* __methods:__ ['GET', 'POST', 'OPTIONS']
* __type:__ list

Allows to create and list service catalog

### Code Example:

##### POST:
Create service catalog item (You Must be Root)
### Request:

    ```bash
        #bash
        curl \
             --request POST                                                                 \
             --header "Content-Type: application/json"                                      \
             --header "AUTHORIZATION: sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"  \
             --body "{                                                              \
                            "codeName":"roc",                                   \
                            "name":"Real Time Online Chat",                     \
                            "description":"Real Time Online Chat is funny!"     \
                    }"                                                              \
             https://api_baseurl/api/v1/services
    ```

    ```python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"
                  }
        body = {
                    "codeName":"roc",
                    "name":"Real Time Online Chat",
                    "description":"Real Time Online Chat is funny!"
                }
        req = requests.post("https://api_baseurl/api/v1/services",
                                        header=header, data=json.dumps(body))
    ```

### Response:
    201 Accepted.
    ```json
        {
            "codeName":"roc",
            "name":"Real Time Online Chat",
            "description":"Real Time Online Chat is funny!"
        }
    ```


##### GET:
Get all service catalogs
### Request:
    ```bash
        #bash
        curl \
             --request GET                                                                  \
             --header "Content-Type: application/json"                                      \
             --header "AUTHORIZATION: sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"  \
             https://api_baseurl/api/v1/services
    ```

    ```python
        #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"
                    }
        req = requests.get("https://api_baseurl/api/v1/services",
                                        header=header)
    ```

### Response:
    200 OK.
    ```json

            {
              "meta": {
                "params": {
                  "indent": 0
                }
              },
              "content": [
                {
                  "name": "Real Time Online Chat",
                  "description": "Real Time Online Chat is funny!",
                  "codeName": "roc"
                }
              ]
            }

    ```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| name | string | False |  False |  Service Catalog name |  None | None |
| description | string | False |  False |  Service Catalog description |  None | None |
| codeName | string | False |  False |  Code name of the service. |  None | None |




## Service Create

* __path:__ /api/v1/projects/{project_id}/services
* __methods:__ ['POST', 'OPTIONS']
* __type:__ list

Allows to create attachment between service and project

### Code Example:

##### POST:
### Request:

    ```bash
        #bash
        curl \
             --request POST                                                                 \
             --header "Content-Type: application/json"                                      \
             --header "AUTHORIZATION: sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"  \
             --body "{                                                              \
                            "serviceCatalogCode":"roc",                         \
                            "name":"message",                                   \
                            "description":"fff"                                 \
                    }"                                                              \
             https://api_baseurl/api/v1/projects/{project_id}/services
    ```

    ```python
        #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"
                  }
        body = {
                    "codeName":"roc",
                    "name":"message",
                    "description":"fff"
                }
        req = requests.post("https://api_baseurl/api/v1/projects/{project_id}/services",
                                        header=header, data=json.dumps(body))
    ```

### Response:
    201 Created.
    ```json
            {
              "meta": {
                "params": {
                  "indent": 0
                }
              },
              "content": {
                "id": "316589e74d52490e93a88fdf21c6f2ad",
                "itemLimit": 0,
                "name": "message",
                "description": "fff",
                "serviceCatalogCode": "roc"
              }
            }
    ```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| id | string | False |  True |  ID |  None | None |
| itemLimit | int | False |  True |  Item limit of service. |  None | None |
| itemUsed | int | False |  True |  Item used of service. |  None | None |
| name | string | False |  False |  Service name.Max length 70 Character |  None | None |
| description | string | False |  False |  Service description.Max length 200 Character |  None | None |
| serviceCatalogCode | string | False |  False |  Code name of the service. |  None | None |




## Service Delete

* __path:__ /api/v1/projects/{project_id}/services/{service_catalog_code}
* __methods:__ ['GET', 'DELETE', 'OPTIONS']
* __type:__ object

Allows to delete attachment between project and service

### Code Example:

#### GET:
  Retrieve service with project_id and service_catalog_code
 ### Request:

   ```bash
       #bash
          curl \
                --request GET                                                                       \
                --header "Content-Type: application/json"                                           \
                --header "AUTHORIZATION": Token sdkjfhskjfk32kjh42kj2h342kh34h2k3h4kkhjsdhjkhwr"    \
                https://api_baseurl/api/v1/projects/{project_id}/services/{service_catalog_code}
   ```

   ```python
       #python
        import requests
        import json

            header = {
                        "Content-Type": "application/json",
                        "AUTHORIZATION": "sdkjfhskjfk32kjh42kj2h342kh34h2k3h4kkhjsdhjkhwr"
                      }

        req = requests.get("https://api_baseurl/api/v1/projects/{project_id}/services/{service_catalog_code}",
                                        header=header)
   ```
 ### Response:
  200 OK.
  ```json
        {
          "meta": {
            "params": {
              "indent": 0
            }
          },
          "content": {
            "id": "316589e74d52490e93a88fdf21c6f2ad",
            "itemLimit": 100,
            "itemUsed": 10,
            "name": "message",
            "description": "fff",
            "serviceCatalogCode": "roc"
          }
        }
  ```
  ## Possible Error
   - __Not Found___

##### DELETE:
### Request:

    ```bash
        #bash
        curl \
             --request DELETE                                                               \
             --header "Content-Type: application/json"                                      \
             --header "AUTHORIZATION: sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"  \
             https://api_baseurl/api/v1/projects/{project_id}/services/{service_catalog_code}
    ```

    ```python
        #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"
                  }
        req = requests.delete("https://api_baseurl/api/v1/projects/{project_id}/services/{service_catalog_code}",
                                        header=header)
    ```
### Response:
202 Accepted.
    ```json
            {
              "meta": {
                "params": {
                  "indent": 0
                }
              },
              "content": null
            }
    ```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| id | string | False |  True |  ID |  None | None |
| itemLimit | int | False |  True |  Item limit of service. |  None | None |
| itemUsed | int | False |  True |  Item used of service. |  None | None |
| name | string | False |  False |  Service name.Max length 70 Character |  None | None |
| description | string | False |  False |  Service description.Max length 200 Character |  None | None |
| serviceCatalogCode | string | False |  False |  Code name of the service. |  None | None |




## Consumer Create & List

* __path:__ /api/v1/consumers
* __methods:__ ['GET', 'POST', 'OPTIONS']
* __type:__ list

Allows to create and list consumer

####### Code Example:

#### POST:
  Creates a new consumer, returns consumer id
 ### Request:

   ```bash
       #bash
        curl \
             --request POST                                                    \
             --header "Content-Type: application/json"                         \
             --header "AUTHORIZATION: CI6ImYyMDBiYWNjZGVkNDQxM2E4MiX5I1qH83w"  \
             --body "{}"                                                       \
             https://api_baseurl/api/v1/consumers

   ```

   ```python
       #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "CI6ImYyMDBiYWNjZGVkNDQxM2E4MiX5I1qH83w"
                  }

        body = {}
        req = requests.post("https://api_baseurl/api/v1/consumers",
                            header=header, data=json.dumps(body))
   ```

 ### Response:
 201 Created.
  ```json
        {
          "meta": {
            "params": {
              "indent": 0
            }
          },
          "content": {
            "id": "f074d1b87c774ddfa685b224567b803d"
          }
        }
  ```

#### GET:
  List consumers
 ### Request:
   ```bash
       #bash
        curl \
             --request GET                                                                  \
             --header "Content-Type: application/json"                                      \
             --header "AUTHORIZATION: sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"  \
             https://api_baseurl/api/v1/consumers
   ```
   ```python
       #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"
                  }
        req = requests.get("https://api_baseurl/api/v1/consumers",
                                        header=header)
   ```
 ### Response:
  200 OK.
  ```json

        {
          "meta": {
            "params": {
              "indent": 0
            }
          },
          "content": [
            {
              "id": "f074d1b87c774ddfa685b224567b803d"
            },
            {
              "id": "1fcedd8e7ac345e8ba60db07ae4fb59a"
            },
            {
              "id": "5af03d9fa2ed4f12950717f4d32bd679"
            }
          ]
        }
  ```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| id | string | False |  True |  ID of consumer. |  None | None |




## Project Consumer Delete

* __path:__ /api/v1/projects/{project_id}/consumers/{consumer_id}
* __methods:__ ['DELETE', 'OPTIONS']
* __type:__ object

Allows to delete attachment (between project and consumer)

####### Code Example:

#### DELETE:
  Delete project consumer
 ### Request:

   ```bash
       #bash
        curl \
             --request DELETE                                                               \
             --header "Content-Type: application/json"                                      \
             --header "AUTHORIZATION: sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"  \
             https://api_baseurl/api/v1/projects/$project_id/consumers/$consumer_id
   ```

   ```python
       #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"
                  }
        req = requests.delete("https://api_baseurl/api/v1/projects/$project_id/consumers/{consumer_id}",
                                        header=header)
   ```

 ### Response:
  202 Accepted.
  ```json

        {
          "meta": {
            "params": {
              "indent": 0
            }
          },
          "content": null
        }

  ```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
None




## Project Consumer Create

* __path:__ /api/v1/projects/{project_id}/consumers
* __methods:__ ['POST', 'OPTIONS']
* __type:__ list

Allows to create attachment with project to consumer

####### Code Example:

#### POST:
  Create a project consumer
 ### Request:

   ```bash
       #bash
        curl \
             --request POST                                                                 \
             --header "Content-Type: application/json"                                      \
             --header "AUTHORIZATION: sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"  \
             --body "{                                                            \
                        "consumerId": "f074d1b87c774ddfa685b224567b803d"      \
                     }"                                                           \
             https://api_baseurl/api/v1/projects/{project_id}/consumers
   ```

   ```python
       #python
        import requests
        import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"
                  }

        body = {
                   "consumerId": "f074d1b87c774ddfa685b224567b803d"
                }
        req = requests.post("https://api_baseurl/api/v1/projects/{project_id}/consumers",
                            header=header, data=json.dumps(body))
   ```
 ### Response:
 201 Created.
  ```json
        {
          "meta": {
            "params": {
              "indent": 0
            }
          },
          "content": {
            "consumerId": "f074d1b87c774ddfa685b224567b803d"
          }
        }

  ```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| consumerId | string | False |  False |  List of consumer_id's |  None | None |




## Consumer Token Create

* __path:__ /api/v1/consumer-tokens
* __methods:__ ['POST', 'OPTIONS']
* __type:__ list

Allows to create consumer token

### Code Example:
#### POST:
#### Request:

```bash
    #bash
    curl \
         --request POST                                                                 \
         --header "Content-Type: application/json"                                      \
         --header "AUTHORIZATION: sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"  \
         --body "{                                                      \
                    "consumerId":"$consumer1_id",                   \
                    "projectId":"$project_id",                      \
                    "serviceCatalogCode":"$service_catalog_code"    \
                }"                                                      \
         https://api_baseurl/api/v1/consumer-tokens

```

```python
    #python
    import requests
    import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"
                  }
        body = {
                   "consumerId":"$consumer1_id",
                   "projectId":"$project_id",
                   "serviceCatalogCode":"$service_catalog_code"
                }
        req = requests.post("https://api_baseurl/api/v1/consumer-tokens,
                            header=header, data=json.dumps(body))

```

### Response:
201 Created.
```json

        {
          "meta": {
            "params": {
              "indent": 0
            }
          },
          "content": {
            "consumerId": null,
            "projectId": null,
            "serviceCatalogCode": null,
            "token": "5b72837976e9e81409962c38ad07495c1b4884f7729381ebcaacf41f1c9452a7"
          }
        }

```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
| consumerId | string | False |  False |  Consumer ID |  None | None |
| projectId | string | False |  False |  Project ID |  None | None |
| serviceCatalogCode | string | False |  False |  Service Code |  None | None |
| token | string | False |  True |  Refresh Token |  None | None |




## Consumer Token Delete

* __path:__ /api/v1/consumer-tokens/{token_id}/projects/{project_id}/services/{service_catalog_code}
* __methods:__ ['DELETE', 'OPTIONS']
* __type:__ object

Allows to delete consumer token

### Code Example:

#### DELETE:
#### Request:

```bash
    #bash
    curl \
         --request DELETE                                                               \
         --header "Content-Type: application/json"                                    \
         --header "AUTHORIZATION: sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs" \
         https://api_baseurl/api/v1/consumer-tokens/{consumer_token}/projects/{project_id}/services/{service_catalog_code}

```

```python
    #python
    import requests
    import json

        header = {
                    "Content-Type": "application/json",
                    "AUTHORIZATION": "sdfjskdjhsrk3hfksejhfksefhskefhskeh12123kjhkasdhaıs"
                  }
        req = requests.delete("https://api_baseurl/api/v1/consumer-tokens/{consumer_token}/projects/{project_id}/services/{service_cagalog_code},
                            header=header, data=json.dumps(body))

```

### Response:
201 Created.
```json

```

### Params
| Param   | type | default | required | details | spec | many | label |
|---------|------|---------|----------|---------|------|------|-------|
| indent | integer | 0 |  False |  JSON output indentation. Set to 0 if output should not be formated. |  None |  False |  None |

### Fields
| Field   | type | write_only | read_only | details | spec | label |
|---------|------|------------|-----------|---------|------|-------|
None



All rights reserved zops.io, generated at 26 Feb 2018 14:33
