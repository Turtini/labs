# DO180 Lab 05 – Storage and Persistence

## Purpose

This lab introduces persistent storage concepts in OpenShift. You will learn how applications request storage, how OpenShift provides it, and how data persists beyond the lifecycle of individual pods.

The focus is on understanding **why persistence matters**, how storage is abstracted, and how applications safely use persistent data in a cluster environment.

---

## What You Will Learn

By completing this lab, you will be able to:

- Understand the role of persistent storage in OpenShift
- Explain PersistentVolumes (PV) and PersistentVolumeClaims (PVC)
- Request persistent storage for an application
- Attach storage to a running workload
- Verify that data persists across pod restarts

---

## Prerequisites

- Completion of DO180 Labs 01–04
- Access to an OpenShift cluster
- Ability to log in using the `oc` CLI
- An active project with permissions to create storage-related resources

---

## Key Concepts

- Pods are ephemeral by design
- PersistentVolumes represent storage provided by the cluster
- PersistentVolumeClaims represent storage requested by applications
- Storage is bound dynamically or statically depending on the cluster configuration
- Applications should never assume local filesystem persistence

---

## Lab Tasks

You will complete the following tasks in this lab:

- Inspect available storage classes
- Create a PersistentVolumeClaim
- Attach persistent storage to an application
- Write data to the persistent volume
- Restart pods and verify data persistence

---

## Verification Mindset

After each task, verify:

- Is the PersistentVolumeClaim bound?
- Is the volume mounted inside the pod?
- Does data remain after pod restarts?
- Does the application behave as expected with persistent storage?

Always verify storage state before assuming data safety.

---

## Completion Criteria

You have successfully completed this lab when:

- A PersistentVolumeClaim exists and is bound
- An application successfully mounts persistent storage
- Data written by the application persists across pod restarts
- You can explain the difference between pod storage and persistent storage

---

## Notes

- Storage behavior depends on cluster configuration
- Do not delete PVCs unless explicitly instructed
- Persistent storage concepts apply to nearly all real-world applications

Proceed to the next lab once you understand how OpenShift handles application data persistence.
