# Summary

This workshop demonstrated how to leverage the Azure AI Agent Service to create a robust conversational agent capable of answering sales-related questions, performing data analysis, generating visualizations, and integrating external data sources for enhanced insights. Here are the key takeaways:

## 1. Function Calling and Dynamic SQL Queries

- The agent uses the Azure AI Agent Service to dynamically generate and execute SQL queries against a read-only SQLite database, enabling it to respond to user questions with accurate data retrieval.

## 2. Context Management

- The agent efficiently manages conversation context using the Azure AI Agent Service, ensuring interactions remain relevant and coherent.

## 3. Data Visualization

- With the Code Interpreter, the agent can generate visualizations such as pie charts and tables based on user queries, making data more accessible and actionable. You can attach additional fonts to the Code Interpreter to create visualizations that support multiple languages.

## 4. File Generation

- The agent can create downloadable files, including Excel, CSV, JSON, and image formats, providing users with flexible options to analyze and share data.

## 5. Security Best Practices

- Security risks, such as SQL injection, are mitigated by enforcing read-only database access and running the app within a secure environment.

## 6. Multi-Language Support

- The agent and LLM support multiple languages, offering an inclusive experience for users from diverse linguistic backgrounds.

## 7. Adaptability and Customization

- The workshop emphasizes the flexibility of the Azure AI Agent Service, allowing you to adapt the agent for various use cases, such as customer support or competitive analysis, by modifying instructions and integrating additional tools.

> !TIP
> As a next step you might want to enable the *Grounding with Bing Search* functionality to the Contoso Sales Agent. Look at the steps in this [manual](https://microsoft.github.io/build-your-first-agent-with-azure-ai-agent-service-workshop/lab-4-bing_search/) to learn how to do that.

This workshop equips you with the knowledge and tools to build and extend conversational agents tailored to your business needs, leveraging the full capabilities of the Azure AI Agent Service.
