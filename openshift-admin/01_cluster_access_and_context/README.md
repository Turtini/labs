# Lab 01: Cluster Access & Context

This lab focuses on **cluster access, user identity, and project context** — the most common source of silent failure on the OpenShift Administration (EX280) exam.

Before you can configure applications, storage, or networking, you must be able to reliably answer three questions:

1. Who am I logged in as?
2. Which project am I operating in?
3. What permissions do I have in this context?

This lab builds the habits required to answer those questions **every time**, under exam pressure.

---

## Objectives

By the end of this lab, you will be able to:

- Verify your OpenShift user identity
- Inspect and understand kubeconfig context
- Switch projects intentionally
- Confirm permissions before performing actions
- Detect and recover from context-related mistakes

These skills are foundational and will be assumed in all subsequent labs.

## Scenario & Constraints

You have been granted access to an existing OpenShift cluster used by multiple teams.

During the exam, you will be required to perform tasks across **multiple projects** and **multiple permission scopes**. Mistakes made early due to incorrect context often cause cascading failures later.

This lab simulates that environment.

---

### Assumptions

- You already have access to an OpenShift cluster
- Your `kubeconfig` is configured and functional
- You may be logged in as a non-admin user
- Multiple projects already exist on the cluster

You are **not** expected to create or destroy the cluster itself.

---

### Constraints

- You must not assume your current project
- You must not assume your current user
- You must verify context before performing any action
- You must rely on `oc` commands only (no web console)

These constraints mirror EX280 exam conditions.

---

### Success Criteria

This lab is complete when you can:

- Confidently identify your active user and context
- Switch projects intentionally and verify the change
- Confirm permissions before attempting modifications
- Recognize and correct context-related errors without guesswork

