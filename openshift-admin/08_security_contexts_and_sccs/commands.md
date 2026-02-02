# Lab 08 — Commands
Security Contexts & SCCs

## Context
oc whoami
oc project

## Find failing pods
oc get pods
oc describe pod/<pod>
oc get events --sort-by=.lastTimestamp

## Identify serviceaccount used by a pod
oc get pod/<pod> -o jsonpath='{.spec.serviceAccountName}{"\n"}'
oc describe pod/<pod>

## List SCCs
oc get scc
oc describe scc/restricted
oc describe scc/anyuid
oc describe scc/privileged

## Grant SCC to a serviceaccount (namespace scoped SA, cluster-scoped SCC)
oc adm policy add-scc-to-user anyuid -z <serviceaccount> -n <namespace>

## Remove SCC from a serviceaccount
oc adm policy remove-scc-from-user anyuid -z <serviceaccount> -n <namespace>

## Verify rollout / recreate pod
oc rollout restart deploy/<deploy>
oc rollout status deploy/<deploy>
oc get pods

## Re-check events after change
oc describe pod/<pod>
oc get events --sort-by=.lastTimestamp

## Inspect security context requests
oc get pod/<pod> -o yaml
oc get deploy/<deploy> -o yaml
