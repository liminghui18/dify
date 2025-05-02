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

# install dify2openai so that client/chatbox can connect to dify via openai api
kompose-windows-amd64.exe -f docker-compose-image.yml convert

#build dify2openai image to fix permissions issues null->[]
prepare 4 files package.json, package-lock.json,app.js,Dockerfile
docker build -t dify2openai-j .
docker tag dify2openai-j jenux0erp/dify2openai-j:latest
docker login
docker push jenux0erp/dify2openai:latest



