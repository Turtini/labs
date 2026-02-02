# Lab 02: Projects, Users, and Basic Access Control

## Objective

This lab introduces OpenShift projects (namespaces) and the foundational concepts of user access within a cluster. You will learn how projects isolate resources, how users interact with those projects, and how access is granted and verified.

By the end of this lab, you will be able to:

- Understand the purpose of OpenShift projects
- List, create, and switch between projects
- Identify how users gain access to projects
- Verify permissions using the `oc` CLI
- Develop habits for validating access before performing actions

---

## Prerequisites

- Completion of Lab 01: Getting Started with OpenShift and the CLI
- Access to an OpenShift cluster
- Valid user credentials or login token
- The `oc` CLI installed and configured

---

## Lab Overview

Projects are the primary unit of isolation in OpenShift. Almost every administrative task occurs **within the context of a project**, and many common errors result from operating in the wrong one.

This lab emphasizes:

- Intentional project selection
- Awareness of access boundaries
- Verification before action

These concepts are critical for both exam success and safe cluster operation.

---

## Tasks

You will complete the following tasks in this lab:

1. List all projects you have access to
2. Identify your current active project
3. Switch between existing projects
4. Create a new project (if permitted)
5. Verify access and permissions within a project
6. Observe how access controls affect available actions

---

## Key Concepts

- **Project**: A Kubernetes namespace with additional OpenShift metadata and access controls
- **Context**: The combination of cluster, user, and project used by the `oc` CLI
- **Least Privilege**: Users typically have access only to specific projects and actions

Understanding these concepts helps prevent accidental changes to unintended environments.

---

## Verification Mindset

After completing each task, confirm:

- Which project am I currently using?
- Do I have permission to perform this action?
- Can I verify the result using `oc get` or `oc describe`?
- Does the output match my expectations for this project?

Never assume access. Always verify.

---

## Completion Criteria

You have successfully completed this lab when you can:

- Clearly explain what an OpenShift project is
- Confidently switch between projects
- Create a project when permitted
- Recognize permission-related errors and understand why they occur
- Validate your context before taking action

---

## Notes

- Commands should be typed manually unless explicitly instructed otherwise
- Focus on understanding *why* access is granted or denied
- These skills will be used throughout all remaining DO180 labs
