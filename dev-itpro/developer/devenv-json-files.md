---
title: "JSON Files"
description: "Description of the settings of the app and launch JSON files for AL in Business Central."
author: SusanneWindfeldPedersen
ms.custom: na
ms.date: 04/01/2019
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
ms.assetid: a0ac492d-e3c8-4a76-87b4-b469e08c58e7
ms.author: solsen
---

# JSON Files

In an AL project there are two JSON files; the `app.json` file and the `launch.json` file. These files are generated automatically when you start a new project. The `app.json` file contains information about extension that you are building, such as publisher information and specifies the minimum version of base application objects that the extension is built on. Often the `app.json` file is referred to as the manifest. The `launch.json` file contains information about the server that the extension launches on.

## <a name="Appjson"></a>App.json file
The following table describes the settings in the `app.json` file:

|Setting|Mandatory|Value|
|-------|---------|-----|
|id|Yes|The unique ID of the extension. When app.json file is automatically created, the ID is set to a new GUID value.|
|name|Yes|The unique extension name.|
|publisher|Yes|The name of your publisher, for example: **NAV Partner**, **LLC** |
|brief|No, but required for AppSource submission|Short description of the extension.|
|description|No, but required for AppSource submission|Longer description of the extension.|
|version|Yes|The version of the app package.|
|privacyStatement|No, but required for AppSource submission|URL to the privacy statement for the extension.|
|EULA|No, but required for AppSource submission|URL to the license terms for the extension.|
|help|No, but required for AppSource submission|URL to an online description of the extension. The link is used in AppSource and can be the same as the value of the `contextSensitiveHelpUrl` property or a different link, such as a link to your marketing page.|
|url|No|URL of the extension package.|
|logo|No, but required for AppSource submission|Relative path to the app package logo from the root of the package.|
|dependencies|No|List of dependencies for the extension package. For example: `"dependencies": [ {  "appId": "4805fd15-75a5-46a2-952f-39c1c4eab821", "name": "WeatherLibrary", "publisher": "Microsoft", "version": "1.0.0.0"},{}]`|
|screenshots|No|Relative paths to any screenshots that should be in the extension package.|
|platform|Yes, if system tables are referenced in the extension|The minimum supported version of the platform symbol package file, for example: "11.0.0.0". See the [Symbols](devenv-symbols.md) for the list of object symbols contained in the platform symbol package file.|
|application|Yes, if base application objects are extended or referenced. The AL package will be compiled against the application that is present on the server that you connect to. This allows you to write a single [!INCLUDE[d365al_ext_md](../includes/d365al_ext_md.md)] for multiple country versions as long as you *do not* depend on country-specific code. If you *do* depend on country-specific code you should only try to compile your app against a server set up for that country.|The minimum supported version, for example: `"application": "11.0.0.0"`|
|idRange|Yes|For example: `"idRange": {"from": 50100,"to": 50149}`. A range for application object IDs. For all objects outside the range, a compilation error will be raised. When you create new objects, an ID is automatically suggested.|
|idRanges|Yes|For example: `"idRanges": [{"from": 50100,"to": 50200},{"from": 50202,"to": 50300}]`. A list of ranges for application object IDs. For all objects outside the ranges, a compilation error will be raised. When you create new objects, an ID is automatically suggested. You must use *either* the `idRange` *or* the `idRanges` setting. Overlapping ranges are not allowed and will result in a compilation error. |
|showMyCode|No|This is by default set to `false` and not visible in the manifest. To enable viewing the source code when debugging into an extension, add the following setting: `"showMyCode": true`|
|target|No|By default this is `Extension`. For Dynamics NAV, you can set this to `Internal` to get access to otherwise restricted APIs and .NET Interop. The Dynamics NAV Server setting must then also be set to `Internal`.|
|contextSensitiveHelpUrl|No, but required for AppSource submission|The URL for the website that displays context-sensitive Help for the objects in the app, such as `https://mysite.com/documentation`.|
|helpBaseUrl|No|The URL for the website that overtakes all Help for the specified locales. This property is intended for localization apps specifically since the setting overwrites the default URL of `https://docs.microsoft.com/{0}/dynamics365/business-central`.|
|supportedLocales|No|The list of locales that are supported for looking up Help. The value on the list is inserted into the URL defined in the `contextSensitiveHelpUrl` and `helpBaseUrl` properties. The first locale on the list is default. An example is `"supportedLocales": ["da-DK", "en-US"]`.|
|runtime|Yes|The version of the runtime that the project is targeting. The project can be published to the server with an earlier or the same runtime version. The available options are: `1.0` - Business Central April 2018 release, `2.2` - Business Central October 2018 release CU 2, and `3.0` - Business Central April 2019 release.|

