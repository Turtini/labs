# DO180 Lab 03 – Commands Reference

Type these commands manually.  
Do not copy/paste during practice unless explicitly noted.

---

## 1. Verify Project Context

Confirm you are in the correct project before creating resources.

```bash
oc project
```

If needed, switch projects:

```bash
oc project <project-name>
```

---

## 2. Create a New Application

Create an application from a container image or source repository.

Example using a container image:

```bash
oc new-app <image-name>
```

Example using a source repository (if provided by your environment):

```bash
oc new-app <git-repo-url>
```

---

## 3. Observe Build and Deployment Activity

List builds created by the application:

```bash
oc get builds
```

Watch build progress:

oc logs -f build/<build-name>


List deployments:

```bash
oc get deployments
```

List pods:

```bash
oc get pods
```

---

## 4. Inspect Application Resources

List all resources created for the application:

```bash
oc get all
```

Describe the deployment:

```bash
oc describe deployment <deployment-name>
```

Pay attention to:

Image references

Replica count

Events

---

## 5. Verify Application Status

Check pod readiness:

```bash
oc get pods
```

Inspect pod details if not running:

```bash
oc describe pod <pod-name>
```

Retrieve application logs:

```bash
oc logs <pod-name>
```

---

## 6. Trigger a New Build (If Applicable)

If using a BuildConfig, start a new build manually:

```bash
oc start-build <buildconfig-name>
```

Watch the build output:

```bash
oc logs -f build/<build-name>
```

---

## Verification Checklist

Before moving on, confirm you can answer:

- Which resources were created by oc new-app?

- Is the build successful?

- Is the deployment running the expected image?

- How do I verify application health?

---

## Cleanup

If required by your environment, delete the application:

```bash
oc delete all -l app=<app-name>
```

Only perform cleanup if explicitly instructed.
