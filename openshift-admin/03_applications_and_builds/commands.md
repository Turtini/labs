# Lab 03 — Commands
Applications & Builds

## Context
oc whoami
oc project

## Deploy from existing image
oc new-project exam-apps
oc project exam-apps
oc new-app --name=app1 <image>

## Inspect resources
oc get all
oc get deploy
oc get pods
oc describe deploy app1
oc describe pod <pod>

## Logs
oc logs pod/<pod>
oc logs -f pod/<pod>

## Scale
oc scale deploy/app1 --replicas=2
oc get pods
oc get deploy app1

## Rollout status/history
oc rollout status deploy/app1
oc rollout history deploy/app1

## Update env (triggers rollout)
oc set env deploy/app1 KEY=value
oc rollout status deploy/app1
oc get pods

## Build from source (S2I / buildconfig)
oc new-app <source-repo-or-template> --name=app2
oc get bc
oc describe bc/app2
oc start-build app2
oc start-build app2 --follow

## Inspect build/image streams
oc get builds
oc describe build/<build>
oc get is
oc describe is/<imagestream>

## Verify app2
oc get deploy
oc get pods
oc rollout status deploy/app2
oc logs deploy/app2

## Common failure inspection
oc describe pod <pod>
oc get events --sort-by=.lastTimestamp
