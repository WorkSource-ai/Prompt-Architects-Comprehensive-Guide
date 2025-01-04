# Part 3, Section D: LLM-Assisted Customization & Prompt Generation

Welcome to **Section D**, where we provide **template instructions** that transform your LLM into a “prompt customizer.” Here, the LLM:

1. **Asks the user** relevant questions about domain, style, scope, and any special constraints.  
2. **Generates** tailored one-off prompts or multi-step “master instructions” based on the user’s responses.  

This allows you (or your end-user) to **efficiently** configure specialized prompts without manually crafting them from scratch.

---

## Table of Contents
1. [Overview & Purpose](#overview--purpose)
2. [Basic “Prompt Customizer” Flow](#basic-prompt-customizer-flow)
3. [Template 1: One-Off Prompt Generator](#template-1-one-off-prompt-generator)
4. [Template 2: Multi-Step Instruction Wizard](#template-2-multi-step-instruction-wizard)
5. [Optional Add-Ons & DSL Integration](#optional-add-ons--dsl-integration)
6. [How to Use & Extend](#how-to-use--extend)

---

## 1. Overview & Purpose

Sometimes, you (the Human Architect) want the **LLM** to gather user requirements—like domain specifics, style preferences, or compliance constraints—**before** producing any final prompts. This approach:

- Minimizes guesswork.  
- Ensures the final script or prompt is **customized** to the user’s unique needs.  
- Reduces repetitive manual editing of template prompts.

Using these instructions, the LLM becomes a **wizard** that first **interviews** the user, then auto-generates specialized instructions or one-off prompts.

---

## 2. Basic “Prompt Customizer” Flow

Here’s the general structure:

1. **LLM Asks Preliminary Questions**  
   - “What’s your domain?”  
   - “Do you need compliance checks?”  
   - “How long or detailed should the final prompt be?”  

2. **LLM Summarizes Responses**  
   - Creates a short, structured recap of the user’s answers.  

3. **LLM Generates a Customized Prompt or Instruction Script**  
   - Incorporates user-chosen style, domain, constraints, etc.

4. **Optional Final Confirmation**  
   - LLM can ask the user to confirm or tweak the generated script.

---

## 3. Template 1: One-Off Prompt Generator

**When to Use**: You want the LLM to ask the user a few quick questions, then produce a **single** specialized prompt.

### Instructions to the LLM (Architect Persona)

SYSTEM / INITIAL PROMPT:
You (the LLM) will function as a "Prompt Customizer" for one-off prompts. Step 1: Ask the user up to 5 targeted questions about:

Their domain (e.g., marketing, legal, creative)
The complexity or desired detail level
Any compliance or style constraints
Language or tone preferences
If DSL tokens (Part 3 – C) or bumpers (Part 2) should be automatically embedded
Step 2: Summarize the user's answers in bullet points or a short table.

Step 3: Generate a "custom one-off prompt" that merges the user's answers into a single, well-structured instruction.

Note:

Use minimal placeholders—focus on clarity and alignment with user’s stated preferences.
Reference DSL tokens or short bumpers (like [MAINTAIN_CONTEXT], [COMBAT_HALLUCINATION]) if relevant.
USER: “Hello, please guide me to create a custom one-off prompt for my needs.”


**Sample Execution Flow**:

1. **LLM** asks questions:  
   - “What domain are we working in?”  
   - “Any special compliance or disclaimers needed?” etc.  
2. **User** answers.  
3. **LLM** recaps user input.  
4. **LLM** produces a final, single-prompt script, e.g.:

   ```plaintext
   "You are a [Role], focusing on [Domain]. ...
    [MAINTAIN_CONTEXT] if necessary.
    Provide an immediate solution with a [Tone or Style] approach..."


4. Template 2: Multi-Step Instruction Wizard
When to Use: You want a more complex, multi-phase script or “master thread instructions,” tailored to the user’s situation. The LLM will ask more or deeper questions, then output a multi-step blueprint.

Instructions to the LLM (Architect Persona)
SYSTEM / INITIAL PROMPT:
--------------------------------
You (the LLM) are a “Master Thread Instruction Wizard.”
Step 1: Ask the user about:
   - Purpose or objective (type of project, domain)
   - Number of phases or steps they foresee
   - Any domain-based constraints (compliance, style, advanced disclaimers)
   - Whether they want agentic system orchestration or single-thread approach
   - If they plan to upload Part 2 (LLM operating protocol) to handle self-regulation
Step 2: Recap their answers in a structured mini-outline.
Step 3: Produce a multi-step “master thread instruction script” that the user can copy-paste into the LLM or system prompts.
   - Each step includes relevant DSL tokens or references to the bumpers from Part 2.
   - Include optional conflict resolution or scenario testing segments as placeholders.
--------------------------------

USER:
"Help me build a detailed multi-step instruction set for a large writing project, focusing on compliance and a multi-agent approach."
Sample Execution Flow:

LLM asks in-depth questions:

“What’s the main domain (fiction, research, legal, etc.)?”
“Do you need sub-agents?”
“How many phases do you envision?” etc.
User provides answers.

LLM merges that info into a multi-step instruction script. For instance:

SYSTEM:
"ROLE: Orchestrator for a multi-agent setup...
 Step 1: gather outline
 Step 2: assign tasks to Agent A and Agent B
 [TIME_TRAVEL reference=prompt# if needed]
 ...
USER:
'Begin with Step 1...' "

The final script can be very detailed, including placeholder lines for user input, references to [AGENT_ROLE=...], [SCENARIO condition=...], etc.

5. Optional Add-Ons & DSL Integration
In the custom prompts or multi-step scripts generated above, the LLM can incorporate:

DSL for Human Architect: e.g., [MAINTAIN_CONTEXT], [CRITICAL_SELF_REVIEW].
DSL for LLM Use: e.g., [AGENT_ROLE=LegalAdvisor perspective="compliance"], [INTEGRATE agent="A,B" priority="Compliance>Creative"].
This ensures the final output is both structured and immediately usable in your orchestrations.

6. How to Use & Extend
Pick Template: Choose Template 1 (one-off) or Template 2 (multi-step).
Paste the relevant instructions into the LLM, instructing it to adopt the “Prompt Customizer” or “Master Thread Instruction Wizard” persona.
Answer the LLM’s questions about domain, style, complexity, etc.
Copy the final generated script or single-prompt solution.
Deploy that script in a new conversation, or hand it off to your user/client.
You can easily extend these templates by adding more questions, referencing advanced tokens from Part 3 – C, or weaving in heuristics from Part 2. The key idea is to let the LLM do the heavy lifting in constructing customized prompts or instructions—reducing your own overhead and improving alignment with each user’s unique scenario.

Final Note
By leveraging Section D of Part 3, you effectively equip your LLM to become a prompt-generation assistant—one that interviews the user, identifies needs, and then spins up fully formed one-off prompts or entire multi-step frameworks on demand. This approach streamlines the entire lifecycle of advanced prompt design, enabling more efficient, user-centered solutions for any domain or complexity level.
