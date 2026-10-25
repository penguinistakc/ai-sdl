# Proposed changes to create-scope.md for Test Case 1

Source prompt: `ai-sdl/module-1/create-scope.md`  
Rubric: Test Case 1 in `ai-sdl/module-1/create-scope-tests.md`

These changes are intended to be applied together. Each proposal edits only one section of the prompt; none requires a paired edit in another section. "Constraint" below refers to the existing **Constraints** heading. The prompt already requests measurable requirements and environment-aware acceptance criteria, but does not explicitly require several timer-specific details tested by Case 1. No Role or Task changes are needed.

## 1. Explain browser timer scheduling limits

**Target section:** Context  
**Location:** After the sentence about browser execution limits, API availability, and permissions.

**Proposed addition:**

> For timer features, browser callbacks may be delayed or throttled when a tab is in the background, and execution may be suspended. A callback scheduled every 1,000 milliseconds is not a guarantee of one execution per elapsed second. OS sleep and browser background-tab behavior are distinct operating conditions that the scope must address.

**Why:** Makes the browser-specific limitation explicit instead of relying on the model to infer it from generic platform context. Covers the first expected criterion and guards against the `setInterval(1000)` failure condition.

## 2. Require elapsed-time reconciliation

**Target section:** Constraint  
**Location:** Append to constraint 8, Environment constraints.

**Proposed addition:**

> For timers, explicitly require elapsed-time reconciliation or drift correction that accounts for delayed or missed callbacks. State that counting one-second callback executions alone is insufficient to determine elapsed time. Define the required behavior without prescribing a particular JavaScript library or implementation.

**Why:** Covers the second expected criterion. Reconciliation limited to OS resume is insufficient to establish behavior under browser callback delays.

## 3. Require a numeric timer tolerance or a blocking decision

**Target section:** Constraint  
**Location:** Append to constraint 3, Measurable quality requirements.

**Proposed addition:**

> For timer features, specify a numeric accuracy tolerance and the operating conditions to which it applies, covering both work and break intervals. If no tolerance has been established, explicitly identify it as an unresolved product decision blocking timer implementation, explain its impact, and label any suggested value as a proposal. Do not leave accuracy described only as "accurate" or scoped to undefined "normal operation."

**Why:** Covers the third expected criterion and the failure condition for missing measurable accuracy or a documented blocking decision. Avoids silently inventing an approved product threshold.

## 4. Define return behavior after a background deadline

**Target section:** Constraint  
**Location:** Append to constraint 8, Environment constraints, after proposal 2.

**Proposed addition:**

> Explicitly address returning to a background tab after a timer's intended deadline. Define how the timer reconciles its remaining time and completion state, and what completion recording or interval transition occurs on return. If that behavior has not been decided, document the specific question and mark it as blocking implementation of that behavior. A statement about OS sleep/suspend alone does not satisfy this requirement.

**Why:** Covers the fourth expected criterion and the failure condition for unspecified background-tab behavior. Allows the blocking-question alternative permitted by the rubric.

## 5. Add a verifiable accuracy acceptance condition

**Target section:** Constraint  
**Location:** Append to constraint 9, Acceptance coverage.

**Proposed addition:**

> Include at least one explicit timer-accuracy acceptance criterion. State the interval duration, operating conditions, elapsed-time reference, measurement point, and allowed error so a tester can compare observed timer state with independently elapsed time. Cover 25-minute work and 5-minute break intervals when those durations are requested, including delayed callbacks and returning after a background deadline. Reference the stated numeric tolerance. If the tolerance or return behavior is unresolved, provide the test procedure with clearly identified pending parameters and state that the affected acceptance test and implementation remain blocked until those product decisions are resolved. Do not substitute a generic "all requirements pass" statement for an accuracy test.

**Why:** Covers the fifth expected criterion and connects the accuracy NFR to a concrete verification procedure. Pending parameters make an unresolved decision visible; they do not make the test executable or constitute a passing verification result.

## 6. Check every performance and responsiveness claim

**Target section:** Constraint  
**Location:** Append to constraint 3, Measurable quality requirements, after proposal 3.

**Proposed addition:**

> Before finalizing the scope, review every performance and responsiveness claim throughout the document, including goals, functional requirements, and acceptance criteria. Give each claim a measurable limit and applicable conditions, or explicitly mark the missing measure as requiring a product decision. Apply this check to terms such as "immediately," "real-time," "fast," and "responsive," as well as timer accuracy.

**Why:** Reinforces the sixth expected criterion across the entire output, rather than only within the Non-functional Requirements section.

## Coverage check

| Test Case 1 expected criterion | Proposed changes |
|---|---|
| Acknowledge delayed/throttled browser callbacks | 1, 2 |
| Reject callback counting alone or require drift correction | 1, 2 |
| Numeric timer tolerance or explicit blocking decision | 3 |
| Return after a background deadline: behavior or blocking question | 4 |
| Verifiable timer-accuracy acceptance criterion | 5 |
| All performance/responsiveness claims measurable or awaiting product decisions | 3, 6 |

These are prompt changes, not a guarantee that a generated scope will pass. Regenerate the scope and evaluate every Case 1 criterion, including whether an accuracy acceptance condition is actually verifiable and any permitted unresolved decisions are explicitly blocking.
