# Customizing "modern" site pages
During autumn 2016 the "modern" page experience was released by the SharePoint team. Modern team site pages are fast, easy to author and support rich multimedia content. And pages look great on any device, in a browser or from within the SharePoint mobile app. This article focuses on the extensibility options there are in the "modern" page experience, if you however want to learn more about the functionalities offered by the "modern" experiences then following links will help:
 - New capabilities in SharePoint Online team sites: https://blogs.office.com/2016/08/31/new-capabilities-in-sharepoint-online-team-sites-including-integration-with-office-365-groups

In remainder of this article we'll use "modern" for the new user experience and "classic" for the legacy user experience. 

>**Important:** 
We're not deprecating the "classic" experience, both "classic" and "modern" will coexist.

_**Applies to:** SharePoint Online_


## Overview of the customization options
Below table gives a quick overview of the supportability of "modern" pages, in this article we'll provide more details and examples on the supported options. The SharePoint team is working to support more options in the future.

| **Not Supported** | **Supported options** |
|:-----|:-----|
| Alternative layouts| Custom branding  |
| Custom page templates (layout templates) |   |
| Custom CSS via AlternateCSSUrl web property |  |
| Custom JavaScript embedded via User Custom Actions |  |
| Custom master pages |  |
| Minimal Download Strategy (MDS) |  |
| SharePoint Server Publishing |  |


## Custom branding
<a name="themingimpact"> </a>
If you're site happens to use a custom theme then this custom theme will be respected in the "modern" page experience as shown in below sample:

![Modern page with custom branding coming from theme settings](media/modern-experiences/modern-page-with-custom-theme.png)

## How to configure the end user experience
<a name="configuremodernpages"> </a>
You do have multiple options to control whether the "modern" or "classic" page experience will be used. 

### Tenant level configuration
If you completely want to disable the "modern" experience then it's best to use the tenant setting for this. navigate to your tenant admin center (e.g. contoso-admin.sharepoint.com), go to settings and select the "classic" experience:

![Site Pages section in the SharePoint tenant scoped settings in admin UI](media/modern-experiences/site-pages-setting-admin-ui.png)

>**Notes:**
> - The tenant level setting is a little bit confusing: "Preventing users from creating Site Pages" will actually bring back the "classic" experience.
> - The current configuration is cached, logging off the session will immediately show the effect of this change

### Site level configuration
You can prevent a site collection or web to use the "modern" page experience by disabling a feature the site collection scoped feature with ID **B6917CB1-93A0-4B97-A84D-7CF49975D4EC**. To again enable the "modern" page experience at site level you'll need to activate the feature again

You can use below PnP provisioning XML to **disable** this feature on your site collection:

```XML
<pnp:ProvisioningTemplate ID="disablemodernpages" Version="1" xmlns:pnp="http://schemas.dev.office.com/PnP/2015/12/ProvisioningSchema">
  <pnp:Features>
    <pnp:SiteFeatures>
      <pnp:Feature ID="B6917CB1-93A0-4B97-A84D-7CF49975D4EC" Deactivate="true" Description="Disable modern list experience"/>
    </pnp:SiteFeatures>
  </pnp:Features>
</pnp:ProvisioningTemplate>
```

You can use below PnP provisioning XML to **enable** this feature on your site collection:

```XML
<pnp:ProvisioningTemplate ID="enablemodernpages" Version="1" xmlns:pnp="http://schemas.dev.office.com/PnP/2015/12/ProvisioningSchema">
  <pnp:Features>
    <pnp:SiteFeatures>
      <pnp:Feature ID="B6917CB1-93A0-4B97-A84D-7CF49975D4EC" Description="Disable modern list experience"/>
    </pnp:SiteFeatures>
  </pnp:Features>
</pnp:ProvisioningTemplate>
```

Use following PnP PowerShell to apply this template:

```PowerShell
Connect-PnPOnline -Url <url_to_your_SharePoint_Online_site>
Apply-PnPProvisioningTemplate -Path c:\experiencecontrol.xml -Handlers Features
```

## Additional resources
<a name="bk_addresources"> </a>

 - [Allow or prevent creation of site pages by end users](https://support.office.com/en-us/article/Allow-or-prevent-creation-of-site-pages-by-end-users-c41d9cc8-c5c0-46b4-8b87-ea66abc6e63b?ui=en-US&rs=en-US&ad=US)