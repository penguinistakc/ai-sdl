# Scope Tests

## Test Case 0: Required Scope Document Sections

**Input:** Pomodoro timer -- evaluate structure and completeness of scope doc

**Expected Output Criteria:**

- Includes product overview and objectives, including the intended user and the
  product purpose.
- Includes functional requirements that cover specific behaviors for each
  feature included in the prompt.
- Includes non-functional requirements, including timing accuracy and a minimum
  of two additional relevant quality attributes.
- Includes acceptance criteria with a minimum of one observable, testable
  condition for each feature included in the prompt.
- Data requirements that address session tracking and storage.
- Explicitly states out-of-scope functionality.
- Includes assumptions, unresolved questions, and decisions that are required
  before implementation can proceed.
- Includes section headings to define each of the sections above.

**Failure Criteria (must NOT occur):**

- Fail if any of the seven required categories is missing.
- Fail if the document merely restates the four features without specifying
  behaviors.
- Fail if acceptance criteria contain only subjective language such as "works
  correctly" or "provides a good user experience."

## Test Case 1: Timer Accuracy Requirements

**Input:** Pomodoro timer -- evaluate implied non-functional requirements for
25-minute work interval and 5-minute break interval.

**Expected Output Criteria:**

- The document must acknowledge that browser timer callbacks could be delayed or
  throttled.
- Must establish that elapsed time can't be reliably calculated only by counting
  one-second callback executions, or explicitly require drift correction.
- Must specify a numeric timer-accuracy tolerance or identify the tolerance as
  an unresolved product decision blocking implementation.
- Has to address expected behavior when a user returns to a background tab after
  the timer's intended deadline through a defined requirement or a documented
  blocking question.
- A minimum of one verifiable acceptance criterion for timer accuracy.
- All performance or responsiveness requirements must have measurable
  definitions or be explicitly marked as requiring product decisions.

**Failure Criteria (must NOT occur):**

- Fail if timer accuracy does not contain a measurable threshold or documented
  blocking decision.
- Fail if the document assumes that `setInterval(1000)` guarantees exactly one
  callback per second.
- Fail if background-tab behavior is not specified.

## Test Case 2: Productivity Heat Map and Session Tracking

**Input:** Pomodoro timer -- evaluate data requirements, persistence, and
definition of the weekly productivity heat map.

**Expected Output Criteria:**

- The document must define a completed work session or explicitly identify the
  definition as a blocking product decision.
- Must specify whether session records survive browser refreshes and restarts,
  or explicitly identify persistence as an unresolved product decision.
- Must describe minimum information necessary to represent a recorded session,
  including the type of session (distinguishing work sessions from breaks), when
  the session began, when it ended, its duration, and whether the session was
  completed.
- Must define "weekly" as seven days, the rule for
  assigning sessions to calendar dates, and how days with no activity are
  represented.
- Must define a metric that the heat map will track, such as completed-session
  count or focused minutes, or flag it as unresolved.
- Must contain at least one acceptance criterion connecting record sessions to
  the displayed heat map values.

**Failure Criteria (must NOT occur):**

- Fail if the document does not define metric and aggregation rules.
- Fail if session tracking is described without addressing persistence.
- Fail if document silently assumes cloud storage or user accounts are
  necessary.
- Fail if it presents a session-counting rule without defining which sessions
  qualify.

## Test Case 3: Browser API Dependencies and Notifications

**Input:** Pomodoro app -- evaluate implied browser capabilities,
interval-transition notifications, and background execution constraints.

**Expected Output Criteria:**

- Document addresses whether user receives audible or visual feedback when work
  or break intervals end, as defined behavior or as an unresolved product
  decision.
- Must identify that browser audio playback could be restricted by autoplay
  policies or user-interaction requirements.
- If operating system notifications are proposed, must identify the associated
  permission requrements and describe behavior when permission is denied.
- Must acknowledge background-tab throttling, suspension, or delayed JavaScript
  execution.
- Must distinguish timer accuracy from the ability to deliver notifications
  precisely at interval deadline.
- Must address expected behavior when browser APIs are unavailable or blocked,
  by defining a fallback or flagging fallback as an unresolved decision.
- Must include at least one testable acceptance criterion involving an interval
  ending while the tab is inactive.

**Failure Criteria (must NOT occur):**

- Fail if document guarantees audible notifications without acknowledging
  browser playback restrictions.
- Fail if it guarantees precisely-timed background notifications without
  acknowledging limitations on browser execution.
- Fail if notification features are included but issues like denial of
  permissions or unavailable APIs are ignored.

## Test Case 4: Scope Boundaries, Open Questions, Implementation Readiness

**Input:** Pomodoro timer -- evaluate MVP scope discipline, unresolved
decisions, and whether the scope can be implemented by developers as defined.

**Expected Output Criteria:**

- Document must contain an explicitly-labeled out-of-scope section with at least
  three capabilities that are not to be included in the proposed MVP, such as
  user accounts, cross-device synchronization, third-party integrations,
  configuration timer durations, advanced analytics, etc.
- Must distinguish functionality that has been explicitly requested from
  additional proposed functionality.
- Must identify at least three genuinely unresolved product decisions that could
  materially impact implementation. Examples include automatic interval
  transitions, session persistence, heat-map calculation rules, notification
  behavior.
- Each unresolved decision must specify either its impact on implementation or
  why it must be resolved before work begins.
- Must distinguish product decisions from software engineering implementation
  choices, using at least one concrete example of each.
- Must identify a minimum of two implementation dependencies, such as heat map
  aggregation depending on session recording.
- Must define a minimum of three verifiable release-completion conditions,
  including functional correctness, data consistency, and testing in supported
  environment.

**Failure Criteria (must NOT occur):**

- Fail if document does not contain an explicit out-of-scope list.
- Fail if it silently adds authentication, cloud synchronization, or third-party
  integrations as mandatory features.
- Fail if it makes unsupported product decisions without labeling them as
  assumptions or proposals.
- Fail if significant implementation blocking questions remain unidentified.
- Fail if completion criteria consist solely of subjective phrases such as
  "product-ready" or "fully functional."
