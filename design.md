# Preliminary Agent Design

## Purpose

The proposed Career Survival Agent will act as a newly hired engineer in the 48-month workplace simulation. It will aim to complete the full run while building a strong, sustainable career outcome across the dimensions exposed by the official interface and scoring method.

## Operating constraints

- Run with JiuwenSwarm 0.2.4b3 in single-agent mode (`mode: agent`).
- Use only the official CLI, MCP tools, public handbook, public rules, and information returned during the run.
- Do not inspect internal package data or hidden evaluation material, and do not hard-code hidden answers, rules, or thresholds.
- Keep all deliverables in English and follow the competition's published fair-play and submission requirements.

## Decision approach

The agent will maintain a compact state summary from the observations provided by the official interface. Before acting, it will identify the current phase, available actions, resource constraints, visible career dimensions, and any immediate risks. It will choose actions based on stated goals and observed consequences rather than assumed hidden mechanics.

For workplace events, the agent will compare the options using their visible effects, likely near-term consequences, and consistency with sustainable long-term progress. It will avoid repeatedly selecting a single action without checking the current state.

At quarterly decision points, it will budget energy and select the main action by considering current needs, visible performance, and remaining time. It will preserve enough capacity to avoid preventable failure, while still pursuing output and career development. It will reassess after each new observation and adjust priorities when the state changes.

## Information and uncertainty

The agent will distinguish observed facts from estimates. When information is incomplete, it will prefer robust choices with limited downside and avoid inventing exact thresholds. It will use only information legitimately available through the competition interface and public documentation.

## Reliability and token efficiency

Prompts will request concise state summaries and structured reasoning over the available options. The agent will avoid restating the entire history when a short state summary is sufficient. Tool calls will be made only when needed to observe or advance the official simulation. The agent will respect tool schemas and handle errors by checking the returned status before deciding what to do next.

## Development and evaluation plan

After receiving the competition API key and connection details, the team will install the official participation repository and required package versions, configure only the prescribed API settings, and run local validation using the public development dataset and official interfaces. We will inspect run artifacts, identify recurring failure modes, revise the Skill, and compare valid versions using the published scoring process. We will not use prohibited internal data or attempt to manipulate evaluation.

## Preliminary status

This is a proposed design for the preliminary participation check. The final agent behavior and Skills will be refined using the official public materials and permitted local runs.
