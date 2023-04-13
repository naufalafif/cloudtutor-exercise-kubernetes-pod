#### Pod YAML

`contoh-pod.yml`

```{.yaml .copy}
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - image: nginx:latest
    name: nginx
    ports:
    - containerPort: 80
      protocol: TCP
```

Diatas adalah contoh file YAML untuk Pod dengan nama `nginx-pod` yang menggunakan image `nginx:latest`. Hasil dari file tersebut adalah equivalent dari perintah `kubectl run nginx --image nginx:latest --port 80`

Buat file `contoh-pod.yml` menggunakan editor disebelah kanan dan gunakan contoh yaml diatas.

Selanjutnya jalankan Pod menggunakan file `contoh-pod.yml`

```{.bash .copy}
kubectl create -f contoh-pod.yml
```

Cek apakah pod sudah berjalan menggunakan perintah `get pod`

```{.bash .copy}
kubectl get pod nginx-pod
```

```{.bash}
NAME                     READY   STATUS    RESTARTS   AGE
nginx-pod                1/1     Running   0          10m
```

Kita berhasil menjalankan pod menggunakan file YAML. Pod yang dijalankan menggunakan file YAML ataupun perintah `run` akan menghasilkan hasil yang sama. Hasil dari Pod yang dijalankan dapat dicek dengan menampilkan detail pod menggunakan parameter `output`

Gunakan perintah berikut untuk menampilkan Pod yang berjalan dalam format YAML. Output dari perintah ini akan menampilkan banyak attribute baru yang digenerate oleh Kubernetes, kita bisa mengabaikan attribute barunya

```{.yaml .copy}
kubectl get pod nginx-pod -o yaml
```

```{.bash}
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2023-04-05T10:30:25Z"
  labels:
    run: nginx
  name: nginx
  namespace: default
  resourceVersion: "740"
  uid: 50f64080-3a97-4f75-b14b-0ce923698237
spec:
  containers:
  - image: nginx:latest
    imagePullPolicy: Always
    name: nginx
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-vpggq
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  nodeName: kind-worker
  preemptionPolicy: PreemptLowerPriority
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - name: kube-api-access-vpggq
    projected:
      defaultMode: 420
      sources:
      - serviceAccountToken:
          expirationSeconds: 3607
          path: token
      - configMap:
          items:
          - key: ca.crt
            path: ca.crt
          name: kube-root-ca.crt
      - downwardAPI:
          items:
          - fieldRef:
              apiVersion: v1
              fieldPath: metadata.namespace
            path: namespace
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2023-04-05T10:30:25Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2023-04-05T10:30:30Z"
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2023-04-05T10:30:30Z"
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2023-04-05T10:30:25Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: containerd://0a3def647fa8508b76ccf26996b765da7a2f8d1a01ab2a045c5aa131a789bb32
    image: docker.io/library/nginx:latest
    imageID: docker.io/library/nginx@sha256:2ab30d6ac53580a6db8b657abf0f68d75360ff5cc1670a85acb5bd85ba1b19c0
    lastState: {}
    name: nginx
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2023-04-05T10:30:29Z"
  hostIP: 172.18.0.3
  phase: Running
  podIP: 10.244.1.3
  podIPs:
  - ip: 10.244.1.3
  qosClass: BestEffort
  startTime: "2023-04-05T10:30:25Z"
```
