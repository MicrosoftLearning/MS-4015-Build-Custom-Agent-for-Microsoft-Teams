
lab:
'Create a custom engine agent with Microsoft 365 Agents SDK'
---
<!--
Edit the metadata above to manage the list of exercises in the home page of the GitHub site that gets generated.
You can delete the module and edit index.md in the root of the repo to customize the display so that only the exercises are listed
To enable GitHub page publishing, edit the Page settings for the repo and publish from the main branch
-->

# Create and test a Custom Agent

In this exercise you will create an Azure OpenAI resource that serves as the foundation for creating your custom agent.

This exercise should take approximately **60** minutes to complete. <!-- update with estimated duration -->

**Note:** Learners can complete this lab with these options
1) A lab environment provided for the learners.
2) Learners are expected to complete this lab on their own environments for all other ALHs.

##  Task 1: Create Azure OpenAI resource 

First, you need to ...

1. Navigate to **https://portal.azure.com** in your edge browser.
1. Sign into the azure portal.
2. Click on **+ Create a resource** on the upper left hand  side of the screen.
1. In the search box type in **azure openai** and press enter.
1. A result called **Azure OpenAI** should appear as an option. At the bottom left hand corner of this option is a button labeled **Create**. Press> **Create** > **Aure OpenAI**.
1. Under the page **Create Azure OpenAI** set the following fields:

**Note:** For learners using their own environment, learners will have to use their own discretion when selecting values for fields **Subscription** , **Pricing Tier** and **Resource Group**. For learners using the provided lab environment, select the default values for the fields in steps a-d below.
   
   a. **Subscription** Use your own discretion when filling this field.
   
   b. **Resource Group** : Use your own discretion when filling this field.
   
   c. **Name** : Type in any name you choose.
   
   d. **Pricing tier**: the default value  is **Standard S0**, but Use your own discretion when filling this field.
   
Select **Next**.

7. Under the next page, in the **Network** tab, Select the option **All networks, including the internet, can access this resource.**
Select **Next**.
8. Under the next page in the **Tags** tab, leave the Name and Value fields blank.
Select **Next**.
9. Under the next page, in the **Review + submit** tab, press **Create**.
10. You will be taken to a page where this newly created Azure OpenAI resource is being created. You will see the words **Deployment in progress**. Wait for a few second for this resource to finish deploying. Once the resource is deployed, click on the button **Go to Resource**.
11. **Result:** You will now be in the page with newly created Azure OpenAI resource. You can verify by checking the name of the resource in the top left hand corner of the page. This name should match the name you chose for step 5c above.


## Task 2: Implement RAG for the Azure OpenAI model

In this task, you will learn how to implement RAG using a data source for your own test environment.

1. In the page for your newley created Azure OpenAI resource, click **Go to Azure AI Foundry portal** in the ribbon at the top of the page.
2. On the left hand side, under **Playgrounds**, select **Chat**. Now under page **Chat playground**, in the section called **Setup**, select **+ Create new deployment** .
3. In the pop up window titled **Select a chat completion model** scroll down and select the option **gpt-4** > **Confirm**.
4. In the **Deploy model gtp-4** window, leave everything in it's default setting and select **Deploy**.
5. In the **Chat playground** page, select **Add your data** located near the bottom of the screen > **+ Add a data source**.
6. In the **Select or add data source** window, select  the dropdown for **Select data source** and select **Upload files (preview)**.
7. In the next page for **Data source**, ensure the dropdown for **Select data source** is set to **Upload files (preview)**

**Notes:** For learners using their own environment, users may have to use your own discretion when filling out fields for steps a-c below. For Learners using the provided lab environment, follow use the default values as instructed in steps a-b below. 
  
   a. In the **Subscription** field, ensure the default value is selected.
   
   b. In the **Select Azure Blob storage resource** field, select **Create a new Azure Blob storage resource** > in the new window titled **Create a storage account**, under the **Basics** tab, ensure the fields **Subscription** and **Resource group** are set to the default values-choose the only value available for **Resource group**. Under **Instance details**, set a name for **Storage account name**. Leave the rest of the fields as is. Select **Review + create**. Under the **Review + create** tab, select the **Create** button. The Azure Blob Storage resource will take a moment to deploy.
   
   c. Navigate back to the window for **Chat playground**. Select the refresh button next to the field **Select Azure Blob storage resource** > select the resource you made in step b above. Select the button **Turn on CORS**.
   
8. For the field **Select Azure AI Search resource**, select  **Create a new Azure AI Search resource**.  Ensure the fields **Subscription** and **Resource group** are set to values of your choosing.

   **Note:** For learners using their on environment, please use your own discretion when selecting values for fields **Subscription** and, **Resource Group**.

