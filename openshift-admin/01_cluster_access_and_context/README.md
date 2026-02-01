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
