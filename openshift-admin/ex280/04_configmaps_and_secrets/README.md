# Lab 04: Configuration with ConfigMaps & Secrets

This lab focuses on **externalizing application configuration** using ConfigMaps and Secrets, and correctly consuming that configuration inside running applications.

On the EX280 exam, a very common failure mode is creating configuration objects correctly — but **not actually using them**. This lab builds the discipline required to ensure configuration is both present and actively consumed.

ConfigMaps and Secrets are not standalone artifacts. Their value is proven only when applications depend on them.

---

## Objectives

By the end of this lab, you will be able to:

- Create ConfigMaps using different input methods
- Create Secrets securely and intentionally
- Inject configuration into applications using:
  - environment variables
  - mounted volumes
- Verify that applications are consuming configuration correctly
- Update configuration and observe application behavior
- Identify and fix misconfigured or unused configuration objects

These skills are heavily tested on the EX280 exam and often carry partial credit.

## Scenario & Constraints

You are responsible for deploying applications that require **externalized configuration**.

Some configuration values are non-sensitive and may be stored in ConfigMaps. Other values are sensitive and must be stored securely using Secrets. Applications must be configured to **actively consume** this data at runtime.

This lab simulates configuration-driven application tasks commonly found on the EX280 exam.

---

### Assumptions

- You have access to an OpenShift cluster
- Your kubeconfig is functional
- You can deploy applications in at least one project
- At least one running application exists or can be deployed for testing

You are **not** expected to modify cluster-wide security configuration.

---

### Constraints

- Non-sensitive configuration must use ConfigMaps
- Sensitive values must use Secrets
- Configuration objects must be **consumed by the application**
- Configuration must be injected using supported OpenShift mechanisms
- You must verify application behavior using `oc` commands
- You must not rely on the web console

These constraints mirror EX280 exam expectations.

---

### Success Criteria

This lab is complete when you can:

- Create ConfigMaps and Secrets with exact names and keys
- Inject configuration into applications using env vars or volumes
- Verify configuration is available inside running pods
- Update configuration and observe the expected behavior
- Detect and fix configuration that exists but is unused

## ConfigMaps & Secrets Concepts (Exam-Aligned)

This lab tests your ability to choose the **correct configuration object** and ensure it is **actively consumed** by an application.

On the EX280 exam, configuration that exists but is unused earns little or no credit.

---

### ConfigMaps (Non-Sensitive Data)

Use ConfigMaps for:
- application configuration values
- feature flags
- non-secret environment variables
- configuration files

Common creation methods:
- From literals
- From files
- From directories

ConfigMaps can be consumed via:
- Environment variables
- Volume mounts

---

### Secrets (Sensitive Data)

Use Secrets for:
- passwords
- tokens
- API keys
- credentials

Important expectations:
- Sensitive data must not appear in ConfigMaps
- Secrets should not be exposed in plaintext elsewhere
- Applications must explicitly reference the Secret

Secrets can be consumed via:
- Environment variables
- Volume mounts

---

### Consumption Is Required

Creating a ConfigMap or Secret is **not sufficient**.

To receive full credit:
- The application must reference the object
- The pod must have access to the data
- The application must start successfully using the provided values

Verification should show that configuration is present **inside the running pod**.

---

### Update & Rollout Awareness

Configuration updates may require:
- Pod restarts
- Deployment rollouts

Do not assume changes are picked up automatically.

Always verify whether a rollout is required and confirm behavior after updates.

---

### Discipline Reminder

- Choose the correct object type
- Inject configuration intentionally
- Verify inside the pod
- Observe application behavior

Correct configuration + active consumption = points.

## Guided Tasks

Complete the following tasks **in order**.  
Treat each task as if it were an exam requirement.

Do not skip verification steps.

---

### Task 1 — Create a ConfigMap from Literals

1. Create a ConfigMap containing at least two non-sensitive key/value pairs.
2. Verify the ConfigMap exists with the exact name and keys specified.
3. Inspect the ConfigMap contents.

Do not attach it to an application yet.

---

### Task 2 — Inject ConfigMap via Environment Variables

1. Deploy or select an existing application.
2. Inject values from the ConfigMap as environment variables.
3. Trigger a rollout if required.
4. Verify the application starts successfully.

After deployment:
- Inspect the pod environment
- Confirm the variables are present

---

### Task 3 — Create a Secret Securely

1. Create a Secret containing at least one sensitive value.
2. Verify the Secret exists with the correct key.
3. Confirm the value is not displayed in plaintext output.

Secrets must be created intentionally and referenced explicitly.

---

### Task 4 — Inject Secret via Volume Mount

1. Mount the Secret into the application as a volume.
2. Specify the correct mount path.
3. Trigger a rollout if required.
4. Verify the pod starts successfully.

Inside the pod:
- Confirm the secret file exists
- Confirm permissions are appropriate

---

### Task 5 — Update Configuration and Observe Behavior

1. Update a value in the ConfigMap or Secret.
2. Determine whether a rollout is required.
3. Apply the update.
4. Verify whether the application reflects the change.

Do not assume the update is picked up automatically.

---

### Task 6 — Introduce and Recover from a Configuration Error

Intentionally misconfigure one of the following:
- Incorrect key name
- Incorrect mount path
- Missing environment variable reference

Then recover by:
1. Identifying the misconfiguration
2. Correcting it
3. Verifying the application returns to a healthy state

Recovery is part of the exam skill set.

## Verification Checklist

Before marking this lab complete, verify the following without hesitation:

- You can create ConfigMaps with the correct names and keys
- You can inspect ConfigMap contents and explain their purpose
- You can inject ConfigMap values via environment variables
- You can create Secrets securely without exposing sensitive data
- You can mount Secrets into applications as volumes
- You can verify configuration inside running pods
- You can update configuration and observe the correct application behavior
- You can identify and fix unused or misconfigured configuration objects

If any item above feels uncertain or slow, repeat the relevant task.

---

## Lab Completion Criteria

This lab is complete when:

- You always choose ConfigMaps for non-sensitive data
- You always choose Secrets for sensitive data
- Configuration objects are actively consumed by applications
- You verify configuration inside the pod, not just in manifests
- You understand when configuration changes require rollouts
- You can recover from configuration errors calmly and methodically

On the EX280 exam, configuration that is **created but unused** earns little or no credit.  
Verified, consumed configuration earns points.

