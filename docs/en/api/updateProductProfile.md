---
title: Update Product Profiles
layout: default
nav_link: Update Product Profile
nav_order: 475
nav_level: 4
lang: en
---
# <a name="updateProfile" class="api-ref-title">Update Product Profile</a>

**DEPRECATED:** These APIs have been deprecated. Please refer to the [User Management Action API](ActionsRef.md) for details on the supported approach to assign and manage membership and administrative rights within your Organization.

<hr class="api-ref-rule">

```
POST [UM_Server]/{orgId}/products/{productId}/configurations/{profileId}
```
Manage membership and administrative rights for a specific product profile in a POST request to the profile endpoint. Use this API to grant or revoke the Product Profile Admin role for one or more users.

* [Parameters](#parameters)
* [Request Body](#requestBody)
* [Responses](#responses)
* [Example Requests](#example)
* [Throttling Limits](#throttle)

## <a name="parameters" class="api-ref-subtitle">Parameters</a>
This table summarizes the parameters and how they are provided:

| Name | Type | Required | Description |
| :--- | :------ | :---: | :------ |
| orgId | path | true | {% include_relative partials/orgIdDescription.md %} |
| productId | path | true | The ID of the product. |
| profileId | path | true | The ID of the product profile. |
| x-api-key | header | true | {% include_relative partials/apiKeyDescription.md %} |
| Authorization | header | true | {% include_relative partials/authorizationDescription.md %} |
| Content-type | header | false | {% include_relative partials/contentTypeDescription.md %} |
| X-Request-Id | header | false | {% include_relative partials/requestIdDescription.md %} |
{:.bordertablestyle}

## <a name="requestBody" class="api-ref-subtitle">Request Body</a>

The JSON payload specifies lists of users and user groups to add or remove from membership, and users for whom to add or remove the admin role. You only need to specify the lists you are modifying.

| Name |   Description |
| :--- | :------- |
| addUsers | A list of users to be added to this profile. |
| removeUsers | A list of users to be removed from this profile.  |
| addUserGroups | A list of user groups to be added to this profile. |
| removeUserGroups | A list of user groups to be removed from this profile.  |
| addAdminUsers | A list of users that are to be granted the ProductAdmin role for this profile. |
| removeAdminUsers | A list of users for whom the ProductAdmin role is to be removed for this profile. |
{:.bordertablestyle}

### Example

```json
{
    "addUsers": [
        "a.smith@myCompany.com"
    ],
    "removeUsers": [
        "b.jones@myCompany.com"
    ],
    "addUserGroups": [
        "UMSDK User Group"
    ],
    "removeUserGroups": [
        "UMSDK User Group 2"
    ],
    "addAdminUsers" : [
        "jdoe@myCompany.com"
    ],
    "removeAdminUsers": [
        "ann.other@myCompany.com"
    ]
}
```
## <a name="responses" class="api-ref-subtitle">Responses</a>

__Content-Type:__ _application/json_

- [200: OK](#200updateUserGroup)
- [400: Bad Request](#400updateUserGroup)
- [401: Unauthorized](#401updateUserGroup)
- [403: Forbidden](#403updateUserGroup)
- [429: Too Many Requests](#throttle)

### <a name="200updateUserGroup" class="api-ref-subtitle">200 OK</a>
The response body contains the updated product in JSON format.

{% include_relative partials/badRequest.md object="user-group" anchor="400updateUserGroup" %}

{% include_relative partials/unauthorized.md anchor="401updateUserGroup" %}

{% include_relative partials/forbidden.md anchor="403updateUserGroup" %}

## <a name="throttle" class="api-ref-subtitle">Throttling</a>

{% include_relative partials/throttling.md client=5 global=50 %}
