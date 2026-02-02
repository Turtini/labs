# DO180 Lab 04 – ConfigMaps and Secrets

## Purpose

This lab introduces configuration management in OpenShift using ConfigMaps and Secrets. You will learn how applications consume external configuration and sensitive data without embedding them directly into container images.

The focus is on **separating configuration from application code** and understanding how OpenShift injects configuration into running workloads.

This lab emphasizes correctness, verification, and safe handling of sensitive information.

---

## What You Will Learn

By completing this lab, you will be able to:

- Create and manage ConfigMaps
- Create and manage Secrets
- Inject configuration data into applications
- Understand the difference between ConfigMaps and Secrets
- Verify configuration usage in running pods

---

## Prerequisites

- Completion of DO180 Labs 01–03
- Access to an OpenShift cluster
- Ability to log in using the `oc` CLI
- An active project with permissions to create resources

---

## Key Concepts

- ConfigMaps store non-sensitive configuration data
- Secrets store sensitive data such as passwords and tokens
- Configuration can be injected via environment variables or mounted files
- Changes to configuration may require pod restarts or redeployments

---

## Lab Tasks

You will complete the following tasks in this lab:

- Create a ConfigMap from literal values
- Create a Secret from literal values
- Attach configuration data to an application
- Inspect how configuration is exposed inside a pod
- Verify application behavior with injected configuration

---

## Verification Mindset

After each task, verify:

- Does the ConfigMap or Secret exist?
- Is the data stored correctly?
- Is the configuration visible inside the pod?
- Is the application behaving as expected?

Never assume configuration is applied correctly without validation.

---

## Completion Criteria

You have successfully completed this lab when:

- ConfigMaps and Secrets exist in your project
- An application consumes configuration from both sources
- You can explain how configuration reaches the running container
- You can verify configuration using `oc` inspection commands

---

## Notes

- Do not expose Secrets in logs or command history
- Configuration management is foundational for real-world deployments
- Later labs will build on these concepts with more complex applications

Proceed to the next lab once you are comfortable managing configuration in OpenShift.
