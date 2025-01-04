# Part 3, Section C: Additional DSL & Bumpers

This document supplements our “bowling bumpers” by providing **Domain-Specific Language (DSL)** tokens that can be inserted into prompts for more **structured** or **trackable** interactions.

We present two sets of DSL tokens:

1. **DSL for Human Architect Use**:  
   - Simple, high-level tags a human can copy-paste into prompts.  
   - Minimally parameterized—enough to direct the LLM effectively without overcomplicating usage.

2. **DSL for LLM Use**:  
   - More granular tokens with advanced parameters, allowing an LLM to embed or auto-generate them for orchestrating multi-agent or multi-thread tasks.

---

## Table of Contents
1. [DSL for Human Architect Use](#dsl-for-human-architect-use)
2. [DSL for LLM Use](#dsl-for-llm-use)
3. [Best Practices & Integration Tips](#best-practices--integration-tips)

---

## **DSL for Human Architect Use**

These tokens are **short, straightforward** directives. The human can embed them within a prompt to trigger specific behaviors or “bumpers” in the LLM.

### 1. `[MAINTAIN_CONTEXT]`
- **Purpose**: Reminds the LLM to restate or reconnect with the core objective.
- **Example Usage**:
[MAINTAIN_CONTEXT] Please summarize our main goal and how this new idea fits into it.

- **Effect**: The LLM clarifies or reaffirms the guiding objective, preventing drift.

### 2. `[COMBAT_HALLUCINATION]`
- **Purpose**: Instructs the LLM to verify or disclaim any uncertain claims.
- **Example Usage**:
[COMBAT_HALLUCINATION] Re-check any factual claims about historical events. Provide disclaimers or source references if unsure.

- **Effect**: The LLM identifies potential misinformation or disclaimers.

### 3. `[CONFLICT_RESOLUTION]`
- **Purpose**: Signals that the LLM should reconcile contradictory instructions or data.
- **Example Usage**:
[CONFLICT_RESOLUTION] We have conflicting requirements: X says we need a formal tone, Y says casual. Please resolve.

- **Effect**: The LLM systematically addresses the conflict, prompting user input if needed.

### 4. `[TIME_TRAVEL reference=prompt_number]`
- **Purpose**: Directs the LLM to revisit a specific earlier prompt or statement.
- **Example Usage**:
[TIME_TRAVEL reference=Prompt_5] Align our current plan with the constraints we stated in Prompt #5.

- **Effect**: The LLM re-checks or re-applies constraints from the specified earlier step.

### 5. `[SCENARIO_TEST condition=...]`
- **Purpose**: Tells the LLM to test a solution under specific conditions.
- **Example Usage**:
[SCENARIO_TEST condition="budget_cut"] Evaluate how our plan changes if the budget is cut in half.

- **Effect**: The LLM modifies or critiques the solution based on the new scenario.

### 6. `[CRITICAL_SELF_REVIEW]`
- **Purpose**: Asks the LLM to adopt a critical lens on its own logic.
- **Example Usage**:
[CRITICAL_SELF_REVIEW] Identify potential weak spots in the proposal and propose mitigations.

- **Effect**: The LLM checks for flaws, leaps in logic, or contradictory statements.

### 7. `[SUMMARIZE_NEXT_STEPS]`
- **Purpose**: Requests a concise set of immediate actions or concluding bullet points.
- **Example Usage**:
[SUMMARIZE_NEXT_STEPS] Please conclude with a bullet list of next steps and responsibilities.

- **Effect**: The LLM wraps up the current phase with clarity.

---

## **DSL for LLM Use**

These tokens are **more granular** and can be embedded by an LLM (e.g., the Orchestrator or Architect LLM) when orchestrating multi-agent tasks or generating structured directives. They often include **parameters** that shape the behavior or define sub-scenarios.

### 1. `[AGENT_ROLE=XYZ perspective=ABC]`
- **Purpose**: Declares an agent’s role and optional perspective.
- **Example**:
[AGENT_ROLE=FinancialAnalyst perspective="risk_assessment"]

- **Effect**: Tells a subordinate LLM or thread to approach the content from a “Financial Analyst” vantage point, focusing on “risk assessment.”

### 2. `[USE_BUMPER type=CombatHallucination disclaim_if_unsure=true]`
- **Purpose**: Instructs the agent to apply a specific bumper with optional parameters.
- **Example**:
[USE_BUMPER type=CombatHallucination disclaim_if_unsure=true]

- **Effect**: The agent enforces hallucination checks, disclaiming uncertain statements.

### 3. `[SCENARIO condition="UserLoadSpike" severity=3]`
- **Purpose**: Introduces a scenario (e.g., heavy user load) with a severity scale.
- **Example**:
[SCENARIO condition="UserLoadSpike" severity=3]

- **Effect**: The agent or LLM evaluates the plan under a “medium-high” load scenario, adjusting solutions accordingly.

### 4. `[REVIEW output=AgentB step=CriticalSelfReview]`
- **Purpose**: Orders a review of another agent’s output, specifying a step or method to use.
- **Example**:
[REVIEW output=AgentB step=CriticalSelfReview] Please examine Agent B's proposed marketing plan for inconsistencies.

- **Effect**: The orchestrating LLM systematically critiques Agent B’s content.

### 5. `[TIME_TRAVEL ref=Prompt7 fallback=ConflictResolution]`
- **Purpose**: Directs an agent to revert to the constraints in Prompt #7, or do conflict resolution if contradictory instructions are found.
- **Example**:
[TIME_TRAVEL ref=Prompt7 fallback=ConflictResolution]

- **Effect**: The agent re-checks earlier constraints, automatically applying conflict resolution if needed.

### 6. `[INTEGRATE agent="A,B,C" priority="A>shared>B"]`
- **Purpose**: Tells the orchestrator to merge outputs from Agent A, B, and C, following a specified priority or hierarchy.
- **Example**:
[INTEGRATE agent="A,B,C" priority="A>shared>B"]

- **Effect**: The LLM merges the content in the specified order, giving Agent A’s constraints precedence, then shared constraints, then B’s constraints.

### 7. `[SUMMARIZE_OUTCOME style="executive"]`
- **Purpose**: Requests a final high-level summary in a style (e.g., executive, technical, user-friendly).
- **Example**:
[SUMMARIZE_OUTCOME style="executive"]

- **Effect**: Produces a short, top-level summary for decision-makers.

---

## **Best Practices & Integration Tips**

1. **Limit Overuse**  
 - DSL tokens are helpful but can clutter prompts if overused. Strike a balance between clarity and brevity.

2. **Maintain a Shared Reference**  
 - If your multi-agent system uses these tokens, store them in a shared context or “glossary” so each agent/LLM can parse them correctly.

3. **Mix & Match**  
 - It’s fine to combine “Human Architect” DSL tokens (e.g., `[MAINTAIN_CONTEXT]`) with the more advanced “LLM Use” tokens if it suits your workflow. Just ensure the meaning remains unambiguous.

4. **Context Window Awareness**  
 - If your system uses many tokens or long references, keep an eye on your context token limit. Summaries or partial transcripts can help.

5. **Conflict Resolution & Hierarchies**  
 - In large orchestrations, define a **priority** for each agent’s domain. E.g., “Security compliance outranks creative writing,” so if a security check conflicts with a creative idea, the security check wins out.

---

## **How to Apply These DSLs in Practice**

1. **Human to LLM**:  
 - Insert tokens like `[MAINTAIN_CONTEXT]`, `[CONFLICT_RESOLUTION]` when you see drift or contradictory instructions.  
 - The LLM interprets these tokens as triggers for applying the relevant bumper or heuristic from **Part 2**.

2. **LLM (Orchestrator) to Agent LLM(s)**:  
 - Auto-generate the advanced DSL tokens: `[AGENT_ROLE=...]`, `[REVIEW output=...]`, `[TIME_TRAVEL ref=...]`.  
 - Each agent sees and follows these tokens, ensuring a consistent, trackable approach.

3. **During Multi-Thread Projects**:  
 - Use `[AGENT_ROLE=UIExpert]` in the UI design thread, `[AGENT_ROLE=DBAnalyst]` in the data thread, etc.  
 - Integrate them via `[INTEGRATE agent="UIExpert,DBAnalyst,SecurityCheck"]` in the orchestrator’s final step.

By coupling **bowling bumpers** with **DSL tokens**, you create a robust mechanism for specifying, tracking, and enforcing roles, scenarios, and conflict resolution across any scale of LLM interactions—from a single user query to a multi-LLM “cathedral” of collaborative intelligence.