## <a name="Launchjson"></a>Launch.json file

The following table describes the settings in the `launch.json` file. The `launch.json` file has two configurations depending on whether the extension is published to a local server or to the cloud.

### Publish to local server settings
|Setting|Mandatory|Value|
|-------|---------|-----|
|name|Yes|"Publish to your own server"|
|type|Yes|Must be set to `".al"`. Required by Visual Studio Code.|
|request|Yes|Request type of the configuration. Must be set to `"launch"`. Required by Visual Studio Code.|
|server|Yes|The HTTP URL of your server, for example: `"http://localhost|serverInstance"`|
|port|No|The port assigned to the development service.|
|serverInstance|Yes|The instance name of your server, for example: `"US"`|
|authentication|Yes|Specifies the server authentication method and can be set to `"UserPassword"`, `"Windows"`, or `"AAD"`. Currently, AAD authentication is supported only for [!INCLUDE[d365fin_long_md](includes/d365fin_long_md.md)] sandboxes. AAD authentication cannot be used for on-premise servers.|
|startupObjectType|No|Specifies whether the object to open after publishing is a Page type (`"Page"`) or Table type (`"Table"`) object. The default is `"Page"`.|
|startupObjectId|No|Specifies the ID of the object to open after publishing. Only objects of type Page and Table are currently supported.|
|schemaUpdateMode|No|Specifies the data synchronization mode when you publish an extension to the development server, for example: <br>`"schemaUpdateMode": "Recreate"`</br> The default value is Synchronize. For more information, see [Retaining table data after publishing](devenv-retaining-data-after-publishing.md)  <br>[!INCLUDE[nav_not_supported](includes/nav_not_supported.md)]  |
|breakOnError | No |Specifies whether to break on errors when debugging. The default value is `true`. | 
|breakOnRecordWrite | No |Specifies if the debugger breaks on record changes. The default value is `false`.| 
|launchBrowser|No|Specifies whether to open a new tab page in the browser when publishing the AL extension (Ctrl+F5). The default value is `false`. If the value is not specified or set to `true`, the session is started. If the value is explicitly set to `false`, the session is not started unless you launch your extension in debugging mode.|

### Publish to cloud settings
|Setting|Mandatory|Value|
|-------|---------|-----|
|name|Yes|"Publish to Microsoft cloud sandbox"|
|type|Yes|Must be set to `".al"`. Required by Visual Studio Code.|
|request|Yes|Request type of the configuration. Must be set to `"launch"`. Required by Visual Studio Code.|
|startupObjectType|No|Specifies whether the object to open after publishing is a Page type (`"Page"`) or Table type (`"Table"`) object.  The default is `"Page"`.|
|startupObjectId|No|Specifies the ID of the object to open after publishing. Only objects of type Page and Table are currently supported.|
|tenant|No|Specifies the tenant to which the package is deployed. If you specify multiple configurations, a drop-down of options will be available when you deploy. This parameter must contain a tenant AAD domain name, for example `mycustomer.onmicrosoft.com`.|
|sandbox|No|Specifies which sandbox to use in cases where multiple sandboxes are owned by the same tenant.|

## The platform symbol file
The platform symbol file contains all of the base app objects that your extension builds on. If the [!INCLUDE[d365al_ext_md](../includes/d365al_ext_md.md)] in Visual Studio Code detects that the referenced symbols are not present on local disk, you will get a visual prompt in Visual Studio Code to download the symbols from one of the servers specified in the launch.json file. For more information about the platform symbol file, see [Symbols](devenv-symbols.md).

## See Also
[AL Development Environment](devenv-reference-overview.md)  
[Debugging in AL](devenv-debugging.md)  
[Security Setting and IP Protection](devenv-security-settings-and-ip-protection.md)  
[Configure Context-Sensitive Help](../help/context-sensitive-help.md)  
