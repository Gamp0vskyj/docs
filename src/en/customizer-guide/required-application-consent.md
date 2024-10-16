
# Applications

| Name | Consent Link | Owner | Client ID |
| - | - | - | - |
| [TALXIS Deployments](#talxis-deployments) | [LINK](https://talxis.com/add-deployment-app) | INT0006 | 4ab337b1-27bc-421d-8d56-7462bbea9831
| [TALXIS Data Feed](#talxis-data-feed) | [LINK](https://login.microsoftonline.com/common/adminconsent?client_id=e8af2b8e-a8de-4669-8d94-6b684068beef) | INT0010 | e8af2b8e-a8de-4669-8d94-6b684068beef
| [TALXIS Data Feed - Flow](#talxis-data-feed---flow) | [LINK](https://talxis.com/add-connectors-app) | INT0010 | 28d529aa-b85e-4469-9cf3-937bea582555
| [TALXIS - PCF.MapPicker](#talxis---pcfmappicker) | [LINK](https://login.microsoftonline.com/common/adminconsent?client_id=1dc2b128-6003-42b6-a989-d78d6c0d0a5c) | INT0015 | 1dc2b128-6003-42b6-a989-d78d6c0d0a5c
| [TALXIS - PCF.FilePicker](#talxis---pcffilepicker) | [LINK](https://talxis.com/add-dms-app) | INT0015 | 1fd1cbbe-eefe-4583-b422-4a7661cf5c60
| [TALXIS - PCF.FilePicker - Group Creation](#talxis---pcffilepicker---group-creation) | [LINK](https://login.microsoftonline.com/common/adminconsent?client_id=6fc7f36a-b972-45c9-8516-06c0600b4183) | INT0015 | 6fc7f36a-b972-45c9-8516-06c0600b4183
| [TALXIS - PCF.FilePicker - Advanced Permissions](#talxis---pcffilepicker---advanced-permissions) | [LINK](https://login.microsoftonline.com/common/adminconsent?client_id=a6631d2e-c9f0-4327-ba73-5fc8cb87a037) | INT0015 | 6fc7f36a-b972-45c9-8516-06c0600b4183
| [TALXIS - PCF.CompanyProfileHinting](#talxis---pcfcompanyprofilehinting) | [LINK](https://talxis.com/add-controls-app) | INT0015 | b8becf32-7f36-4d2f-bbdc-456c6e910405
| [TALXIS - PCF.AddressPicker](#talxis---pcfaddresspicker) | [LINK](https://login.microsoftonline.com/common/adminconsent?client_id=7941f3c9-f4db-441d-9fce-7b3eb7a2ef10) | INT0015 | 7941f3c9-f4db-441d-9fce-7b3eb7a2ef10
| [TALXIS - Client](#talxis---client) | [LINK](https://login.microsoftonline.com/common/adminconsent?client_id=526f3cf8-fd5c-4648-87f6-b0e4b986acdb) | INT0015 | 526f3cf8-fd5c-4648-87f6-b0e4b986acdb
| [TALXIS - PCF.PeopleGrid](#talxis---pcfpeoplegrid) | [LINK](https://login.microsoftonline.com/common/adminconsent?client_id=7facec0a-d26e-4f71-a213-38b317b4dfe0) | INT0015, PCT21016 | 7facec0a-d26e-4f71-a213-38b317b4dfe0

# Why Do We Need Theese Consents
Until now we have been using standalone authentication per [PFC](https://netwiseglobal.com/blog/2024/03/15/what_are_pcf_components_and_how_do_they_help_users_and_developers/) control. 

The issue is, that when [3rd party cookies are blocked in the browser](https://cookie-script.com/all-you-need-to-know-about-third-party-cookies.html) (Safari by default, you can enable this behavior in other browsers as well). This effectively breaks any silent [SSO](https://gatekeeperhelp.zendesk.com/hc/en-us/articles/1500003649281-What-is-Silent-Authentication) method in OpenID Connect (via MSAL.js for example) which uses iframe behind the scenes to obtain the token, and you will end up with [AADSTS50058](https://github.com/AzureAD/microsoft-authentication-library-for-js/issues/4782) error.
This issue is not just Microsoft auth stack related, but is also faced by other including [Salesforce](https://help.salesforce.com/s/articleView?id=sf.external_identity_login_considerations.htm&type=5) and Microsoft Dynamics. More perspective on this issue from AAD [here](https://learn.microsoft.com/en-us/azure/active-directory/develop/reference-third-party-cookies-spas).

# Details
Preview of permissions could be found [here](https://learn.microsoft.com/en-us/graph/permissions-reference).
## TALXIS Deployments

Used for deployments of applications to Power Platform environment. Application can only write to environments where permissions have been [explicitly granted to the service principal](https://learn.microsoft.com/en-us/power-platform/admin/manage-application-users). The principal is non-interactive.

### Permissions
* Access Common Data Service (Dataverse) as organization user
* Sign in and read user profile

## TALXIS Data Feed

Used as a resource to verify TALXIS Data Feed access. Doesn't need to be explicitly consented.

## TALXIS Data Feed - Flow

Enables use of TALXIS Data Feed API from Power Automate.

### Permissions
* Access Data Feed as Current User
* Sign in and read user profile

## TALXIS - PCF.MapPicker

Map control used in TALXIS applications.

### Permissions
* Access Data Feed as Current User
* Sign in and read user profile

## TALXIS - PCF.FilePicker

Custom control that allows users to work with SharePoint or Dataverse documents easily and directly from TALXIS applications. Optionally complemented with [TALXIS - PCF.FilePicker - Group Creation](#talxis---pcffilepicker---group-creation) application.

### Permissions
* Read items in all site collections
* Have full access to all files user can access
* Have full access to user files
* Read all groups
* Sign in and read user profile

## TALXIS - PCF.FilePicker - Group Creation

Optional app registration if you want the File Picker PCF to allow for group creation via UI. Primarily used in the previous version of File Picker.

### Permissions
* Read and write all groups
* Read and write group memberships
* Sign in and read user profile

## TALXIS - PCF.FilePicker - Advanced Permissions

TBD

## TALXIS - PCF.CompanyProfileHinting

Company autosuggest control used in TALXIS applications.

### Permissions
* Access Data Feed as Current User
* Sign in and read user profile

## TALXIS - PCF.AddressPicker

Address autosuggest control used in TALXIS applications.

### Permissions
* Access Data Feed as Current User
* Sign in and read user profile

## TALXIS - Client

Used in an [authentication broker (internal)](https://dev.azure.com/thenetworg/INT0015/_wiki/wikis/INT0015.wiki/4301/Authentication-Flow?anchor=authentication-broker) scenario, where a token is required from PCF or custom code. It prevents users from getting multiple authentication popups due to 3rd party cookie restrictions.

## TALXIS - PCF.PeopleGrid

* INT0015 - PoepleGrid connects accounts with contacts and allows tracking of additional metadata such as contact's function withing specified account from Data Feed.
* PCT21016 - PoepleGrid connects accounts with contacts and allows tracking of extensive amount of metadata from Data Feed.

### Permissions
* Access Data Feed as Current User
* Sign in and read user profile
