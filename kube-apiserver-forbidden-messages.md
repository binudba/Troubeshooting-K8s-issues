
### K8s ver 1.5.x, 1.6.x

#### Kube-apiserver curl commands failing with following messages. 

```
curl https://localhost:6443/apis -k
{
  "kind": "Status",
  "apiVersion": "v1",
  "metadata": {
    
  },
  "status": "Failure",
  "message": "forbidden: User \"system:anonymous\" cannot get path \"/apis\"",
  "reason": "Forbidden",
  "details": {
    
  },
  "code": 403
  }
  ```
  
  
  Fix:
  
  kubectl get secrets -n default
  
  Replace the secrets name in following:
  
  ```
  export token=$(kubectl describe secrets default-token-xyzabc | grep token: | awk '{ print $2 }') 
  
   curl -k  https://localhost:6443/apis  -H "Authorization: Bearer $token"
   
   ```
