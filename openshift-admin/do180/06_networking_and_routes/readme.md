# DO180 Lab 06 – Networking and Routes

## Purpose

This lab introduces OpenShift networking fundamentals and how applications are exposed inside and outside the cluster. You will learn how services provide internal connectivity and how routes expose applications to users.

The focus is on understanding **how traffic flows** to applications and how OpenShift simplifies networking compared to raw Kubernetes.

---

## What You Will Learn

By completing this lab, you will be able to:

- Understand how OpenShift networking differs from traditional networking
- Explain the role of Services in application connectivity
- Create and inspect Services
- Create and manage Routes
- Verify application accessibility from inside and outside the cluster

---

## Prerequisites

- Completion of DO180 Labs 01–05
- Access to an OpenShift cluster
- Ability to log in using the `oc` CLI
- An application deployed in your project

---

## Key Concepts

- Pods are not directly reachable in a stable way
- Services provide a stable virtual IP and DNS name
- Routes expose Services externally via the OpenShift router
- OpenShift manages load balancing and ingress automatically
- Application exposure is declarative, not manual

---

## Lab Tasks

You will complete the following tasks in this lab:

- Inspect existing Services in a project
- Create a Service for an application
- Verify internal connectivity using the Service
- Create a Route to expose the application externally
- Test application access through the Route

---

## Verification Mindset

After each task, verify:

- Does the Service exist and point to the correct pods?
- Are endpoints populated for the Service?
- Does the Route target the correct Service?
- Is the application reachable through the Route URL?

Always validate connectivity rather than assuming exposure worked.

---

## Completion Criteria

You have successfully completed this lab when:

- An application is accessible internally via a Service
- An application is accessible externally via a Route
- You can explain the difference between Services and Routes
- You can trace traffic flow from user to pod at a high level

---

## Notes

- Routes are an OpenShift-specific feature
- Do not manually configure load balancers or ingress controllers
- Networking issues are common sources of misconfiguration; verification is essential

Proceed to the next lab once you are comfortable exposing applications in OpenShift.
