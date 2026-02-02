# Lab 05 — Commands
Storage & Persistence

## Context
oc whoami
oc project

## StorageClasses
oc get storageclass
oc describe storageclass <sc>

## Create PVC
oc apply -f - <<'EOF'
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: app-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
EOF

## Check PVC status
oc get pvc
oc describe pvc/app-pvc

## Mount PVC into deployment
oc set volume deploy/app1 --add --name=data-vol --type=pvc --claim-name=app-pvc --mount-path=/data
oc rollout status deploy/app1

## Verify mount inside pod
oc get pods
oc exec -it pod/<pod> -- df -h
oc exec -it pod/<pod> -- mount | grep /data
oc exec -it pod/<pod> -- ls -la /data

## Write data
oc exec -it pod/<pod> -- sh -c "date > /data/persist.txt"
oc exec -it pod/<pod> -- cat /data/persist.txt

## Restart pod to prove persistence
oc delete pod/<pod>
oc get pods
oc exec -it pod/<new-pod> -- cat /data/persist.txt

## Inspect volume usage
oc describe pod/<pod>
oc describe deploy/app1
