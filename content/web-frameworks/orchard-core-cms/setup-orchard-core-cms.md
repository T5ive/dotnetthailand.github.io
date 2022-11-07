---
title: Setup Orchard Core CMS
showMetadata: true
editable: true
showToc: true
order: 1
---

# Install .NET 5
- Launch a new shell.
- Use the following commands to install .NET 5 on Ubuntu Linux 18.04.
  ```sh
    wget https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
    sudo dpkg -i packages-microsoft-prod.deb

    sudo apt-get update; \
      sudo apt-get install -y apt-transport-https && \
      sudo apt-get update && \
      sudo apt-get install -y dotnet-sdk-5.0
  ```

- To install .NET on other platforms/versions, please check https://docs.microsoft.com/en-us/dotnet/core/install/.
- Check .NET SDK version with a command:
  ```
    dotnet --list-sdks
  ```
- It should return `5.0.202 [/usr/share/dotnet/sdk]` or a newer version of .NET Framework.

# Install Orchard Template
- Use the following command to install a new project template
  It'll use [nightly build](https://github.com/OrchardCMS/OrchardCore/#build-status) packages.
  ```sh
    dotnet new -i "OrchardCore.ProjectTemplates::1.0.0-rc2-*" --nuget-source https://nuget.cloudsmith.io/orchardcore/preview/v3/index.json
  ```
- Create a new folder with name `orchard-example` as a root folder of your project.
- Inside the root folder, create a folder `src` to store the project's source code.
- CD To `orchard-example/src`.
- Use `dotnet new occms` command to create OrchardCore CMS project with name `OrchardExample.Cms`.
- You can change a project's name to any name that you want.
  ```sh
    mkdir -p orchard-example/src
    cd orchard-example/src
    dotnet new occms --name OrchardExample.Cms
  ```
# Open the project with VS Code
- CD back to the root folder (`codesanook-example`).
- Launch VS Code.
  ```sh
    $ cd orchard-example
    $ code .
  ```
# Add preview package source
- At root of the project, create `nuget.config` file.
- Add the following code to the file.
  ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <packageSources>
        <clear />
        <add key="NuGet" value="https://api.nuget.org/v3/index.json" />
        <add key="OrchardCorePreview" value="https://nuget.cloudsmith.io/orchardcore/preview/v3/index.json" />
      </packageSources>
      <disabledPackageSources />
    </configuration>
  ```
- *Warning*, we do not suggest you to use the dev packages in production.

# Project file structure
  ```sh
    $ tree -I "bin|obj" orchard-example
    orchard-example
    ├── nuget.config
    └── src
        └── OrchardExample.Cms
            ├── NLog.config
            ├── OrchardExample.Cms.csproj
            ├── Program.cs
            ├── Properties
            │   └── launchSettings.json
            ├── Startup.cs
            ├── appsettings.json
            └── wwwroot
  ```
# Launch a website
- Use VS Code integrated terminal by pressing **ctrl + `**
- CD to `src/OrchardExample.Cms` folder.
- Run the project with the following command:
  ```sh
    $ cd src/OrchardExample.Cms
    $ dotnet run
  ```
*Note*, please make sure you've saved all changes before running the command.
- FYI, `dotnet run` automatically download all Nuget packages so you don't need to explicitly run `dotnet restore`.
- Please refer to https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-run#implicit-restore for more information.

# Set up new Orchard CMS website
- Open a browser and navigate to http://localhost:5000.
- You will find Orchard Core CMS setup page.

![Orchard setup page](./images/orchard-setup-page.png)
- *Tip* you can put **chrome://flags/#allow-insecure-localhost** command setting in Chrome's address bar, enable that setting and relaunch Chrome to not show warning message on localhost.
- Set up a new website with any name you want and use **Blog recipe**.
- Use SQLite to simplify our project. For using it as production database, please check  https://www.sqlite.org/whentouse.html.
- *Note* If you are going to use other database types,  you need to create an empty database before setting up a website.**.
- Set admin username and email to any value you want.
- Click `Finish setup` button.
- You will be redirected to a home page.
- Go to an admin panel by navigating to http://localhost:5000/admin and log in with your admin's username and password.

# Example of a home page with blog recipe
![](images/orchard-core-cms-home-page.png)

# Example of an admin page
![](images/orchard-core-cms-admin-page.png)

# All Orchard Core Cms Templates
- You can use `dotnet new` for listing all installed templates, and you can select by using `Short Name` of the template.

# Update Orchard Core CMS template
- Execute the following command to update Orchard Core CMS template:
  ```sh
    dotnet new --install OrchardCore.ProjectTemplates::1.3.0
  ```

```
Templates                                     Short Name      Language    Tags
--------------------------------------------  --------------  ----------  ----------------------
Orchard Core Cms Module                       ocmodulecms     [C#]        Web/Orchard Core/CMS
Orchard Core Cms Web App                      occms           [C#]        Web/Orchard Core/CMS
Orchard Core Theme                            octheme         [C#]        Web/Orchard Core/CMS
Orchard Core Mvc Module                       ocmodulemvc     [C#]        Web/Orchard Core/Mvc
Orchard Core Mvc Web App                      ocmvc           [C#]        Web/Orchard Core/Mvc
```

For example:
**Orchard Core Cms Web App Template** to create a new Orchard Core CMS website project.
```sh
  $ dotnet new occms --name [PROJECT_NAME]
```
