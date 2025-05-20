# Part 5 - Azure AI Agents

Welcome to Part 5 of this workshop! 

So far, we have interacted with Large Language Models in many different ways. However, these interactions have been isolated and tied to a very specific purpose. **Azure AI Agents** represent the next step in our interactions, as they help us integrate previous interactions into one solution.


> [!TIP] 
> **What is Azure AI Agent Service?**  It's a fully managed service designed to empower developers to securely build, deploy, and scale high-quality, and extensible AI agents without needing to manage the underlying compute and storage resources. It integrates capabilities such as state management, context association, chat threads, and code execution, making it easier to access third-party extensions​.

Previously, building custom AI Agents needed heavy lifting even for experienced developers. While the chat completions API is lightweight and powerful, it's inherently stateless, which means that developers had to manage conversation state and chat threads, tool integrations, retrieval documents and indexes, and execute code manually.

Within Azure AI Foundry, an AI Agent acts as a "smart" microservice that can be used to answer questions based on custom data (RAG), perform actions, or completely automate workflows. It achieves this by combining the power of generative AI models with tools that allow it to perform an action on behalf of the user.

Agents can also access multiple tools in parallel, if needed. Some of these tools include:
- **Function Calling**
- **Code Interpreter**
- **File Search**
- **Grounding with Bing Search**
- **Azure Functions** 
... and more..

In this section, we will be covering Code Interpreter.

## Understanding the Components of Agents

To begin working with AI Agents, it is important to understand and address the different components that take part in its functionality.

As stated above, an **Agent** is simply a "smart" micrososervice that can perform actions, automate workflows or answer questions using RAG.

The next step once the Agent has been created, is to create a **Thread**. A **Thread** is a conversation session between an Agent and a user. Threads store Messages and automatically handle truncation to fit content into a model’s context.

The **Messages** are created by either the Agent or an user. They can include text, images and other files. These are stored as a list on the thread.

Lastly, we can **Run** the Agent. This means activating an Agent to begin running based on the contents of the Thread. The Agent uses its configuration and the *Thread’s Messages* to perform tasks by calling models and tools. As part of a Run, the Agent *appends Messages to the Thread*.

When building and interacting with an AI Agent in the Foundry Portal - as you are going to do in the next section - most of the complexity of its components are hidden to the user.

## Creating the Agent

First thing first, download the data we are going to use to ground your agent's responses from [here](https://github.com/microsoft/aitour-interact-with-llms/tree/main/lab/Skillable%20Workshop%20Instructions/assets).

Next, follow the steps below to create an customize your agent.
1. Under _Build and customize_ on the left navigation bar, select **Agents.**

1. If this is your first time trying the Agents playground, a page titled "Select or Deploy a model" will appear. Click on the down arrow to select **gpt-4o-mini** model. Then click **Next**.

![screenshot to select Aure OpenAI Service Resource](Images/agents-aoai-select.jpeg)

2. A new Agent will be created for you. Click on it, to be able to configure its properties. In the **Deployments** section, ensure you select **gpt-4o-mini** model.

    >[!TIP] 
    > **Ensure that you chose the correct deployment**. It should say **gpt-4o-mini** along with its version. 

3. Next, let's name our Agent. Type the following in the Agent Name textbox:

    ```Contoso Outdoor Sales Agent```

4. Next, we can provide the Agent with a set of **instructions**. Similar to the *System Message* we saw in previous sections, it provides the Agent with goals to follow. Copy the following instructions into the Instructions textbox.

    ``` 
    You are a sales Agent for Contoso Outdoor. You are polite, professional, helpful and friendly.

    You get all the sales data from the uploaded .csv files. There is sales revenue data that is broken down by region, product category, product type and separated by year and month.

    Examples of regions include Africa, Asia, Europe and America. Categories include climbing gear, camping equipment, apparel and others. Product categories include jackets, hammocks, wet suits, shoes and more. 

    If a question is not related to sales or you cannot answer the question, you **must** respond: "Please contact IT for more assistance". If the user asks for help or says 'help', provide a list of sample questions that you can answer.
    ```

    ![Agents Playground](./Images/agents-playground-update-details.jpeg)

    >[!NOTE]
    >How many prompt engineering techniques from the previous sections are you able to identify in this prompt? For clues, check Part 2 of the workshop.

1. Scroll down to the **Actions** section, and click **Add**.

    ![Agent attach new file](Images/agents-actions.jpeg)

1. In the new tab that appears, click **Code interpreter**.

1. On the next window, click on **select local files** and select the `Contoso_Sales_Revenue.csv` file on your Desktop.
    ![Agents code interpreter](Images/aifoundry-codeinterpreter-upload-file.jpeg)

1. Click on the **Upload and save** button. You should now see the file under the *Code Interpreter* tool.

The Agent is now ready for us to interact with it.

## Interacting with our Agent

1. On the top right of our Agents window, select **Try in playground**

![](Images/agents-try-in-playground.jpeg)

2.  Let's begin by typing `help` in the prompt box. You will notice this starts a New Thread. 
You will notice that we get a series of sample questions that we can test. Test one of the questions and see what the Agent replies!

2. Next, let's try a specific query. Type the following:

    ```What are the total sales for Europe broken down by category? ```

    You will notice the Agents makes use of the code interpreter to provide you with an answer.

3. Now, let's try working with this data. Type the following prompt:

    ```Put this data in a graph. ```

    Through code interpreter, the Agent is able to convert the structured data into a graph!

4. If you would like to see another type of graph, try the following prompt and request the data to be in a graph:

    ```What is the trending product category? Give the output as a graph. ```

    The Agent should provide you with a graph showcasing a trending product by carrying out an analysis of the sales revenue data overtime.

Congratulations! You have now completed the last part of the workshop and have learnt what AI Agents are, how they work and how to create one using Azure AI Foundry portal.

Click **Next** to advance to the Summary section of the workshop.