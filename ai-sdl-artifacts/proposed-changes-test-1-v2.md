# Proposed changes to create-scope.md — version 2

These proposals strengthen a broadly generalizable scope-writing skill. They introduce no product-specific features, browser-specific rules, interval durations, APIs, or prescribed technical solutions. Each change targets only one existing prompt section. "Constraint" refers to the existing **Constraints** heading.

Test each proposal independently against the unchanged baseline prompt. Apply only one proposal per experiment; do not carry changes from an earlier experiment into the next. Their purpose is to measure whether an individual change improves the skill's derivation of measurable requirements, environmental limitations, recovery behavior, or acceptance tests from the supplied product description. Each proposal is self-contained; references to existing constraints refer to the baseline prompt, not another proposal.

## 1. Require an analysis of implied requirements

**Target section:** Task  
**Location:** Append to the existing task description.

**Proposed addition:**

> Derive requirements implied by the requested behavior and deployment context, including conditions under which dependencies or environmental limitations could prevent the intended outcome. Carry each material finding into a defined requirement, a labeled proposal, or an unresolved decision with its implementation impact and blocking status.

**Why:** Makes the derivation of implied requirements an explicit deliverable. Merely mentioning general platform constraints does not ensure they appear in the resulting scope.

## 2. Separate product expectations from environmental guarantees

**Target section:** Context  
**Location:** Append to the existing deployment-context discussion.

**Proposed addition:**

> A requested outcome may depend on capabilities whose availability, execution, or delivery is not guaranteed by the operating environment. Distinguish the intended product behavior from guarantees the environment can actually support. Do not assume that initiating an operation proves its successful execution, or that an observed signal is an authoritative measure of the underlying state.

**Why:** Encourages recognition of unreliable environmental signals and execution guarantees without naming a particular platform, feature, or implementation technique.

## 3. Make correctness and quality requirements measurable

**Target section:** Constraint  
**Location:** Append to constraint 3, Measurable quality requirements.

**Proposed addition:**

> For each material correctness or quality requirement, define the observable quantity, reference or basis of comparison, applicable operating conditions, and measurable acceptance boundary. Where relevant, specify tolerances and limits. If a required measure has not been established, identify it as a product decision, explain its impact, and state whether it blocks implementation or verification. An unresolved measure necessary to determine correctness must be marked as blocking the affected work. Label suggested values as proposals. Apply these rules to claims throughout the document, not only the non-functional requirements section.

**Why:** Produces explicit accuracy and responsiveness requirements when relevant, without assuming which measures or values a product needs. Prevents undefined qualifiers such as "normal operation" from obscuring the conditions being specified.

## 4. Specify behavior when normal execution is interrupted

**Target section:** Constraint  
**Location:** Append to constraint 8, Environment constraints.

**Proposed addition:**

> For each material environmental limitation, identify the affected product behavior and address relevant delays, interruptions, unavailability, and recovery. When execution or observation resumes, define how the product establishes its current state and handles outcomes that became due or occurred during the interruption. Distinguish correctness of recovered state from timeliness of execution or user feedback. Define the required observable behavior without prescribing an engineering mechanism unless a supplied constraint requires it. If behavior is undecided, document the specific decision, its impact, and whether it blocks the affected implementation.

**Why:** Elicits recovery and reconciliation requirements for products that need them, while allowing engineering to choose an appropriate mechanism. Avoids treating acknowledgment of a limitation as a complete behavioral specification.

## 5. Connect critical requirements to verification

**Target section:** Constraint  
**Location:** Append to constraint 9, Acceptance coverage.

**Proposed addition:**

> Trace each material correctness or quality requirement to at least one explicit acceptance condition. State the initial conditions, action or environmental event, observation point, and expected result, including applicable measures and tolerances. Cover normal operation and material adverse or recovery conditions identified in the scope. A general statement that all requirements must pass is not a substitute for these conditions. If a necessary product decision remains unresolved, identify the affected test parameters and mark verification as blocked until they are resolved; do not present an incomplete test as executable.

**Why:** Ensures that measurable requirements lead to actual acceptance conditions, including environmental edge cases, rather than remaining isolated statements.

## 6. Add a final consistency and completeness check

**Target section:** Constraint  
**Location:** Add a new constraint after constraint 10, Release completion.

**Proposed addition:**

> **Requirements consistency:** Before finalizing, check that each material environmental risk has corresponding behavior or an explicitly unresolved decision; each material correctness or quality claim has a measurable boundary or a documented blocking decision; and each such requirement has an acceptance condition or explicitly blocked verification. Resolve contradictions across sections. Do not infer that coverage of one operating condition establishes behavior for a different condition. Retain only requirements relevant to the supplied product and context.

**Why:** Closes gaps between context, requirements, open questions, and acceptance criteria. The relevance rule prevents the skill from adding a fixed checklist of unrelated product capabilities.

## Relationship to Test Case 1

| What the test requires | General principle strengthened | Proposals |
|---|---|---|
| Recognition of environmental delays and limitations | Derive implied requirements; separate expectations from actual guarantees | 1, 2, 4 |
| Reliable determination of underlying state | Do not treat environmental signals as authoritative; define recovery correctness | 2, 4 |
| Numeric accuracy tolerance or a blocking decision | Define measurable boundaries and explicit decision status | 3, 6 |
| Behavior after interruption beyond an intended completion point | Define recovery state and handling of outcomes due during interruption | 4 |
| Verifiable accuracy acceptance condition | Trace correctness and quality requirements to explicit tests | 5, 6 |
| Measurable performance and responsiveness claims | Review measures and conditions throughout the document | 3, 6 |

These changes improve the reasoning process rather than embedding the test's product details into the skill. Whether the resulting scope passes Test Case 1 still depends on applying that process to the supplied product and identifying its specific constraints. Regenerate the scope and evaluate it against every criterion; prompt changes alone do not establish a pass.

## Independent experiment procedure

1. Keep the original `create-scope.md` as the baseline. For each experiment, create a variant containing exactly one of the six proposed changes.
2. Generate a scope using the same product description, model, and generation settings as the baseline. Use a fresh conversation for each run to avoid influence from previous evaluations.
3. Evaluate each output against the same version of the rubric. Record PASS/FAIL for every individual criterion, supporting evidence, and the overall case result.
4. Compare each variant directly with the baseline. Record FAIL → PASS improvements and PASS → FAIL regressions. For compound criteria, also note improved subrequirements even when the full criterion remains FAIL.
5. Treat a single run as preliminary evidence; repeat promising experiments under comparable conditions to check whether gains persist despite output variability. Test combinations separately only after assessing the individual changes.

A useful change can improve individual criteria without making the entire case pass. Product-specific technical gaps may still require additional input context; they do not automatically justify adding technical rules to the general skill.
