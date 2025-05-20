# Get started

> [!TIP]
> What is **Azure Azure AI Foundry**? Azure AI Foundry is the ultimate platform for innovators to create generative AI solutions. It offers a comprehensive suite of Azure AI capabilities and tools to design, customize, and manage AI applications and agents. It's seamlessly integrated with the world's most loved developer tools, including GitHub, Visual Studio, and Copilot Studio. Azure AI Foundry empowers developers and IT admins to bring their AI visions to life with ease and efficiency.

## Prerequisites

To complete the lab, you will need:

- An Azure subscription - If you don't have one already, you can [create one for free.](https://azure.microsoft.com/free/cognitive-services?WT.mc_id=aiml-132569-bethanycheum)
- An Azure OpenAI resource with [GPT-4o-mini, GPT-4o-mini-realtime-preview, DALL-E 3 and o4-mini models available in a supported region.](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/models#assistants-preview?WT.mc_id=aiml-132569-bethanycheum) If you don't have one already, jump to the next paragraph to provision the required resources. 

> ! NOTE
> If you are running this lab as an event attendee in a guided workshop, pls check with the speaker if you should use an Azure sponsored subscription created for that lab. 

## Deploying your resources

In this workshop we will be working with Azure AI Foundry. First, deploy the necessary resources by following the steps below:

1. Click the deploy to Azure button to deploy your resources: [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure-ai-foundry%2Fmultimodal-models%2Fmain%2F%2FWorkshop%20Instructions%2Fassets%2Flab324-template.json)

2. In the newly opened tab, sign in to your Azure account.

3. Once signed in, you will be redirected to create resources based on the custom template. Create a new resource group and name it **interact-with-llms**. 

4. Next in the **Unique Suffix** field, add any unique four letters. Once done, click **Review and Create** button to create your resources

> [!NOTE]
> Deployment of the resources will take ~2-3 minutes to complete.

5. In this workshop, we will be working in Azure AI Foundry, focusing particularly on the playground feature. Once your deployment is complete, in your browser, navigate to Azure AI Foundry by visiting the link [https://ai.azure.com](https://ai.azure.com?WT.mc_id=aiml-132569-bethanycheum)


## Navigating Azure AI Foundry

![Azure AI Foundry logged in homepage](./Images/aifoundry-homepage.jpeg)

1.Start by clicking Sign In, you can find the sign in link in the top right of the window, and enter the your credentials when prompted for the login credentials. Now that we are logged in, we can start navigating around the platform.

2.Next, let's take a look at the resources we will be working with. Type in https://ai.azure.com/AllResources at the navigation bar to visit the resources page.

![AI Foundry Welcome](./Images/aifoundry-welcomepage.png)

![AI Foundry All Resources](./Images/aifoundry-allresources.png)



> [!NOTE]
 > If you used the [workshop template](./assets/lab324-template.json) to provision the resources, an AI project with its related assets has been already created for you, so you can focus on usage. Here's a list of resources that have been pre-provisioned in the workshop environment:
 > - Azure AI Hub, which is your workspace in Azure AI Foundry and a container of projects. it comes with an Azure Key Vault and an Azure Storage 
 > Account attached to store secrets and data.
 > - Azure AI Project, which encapsulates the tools and assets used to create a specific AI solution
 > - Azure AI Services, which provides access to generative AI models 
 > - Azure AI Search, which enables advanced search capabilities

## Project

![project overview tab](./Images/aifoundry-project-overview.jpg)

### Project Overview

On this page, we can see an overview of our Azure AI Foundry portal Project. This includes:
- **Project Name and Description**: The name of the project and a short description of the Azure AI Foundry portal Project we are in.
- **Project details**: A collection of various properties such as the Project's connection string, its location, resource group, etc. 
- **Endpoints and keys**: Azure AI Foundry portal allows for multiple resources to be connected to it, expanding its features and functionality. Resources such as Azure OpenAI, Azure AI Search and Azure AI Services further enhance the capabilities of our Project, granting us access to deployments such as LLMs or functionalities such as vector search.  Here we can find useful information such as *API endpoints and keys* and documentation.
- **Recent resources**: Once you deploy a model, connect data, or create any assets, they'll show up here, so you can always pick up where you left off.
- **Tutorials and examples to help you get started**: In this section, you can find useful learning resources and tutorials to help you get started.

### Navigation Bar

You will notice the navigation bar has updated with new tabs, which represent functionalities tied to our project.

![project navigation bar](./Images/aifoundry-project-navigation.jpg)

We have two new sections:
1.  The first section includes _Overview_ which provides a general overview of your project, _Model Catalog_ which showcases the available models inside Azure AI Foundry, _Playgrounds_ to interact with the models, and _AI Services_ where you can see a list of Azure AI Services available along with demos, use cases and more.
1. **Build and Customize**: This includes useful opportunities to expand your project's reach, such as _working in Code_ by running a cloud compute, creating executable flows that link LLMs, prompts, and Python tools with _Prompt Flow_, and the ability to carry out _Fine Tuning_ on your deployments.
1. **Observe and Improve:** this includes _Evaluation_ processes for your applications, _Tracing_ to debug your flows and _content filters_ to add guardrails to prompt inputs and completion outputs.
1. **Protect and govern**: This includes _Evaluation_ processes for your applications, _content filters_ to add guardrails to prompt inputs and completion outputs and _governance_ facilities to ensure compliance with your organization policies.
1. **My assets**: Here you can add additional elements to the project, with resources such as _Data_, _Indexes_, _Models and endpoints_ and _Web apps_ to be used as part of your work.
1. **Management Center:** a location to manage all you  hub and project details and resources.

## Data and indexes

In this lab we are going to provide models access to a set of private data, to test their ability to ground responses. In this step, let's add this data in our Azure AI project. 

Download the data on your machine from [this folder](https://github.com/microsoft/aitour-concept-to-creation-ai-studio/tree/main/src/data/products). For the sake of this lab, you don't need to download the whole list of files, pick the first 5 (from *product_info_1.md* to *product_info_5.md*) and save them into a folder named **product_catalog** on your Desktop.

1. Navigate to **Data + Indexes**
2. Select, **New data,** and select **Upload files/folders** as **Data source**
        ![Select your data](./Images/ai-foundry-select-data.png)
3. Open the **Upload files or folder** dropdown, select **Upload folder** and upload the files hosted in the **product_catalog** folder you just created.
        ![Upload folder](./Images/ai-foundry-upload-folder.png) 
4. Once data is uploaded, name your data as **contoso-products** and finish.
5. Next, in the same tab, navigate to _Indexes_ and create an index for your data.
   - Move to the **Indexes** tab in the _Data + Indexes_ page.
   - Click on the **+ New index** button.
   - Select **Data in Azure AI Foundry** as the data source and then the data source you just uploaded.
        ![Create Vector Index](./Images/ai-foundry-create-index.png)
   - In the **Index Configuration** section, change the default name of your Vector index to **products-catalog**. 
   - Open the dropdown menu for the Azure AI Search Service selection and then click on **Connect other Azure AI Search resource**.
        ![Select Azure AI Search Service](./Images/ai-foundry-select-search-service.png)
   - A new window will be opened, where you can select the Azure AI Search resource that you provisioned beforehand through the deployment template. 
        ![Add connection](./Images/ai-foundry-add-connection.png)
- Back to the previous window, the **Select Azure AI Search service** dropdown menu has been populated with the new connection. Select it and then click **Next**.
        ![Confirm Search Service](./Images/aifoundry-confirm-search-service.png)
   - In the **Search Settings** section, leave default configurations. Confirm by clicking on **Next**, and then click **Create vector index**.

## Playgrounds

Click on **Playgrounds** in the left navigation. You will notice we have different options for our **Playground**. Each option represents a different approach to interacting and using AI models, which can be tailored to our specific needs.

We will be doing most of our work in these Playgrounds, but namely in the following:

1. **Chat Playground**
1. **Images Playground**
1. **Audio playground**
1. **Agents playground**

![Image of Azure AI Foundry Playgrounds](./Images/aifoundry-playgrounds.png)

### Chat Playground

Within the playground section, navigate to the **Chat playground** and select **Try the Chat Playground.** This feature allows you to engage with and test various AI models in a conversational format.

![Image of Azure AI Foundry Playground Chat Mode](./Images/aifoundry-chat-playground.jpeg)

1. **Deployment**: This section allows us to change between our deployed models.
1. **System Message Box**: Here is where we enter instructions for the model, previous to the user interaction.
1. **Add your data**: Azure AI Foundry portal supports providing the deployed models with external data, allowing for better search and context.
1. **Parameters**: This tab contains the models detailed settings, such as temperature.
1. **Chat history**: The chat box is where we will see our interactions with the model in the form of chat messages.
1. **Prompt Box**: This is where we type the user queries ("prompts") we want to send to the model.

### Images Playground

Navigate back to Playgrounds, select the **Images playground** and click **Try the Image Playground.** This option allows you to work with image generation

![Image of Azure AI Foundry Playground Images Mode](./Images/aifoundry-image-playground.jpg)

1. **Deployments**: In this drop-down we are able to choose the model to prompt for image generation. These models, just like the chat ones, come from our deployments.
1. **Prompt Box**: Similar to the chat playground's box, this is where the models get their input from the user. In the case of images, descriptions of what we want to generate.
1. **Results Box**: Finally, here is where the generated images are displayed.

### Audio playground

Navigate back to Playgrounds, then select the **Audio playground** and click **Try the Audio Playground.** This feature allows you to engage with and test various AI models in an audio conversational format.

![Image of Azure AI Foundry Playground Real time audio mode](./Images/aifoundry-real-time-audio.png)

1. **Deployment**: This section allows us to change between our deployed models.
1. **System Message Box**: Here is where we enter instructions for the model, previous to the user interaction.
1. **Choose a voice**: gpt-4o-realtime offers a variety of voices to choose from with unique accents or tonal capabilities tailored to your liking.
1. **Server turn detection**: additional parameters to help optimize the model's efficiency and performance by improving voice activity detection.
1. **Parameters**: This tab contains the models detailed settings, such as temperature and max response.
1. **Prompt Button**: Similar to the chat playground's box, this is where the models get their input from the user. 

> NOTE:
> You need to click on **Enable microphone** to be able to use real-time audio as chat input.

## Agents playground

In the Navigation bar, select **Agents**. Select the dropdown under **Select an Azure OpenAI resource** and choose the Hub resource provided for you. Then click "Let's go".

This feature provides you with the tools to build, test, and customize AI-driven agents.

![Image of Azure AI Foundry Playground Agents Mode](./Images/agents-playground-pt1.jpeg)

Once you _create your first Agent_ you will see the UI components as follows:
1. **Agent id and name:** Here you can give your Agent a name.
1. **Deployment**: In this drop-down we are able to choose the model to prompt for image generation. These models, just like the chat ones, come from our deployments.
1. **Instructions Box:** Here is where we enter instructions for the model, previous to the user interaction.

![](Images/agents-playground-pt2.jpeg)

4. **Knowledge:** Knowledge gives the agent access to data sources for grounding responses.
1. **Actions:** Enhance the agent's capabilities by allowing it to run various tools at runtime.
1. **Model settings**: This tab contains the models detailed settings, such as temperature and Top P.
1. **Prompt Box:** Similar to the chat playground's box, this is where the models get their input from the user. 

## Ready to start

That covers the necessary setup and basics of Azure AI Foundry. We will now move forward to begin interacting with the models.



> [!IMPORTANT]
> Go back to the **Chat Playground** and move to [Part 1: Text Generation](./02_Text_Generation.md)
