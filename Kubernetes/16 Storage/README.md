<img src="../../../img/logo.png" alt="Chmurowisko logo" width="200" align="right">
<br><br>
<br><br>
<br><br>

# Storage

---

## Tasks

1. A list of available StorageClass

   ```bash
   kubectl get sc
   ```

1. Print StorageClass details

   ```bash
   kubectl describe sc default
   ```

   ```bash
   kubectl describe sc managed-premium
   ```

1. Create PersistanceVolumeClaim with Azure Files storage class

   ```yaml
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: azurefile
   spec:
     accessModes:
       - ReadWriteMany
     storageClassName: azurefile
     resources:
       requests:
         storage: 10Gi
   ```

1. Create new Deployment with container using Azure Files PVC

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: netcoresample
     labels:
       app: sample
   spec:
     replicas: 2
     selector:
       matchLabels:
         app: sample
     template:
       metadata:
         labels:
           app: sample
       spec:
         containers:
           - name: netcoresample
             image: mcr.microsoft.com/dotnet/core/samples:aspnetapp
             ports:
               - containerPort: 80
             volumeMounts:
               - mountPath: "/mnt/test"
                 name: volume
         volumes:
           - name: volume
             persistentVolumeClaim:
               claimName: azurefile
   ```

1. Create a new file in Azure Files (using Portal).
1. Use `kubectl exec` to get a shell to a running Container.
1. List files inside `/mnt/test`.

## END LAB

<br><br>

<center><p>&copy; 2021 Chmurowisko Sp. z o.o.<p></center>
