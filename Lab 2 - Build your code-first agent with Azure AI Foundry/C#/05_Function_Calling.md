## Introduction

### What is Function Calling

Function calling enables Large Language Models to interact with external systems. The LLM determines when to invoke a function based on instructions, function definitions, and user prompts. The LLM then returns structured data that can be used by the agent app to invoke a function.

It's up to the developer to implement the function logic within the agent app. In this workshop, we use function logic to execute SQLite queries that are dynamically generated by the LLM.

### Enabling Function Calling

If you’re familiar with [Azure OpenAI Function Calling](https://learn.microsoft.com/azure/ai-services/openai/how-to/function-calling), you know it requires you to define a function schema for the LLM.

With the Azure AI Agent Service and its Python SDK, you can define the function schema directly within the Python function’s docstring. This approach keeps the definition and implementation together, simplifying maintenance and enhancing readability.

For example, in the **sales_data.py** file, the **async_fetch_sales_data_using_sqlite_query** function uses a docstring to specify its signature, inputs, and outputs. The SDK parses this docstring to generate the callable function for the LLM:

With the Azure AI Agent Service and its .NET SDK, you define the function schema as part of the C# code when adding the function to the agent.

For example, in the **Lab.cs** file, the `InitialiseTools` method defines the function schema for the `FetchSalesDataAsync` function:

```csharp
new FunctionToolDefinition(
    name: nameof(SalesData.FetchSalesDataAsync),
    description: "This function is used to answer user questions about Contoso sales data by executing SQLite queries against the database.",
    parameters: BinaryData.FromObjectAsJson(new {
        Type = "object",
        Properties = new {
            Query = new {
                Type = "string",
                Description = "The input should be a well-formed SQLite query to extract information based on the user's question. The query result will be returned as a JSON object."
            }
        },
        Required = new [] { "query" }
    },
    new JsonSerializerOptions() { PropertyNamingPolicy = JsonNamingPolicy.CamelCase })
)
```

### Dynamic SQL Generation

When the app starts, it incorporates the database schema and key data into the instructions for the Azure AI Agent Service. Using this input, the LLM generates SQLite-compatible SQL queries to respond to user requests expressed in natural language.

## Lab Exercise

In this lab, you will enable the function logic to execute dynamic SQL queries against the SQLite database. The function is called by the LLM to answer user questions about Contoso sales data.

1. Open the `Program.cs` file.

2. **Uncomment** and update the following code:

    ```csharp
    await using Lab lab = new Lab1(projectClient, apiDeploymentName);
    await lab.RunAsync();
        ```

### Review the Instructions

 1. Open the **shared/instructions/function_calling.txt** file.

    !!! tip "In VS Code, press Alt + Z (Windows/Linux) or Option + Z (Mac) to enable word wrap mode, making the instructions easier to read."

 2. Review how the instructions define the agent app’s behavior:

     - **Role definition**: The agent assists Contoso users with sales data inquiries in a polite, professional, and friendly manner.
     - **Context**: Contoso is an online retailer specializing in camping and sports gear.
     - **Tool description – “Sales Data Assistance”**:
         - Enables the agent to generate and run SQL queries.
         - Includes database schema details for query building.
         - Limits results to aggregated data with a maximum of 30 rows.
         - Formats output as Markdown tables.
     - **Response guidance**: Emphasizes actionable, relevant replies.
     - **User support tips**: Provides suggestions for assisting users.
     - **Safety and conduct**: Covers how to handle unclear, out-of-scope, or malicious queries.

     During the workshop, we’ll extend these instructions by introducing new tools to enhance the agent’s capabilities.

    !!! info
        The {database_schema_string} placeholder in the instructions is replaced with the database schema when the app initializes.

    ```csharp
    // Replace the placeholder with the database schema string
    instructions = instructions.Replace("{database_schema_string}", databaseSchemaString);
    ```

## Run the Agent App

1. Press <kbd>F5</kbd> to run the app.
2. In the terminal, you'll see the app start, and the agent app will prompt you to **Enter your query**.

    ![Agent App](../media/run-the-agent.png)

### Start a Conversation with the Agent

Start asking questions about Contoso sales data. For example:

1. **Help**

    Here is an example of the LLM response to the **help** query:

    *I’m here to help with your sales data inquiries at Contoso. Could you please provide more details about what you need assistance with? Here are some example queries you might consider:*

    - *What were the sales by region?*
    - *What was last quarter's revenue?*
    - *Which products sell best in Europe?*
    - *Total shipping costs by region?*

    *Feel free to ask any specific questions related to Contoso sales data!*

    !!! tip
        The LLM will provide a list of starter questions that were defined in the instructions file. Try asking for help in your language, for example `help in Hindi`, `help in Italian`, or `help in Korean`.

2. **Show the 3 most recent transaction details**

    In the response you can see the raw data stored in the SQLite database. Each record is a single
    sales transaction for Contoso, with information about the product, product category, sale amount and region, date, and much more.

    !!! warning
        The agent may refuse to respond to this query with a message like "I'm unable to provide individual transaction details". This is because the instructions direct it to "provide aggregated results by default". If this happens, try again, or reword your query.

        Large Language models have non-deterministic behavior, and may give different responses even if you repeat the same query.

3. **What are the sales by region?**

    Here is an example of the LLM response to the **sales by region** query:

        | Region         | Total Revenue  |
        |----------------|----------------|
        | AFRICA         | $5,227,467     |
        | ASIA-PACIFIC   | $5,363,718     |
        | CHINA          | $10,540,412    |
        | EUROPE         | $9,990,708     |
        | LATIN AMERICA  | $5,386,552     |
        | MIDDLE EAST    | $5,312,519     |
        | NORTH AMERICA  | $15,986,462    |

    !!! info
        So, what’s happening behind the scenes to make it all work?

        The LLM orchestrates the following steps:

        1. The LLM generates a SQL query to answer the user's question. For the question **"What are the sales by region?"**, the following SQL query is generated:

            **SELECT region, SUM(revenue) AS total_revenue FROM sales_data GROUP BY region;**

        2. The LLM then asks the agent app to call the **async_fetch_sales_data_using_sqlite_query** function, which retrieves the required data from the SQLite database and returns it to the LLM.
        3. The LLM uses the retrieved data to create a Markdown table, which it then returns to the user. Check the instructions file, you'll see that Markdown is the default output format.

4. **Show sales by category in Europe**

    In this case, an even more complex SQL query is run by the agent app.

5. **Breakout sales by footwear**

    Notice how the agent figures out which products fit under the "footwear" category and understands the intent behind the term "**breakout**".

6. **What brands of tents do we sell?**

    !!! info
        We haven't provided the agent with any data containing information about product brands. That's why the agent isn't able to properly answer this question.

        In the previous responses you may have noticed that the transaction history from the underlying database did not include any product brands or descriptions, either. We'll fix this in the next lab!

### Ask More Questions

Now that you’ve set a breakpoint, ask additional questions about Contoso sales data to observe the function logic in action. Step through the function to execute the database query and return the results to the LLM.

Try these questions:

1. **What regions have the highest sales?**
2. **What were the sales of tents in the United States in April 2022?**

### Disable the Breakpoint

Remember to disable the breakpoint before running the app again.

### Stop the Agent App

When you're done, type **exit** to clean up the agent resources and stop the app.
