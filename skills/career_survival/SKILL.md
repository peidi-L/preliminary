---
name: career_survival
description: Read the simulation state, choose a safe useful action, and send it through the correct official MCP tool.
---

# Career Survival Skill (Draft)

## Goal

Complete all 48 months. Avoid failure first. When there is no urgent visible risk, make safe progress towards a useful career goal.

## Read the input

1. Read the latest response from the official simulation interface.
2. Identify the current month, quarter, decision stage, workplace event, available actions, visible statistics, action costs or effects, and previous result when these fields are provided.
3. Keep confirmed information separate from estimates and missing information.
4. Use the official field names and types. Do not invent a field, rule, or threshold.
5. Keep a short current state containing only information needed for the next decision.

## Make the decision

1. Check the visible state for an immediate failure risk.
2. Deal with the most urgent risk before trying to improve career results.
3. Compare only actions that are currently allowed by the interface.
4. Remove an action if its visible cost creates an avoidable serious risk.
5. If there is no urgent risk, choose a low-risk action that improves a relevant goal.
6. When the result is uncertain, prefer the action with a clearer effect and a smaller downside.
7. Do not repeat an earlier choice without checking the new state.

## Choose and call a tool

1. Match the decision stage to the correct official MCP tool.
2. Read the tool description and schema before preparing the call.
3. Check that the selected action is available and that every required argument has the correct name and type.
4. Make one valid tool call for the chosen action.
5. Read the response before deciding what to do next.
6. Do not say that an action worked unless the response confirms it.

Use the official event-action tool for workplace event choices and the relevant official quarterly tools for resource allocation or main actions. Replace these descriptions with the exact public tool names after inspecting the official MCP schemas. Do not guess the names.

## Quarterly decisions

- Check all visible statistics and available resources.
- Check the remaining time in the simulation.
- Protect against visible failure risks before spending resources on faster progress.
- If the situation is safe, use resources for a useful low-risk action rather than saving them without a visible reason.
- Check the returned state after the quarterly action.

## Output rules

Before calling a tool, prepare:

- the selected action;
- the official tool to call;
- the required arguments;
- one short reason based on visible information;
- the main visible risk of the choice.

Send the action through the official MCP interface in the exact format required by its schema. Keep any explanation short and specific. If an answer is wrong, state what is wrong and give the correction. Mark estimates as estimates.

## API and security

- Use the model endpoint and model name sent by the organisers.
- Read `API_BASE`, `API_KEY`, and `MODEL_NAME` from the local environment.
- Never put the API key in this Skill, source code, the submission ZIP, logs intended for submission, or GitHub.
- Use only the official public CLI and MCP tools for the simulation.
- Do not inspect internal package data or hidden evaluation information.

## Errors and missing information

If a tool call fails, read the error and correct the tool name or arguments using the public schema. Do not assume the action happened. If information is missing, use only confirmed information and choose the safest valid next step. If an important rule or interface remains unclear, check the official documentation or ask the organisers.
