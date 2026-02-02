# Lab 01 — Commands Reference
Cluster Access & Context

This file contains the **exact commands** used in Lab 01.
Type them manually when practicing. Avoid copy/paste during study sessions.

---

## Identity & Context Inspection

Confirm the current OpenShift user:

oc whoami

Confirm the active project (namespace):

oc project

Confirm the active kubeconfig context:

oc config current-context

List all configured contexts:

oc config get-contexts

## Project Discovery & Switching

List all projects you have access to:

oc get projects

Switch to a specific project:

oc project <project-name>

Always verify the switch succeeded:

oc project

## Permission Inspection

Check whether you can perform an action in the current project:

oc auth can-i <verb> <resource>

Check permissions in a specific project:

oc auth can-i <verb> <resource> -n <project-name>

Examples:

oc auth can-i create pods
oc auth can-i create deployments
oc auth can-i create services

## Intentional Context Error & Recovery

Switch to an unintended project:

oc project <wrong-project-name>

Attempt an action that should fail:

oc auth can-i create deployments

Recover by switching back to the intended project:

oc project <correct-project-name>

Re-verify identity and permissions:

oc whoami
oc project
oc auth can-i create deployments

## Final Confirmation Commands

Before completing the lab, confirm:

oc whoami
oc project
oc config current-context
oc auth can-i create pods

## Exam Habit Reminder

On the EX280 exam:

- Run context checks before every task
- Run permission checks before debugging failures
- Never assume a project switch succeeded
- Verification earns points; assumptions lose them

Context discipline is a graded skill.
