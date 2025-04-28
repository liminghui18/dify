# dify
# 1 prepare dependent resources
      posgresql, 
      redis, 
      vectordb/milvus  
      external storage/OBS etc    
      ELB as ingress controller  -> done  
# 2 check myvalues.yaml for production 
      check latest production version e.g. 1.2.0  
      host value should be registered as private zone in DNS, one subdomain name and IP address of ELB(as ingress controller) has been added to record set
# create namespace
kubectl patch storageclass сsi-disk -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
kubectl exec -it dify-api-pod -n dify -- flask db upgrade

kubectl run test-pod --image=busybox --rm -it --restart=Never -- sh to test pods
nc -zv 10.0.0.115 5432
telnet 10.0.0.115 5432 to test if port can be connected

