# Lab 01: Getting Started with OpenShift and the CLI

## Objective

This lab introduces the OpenShift command-line interface (`oc`) and the foundational concepts required to interact with an OpenShift cluster.

By the end of this lab, you will be able to:

- Log in to an OpenShift cluster using the `oc` CLI
- Identify the current user and active project
- Navigate projects (namespaces)
- Inspect cluster resources using `oc get`, `oc describe`, and `oc explain`
- Develop early verification habits that carry forward into advanced administration

---

## Prerequisites

- Access to an OpenShift cluster (training, lab, or shared environment)
- The `oc` CLI installed on your workstation
- Credentials or a login token provided by your instructor or platform

---

## Lab Overview

This lab focuses on **orientation, correctness, and confidence**, not speed.

You will practice establishing cluster access, confirming identity and context, and validating results after every action. These habits are essential for success in later DO180 labs and in real-world OpenShift administration.

---

## Tasks

You will complete the following tasks in this lab:

1. Verify that the `oc` CLI is installed and functional
2. Log in to an OpenShift cluster
3. Confirm your current user identity
4. Identify and switch between projects
5. Inspect cluster resources using basic `oc` commands
6. Practice verification after each action

---

## Verification Mindset

After completing each task, always ask:

- Did the command succeed?
- Am I operating as the expected user?
- Am I in the correct project?
- Can I verify the result using `oc get` or `oc describe`?

Do not assume context. Always verify.

---

## Completion Criteria

You have successfully completed this lab when you can:

- Log in to the cluster without errors
- Correctly identify your user and active project
- Switch projects intentionally
- Retrieve and inspect resources using the `oc` CLI
- Explain why context matters for every OpenShift command

---

## Notes

- Commands should be typed manually unless explicitly instructed otherwise
- This repository is not an answer key
- Accuracy and verification matter more than speed
