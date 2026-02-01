# EX280 Exam Day Playbook  
OpenShift Administration Exam Day Playbook (EX280)

This playbook is designed to be used during a timed mock exam or as a mental checklist on real exam day.
It emphasizes context awareness, verification habits, and efficient sequencing.

These instructions are meant to be followed, not memorized line-by-line.

Core Principles (Read First)

Verify everything

Never assume context

Small wins > perfect elegance

Move forward, then return to optimize

Context Hygiene (CRITICAL)

Before ANY task:

oc whoami
oc project

If something fails unexpectedly, check context first.

Recommended Execution Order

Project creation and access

RBAC and permissions

Application deployments

ConfigMaps and Secrets

Storage

Routes and networking

Resource limits and quotas

Troubleshooting tasks

Do not follow task order blindly if a better sequence exists.

Verification Mindset

After each task, ask:

Does the resource exist?

Is it in the correct namespace?

Is it named EXACTLY as requested?

Is it running, bound, or exposed correctly?

Useful verification commands:

oc get all
oc get pods
oc describe <resource>
oc logs <pod>
oc get events

Time Management Strategy

Total exam time is limited. Treat time as a resource.

Suggested pacing:

First 10 minutes: read ALL tasks

First 60% of time: complete easy/medium tasks

Middle 25%: complete complex builds

Final 15%: verification and fixes

If stuck longer than 5 minutes:

Skip

Move on

Return later

Partial credit matters.

Project & Namespace Strategy

Create all required projects early.

Verify before switching:

oc project <name>

Avoid working in the wrong namespace — this is the #1 cause of lost points.

RBAC Checklist

When working with permissions:

Confirm subject (user/serviceaccount)

Confirm role vs clusterrole

Confirm rolebinding vs clusterrolebinding

Confirm namespace scope

Verify with:

oc auth can-i <verb> <resource> --as=<user> -n <namespace>

Application Deployment Checklist

For deployments:

Image name correct

Image pull succeeds

Pod is Running or Completed

Replicas match requirements

Verify:

oc get deployment
oc describe deployment <name>
oc get pods

ConfigMaps and Secrets

Confirm:

Correct key names

Correct mount paths or env vars

Application actually consumes them

Verify:

oc describe configmap <name>
oc describe secret <name>

Storage Checklist

Confirm:

PVC exists

PVC is Bound

Pod mounts correct path

StorageClass matches requirements

Verify:

oc get pvc
oc describe pvc <name>

Networking and Routes

Confirm:

Service exists

Route points to correct service

Correct port exposed

Application responds

Verify:

oc get svc
oc get route
curl <route>

Resource Limits and Quotas

Confirm:

Limits and requests defined

Quotas enforced in namespace

Pod respects constraints

Verify:

oc describe pod <name>
oc describe quota

Troubleshooting Strategy

When something fails:

Check pod status

Check events

Check logs

Check configuration objects

Re-read the task carefully

Never assume the platform is broken.

Final Verification Pass (DO THIS)

Before time expires:

oc get all -A

Scan for:

Crashing pods

Pending PVCs

Failed builds

Misnamed resources

Fix low-effort issues first.

Mental Reset (Last 2 Minutes)

Breathe

Do not refactor

Do not delete working resources

Trust what you verified

After the Exam (For Practice Runs)

Write down:

Tasks you skipped

Tasks that cost the most time

Mistakes caused by context or naming

These become your next practice targets.
