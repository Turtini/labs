# Lab 06 — Commands
Networking & Routes

## Context
oc whoami
oc project

## Inspect pod labels and container ports
oc get pods --show-labels
oc describe pod/<pod>

## Create Service (target by selector labels)
oc expose deploy/app1 --name=app1-svc --port=8080 --target-port=8080
oc get svc
oc describe svc/app1-svc

## Verify endpoints
oc get endpoints
oc describe endpoints/app1-svc

## Create Route
oc expose svc/app1-svc --name=app1-route
oc get route
oc describe route/app1-route

## Get route host
oc get route app1-route -o jsonpath='{.spec.host}{"\n"}'

## Test route (if curl available)
curl -I http://$(oc get route app1-route -o jsonpath='{.spec.host}')

## Debug selector mismatch
oc get svc app1-svc -o yaml
oc get pods --show-labels
oc get endpoints app1-svc -o yaml

## Debug port mismatch
oc describe svc/app1-svc
oc describe route/app1-route
oc describe pod/<pod>
