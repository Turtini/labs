# DO180 Lab 04 – Commands Reference

Type these commands manually.  
Do not copy/paste during practice unless explicitly noted.

---

## 1. Verify Project Context

Confirm you are in the correct project before creating configuration.

```bash
oc project
```

If needed:

```bash
oc project <project-name>
```

---

## 2. Create a ConfigMap

Create a ConfigMap from literal key/value pairs:

```bash
oc create configmap app-config --from-literal=APP_MODE=demo --from-literal=LOG_LEVEL=info
```

Verify it exists:

```bash
oc get configmap
```

```bash
oc describe configmap app-config
```

---

## 3. Create a Secret

Create a Secret from literal values:

```bash
oc create secret generic app-secret --from-literal=DB_USER=demo --from-literal=DB_PASS='changeme'
```

Verify it exists:

```bash
oc get secret
```

```bash
oc describe secret app-secret
```

Note: oc describe will not reveal secret values.

---

## 4. Attach ConfigMap and Secret to an Application

If you have an existing deployment, inject configuration as environment variables.

Set ConfigMap values as env vars:

```bash
oc set env deployment/<deployment-name> --from=configmap/app-config
```

Set Secret values as env vars:

```bash
oc set env deployment/<deployment-name> --from=secret/app-secret
```

Watch for a rollout (pods may restart):

```bash
oc get pods
```

---

## 5. Verify Configuration Inside the Pod

Identify a running pod:

```bash
oc get pods
```

Open a shell or run a command in the container:

```bash
oc exec <pod-name> -- env | egrep 'APP_MODE|LOG_LEVEL|DB_USER'
```

(Secret values may be present in env output depending on how your environment is configured.)

---

## 6. Inspect Deployment Changes

Confirm environment variables are attached:

```bash
oc describe deployment <deployment-name>
```

Look for the Environment section.

---

## Verification Checklist

Before moving on, confirm you can answer:

- What is the difference between a ConfigMap and a Secret?

- How do you verify a ConfigMap was created correctly?

- Why does oc describe secret not show secret values?

- How do you prove a pod received configuration?

---

## Cleanup

If required, remove the env vars from the deployment:

```bash
oc set env deployment/<deployment-name> --from=configmap/app-config --remove
```

```bash
oc set env deployment/<deployment-name> --from=secret/app-secret --remove
```

Optionally delete the objects:

```bash
oc delete configmap app-config
```

```bash
oc delete secret app-secret
```

Only perform cleanup if explicitly instructed.
