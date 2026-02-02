# DO180 Lab 03 – Applications and Builds

## Purpose

This lab introduces the OpenShift application lifecycle. You will learn how applications are created, built, deployed, and managed using OpenShift-native workflows and the `oc` CLI.

The focus is on understanding **how OpenShift builds and runs applications**, not on application code itself.

This lab emphasizes correctness, verification, and awareness of build and deployment state.

---

## What You Will Learn

By completing this lab, you will be able to:

- Create applications using OpenShift build strategies
- Understand the relationship between Builds, BuildConfigs, and Images
- Deploy applications from source or container images
- Inspect application resources and deployment status
- Verify application health and accessibility

---

## Prerequisites

- Completion of DO180 Lab 01 and Lab 02
- Access to an OpenShift cluster
- Ability to log in using the `oc` CLI
- An active project where you have permission to create resources

---

## Key Concepts

- Applications in OpenShift are composed of multiple resources
- Builds transform source code into runnable container images
- Deployments manage the lifecycle of running application pods
- OpenShift automates image rebuilds and redeployments when inputs change

---

## Lab Tasks

You will complete the following tasks in this lab:

- Create a new application using `oc new-app`
- Examine the generated OpenShift resources
- Observe build and deployment processes
- Verify that the application is running correctly
- Inspect logs and resource status for validation

---

## Verification Mindset

After each task, verify:

- Does the expected resource exist?
- Is the build completed successfully?
- Are pods running and ready?
- Is the application accessible as intended?

Do not assume success without checking resource state.

---

## Completion Criteria

You have successfully completed this lab when:

- An application has been built and deployed in your project
- All related resources are running without errors
- You can explain the flow from source or image to running pod
- You can verify application status using `oc` commands

---

## Notes

- Focus on understanding resource relationships, not memorizing commands
- Troubleshooting skills will be reinforced in later labs
- Clean up resources only if instructed by your environment

Proceed to the next lab once you are confident with application builds and deployments.
