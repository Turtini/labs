# Lab 01: Getting Started with OpenShift and the CLI

## Objective

This lab introduces the OpenShift command-line interface (`oc`) and the basic concepts required to interact with an OpenShift cluster.

By the end of this lab, you will be able to:

- Log in to an OpenShift cluster using the `oc` CLI
- Identify the current user and project
- Navigate projects (namespaces)
- Inspect cluster resources using `oc get`, `oc describe`, and `oc explain`
- Develop early verification habits that carry forward into advanced administration

---

## Prerequisites

- Access to an OpenShift cluster
- The `oc` CLI installed on your workstation
- Valid cluster credentials

> ⚠️ These labs assume you are working against a **real OpenShift cluster**, not a simulator.

---

## Key Concepts Introduced

- OpenShift vs Kubernetes
- The role of the `oc` CLI
- Projects (OpenShift) vs Namespaces (Kubernetes)
- Declarative resource inspection
- Verification-first workflows

---

## Lab Tasks

You will perform the following tasks:

1. Verify access to the OpenShift cluster
2. Confirm your identity and current context
3. List and switch between projects
4. Inspect common cluster resources
5. Learn how to self-verify actions

Follow the steps carefully and **verify each action before moving on**.

---

## Verification Mindset (Important)

After every command, ask yourself:

- Did the command succeed?
- Did it change cluster state or only read it?
- How would I prove this worked if asked?

These habits matter more than speed at this stage.

---

## Completion Criteria

You have completed this lab successfully when you can:

- Confidently navigate projects using the `oc` CLI
- Explain what project you are in and why
- Retrieve and describe cluster resources without guessing
- Use `oc explain` to explore unfamiliar objects

---

## Next Lab

Proceed to **Lab 02: Images, Containers, and Pods** once you are comfortable navigating the cluster and CLI.
