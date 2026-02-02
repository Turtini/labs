# Lab 06: Networking & Routes

This lab focuses on **exposing applications in OpenShift** using Services and Routes, and verifying that applications are reachable as specified.

On the EX280 exam, many candidates deploy healthy applications that **cannot be accessed**. A running pod without a correctly configured Service or Route does not meet the requirement.

This lab builds the habit of proving application reachability, not just deployment success.

---

## Objectives

By the end of this lab, you will be able to:

- Create Services that correctly target application pods
- Expose applications using Routes
- Understand port mappings and service selectors
- Verify application reachability through Routes
- Diagnose and fix common networking misconfigurations
- Confirm that exposed applications behave as required

Networking tasks often carry partial credit — verification is the difference between partial and full points.

## Scenario & Constraints

You are responsible for exposing applications so they can be accessed by other services and external users.

Applications may already be running, but they are **not reachable** until the correct networking resources are configured. OpenShift exposes applications through Services and Routes, and both must be configured correctly to meet task requirements.

This lab simulates networking and exposure tasks commonly encountered on the EX280 exam.

---

### Assumptions

- You have access to an OpenShift cluster
- Your kubeconfig is functional
- At least one application is running in a project
- You can create networking resources in that project

You are **not** expected to modify cluster-wide networking configuration.

---

### Constraints

- Applications must be exposed using **Services and Routes**
- Service selectors must correctly target application pods
- Ports must be mapped correctly between pod, Service, and Route
- Routes must reference the correct Service
- You must verify reachability using `oc` commands and simple connectivity tests
- You must not rely on the web console

These constraints mirror EX280 exam expectations.

---

### Success Criteria

This lab is complete when you can:

- Create Services that correctly select application pods
- Expose Services using Routes
- Verify that Routes resolve and respond as expected
- Identify and fix common Service and Route misconfigurations
- Prove application reachability, not just configuration existence

## Networking Concepts (Exam-Aligned)

This lab tests your ability to correctly expose applications using **Services** and **Routes**, and to prove that traffic flows end-to-end.

On the EX280 exam, networking is graded on **reachability**, not intent.

---

### Services (What Matters)

A Service provides a stable endpoint for a set of pods.

Key attributes you must get right:
- **Name**
- **Selector labels** (must match pod labels)
- **Service port**
- **Target port** (container port)

If the selector is wrong, the Service will exist but route no traffic.

---

### Service Types (Exam-Relevant)

You will most commonly use:
- **ClusterIP** — internal access (default)

Other types may exist, but use only what the task requires.

---

### Routes (What Matters)

A Route exposes a Service externally.

Key attributes you must get right:
- **Target Service**
- **Target port**
- **Hostname** (if specified)
- **TLS settings** (if specified)

A Route that points to the wrong Service or port will exist but not work.

---

### Port Mapping Discipline

Traffic flows as follows:

Client → Route → Service → Pod → Container port

Every hop must align:
- Route port → Service port
- Service targetPort → Container port

Mismatch at any point breaks reachability.

---

### Verification Expectations

To receive full credit, you must be able to show:
- The Service selects the correct pods
- The Route points to the correct Service and port
- The application responds through the Route

Configuration without reachability earns partial credit at best.

---

### Discipline Reminder

- Inspect labels before creating Services
- Verify endpoints after Service creation
- Test Routes explicitly
- If it doesn’t respond, trace the path hop-by-hop

Reachable applications earn points. Assumptions do not.

## Guided Tasks

Complete the following tasks **in order**.  
Treat each task as if it were an exam requirement.

Do not skip verification steps.

---

### Task 1 — Inspect Application Labels and Ports

1. Select a running application in your project.
2. Inspect the pod labels.
3. Identify the container port exposed by the application.

Before creating any networking resources, you must know:
- Which labels to target
- Which port the application listens on

---

### Task 2 — Create a Service

1. Create a Service that targets the application pods.
2. Use a selector that matches the pod labels exactly.
3. Map the Service port to the correct container port.

After creation:
- Verify the Service exists
- Verify the Service has endpoints
- Confirm endpoints correspond to the correct pods

A Service without endpoints does not route traffic.

---

### Task 3 — Expose the Service with a Route

1. Create a Route that exposes the Service.
2. Use the correct Service name and port.
3. Specify a hostname if required by the task.

After creation:
- Verify the Route exists
- Inspect the Route configuration
- Confirm it points to the intended Service and port

---

### Task 4 — Verify Application Reachability

1. Retrieve the Route hostname.
2. Access the application through the Route.
3. Confirm the application responds as expected.

Reachability must be proven, not assumed.

---

### Task 5 — Introduce and Diagnose a Networking Error

Intentionally create a networking misconfiguration, such as:
- An incorrect Service selector
- An incorrect Service target port
- A Route pointing to the wrong Service

Then diagnose by:
1. Inspecting pod labels
2. Inspecting Service selectors and endpoints
3. Inspecting Route configuration

You should be able to identify exactly where traffic breaks.

---

### Task 6 — Correct the Networking Configuration

1. Fix the misconfiguration.
2. Verify endpoints are restored (if applicable).
3. Re-test application reachability through the Route.

Recovery is part of the exam skill set.

## Verification Checklist

Before marking this lab complete, verify the following without hesitation:

- You can inspect pod labels and identify the correct selector
- You can identify the container port exposed by the application
- You can create a Service that correctly targets application pods
- You can verify the Service has active endpoints
- You can create a Route that points to the correct Service and port
- You can retrieve the Route hostname
- You can access the application successfully through the Route
- You can diagnose and fix Service selector and port mismatches
- You can trace traffic flow from Route → Service → Pod → Container

If any item above feels uncertain or slow, repeat the relevant task.

---

## Lab Completion Criteria

This lab is complete when:

- You never expose an application without verifying reachability
- You treat Services and Routes as functional dependencies, not checkboxes
- You confirm endpoints exist before debugging applications
- You can isolate networking failures quickly and methodically
- You recover from misconfigurations calmly and precisely

On the EX280 exam, a Route that exists but does not respond earns little or no credit.  
Verified, reachable applications earn points.

