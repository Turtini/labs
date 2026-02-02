# DO180 Lab 07 – Troubleshooting and Debugging

## Purpose

This lab introduces foundational troubleshooting and debugging techniques in OpenShift. You will learn how to identify common application and platform issues and how to methodically diagnose problems using OpenShift-native tools.

The focus is on **observability, verification, and structured problem-solving**, not guesswork.

---

## What You Will Learn

By completing this lab, you will be able to:

- Identify common causes of application failures
- Use `oc` commands to inspect resource state
- Interpret pod status and events
- Retrieve and analyze container logs
- Perform basic in-cluster debugging

---

## Prerequisites

- Completion of DO180 Labs 01–06
- Access to an OpenShift cluster
- Ability to log in using the `oc` CLI
- An application deployed in your project

---

## Key Concepts

- Most OpenShift failures are visible through status and events
- Pods transition through well-defined lifecycle states
- Logs are the primary signal for application-level failures
- Debugging is an iterative process: observe, verify, adjust

---

## Lab Tasks

You will complete the following tasks in this lab:

- Identify pods that are not running successfully
- Inspect pod status and conditions
- Review pod events to identify failure causes
- Retrieve container logs
- Execute basic debugging commands inside a running container

---

## Verification Mindset

After each troubleshooting step, verify:

- What signal led you to this investigation?
- What does the resource status indicate?
- Do events support or contradict your assumption?
- Does the evidence explain the failure?

Avoid jumping to conclusions without supporting data.

---

## Completion Criteria

You have successfully completed this lab when:

- You can identify why a pod is failing
- You can explain the meaning of common pod states
- You can retrieve logs from containers
- You can articulate a structured troubleshooting approach

---

## Notes

- Troubleshooting skills improve with repetition
- Always start with `oc get` and `oc describe` before making changes
- Advanced debugging techniques will be introduced in later tracks

Proceed to the final lab once you are comfortable diagnosing common OpenShift issues.
