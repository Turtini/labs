# Lab 07 — Commands
Troubleshooting & Debugging

## Context first
oc whoami
oc project
oc config current-context

## Find failing pods
oc get pods
oc get pods -A | egrep -i 'CrashLoopBackOff|ImagePullBackOff|Err|Pending'

## Describe and events
oc describe pod/<pod>
oc get events --sort-by=.lastTimestamp
oc get events -n <ns> --sort-by=.lastTimestamp

## Logs
oc logs pod/<pod>
oc logs -f pod/<pod>
oc logs deploy/<deploy>

## Inspect deployment/config
oc get deploy
oc describe deploy/<deploy>
oc get dc
oc describe dc/<dc>

## Check configmaps/secrets references
oc get cm
oc describe cm/<cm>
oc get secret
oc describe secret/<secret>

## Check env and mounts in running pod
oc exec -it pod/<pod> -- env | sort
oc exec -it pod/<pod> -- mount
oc exec -it pod/<pod> -- ls -la /etc
oc exec -it pod/<pod> -- ls -la /data

## Storage checks
oc get pvc
oc describe pvc/<pvc>

## Networking checks
oc get svc
oc describe svc/<svc>
oc get endpoints
oc describe endpoints/<svc>
oc get route
oc describe route/<route>

## Permission checks
oc auth can-i <verb> <resource> -n <ns>
