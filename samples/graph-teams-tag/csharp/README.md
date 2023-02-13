---
page_type: sample
description: This is a sample application which demonstrates how to use CRUD Graph operations related to team tags.
products:
- office-teams
- office
- office-365
languages:
- csharp
extensions:
 contentType: samples
 createdDate: "06/24/2022 12:00:00 AM"
urlFragment: officedev-microsoft-teams-samples-graph-teams-tag-csharp
---

# This is a sample application that shows the usage of Graph CRUD operations related to team tags.

This is a sample application where user can create, update, add or remove members of a tag. All of Graph CRUD operations related to tags can be performed within this sample.

## Interaction with app

![Create new tag](GraphTeamsTag/Images/CreateTagFlow.gif)

![View/Edit tag](GraphTeamsTag/Images/ViewOrEditTagFlow.gif)

## Prerequisites

- Microsoft Teams is installed and you have an account (not a guest account)
-  .[NET 6.0](https://dotnet.microsoft.com/en-us/download) SDK.
    ```bash
        # determine dotnet version
        dotnet --version
    ```
-  [ngrok](https://ngrok.com/) or equivalent tunneling solution
-  [M365 developer account](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant) or access to a Teams account with the appropriate permissions to install an app.

## Setup

1) Register your application with Azure AD

1. Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.
2. On the overview page, copy and save the **Application (client) ID, Directory (tenant) ID**. You’ll need those later when updating your Teams application manifest and in the appsettings.json.
3. Navigate to **API Permissions**, and make sure to add the follow permissions:
-   Select Add a permission
-   Select Microsoft Graph -> Application permissions.
   - `TeamworkTag.ReadWrite.All`

-   Click on Add permissions. Please make sure to grant the admin consent for the required permissions.

4.  Navigate to the **Certificates & secrets**. In the Client secrets section, click on "+ New client secret". Add a description (Name of the secret) for the secret and select “Never” for Expires. Click "Add". Once the client secret is created, copy its value, it need to be placed in the appsettings.json file.

> Note these instructions are for running the sample on your local machine, the tunnelling solution is required because
> the Teams service needs to call into the app.

5. Create a [Azure Bot resource](https://docs.microsoft.com/en-us/azure/bot-service/bot-service-quickstart-registration).
- For bot handle, make up a name.
    - Select "Use existing app registration" (Create the app registration in Azure Active Directory beforehand.)
    - __*If you don't have an Azure account*__ create an [Azure free account here](https://azure.microsoft.com/en-us/free/)
    
   In the new Azure Bot resource in the Portal, 
    - Ensure that you've [enabled the Teams Channel](https://learn.microsoft.com/en-us/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0)
    - In Settings/Configuration/Messaging endpoint, enter the current `https` URL you were given by running ngrok. Append with the path `/api/messages`

2) Clone the repository
   ```bash
   git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
   ```

3) Launch Visual Studio
   - File -> Open -> Project/Solution
   - Navigate to folder where repository is cloned then `samples/graph-teams-tag/csharp/GraphTeamsTag.sln`
    
4) Start ngrok on localhost:3978
- Open ngrok and run command `ngrok http -host-header=rewrite 3978` 
- Once started you should see link `https://xxxxx.ngrok.io`. Copy it, this is your baseUrl that will used as endpoint for Azure bot.

![Ngrok](GraphTeamsTag/Images/NgrokScreenshot.png)

5) Update appsettings.json
Update configuration with the ```MicrosoftAppId```,  ```MicrosoftAppPassword``` and ```MicrosoftAppTenantId``` with the values generated while doing AAD app registration in Azure Portal.

6) Run the bot from Visual Studio: 
   - Press `F5` to run the project

7) Setup the `manifest.json` in the `/AppPackage` folder 
Replace the following details:
- `{{APP-ID}}` with any GUID id value or your MicrosoftAppId.
- `{{BASE-URL}}` with base Url domain. E.g. if you are using ngrok it would be `https://1234.ngrok.io` then your domain-name will be `1234.ngrok.io`.
- **Zip** up the contents of the `Manifest` folder to create a `manifest.zip`
- **Upload** the `manifest.zip` to Teams (in the Apps view click "Upload a custom app")

## Running the sample

**User can see list of tags created for the current team.**
![Manage Tag Dashboard](GraphTeamsTag/Images/Dashboard.png)

**User can view/edit the existing team tags.**
![View/Edit Tags](GraphTeamsTag/Images/ViewOrEditTag.png)

**User can create new team tags.**
![Create new Tag](GraphTeamsTag/Images/CreateTagTaskModule.png)

**User can delete existing team tags.**

## Further reading
- [TeamworkTag resource type](https://docs.microsoft.com/en-us/graph/api/resources/teamworktag?view=graph-rest-beta)
