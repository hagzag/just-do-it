# A pod that mounts an s3 bucket

On the infra side, the bucket `devlelopers-bucket` is already created.
Ahe s3-csi driver is already installed, and configured to use a service account allowing to list all data in bucket `devlelopers-bucket`, cnd create new objects under `/*firstname-lastname*/` path.
a storage class `s3` is created to allow the pod to mount the bucket.

I order to utlize buckets provided by the infra team, you need to create a PersistentVolume and a PersistentVolumeClaim like so:


```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: s3-pv-devlelopers-bucket
spec:
  capacity:
    storage: 5Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  storageClassName: s3
  csi:
    driver: s3.csi.aws.com
    volumeHandle: devlelopers-bucket
    volumeAttributes:
      bucketName: devlelopers-bucket
      mountOptions: "--dir-mode=0777 --file-mode=0666"
---

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: s3-pvc-devlelopers-bucket
spec:
  accessModes:
    - ReadWriteMany
  storageClassName: s3
  resources:
    requests:
      storage: 5Gi
  volumeName: s3-pv-devlelopers-bucket
```

## And in order to use the bucket in your pod, you need to add the following to your pod spec:

```yaml
volumes:
- name: s3-storage
  persistentVolumeClaim:
    claimName: s3-pvc-devlelopers-bucket
```

A demo deployment is provided in the `deploy.yaml` file.