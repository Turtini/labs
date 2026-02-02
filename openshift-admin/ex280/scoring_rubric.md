# EX280 Timed Mock Exam — Scoring Rubric

This rubric is used to evaluate the **OpenShift Administration (EX280) Timed Mock Exam**.

Scoring is **outcome-based**, closely mirroring how Red Hat practical exams are graded.

The goal is not perfect code or elegance — the goal is **correct, verifiable results** produced under time constraints.

---

## Total Score: 100 Points  
**Recommended Passing Score: 70–75**

Partial credit is intentionally available.

---

## Scoring Philosophy

Points are awarded based on **observable outcomes**, not intent.

- If a resource exists, is correctly named, and behaves as required → points awarded
- If a resource is partially correct → partial credit may apply
- If work cannot be verified → no credit is awarded

Verification matters as much as configuration.

---

## How to Use This Rubric

This rubric can be used by:

- Learners performing self-assessment
- Mentors or peers acting as graders
- Instructors running timed mock exams

Each section defines:
- What is being evaluated
- How many points are available
- Common causes of point loss

Score honestly. The value is in identifying gaps.

## Cluster Access & Context — 15 Points

This section evaluates the candidate’s ability to correctly manage **authentication, project context, and permissions** throughout the exam.

Most OpenShift exam failures are caused by context errors, not technical misunderstanding.

---

### Evaluation Criteria

| Requirement | Points |
|------------|--------|
| Correct user identity verified | 5 |
| Correct project (namespace) used consistently | 5 |
| No resources created in unintended namespaces | 5 |

---

### What the Grader Looks For

- Candidate consistently works in the correct project
- Resources are created in the namespaces specified by the tasks
- No evidence of “default project” mistakes
- Context is re-verified before validation

---

### Common Deductions

- Resources created in the wrong project: −5 to −10
- Correct configuration in the wrong namespace: −5
- Verification performed from incorrect context: −5

---

### Partial Credit Notes

- If resources are correct but exist in the wrong project, **partial credit may apply**
- If context errors cause cascading failures, deductions may apply across multiple sections

---

### Grader Guidance

Context errors should be penalized consistently.

A technically correct solution in the wrong namespace is **less valuable** than a simpler solution correctly scoped.

## Projects, Users & RBAC — 15 Points

This section evaluates the candidate’s ability to correctly create projects and apply **role-based access control (RBAC)** according to task requirements.

Correct permissions are foundational. Mis-scoped RBAC often blocks otherwise correct work.

---

### Evaluation Criteria

| Requirement | Points |
|------------|--------|
| Projects created correctly | 5 |
| Roles / ClusterRoles selected appropriately | 5 |
| RoleBindings / ClusterRoleBindings scoped correctly | 5 |

---

### What the Grader Looks For

- Projects exist with the exact names specified
- Users or ServiceAccounts are granted the correct permissions
- Namespace-scoped access uses RoleBindings
- Cluster-wide access uses ClusterRoleBindings only when required
- Permissions are verified using `oc auth can-i`

---

### Common Deductions

- RoleBinding created instead of ClusterRoleBinding (or vice versa): −5
- Permissions granted in the wrong namespace: −5
- Over-permissioning beyond task requirements: −3
- No verification of access: −2

---

### Partial Credit Notes

- Correct permissions applied to the wrong subject may receive partial credit
- Overly broad permissions may reduce points even if functionality works

---

### Grader Guidance

RBAC should be evaluated on **precision**, not generosity.

Granting more access than required indicates misunderstanding and should be penalized accordingly.

## Application Deployment & Builds — 20 Points

This section evaluates the candidate’s ability to deploy applications using OpenShift-native workflows, including builds, image usage, and rollout behavior.

Applications must not only deploy — they must **run correctly and be verifiable**.

---

### Evaluation Criteria

| Requirement | Points |
|------------|--------|
| Application deployed using correct method | 5 |
| Build or image source configured correctly | 5 |
| Pods reach expected state (Running/Completed) | 5 |
| Replica count and rollout behavior correct | 5 |

---

### What the Grader Looks For

- Deployments or DeploymentConfigs exist as specified
- ImageStreams or external images are referenced correctly
- Builds complete successfully (if required)
- Pods are running without errors
- Replica counts match task requirements
- Rollouts occur as expected after configuration changes

Verification should be visible using `oc get`, `oc describe`, and logs.

---

### Common Deductions

- Deployment exists but pods are failing: −5 to −10
- Incorrect image or image tag used: −5
- Build created but never executed: −5
- Replica count incorrect: −3
- Rollout not triggered when required: −3

---

### Partial Credit Notes

- A deployment that exists but fails to run may receive partial credit
- A working application missing a required configuration detail may receive partial credit
- Manual fixes not captured in configuration may reduce points

---

### Grader Guidance

Prioritize **running, verifiable applications** over sophisticated configurations.

A simple deployment that works and can be validated should score higher than a complex deployment that does not fully function.

## Configuration with ConfigMaps & Secrets — 15 Points

This section evaluates the candidate’s ability to correctly create and **consume** configuration data using ConfigMaps and Secrets.

Creating configuration objects alone is not sufficient — applications must actively use them.

---

### Evaluation Criteria

| Requirement | Points |
|------------|--------|
| ConfigMaps created correctly | 5 |
| Secrets created correctly | 5 |
| Configuration consumed by applications | 5 |

---

### What the Grader Looks For

