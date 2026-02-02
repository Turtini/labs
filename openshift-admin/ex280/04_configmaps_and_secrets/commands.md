# Lab 04 — Commands
ConfigMaps & Secrets

## Context
oc whoami
oc project

## Create ConfigMap from literals
oc create configmap app-config --from-literal=APP_MODE=demo --from-literal=LOG_LEVEL=info
oc get configmap app-config -o yaml
oc describe configmap app-config

## Create ConfigMap from file
oc create configmap app-config-file --from-file=app.conf=./app.conf
oc get configmap app-config-file -o yaml

## Inject ConfigMap as env vars
oc set env deploy/app1 --from=configmap/app-config
oc rollout status deploy/app1

## Verify env inside pod
oc get pods
oc exec -it pod/<pod> -- env | sort

## Create Secret from literals
oc create secret generic app-secret --from-literal=API_KEY='changeme'
oc get secret app-secret
oc describe secret app-secret
oc get secret app-secret -o yaml

## Mount Secret as volume (create or patch deployment)
oc set volume deploy/app1 --add --name=secret-vol --type=secret --secret-name=app-secret --mount-path=/etc/secret
oc rollout status deploy/app1

## Verify mounted secret inside pod
oc exec -it pod/<pod> -- ls -la /etc/secret
oc exec -it pod/<pod> -- cat /etc/secret/API_KEY

## Update ConfigMap
oc edit configmap app-config
oc get configmap app-config -o yaml

## Update Secret
oc edit secret app-secret
oc get secret app-secret -o yaml

## Restart rollout if needed
oc rollout restart deploy/app1
oc rollout status deploy/app1

## Inspect references
oc describe deploy/app1
oc describe pod/<pod>
