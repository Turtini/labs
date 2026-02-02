# Full Mock EX280 Exam Scenario

This mock exam simulates the **Red Hat Certified OpenShift Administrator (EX280)** exam as closely as possible in structure, scope, and pressure.

You are expected to complete a series of independent but related tasks on a live OpenShift cluster. Tasks may be partially broken, incomplete, or blocked by configuration, security, or permissions.

This is not a learning lab. This is an **execution and verification exam**.

---

## Exam Rules

- Total time: **4 hours**
- No external documentation
- No web console
- Use only the `oc` CLI
- Partial credit is awarded only when requirements are met and verified
- Guessing, brute force fixes, or over-privileging may reduce score

Treat this exactly like exam day.

## Scoring Model

The mock exam is scored out of **300 points**.

Each task is graded independently.

General scoring principles:

- Correct resource creation without verification earns partial credit
- Verified, functional outcomes earn full credit
- Over-privileged or unsafe solutions may lose points
- Broken but partially correct solutions may earn partial credit

You should always aim for:
Correct → Minimal → Verified

## Environment Assumptions

- You are provided with a functional kubeconfig
- Multiple projects already exist
- Some applications are intentionally broken
- You are not a cluster-admin unless explicitly stated
- Default StorageClass exists
- Default SCCs are enforced

You are not expected to modify cluster-wide infrastructure unless explicitly instructed.

## Exam Tasks Overview

You are responsible for completing the following tasks:

1. Cluster access & context verification
2. Project creation and RBAC configuration
3. Application deployment from image
4. Application build from source
5. Configuration using ConfigMaps and Secrets
6. Persistent storage configuration
7. Service and Route exposure
8. Troubleshooting a broken application
9. Resolving SCC-related failures
10. Final verification and cleanup

Each task includes explicit requirements.

## Task 1 — Cluster Access & Context (20 points)

- Verify your user identity
- Verify your current project
- Switch to the project named `exam-apps`
- Verify permissions before proceeding

Scoring:
- 10 pts: correct context
- 10 pts: verification shown

## Task 2 — Projects & RBAC (30 points)

- Create a project named `exam-dev`
- Grant a user or ServiceAccount edit access to `exam-dev`
- Ensure the subject has no access to `exam-prod`
- Verify permissions using `oc auth can-i`

Scoring:
- 10 pts: correct project
- 10 pts: correct RBAC scope
- 10 pts: verification

## Task 3 — Deploy from Existing Image (25 points)

- Deploy an application from a provided container image
- Ensure at least one pod reaches `Running`
- Verify replica count and image usage

Scoring:
- 15 pts: deployment works
- 10 pts: verification

## Task 4 — Build from Source (30 points)

- Create a BuildConfig using provided source
- Ensure the build completes successfully
- Deploy the resulting image
- Verify application runs

Scoring:
- 15 pts: successful build
- 15 pts: verified deployment

## Task 5 — Configuration (30 points)

- Create a ConfigMap with required values
- Create a Secret for sensitive data
- Inject both into the application
- Verify configuration inside the running pod

Scoring:
- 15 pts: correct configuration objects
- 15 pts: verified consumption

## Task 6 — Persistent Storage (30 points)

- Create a PVC with specified size and access mode
- Mount it into the application
- Write data to the volume
- Restart the pod and confirm persistence

Scoring:
- 15 pts: correct PVC and mount
- 15 pts: verified persistence

## Task 7 — Networking & Routes (30 points)

- Create a Service targeting the application
- Expose the Service using a Route
- Verify application reachability

Scoring:
- 15 pts: correct Service/Route
- 15 pts: verified access

## Task 8 — Troubleshooting (30 points)

- Diagnose a failing application
- Identify root cause
- Apply minimal fix
- Verify recovery

Scoring:
- 15 pts: correct diagnosis
- 15 pts: verified fix

## Task 9 — Security Contexts & SCCs (25 points)

- Identify SCC-related pod failure
- Determine required SCC
- Grant SCC to correct ServiceAccount
- Verify pod startup

Scoring:
- 15 pts: correct SCC selection
- 10 pts: verified behavior

## Task 10 — Final Verification (20 points)

- Confirm all applications are running
- Confirm no pods are in error states
- Confirm storage, routes, and configuration remain functional

Scoring:
- 20 pts: clean final state

## Exam Completion Criteria

You pass the mock exam when:

- You complete all tasks within time
- You verify every requirement
- You avoid unnecessary privilege escalation
- You remain calm and methodical throughout

This mock is intentionally harder than many real exam paths.

