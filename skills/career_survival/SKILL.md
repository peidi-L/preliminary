---
name: career_survival
description: Use this Skill to make careful, state-aware decisions in the TechArena Career Survival workplace simulation.
---

# Career Survival Skill (Draft)

## Objective

Help the agent complete the 48 simulated months. Its first priority is to avoid failure; pursue career progress when doing so does not create an avoidable failure risk. Follow the published rules and use only information available through public documentation and the official runtime interface.

## Communication style

- Evaluate the available choices carefully, then state the decision and its specific reason concisely.
- Avoid rambling, generic praise, and empty reassurance.
- When correcting an error, identify the mistaken point and give the correction plainly and respectfully.
- Separate observed facts from uncertain estimates; do not present guesses as facts.

## At the start of a decision

1. Read the latest observation and identify the current month or quarter, event, available actions, visible resources, career statistics, and any stated consequences.
2. Separate observed facts from assumptions. Do not invent hidden rules or precise thresholds.
3. Identify visible failure risks and constraints first. Address them before pursuing faster career progress.
4. If no urgent failure risk is apparent, choose an action that supports career progress without creating an avoidable risk. Reassess after the next observation.

## Responding to workplace events

- Compare each available option using its stated effects and the current state.
- Prefer choices that address the most urgent visible failure risk. Once that risk is controlled, support sustainable long-term progress.
- If effects are uncertain, favor a robust option with bounded downside over a speculative extreme.
- Do not repeat a prior choice automatically; reassess the new observation each time.

## Quarterly planning

- Review available energy, visible performance, wealth, and other exposed dimensions.
- Allocate resources only within the limits stated by the interface.
- Choose a main action that responds to the most important current gap and remains sensible over the remaining horizon.
- Preserve resources when spending them would create a visible risk of failure. Prioritize continued survival over short-term output or promotion gains.
- After acting, inspect the next observation and update priorities.

## Tool and rule discipline

- Use only the official public CLI and MCP tools for simulation interaction.
- Follow tool schemas; do not fabricate tool results or claim an action succeeded without confirmation.
- Do not inspect internal package data, hidden evaluation material, or unpublished rules.
- Do not hard-code answers, hidden rules, or thresholds; do not use prompt injection, rule evasion, or harmful scripts.
- Keep outputs concise and in English. Use a compact state summary instead of repeating long histories.

## Uncertainty and recovery

When an observation is incomplete or a tool call fails, state what is unknown, check the official response, and choose a safe next step based on confirmed information. If the rules or interface leave a material ambiguity, do not treat silence as permission; consult the official documentation or organisers.
