# Preliminary Skills Design

## Understanding of the task

Career Survival Agent is a 48-month workplace simulation. The agent acts as a newly hired engineer and must respond to monthly workplace events, make quarterly resource and career decisions, and manage visible outcome dimensions so it can finish the run with a strong, sustainable result.

## Planned Skills and responsibilities

The preliminary design uses one Skill: `career_survival`.

- It reviews each current observation and identifies the current phase, available actions, visible resources and career statistics, and immediate risks.
- It compares workplace-event choices using their stated consequences and the current state.
- At quarterly decision points, it plans energy use and chooses a main action based on visible needs, remaining time, and sustainability.
- It reassesses after new observations instead of repeating choices mechanically.

## Information used for decisions

The agent will use the public handbook, public rules, and information returned by the official CLI and MCP interface during a run. It will distinguish observed facts from estimates, and will not rely on hidden evaluation information, extracted internal package data, or assumed thresholds. It will follow the tool schemas and confirm outcomes from tool responses.

## Proposed decision approach

Before each decision, the Skill will summarize the relevant state concisely, identify urgent risks and constraints, then compare available actions against immediate needs and longer-term goals. When consequences are uncertain, it will prefer a robust choice with bounded downside and update its priorities when the state changes. At quarterly decisions, it will balance output and development against preserving enough resources to avoid visible sustainability risks.

The agent will reason carefully but communicate concisely: state the decision and its specific reason without rambling, generic praise, or empty reassurance. If it identifies an error, it will name the mistaken point and give the correction plainly and respectfully. It will distinguish observed facts from uncertain estimates.

## Main risks and mitigations

- **Short-term choices can create delayed effects.** Reassess the full visible state after each action and avoid optimizing only the next event.
- **Incomplete information can tempt unsupported assumptions.** Separate known facts from estimates and avoid inventing hidden rules or precise thresholds.
- **Overusing resources can undermine later decisions.** Check visible energy and other constraints before committing resources.
- **Long prompts and repeated calls can waste the limited token/API budget.** Keep state summaries compact and call tools only when needed.
- **Unexpected or malformed tool results can lead to invalid actions.** Respect tool schemas, inspect returned status, and recover from confirmed information only.

## Compliance and development plan

The agent will use JiuwenSwarm 0.2.4b3 in single-agent mode (`mode: agent`) and only the official public interfaces. All deliverables are in English. After organiser verification and receipt of the competition API key, development will follow the official Quickstart and published rules. Local runs will use permitted public development data and official interfaces; no hidden package data or evaluation manipulation will be used.