9. Click the dropdown value for **Resource Group** to select the option of your choosing. Input a **Service name**> Ensure all other fields are set to it's default values > select **Review + create** > **Create**. The Azure AI Search resource will take a moment to deploy.
10. Navigate back to the window for **Chat playground**. Select the refresh button next to the field **Select Azure Blob storage resource** > select the resource you made in step 9 above.
11. Enter a name for the field **Enter the index name** > **Next**. Copy and paste this name somewhere accessible as you will need this in the upcoming tasks.
12. In the **Upload files** section, select **Browse for a file** > In the file explorer, navigate to **Documents** > select all three files: **ContosoAI ChipEnhance Perks Program.docx**, **ContosoAI Insurance Plans.docx**, and **Overview of ContosoAI.docx** > **Open** > the three file should now be present in the **Upload files** page of the window > select **Upload Files** > **Next**.
13. Under the **Data management** section, leave everything as default and select **Next**.
14. Under the**Data connection** select **API key** > **Next** > **Save and close**.
15. In the **Chat playground** window, select **View code** which is in the ribbon at the top left of the window.
16. In the **Sample code** window select the drop down to the right of the first field and select **json** > switch to the **Key authentification**tab:
    
    a. Copy and paste the following values, as you will need them in the upcoming tasks: **Endpoint**, **API key**, and **Azure Search Resource Key**. You can also leave this window open to collect these values for the upcoming tasks.

 ## Task 3: Create and test custom agent in Test Tool and Teams

In this task you will create the custom agent and test the agent.

1. Open **Visual Studio Code**.
2. In the right hand side of the visual studio code window select **View** in the ribbon above > **Extensions** > search for **Microsoft 356 Agents Toolkit** > select **Update** > **Restart Extensions** > select **Create a New Agent/App** > in the dropdown select **Custom Engine Agent**  > **Basic Custom Engine Agent** > **JavaScript** > **Azure OpenAI** . **Note** you may have to close out of VS code and reopen after updating the toolkit.
3. In the blank box at the top of the screen, first enter :

   a. **API Key** from the previous task > **Enter**.

   b. **Endpoint** from the previous task > **Enter**.

   c. For **Azure Open AI deployment name** type in **gpt-4** > **Enter** > **JavaScript**. 

   d. For **Choose the folder where your project room folder will be located**, select **Default folder**.

   e. For **Input application name** type in any name > **Enter**> in the pop up window select **Yes, I trust the authors**.

   f. In the new VS Code window of the newly created app from steps a-f above, navigate to the **M365 Toolkit** icon on the left hand side of the screen.

   **Note:** steps g-i should be for completed for a user's environment that does not have admin access to the Microsoft Teams Admin Center and/or for Learner's using the provided lab environment.
  For Learners with their own environments, perform steps j-m instead.

   g. Under the **Accounts** section, click **Sign in to Microsoft 365**. A new window in your browser will open. Login using the credentials provided.

   h. Navigate back to the VS Code page of your agent. You should now see a green check mark by the words **Custom App Upload Enabled** under **Accounts.

   i. Under the **Accounts** section, click **Sign in to Azure**. Click **OK** on every pop up window. A new window in your browser will open. Login using the credentials provided.

   For users who have an M365 tenant license with admin access to the Microsoft Teams Admin Center, please perform the following steps instead of steps g-i above:

   j. Sign into https://admin.teams.microsoft.com with your admin credentials.

   k. Go to **Teams apps** on the sidebar, and then select **Setup policies**.

   l. Select the **Global (Org-wide default)** policy, and then turn on the **Upload custom apps** toggle.

   m. Scroll down and select the **Save** button to save your changes. Your tenant will now allow custom app sideloading. 

4. Navigate to **src/config.js** file under prompts/chat in the VS Code window of your app. Delete all the text that follows **azureOpenAIKey:**, **azureOpenAIEnpoint:**, and **azureOpenAIDeploymentName:**.

5. After completing the above, replace the the text you deleted after the **:** with the values you saved from the previous task (note: the values must be in quotation marks):

   a. **azureOpenAIKey** is the **API Key** from the previous task.

   b. **azureOpenAIEndpoint** is the **Endpoint** from the previous task.
   
   c. **azureOpenAIDeploymentName** type in **"gpt-4"**
   
**Note** ensure all your text is in between quotation marks.
   
6. **File** > **Save all**
    
7. Press **Ctrl+Shift+d** on your keyboard an a dropdown at the top left  will appear that has a green play button and the word Debug > Select the dropdown> select **Debug in Microsoft 365 Agents Playground** > Press **F5**.
8.Custom engine agent runs within the Debugging tool you have chosen, which opens in your browser. 
9. Navigate back to the VS Code window for your app. Select the **Debug** button dropdown and select **Debug in Teams (Edge)** then press **F5** or the gren play button.
10. A new window in your Edge browser will open. You may or may not be prompted to sign in. Use the login information provided to sign in. After successfully signing in, close the window.
11. There should be a window with the title of your newly created app. Select **Add** > **Open**.
12. Congrats! You can now ask the agent any question pertaining to the RAG data files.
13. **Note:** For Learners completing this lab on their own environment, this agent was made for educational purposes using your own subscription, users should proceed with deleting the agent after completion of this lab. To delete a custom agent in Microsoft Teams, you can:
- Select the agent you want to delete, then choose the **More options icon (…)** and select **Delete**.
- Remove the agent from a chat by selecting the ellipses in the thread and choosing **Manage Apps**.
- From the authoring experience of an agent, select the **ellipses (...)** and choose **Delete**.- From the authoring experience of an agent, select the **ellipses (...)** and choose **Delete**.

**END OF LAB**


**END OF LAB**
