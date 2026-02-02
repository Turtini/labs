# DO180 Lab 08 – Security Basics and Application Permissions

## Purpose

This lab introduces foundational OpenShift security concepts as they relate to applications. You will learn how OpenShift enforces security by default and how applications interact with security constraints without requiring manual privilege escalation.

The focus is on **understanding OpenShift’s secure-by-default model**, not on advanced security configuration.

---

## What You Will Learn

By completing this lab, you will be able to:

- Understand OpenShift’s security-first design
- Explain why containers do not run as root by default
- Identify how permissions affect application behavior
- Recognize common security-related application failures
- Verify security context behavior using the `oc` CLI

---

## Prerequisites

- Completion of DO180 Labs 01–07
- Access to an OpenShift cluster
- Ability to log in using the `oc` CLI
- An application deployed in your project

---

## Key Concepts

- OpenShift enforces stricter defaults than upstream Kubernetes
- Containers typically run as non-root users
- Security constraints are applied automatically to workloads
- Many application issues are caused by incorrect security assumptions
- Understanding defaults prevents unnecessary privilege requests

---

## Lab Tasks

You will complete the following tasks in this lab:

- Inspect the security context of a running pod
- Identify the user ID an application runs as
- Observe filesystem permission behavior inside containers
- Identify security-related error messages
- Verify application behavior under default security constraints

---

## Verification Mindset

After each task, verify:

- What user is the container running as?
- Are filesystem permissions aligned with that user?
- Do error messages indicate a security restriction?
- Is the application behaving securely by default?

Security should be understood, not bypassed.

---

## Completion Criteria

You have successfully completed this lab when:

- You can explain why OpenShift runs containers as non-root
- You can identify security context information for a pod
- You recognize common security-related application failures
- You understand when security configuration is required — and when it is not

---

## Notes

- Do not attempt to disable or bypass security controls
- Advanced security configuration is covered in later tracks
- Secure defaults are a feature, not a limitation

---

## Track Completion

You have now completed the **DO180 OpenShift Administration I** practice labs.

You should be comfortable with:

- Navigating OpenShift using the `oc` CLI
- Deploying and managing applications
- Understanding storage, networking, and configuration basics
- Troubleshooting common issues
- Reasoning about OpenShift security behavior

You are now well prepared to continue into advanced OpenShift administration or exam-focused tracks such as **EX280**.
