# ❄️ Snow-Wise: AI agent to monitor & optimize Snowflake queries

## Inspiration

As builders on Snowflake, we always faced challenges with understanding query patterns and optimizing them for performance and cost. In a world where the Data Cloud is being adopted by Snowflake partners, internal data engineers, data scientists, and even business teams, query observability and optimization become critical. We wondered why this should remain a manual process for data teams and whether AI agents could simplify it!

## What it does

Presenting Snow-Wise, an AI agent that's aware of all activity happening inside the data warehouse, alerts the team in charge in case of anomalies (in performance, latency, or cost), has reasoning and intelligence to suggest query optimizations, and even has access to Snowflake to verify its optimizations!

Data teams can interact with Snow-Wise via conversations today, but the architecture of the AI agent will very soon grow into further agentic patterns that allow for automated schedules, human-in-the-loop, and self-learning behaviors.

In the demo video, you'd be able to see how a data engineer can simply ask, in natural language, "Which were the longest-running queries in the last 3 days?" and almost immediately be presented with suggested optimizations and query logs that verify the veracity of the agent's suggestions.

## How we built it

This AI agent was built on top of a multi-LLM setup (Snowflake Arctic and GPT-4), having access to the relevant Snowflake databases and tables like `warehouse_metering_history` and `query_history`. 

GPT-4 is used to orchestrate function calling, while Arctic is used for specific Snowflake tasks like verifying query correctness.

The conversational user interface was built on Streamlit, which made it extremely simple to prototype and test the whole application.

## Challenges we ran into

We would've loved to use Snowflake Arctic for the entire LLM stack, but the lack of function calling in Cortex limited us. Hence, we had to switch to a multi-model setup.

## What we learned

We learned about Snowflake Arctic's capabilities and tried out different prompts and tool-calling patterns to identify how Arctic compared with other LLMs like GPT-4 and Llama-3+Groq. Eventually, we decided to stick to GPT-4+Arctic as our final stack.
We also learned about the architecture paradigm of chaining together multiple tools and LLM calls to orchestrate user queries in a conversational flow and how short-term history could be maintained across the whole chat session.

## What's next for Snow-Wise: an AI agent to monitor and optimize Snowflake queries

Snow-Wise can be extended to even suggest schema modeling improvements. By analyzing typical query patterns from query logs and the current schemas, Snow-wise could suggest ideas like denormalizing two tables into one.

This is something we're already building for our internal team. Snow-Wise will be given access to a Slack tool, and the agent will run regularly on a schedule to send anomalies and optimizations over Slack every day.

If your Snowflake supports multiple warehouse-native solutions (like BI solutions), Snowflake could analyze all queries originating from them and share these as optimizations or suggestions with the relevant teams.
