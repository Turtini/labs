# DO180 Lab 06 – Commands Reference

Type these commands manually.  
Do not copy/paste during practice unless explicitly noted.

---

## 1. Verify Project Context

Confirm you are in the correct project before creating networking resources.

```bash
oc project
```

If needed:

```bash
oc project <project-name>
```

---

## 2. Inspect Existing Services and Routes

List services:

```bash
oc get services
```

List routes:

```bash
oc get routes
```

List endpoints (shows which pods back a service):

```bash
oc get endpoints
```

---

## 3. Create a Service (If One Does Not Exist)

If your application has a deployment but no service, expose it.

Expose a deployment to create a Service:

```bash
oc expose deployment/<deployment-name> --port=<container-port>
```

Verify the Service exists:

```bash
oc get services
oc describe service <service-name>
```

Verify endpoints populate (this proves the Service selects pods):

```bash
oc get endpoints <service-name>
```

If endpoints are empty, check labels and pod readiness.

---

## 4. Create a Route

Expose the Service externally:

```bash
oc expose service/<service-name>
```

Verify the Route:

```bash
oc get routes
oc describe route <route-name>
```

Retrieve the Route host (URL):

```bash
oc get route <route-name> -o jsonpath='{.spec.host}{"\n"}'
```

---

## 5. Verify External Access

If your environment allows external access, test the route.

Using curl (recommended):

```bash
curl -I http://<route-host>
```

Or open the URL in a browser if provided by your platform.

If the route does not respond:

Check pod readiness

Check service endpoints

Review route/service targeting

---

## 6. Trace Traffic Flow (High-Level Verification)

Verify pods backing the Service:

```bash
oc get pods -o wide
```

Verify the Service selector:

```bash
oc get service <service-name> -o yaml
```

Verify the Route targets the correct Service:

```bash
oc get route <route-name> -o yaml
```

---

## Verification Checklist

Before moving on, confirm you can answer:

- Why do Services exist (why not access pods directly)?

- How do you prove a Service is connected to pods?

- What does a Route add that a Service does not?

- How do you find the external URL for an application?

---

## Cleanup

If required, delete the route:

```bash
oc delete route <route-name>
```

Optionally delete the service:

```bash
oc delete service <service-name>
```

Only perform cleanup if explicitly instructed.
