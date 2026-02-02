# Lab 03: Applications & Builds

This lab focuses on **deploying applications in OpenShift using supported, exam-aligned workflows**.

On the EX280 exam, application tasks are rarely isolated. They depend on:
- correct project context
- correct permissions
- correct image or build configuration
- correct verification of runtime behavior

This lab builds the discipline required to deploy applications that **run, scale, and can be verified**, not just exist.

---

## Objectives

By the end of this lab, you will be able to:

- Deploy applications from existing container images
- Create and manage Builds and BuildConfigs
- Understand ImageStreams and image resolution
- Verify application health and rollout behavior
- Diagnose common application deployment failures
- Confirm that deployments meet task requirements exactly

These skills form the core of most EX280 exam tasks.

## Scenario & Constraints

You are responsible for deploying and managing applications on a shared OpenShift cluster.

Some applications are deployed from **existing container images**, while others must be built from **source using OpenShift Builds**. Tasks may require you to choose the correct deployment method based on the requirements provided.

This lab simulates the mixed deployment patterns commonly encountered on the EX280 exam.

---

### Assumptions

- You have access to an OpenShift cluster
- Your kubeconfig is functional
- You can create resources in at least one project
- You are not guaranteed cluster-admin privileges

You are **not** expected to modify cluster-wide build configuration.

---

### Constraints

- Applications must be deployed using **OpenShift-supported workflows**
- Images and BuildConfigs must be referenced exactly as specified
- Applications must reach a healthy runtime state
- You must verify application behavior using `oc` commands
- You must not rely on the web console

These constraints mirror EX280 exam conditions.

---

### Success Criteria

This lab is complete when you can:

- Deploy applications using the correct method (image or build)
- Confirm that builds complete successfully
- Verify that pods reach the expected state
- Validate rollout behavior after configuration changes
- Identify and fix common deployment failures

## Deployment & Build Concepts (Exam-Aligned)

This lab requires you to choose the **correct application deployment method** based on task requirements.

The EX280 exam does not reward creativity — it rewards correctness.

---

### Supported Deployment Methods

You will encounter two primary patterns:

#### Deploying from an existing image
- Uses a pre-built container image
- No source code or build required
- Faster and simpler when explicitly allowed

Typical resources involved:
- Deployment or DeploymentConfig
- Service (optional, if required)
- Route (optional, if required)

---

#### Building from source using OpenShift Builds
- Uses source code to produce an image
- Requires a BuildConfig
- Often paired with an ImageStream

Typical resources involved:
- BuildConfig
- ImageStream
- Deployment or DeploymentConfig

If a task specifies **building from source**, you must use a BuildConfig.

---

### ImageStreams (What Matters)

ImageStreams provide a stable reference to images and are commonly used on the exam.

Important behaviors:
- ImageStreams can track images built locally or pulled externally
- Deployments may reference ImageStreams instead of raw image names
- A successful build updates the ImageStream automatically

If an ImageStream is specified in the task, it must be used.

---

### Rollouts & Updates

Configuration changes may require a new rollout.

Common triggers:
- Image changes
- Environment variable updates
- ConfigMap or Secret updates (depending on usage)

Verify rollout behavior rather than assuming it occurred.

---

### Verification Expectations

At a minimum, you should be able to verify:

- Build status (if applicable)
- Image resolution
- Pod state
- Replica count
- Deployment health

A deployment that exists but does not run correctly does not meet the requirement.

---

### Discipline Reminder

- Use the method the task asks for
- Verify immediately after deployment
- If something fails, inspect before modifying

Correct method + verified outcome = points.

## Guided Tasks

Complete the following tasks **in order**.  
Treat each task as if it were an exam requirement.

Do not skip verification steps.

---

### Task 1 — Deploy an Application from an Existing Image

1. Select a project where you have permission to deploy applications.
2. Deploy an application using an existing container image.
3. Ensure the deployment creates at least one running pod.

After deployment:
- Verify the deployment exists
- Verify the pod reaches the `Running` state
- Verify the image used matches the task intent

Do not proceed until the application is healthy.

---

### Task 2 — Verify Deployment Health and Replicas

1. Inspect the deployment you created.
2. Confirm the desired and available replica counts.
3. Scale the deployment to a different number of replicas.
4. Verify the change is applied successfully.

Scaling must be observable through `oc` inspection commands.

---

### Task 3 — Build an Application from Source

1. Create a BuildConfig that builds an application from source.
2. Ensure the build produces an image.
3. Confirm the image is stored in an ImageStream.
4. Deploy the resulting image as an application.

After the build:
- Verify the build completes successfully
- Verify the ImageStream is updated
- Verify the deployed application runs correctly

If the build fails, investigate before retrying.

---

### Task 4 — Inspect and Trigger Rollouts

1. Modify the application configuration in a way that should trigger a rollout.
2. Observe rollout behavior.
3. Confirm new pods are created and old pods are replaced.

You must be able to prove that a rollout occurred.

---

### Task 5 — Introduce and Recover from a Deployment Failure

Intentionally create a failure scenario, such as:
- Referencing an incorrect image tag
- Misconfiguring an environment variable

Then recover by:
1. Identifying the failure using inspection commands
2. Correcting the configuration
3. Verifying the application returns to a healthy state

Recovery is part of the exam skill set.

---

### Task 6 — Final Application Verification

Before moving on:
- Confirm all applications are running as expected
- Confirm builds (if any) completed successfully
- Confirm no pods are in error states

If anything is unclear, investigate before proceeding.

## Verification Checklist

Before marking this lab complete, verify the following without hesitation:

- You can deploy an application from an existing container image
- You can confirm pods reach the expected `Running` state
- You can inspect deployments and verify replica counts
- You can scale a deployment and observe the change
- You can create a BuildConfig and trigger a build
- You can confirm a successful build updates an ImageStream
- You can deploy an application from a build-produced image
- You can observe and explain rollout behavior
- You can diagnose and recover from a failed deployment

If any item above feels uncertain or slow, repeat the relevant task.

---

## Lab Completion Criteria

This lab is complete when:

- You can choose the correct deployment method based on task wording
- You verify application health using `oc` commands
- You recognize build and deployment failures quickly
- You recover from errors calmly and methodically
- You never assume an application is healthy without proof

Application deployment and builds represent a **high-value scoring area** on the EX280 exam.  
Verified, running workloads earn points. Assumptions do not.
