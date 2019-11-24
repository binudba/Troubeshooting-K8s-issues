### Metrics Server error - unable to fully collect metrics. 

kubectl top nodes -- not working

K8s ver : v1.16.x
Mertics server ver : v0.3.4


#### Error : 

E1124 02:38:49.808374       1 manager.go:111] unable to fully collect metrics: [unable to fully scrape metrics from source kubelet_summary:host1: unable to fetch metrics from Kubelet host1
 Get https://host1:10250/stats/summary?only_cpu_and_memory=true: x509: certificate signed by unknown authority, unable to fully scrape metrics from source kubelet_summary:
 

#### Fix: 

  Edit metrics server deployment  and add following:

```
       spec:
      containers:
      - args:
        - --cert-dir=/tmp
        - --secure-port=4443
        - --kubelet-insecure-tls
        - --kubelet-preferred-address-types=InternalIP
        image: k8s.gcr.io/metrics-server-amd64:v0.3.4

```