- ConfigMaps and Secrets exist with the exact names specified
- Key names match task requirements
- Configuration is injected via environment variables or mounted volumes
- Applications successfully start using the provided configuration
- Sensitive values are stored only in Secrets, not ConfigMaps

Verification should demonstrate that the application **depends on** the configuration.

---

### Common Deductions

- ConfigMap or Secret exists but is unused: −5
- Incorrect key names: −3
- Configuration mounted to the wrong path: −3
- Secret data exposed in plaintext elsewhere: −5 to −10

---

### Partial Credit Notes

- Correct configuration object created but not consumed may receive partial credit
- Applications running with default values instead of provided config may receive partial credit

---

### Grader Guidance

Configuration must be **intentional and observable**.

If the application does not clearly reference the ConfigMap or Secret, full credit should not be awarded.

## Storage & Persistence — 15 Points

This section evaluates the candidate’s ability to correctly provision, attach, and verify persistent storage for applications.

A PersistentVolumeClaim that exists but is not mounted does **not** satisfy the requirement.

---

### Evaluation Criteria

| Requirement | Points |
|------------|--------|
| PersistentVolumeClaim created correctly | 5 |
| PVC successfully bound | 5 |
| Storage mounted and used by application | 5 |

---

### What the Grader Looks For

- PersistentVolumeClaims exist with correct names
- Requested size, access modes, and StorageClass match requirements
- PVCs reach the `Bound` state
- Pods mount the PVC at the correct path
- Applications successfully read from or write to the mounted storage

Verification should demonstrate that storage is **actively in use**.

---

### Common Deductions

- PVC exists but remains `Pending`: −5
- PVC bound but not mounted in pod: −5
- Incorrect mount path: −3
- StorageClass does not match task requirements: −3

---

### Partial Credit Notes

- PVC created but not mounted may receive partial credit
- Mounted storage not used by the application may receive partial credit

---

### Grader Guidance

Storage should be evaluated end-to-end.

A solution is only complete when the application demonstrably uses the persistent storage provided.

## Networking, Services & Routes — 10 Points

This section evaluates the candidate’s ability to correctly expose applications using OpenShift Services and Routes.

An application that is running but **not reachable as specified** does not fully meet the requirement.

---

### Evaluation Criteria

| Requirement | Points |
|------------|--------|
| Service created correctly | 4 |
| Route created correctly | 4 |
| Application reachable through the Route | 2 |

---

### What the Grader Looks For

- Service exists with the correct name
- Service targets the correct pods using labels
- Correct port is exposed on the Service
- Route points to the intended Service
- Route configuration matches task requirements (hostname, TLS if specified)
- Application responds when accessed through the Route

Verification should include both resource inspection and connectivity testing.

---

### Common Deductions

- Service exists but targets no pods: −4
- Route exists but points to wrong Service: −4
- Incorrect port exposed: −3
- Application not reachable via Route: −2 to −5

---

### Partial Credit Notes

- Service correctly configured without a Route may receive partial credit
- Route exists but application errors may receive partial credit

---

### Grader Guidance

Reachability is the final proof of correctness.

If the application cannot be accessed through the Route as required, full credit should not be awarded.

## Resource Management & Quotas — 10 Points

This section evaluates the candidate’s ability to apply and verify resource constraints at the project or workload level.

Resource limits and quotas must be correctly defined **and enforced**.

---

### Evaluation Criteria

| Requirement | Points |
|------------|--------|
| Resource requests and limits defined | 4 |
| Quotas or LimitRanges created correctly | 4 |
| Constraints enforced as expected | 2 |

---

### What the Grader Looks For

- Resource requests and limits are specified on the correct workloads
- Quotas or LimitRanges exist in the correct project
- Resource definitions match task requirements
- Pods behave as expected under constraints (scheduled, limited, or blocked)

Verification should show that limits are **actively applied**, not merely declared.

---

### Common Deductions

- Limits defined but not applied to workloads: −4
- Quotas created in the wrong project: −4
- Incorrect resource values: −2
- No verification of enforcement: −2

---

### Partial Credit Notes

- Limits defined but not enforced may receive partial credit
- Quotas created without validation may receive partial credit

---

### Grader Guidance

Resource management should be evaluated based on **behavior**, not intent.

If workloads do not reflect the defined constraints, full credit should not be awarded.

## Scoring Interpretation & Final Notes

This rubric is designed to reflect **realistic EX280 exam scoring behavior**.

### Score Interpretation

| Score Range | Interpretation |
|------------|----------------|
| 90–100 | Strong pass — high confidence |
| 80–89 | Solid pass |
| 70–79 | Likely pass |
| 60–69 | Borderline — targeted practice needed |
| < 60 | High risk — repeat mock exam |

---

### Partial Credit Philosophy

- Partial completion may still earn points
- Correct outcomes with missing refinements may score higher than elegant but incomplete solutions
- Idempotency, correctness, and verification carry more weight than speed

---

### Grading Consistency

Graders should:
- Evaluate observable outcomes
- Apply deductions consistently across candidates
- Avoid “all-or-nothing” scoring where partial success exists

Candidates should:
- Score themselves honestly
- Focus remediation on low-scoring sections
- Repeat the timed mock after addressing gaps

---

### Final Reminder

The OpenShift Administration exam is not about memorization or clever tricks.

It rewards:
- correct configuration
- verification
- recovery
- judgment

Calm, disciplined execution is the path to success.

