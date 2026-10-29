# Preliminary Skills Design

## Aim

The challenge is a 48-month workplace simulation. The agent acts as a newly hired engineer. It has to respond to workplace events, make quarterly choices, and balance long-term results such as health, dignity, skills, relationships, productivity, and wealth.

Our first aim is to finish the simulation without failure. When there is no urgent risk, the agent should make safe career progress.

## 1. Input from the simulation

The agent will use `observe(session_id)` to read the current state, event, and choices. The public handbook lists these visible statistics: `Health`, `Dignity`, `Skill`, `Network`, `Level`, `Output`, `Wealth`, `Energy`, and `CurrentLevelDuration`.

We will keep a short state summary with the session ID, current time and stage, returned statistics, available choices, warnings, and the previous result. Action costs and effects will come from the public rules or current observation. Anything else will stay unknown or be marked as an estimate.

Our internal summary will contain:

```text
current_state = {
  session_id,
  time_and_stage,
  visible_statistics,
  event_and_choices,
  stated_costs_and_effects,
  warnings_and_recent_changes,
  unknown_information
}
```

These labels define our own summary. During integration, we will check the actual response fields and types against the official interface before using them.

## 2. Agent architecture

We will use one agent in JiuwenSwarm. Its decision process has six stages:

1. **Input reader:** reads the latest MCP response and builds `current_state`.
2. **Risk check:** checks the visible state for an immediate failure risk or an unsustainable use of resources.
3. **Decision planner:** compares only the actions currently allowed by the simulation. It deals with urgent risks first. If there is no urgent risk, it chooses a low-risk action that makes useful progress.
4. **Tool selector:** uses the official MCP interface to observe, act, or check recent results.
5. **Output checker:** checks that the tool name, action, and arguments match the published schema before making the call.
6. **Result checker:** reads the tool response, confirms whether the action worked, and updates the state for the next decision.

These are stages within one agent. After each action, it will read the new state and reassess. Once the interface reports that the run has ended, it will stop taking actions and record the confirmed result.

## 3. MCP tools

The public documentation lists five tools:

| Tool | Planned use |
| --- | --- |
| `new_game()` | Start a run when one is requested and no session has been supplied. |
| `observe(session_id)` | Read the current situation and choices. |
| `take_action(session_id, choice, notes)` | Submit a workplace or quarterly choice and a short decision note. |
| `check_latest_logs(session_id, count=10)` | Check recent results or warnings when the observation needs clarification. |
| `show_employee_handbook()` | Read the public handbook when needed. |

Both workplace events and quarterly decisions use `take_action`. The current observation determines the available choice. We will check argument types and allowed values against the exposed tool schemas. An existing session will be kept throughout the run; the agent will not start a new game to replace a poor result.

## 4. Decision method

For each decision, the agent will:

1. read the latest state and check whether the run has ended;
2. identify the choices allowed at the current stage;
3. check warnings and worsening statistics for signs of failure risk;
4. compare valid choices using their stated costs, likely effects, and the time left;
5. deal with urgent risks first, then choose useful progress with limited downside;
6. submit one choice, check the result, and update the state.

Risk checks will cover the published failure directions, including poor health, sustained low dignity, weak performance, and persistent problems with wealth, skills, or relationships. The agent will use warnings and trends without assuming hidden thresholds. If every valid choice carries risk, it will choose the least harmful valid option based on the available information.

At quarterly decisions, the agent will check the remaining `Energy` and the action costs. Unused Energy expires at the end of the quarter, so it should use it for recovery or useful progress when the available action is sensible. It should still avoid spending it on an action that worsens an urgent problem. Main actions and performance feedback will be considered alongside the remaining time in the run.

## 5. Output to the simulation

The decision will be sent through `take_action(session_id, choice, notes)`. The `choice` must be valid for the current observation. The `notes` will briefly state the reason and main risk, using the format accepted by the tool schema.

Before each call, the agent will check the session, current stage, required arguments, and accepted types. It will send one action at a time and inspect the response before continuing. If a timeout leaves the result unclear, it will use `observe` and, if needed, recent logs before deciding whether to retry. This avoids applying the same action twice.

## 6. Model and API connection

JiuwenSwarm will connect to the designated competition model using the details supplied by the organisers. During setup, we will put the following values in the local `.env` file and use the official setup process to configure the runtime:

- `API_BASE`
- `API_KEY`
- `MODEL_NAME`

The runtime handles the model connection. The Skill does not need to read the API key or environment files. Credentials will stay out of prompts, agent notes, submitted logs, the ZIP, and GitHub. We will use the exact endpoint and model name supplied by the organisers and leave provider routing under their control.

## 7. Skill and communication style

The preliminary design uses one Skill: `career_survival`. It contains the decision process, tool rules, failure handling, and output checks.

Decision notes should be short: the chosen action, the evidence for it, and its main risk. They should distinguish confirmed information from estimates.

## Main risks

- **Misreading the input or action format.** Check fields, types, and available choices against the public interface.
- **Missing delayed effects.** Review warnings and changes after each action, including persistent weakness in a statistic.
- **Guessing hidden mechanics.** Use public rules and current-run feedback without turning an observed pattern into a fixed rule.
- **Spending resources poorly.** Check costs and risks while accounting for Energy that expires each quarter.
- **Repeating an action after a timeout.** Confirm the current state before resending a call whose result is unclear.
- **Using too many tokens.** Keep state summaries and notes short, and read logs only when needed.

## Development plan

We plan to use JiuwenSwarm 0.2.4b3 in single-agent mode (`mode: agent`). This is a proposed design; gameplay results are not yet available. After setup, we will verify the public schemas, test state handling and action validation, then run the permitted development data and revise the Skill from those results. Questions about unclear rules will go to the organisers before we use the disputed method. Simulation access will stay within the official MCP tools and public CLI for manual testing.

## Public references

- [Preliminary requirements and API setup](https://techarena-career-sim.readthedocs.io/en/latest/api-key.html)
- [Official MCP tools](https://techarena-career-sim.readthedocs.io/en/latest/mcp.html)
- [Public handbook](https://techarena-career-sim.readthedocs.io/en/latest/handbook.html)
- [Published action rules](https://techarena-career-sim.readthedocs.io/en/latest/rules.html)
- [Failure directions](https://techarena-career-sim.readthedocs.io/en/latest/failure-and-ending.html)
