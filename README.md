---
page_type: sample
languages:
- java
products:
- azure-active-directory
description: "Stateless authentication filter Sample project for Azure AD Spring Boot Starter client library"
urlFragment: "azure-spring-boot-sample-active-directory-resource-server-by-filter-stateless"
---

# Stateless authentication filter sample for Azure AD Spring Boot Starter client library for Java


## Getting started
The sample is composed of two layers: vue.js client and Spring Boot RESTful Web Service. You need to make some changes 
to get it working with your Azure AD tenant on both sides.


### Register your application with your Azure Active Directory Tenant

Follow the guide [here](https://docs.microsoft.com/azure/active-directory/develop/v1-protocols-openid-connect-code#register-your-application-with-your-ad-tenant).

### Configure appRoles

In order to use only the `id_token` for our authentication and authorization purposes we will use the
`appRoles` feature which AAD provides. Follow the guide 
[Add app roles in your application](https://docs.microsoft.com/azure/active-directory/develop/howto-add-app-roles-in-azure-ad-apps)

For the test SPA provided with this example you should create the following roles in your manifest:

```
  "appRoles": [
    {
      "allowedMemberTypes": [
        "User"
      ],
      "displayName": "Admin",
      "id": "2fa848d0-8054-4e11-8c73-7af5f1171001",
      "isEnabled": true,
      "description": "Full admin access",
      "value": "Admin"
    },
    {
      "allowedMemberTypes": [
        "User"
      ],
      "displayName": "User",
      "id": "f8ed78b5-fabc-488e-968b-baa48a570001",
      "isEnabled": true,
      "description": "Normal user access",
      "value": "User"
    }
  ],
```

After you've created the roles go to your Enterprise Application in Azure Portal, select "Users and groups" and 
assign the new roles to your Users (assignment of roles to groups is not available in the free tier of AAD).

Furthermore enable the implicit flow in the manifest for the demo application 
(or if you have SPAs calling you):

```
"oauth2AllowImplicitFlow": "true",
```

## Examples
### Configure the sample

### Run with Maven
```shell
cd azure-spring-boot-samples/aad/azure-spring-boot-starter-active-directory/aad-resource-server-by-filter-stateless
mvn spring-boot:run
```

### Check the authentication and authorization
	
1. Access http://localhost:8080
2. Without logging in try the three endpoints (public, authorized and admin). While the public 
   endpoint should work without a token the other two will return a 403.
3. Insert your `client-id` and `tenant-id` and perform a log in. If successfull the token textarea
   should get populated. Also the token header and token payload field will be populated.   
4. Again access the three endpoints. Depending on your user and the assigned `appRoles` you should
   be able to call the authorized and admin endpoints.
   
## Troubleshooting
## Next steps
## Contributing
<!-- LINKS -->

