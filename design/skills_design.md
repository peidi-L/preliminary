# Preliminary Skills Design

## What the agent needs to do

The simulation covers 48 months at work. The agent responds to workplace events and makes choices each quarter. It needs to get through the run and build a career without taking avoidable risks.

## Skill plan

We plan to use one Skill: `career_survival`. It will help the agent:

- read the current situation, available choices, visible resources, and career results;
- compare event choices using the effects shown in the game;
- plan quarterly actions around current needs, available resources, and time left;
- check what happened after each choice and adjust the next decision.

## Information used

We will use the published handbook and rules, along with information returned by the official CLI and MCP tools. The agent should separate what the game shows from what it estimates. It should not use hidden information, inspect internal package data, or make up rules or thresholds. It should follow the tool formats and check the result of each action.

## How it will make choices

Avoiding failure comes first. Before choosing, the agent should check for visible risks and deal with urgent ones. If there is no urgent risk, it should make safe progress towards a relevant career goal rather than save resources without a clear reason. It should check the visible costs of an action and how much time is left. If the result is uncertain, it should prefer the option with more predictable effects and less downside. It should check the new situation after every choice and change its plan when needed.

The agent should keep its answers short and specific. When correcting a wrong answer, it should say what is wrong and give the correction. It should not add generic praise or reassurance. It should say when something is an estimate rather than a fact.

## Main risks

- **A choice may have later effects.** Check the situation again after each choice, not just after the next event.
- **Some information may be missing.** Mark estimates clearly and do not guess hidden rules or thresholds.
- **Using too many resources may cause problems later.** Check the visible limits and costs before spending them.
- **Long messages and unnecessary tool calls may use up the API budget.** Keep notes short and use tools only when needed.
- **A tool may return an error or an unexpected result.** Follow its format and check the response before assuming an action worked.

## Development plan

We plan to use JiuwenSwarm 0.2.4b3 in single-agent mode (`mode: agent`) and the official public interfaces. Once we receive the competition API key, we will follow the official Quickstart and rules. We will test using permitted public development data and will not use internal package data or try to manipulate the evaluation.
