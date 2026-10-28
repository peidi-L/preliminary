# Preliminary Skills Design

## Aim

The challenge is a 48-month workplace simulation. The agent acts as a newly hired engineer. It has to respond to workplace events, make quarterly choices, and balance long-term results such as health, dignity, skills, relationships, productivity, and wealth.

Our first aim is to finish the simulation without failure. When there is no urgent risk, the agent should make safe career progress.

## 1. Input from the simulation

The first part of development is to understand exactly what information the simulation gives to the agent. We will inspect the public handbook and the schemas returned by the official CLI and MCP tools. We expect the useful input to include:

- the current month, quarter, and decision stage;
- the current workplace event and the choices that are allowed;
- visible statistics, including any values provided for health, dignity, skills, relationships, productivity, wealth, energy, or performance;
- the visible cost or effect of each action;
- the result of the previous action;
- tool errors, missing fields, and other limits shown by the interface.

The exact field names and data types will be taken from the official tool schemas. We will not invent fields or assume that a value is available when the interface does not provide it.

The input will be changed into one short internal state:

```text
current_state = {
  time,
  decision_stage,
  visible_statistics,
  current_event,
  available_actions,
  visible_costs_and_effects,
  previous_result,
  unknown_information
}
```

This gives the decision process a consistent input even if different MCP tools return information in different formats.

## 2. Agent architecture

We will use one agent in JiuwenSwarm. The agent will have the following parts:

1. **Input reader:** reads the latest MCP response and builds `current_state`.
2. **Risk check:** checks the visible state for an immediate failure risk or an unsustainable use of resources.
3. **Decision planner:** compares only the actions currently allowed by the simulation. It deals with urgent risks first. If there is no urgent risk, it chooses a low-risk action that makes useful progress.
4. **Tool selector:** chooses the correct official MCP tool and prepares its required arguments.
5. **Output checker:** checks that the tool name, action, and arguments match the published schema before making the call.
6. **Result checker:** reads the tool response, confirms whether the action worked, and updates the state for the next decision.

The agent will not make one fixed plan for all 48 months. It will reassess after every event because the state and available actions can change.

## 3. MCP tools

After setting up the official environment, we will record each public MCP tool in a small tool list containing:

- tool name;
- what the tool does;
- when it can be used;
- required and optional arguments;
- expected response format;
- how to handle an error.

The tool selector will use this list to match a task to the correct tool. For example, an event decision should use the official event-action tool, while a quarterly resource or main-action decision should use the relevant quarterly tool. The exact tool names and arguments will come from the official MCP schemas and will not be guessed or hard-coded from hidden data.

## 4. Decision method

For each decision, the agent will:

1. read and summarise the confirmed input;
2. list the actions that the simulation currently allows;
3. check for visible failure risks;
4. remove actions that are invalid or create an avoidable serious risk;
5. compare the remaining actions using their visible costs, effects, and the time left;
6. choose the safest useful action;
7. call the correct tool and check its response.

Avoiding failure comes first. When the visible state is safe, the agent should use available resources to make steady progress instead of saving them without a reason. If the effects are uncertain, it should prefer an action with a clearer result and a smaller downside. Estimates must be marked as estimates.

## 5. Output to the simulation

The final output must connect correctly to the simulation interface. Internally, the agent will create a decision containing:

```text
decision = {
  selected_action,
  selected_tool,
  tool_arguments,
  short_reason,
  expected_risk
}
```

Before sending it, the output checker will confirm that the selected action is currently available and that all required arguments match the MCP schema. The external output will then be the valid MCP tool call required by the simulation. The agent will not claim that an action worked until the tool response confirms it.

## 6. Model and API connection

The organisers provide an API key for the designated competition model after they approve the preliminary submission. JiuwenSwarm will use that model for the agent's reasoning. We will configure only the values allowed by the official instructions:

- `API_BASE`
- `API_KEY`
- `MODEL_NAME`

The API key will be stored in the local environment and will not be written in the Skill, source files, ZIP, or GitHub repository. The model name and endpoint will be copied from the organisers' email instead of guessed. The official MCP tools will connect the agent to the simulation, while the model API will provide the reasoning used to choose an action.

## 7. Skill and communication style

The preliminary design uses one Skill: `career_survival`. It contains the decision process, tool rules, failure handling, and output checks.

The agent should think through the choices but keep its explanation short. It should state the chosen action and the exact reason. If something is wrong, it should say what is wrong and give the correction without adding generic praise or reassurance.

## Main risks

- **The input schema may be misunderstood.** Use the official schemas and test responses before relying on a field.
- **An action may be sent in the wrong format.** Validate the tool name and arguments before every call.
- **A choice may have delayed effects.** Read the new state after every action and update the plan.
- **Missing information may lead to guessing.** Separate confirmed values from estimates and do not invent hidden rules or thresholds.
- **Resources may be used too quickly.** Check the visible costs, current risks, and time left before spending them.
- **Tool or API calls may fail.** Check the returned status and retry only when the official interface shows that retrying is valid.
- **Long prompts may waste the API budget.** Keep the state summary and reasoning focused on the current decision.

## Development plan

We plan to use JiuwenSwarm 0.2.4b3 in single-agent mode (`mode: agent`) with the official public CLI and MCP interfaces. After receiving the API key, we will install the official environment, inspect every public input and output schema, build the tool list, run local tests with permitted development data, and update the Skill from the test results. We will not inspect internal package data, use hidden evaluation information, or try to manipulate the evaluation.
