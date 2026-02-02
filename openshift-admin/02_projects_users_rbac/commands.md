# Lab 02 — Commands
Projects, Users & RBAC

## Context
oc whoami
oc project
oc config current-context

## Project creation
oc new-project exam-dev
oc new-project exam-prod

## List projects
oc get projects

## Switch projects
oc project exam-dev
oc project exam-prod
oc project

## Inspect default roles
oc get roles
oc describe role admin
oc describe role edit
oc describe role view

## Inspect cluster roles
oc get clusterroles
oc describe clusterrole cluster-admin

## Bind edit role to a user (namespace-scoped)
oc project exam-dev
oc adm policy add-role-to-user edit <user> -n exam-dev

## Bind edit role to a serviceaccount (namespace-scoped)
oc project exam-dev
oc create sa app-sa
oc adm policy add-role-to-user edit -z app-sa -n exam-dev

## Verify permissions (current user)
oc auth can-i create pods -n exam-dev
oc auth can-i create deployments -n exam-dev
oc auth can-i create services -n exam-dev

## Verify permissions as another user (if allowed)
oc auth can-i create pods --as=<user> -n exam-dev
oc auth can-i create pods --as=<user> -n exam-prod

## Inspect rolebindings
oc get rolebindings -n exam-dev
oc describe rolebinding <binding-name> -n exam-dev

## Inspect clusterrolebindings
oc get clusterrolebindings
oc describe clusterrolebinding <binding-name>

## Remove rolebinding (if needed)
oc delete rolebinding <binding-name> -n exam-dev

## Remove a role from user/serviceaccount (if needed)
oc adm policy remove-role-from-user edit <user> -n exam-dev
oc adm policy remove-role-from-user edit -z app-sa -n exam-dev
