---
title: Azure Active Directory Graph API | Microsoft Docs
description: An overview and quickstart guide for Azure AD Graph API which allows programmatic access to Azure AD through REST API endpoints.
services: active-directory
documentationcenter: ''
author: mtillman
manager: mtillman
editor: mbaldwin

ms.assetid: 5471ad74-20b3-44df-a2b5-43cde2c0a045
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/02/2018
ms.author: mtillman
ms.custom: aaddev

---
# Azure Active Directory Graph API
> [!IMPORTANT]
> We strongly recommend that you use [Microsoft Graph](https://graph.microsoft.io/) instead of Azure AD Graph API to access Azure Active Directory resources. Our development efforts are now concentrated on Microsoft Graph and no further enhancements are planned for Azure AD Graph API. There are a very limited number of scenarios for which Azure AD Graph API might still be appropriate; for more information, see the [Microsoft Graph or the Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) blog post in the Office Dev Center.
> 
> 

The Azure Active Directory Graph API provides programmatic access to Azure AD through REST API endpoints. Applications can use Azure AD Graph API to perform create, read, update, and delete (CRUD) operations on directory data and objects. For example, Azure AD Graph API supports the following common operations for a user object:

* Create a new user in a directory
* Get a user’s detailed properties, such as their groups
* Update a user’s properties, such as their location and phone number, or change their password
* Check a user’s group membership for role-based access
* Disable a user’s account or delete it entirely

Additionally, you can perform similar operations on other objects such as groups and applications. To call Azure AD Graph API on a directory, your application must be registered with Azure AD. Your application must also be granted access to Azure AD Graph API. This access is normally achieved through a user or admin consent flow.

To begin using the Azure Active Directory Graph API, see the [Azure AD Graph API Quickstart Guide](active-directory-graph-api-quickstart.md), or view the [interactive Azure AD Graph API reference documentation](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## Features
Azure AD Graph API provides the following features:

* **REST API Endpoints**: Azure AD Graph API is a RESTful service comprised of endpoints that are accessed using standard HTTP requests. Azure AD Graph API supports XML or Javascript Object Notation (JSON) content types for requests and responses. For more information, see [Azure AD Graph REST API Reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
* **Authentication with Azure AD**: Every request to Azure AD Graph API must be authenticated by appending a JSON Web Token (JWT) in the Authorization header of the request. This token is acquired by making a request to Azure AD’s token endpoint and providing valid credentials. You can use the OAuth 2.0 client credentials flow or the authorization code grant flow to acquire a token to call the Graph. For more information, [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* **Role-Based Authorization (RBAC)**: Security groups are used to perform RBAC in Azure AD Graph API. For example, if you want to determine whether a user has access to a specific resource, the application can call the [Check Group Membership (transitive)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/functions-and-actions#checkMemberGroups) operation, which returns true or false.
* **Differential Query**: Differential query allows you to track changes in a directory between two time periods without having to make frequent queries to Azure AD Graph API. This type of request will return only the changes made between the previous differential query request and the current request. For more information, see [Azure AD Graph API Differential Query](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-differential-query).
* **Directory Extensions**: ou can add custom properties to directory objects without requiring an external data store. For example, if your application requires a Skype ID property for each user, you can register the new property in the directory and it will be available for use on every user object. For more information, see [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions).
* **Secured by permission scopes**: Azure AD Graph API exposes permission scopes that enable secure access to Azure AD data using OAuth 2.0. It supports a variety of client app types, including:
  
  * user interfaces that are given delegated access to data via authorization from the signed-in user (delegated)
  * service/daemon applications that operation in the background without a signed-in user being present and use application-defined role-based access control
    
    Both delegated and application permissions represent a privilege exposed by the Azure AD Graph API and can be requested by client applications through application registration permissions features in the [Azure portal](https://portal.azure.com). [Azure AD Graph API Permission Scopes](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes) provides information on what's available for use by your client application.

## Scenarios
Azure AD Graph API enables many application scenarios. The following scenarios are the most common:

* **Line of Business (Single Tenant) Application**: In this scenario, an enterprise developer works for an organization that has an Office 365 subscription. The developer is building a web application that interacts with Azure AD to perform tasks such assigning a license to a user. This task requires access to Azure AD Graph API, so the developer registers the single tenant application in Azure AD and configures read and write permissions for Azure AD Graph API. Then the application is configured to use either its own credentials or those of the currently sign-in user to acquire a token to call Azure AD Graph API.
* **Software as a Service Application (Multi-Tenant)**: In this scenario, an independent software vendor (ISV) is developing hosted multi-tenant web application that provides user management features for other organizations that use Azure AD. These features require access to directory objects, and so the application needs to call Azure AD Graph API. The developer registers the application in Azure AD, configures it to require read and write permissions for Azure AD Graph API, and then enables external access so that other organizations can consent to use the application in their directory. When a user in another organization authenticates to the application for the first time, they are shown a consent dialog with the permissions the application is requesting.  Granting consent will then give the application those requested permissions to Azure AD Graph API in the user’s directory. For more information on the consent framework, see [Overview of the Consent Framework](active-directory-integrating-applications.md).

## See Also
[Azure AD Graph API Quickstart Guide](active-directory-graph-api-quickstart.md)

[Azure AD Graph REST documentation](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)

[Azure Active Directory developer's guide](active-directory-developers-guide.md)

