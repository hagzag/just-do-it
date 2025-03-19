# A pod that mounts an s3 bucket

On the infra side, the bucket `developers-bucket` is already created.
The s3-csi driver is already installed, and configured to use a service account allowing to list all data in bucket `developers-bucket`, and create new objects under `/*firstname-lastname*/` path.
A storage class `s3` is created to allow the pod to mount the bucket.

In order to utilize buckets provided by the infra team, you need to create a PersistentVolume and a PersistentVolumeClaim like so:

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: s3-pv-developers-bucket
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
    volumeHandle: developers-bucket
    volumeAttributes:
      bucketName: developers-bucket
      mountOptions: "--dir-mode=0777 --file-mode=0666"
---

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: s3-pvc-developers-bucket
spec:
  accessModes:
    - ReadWriteMany
  storageClassName: s3
  resources:
    requests:
      storage: 5Gi
  volumeName: s3-pv-developers-bucket
```

## And in order to use the bucket in your pod, you need to add the following to your pod spec:

```yaml
volumes:
- name: s3-storage
  persistentVolumeClaim:
    claimName: s3-pvc-developers-bucket
```

A demo deployment is provided in the `deploy.yaml` file.