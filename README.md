# dify
create helm template  tar -czvf dify2openai.tgz dify2open
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

configure difyopenai
DIFY_API_URL: http://dify.hw-onboarding.ru/v1

troubleshooting dify2openai
https://87.242.94.72  :Congratulations! Your project has been successfully deployed.
https://87.242.94.72/v1/models   {"object":"list","data":[{"id":"dify","object":"model","owned_by":"dify","permission":[]}]}
post: chat/completion: 200 OK

confgure web chatbox:
api hosts: https://87.242.94.72/v1
ingress: https: domain name: blank  path:/  destionation service : dify2openai port:3000
api path:/chat/completions  by defalut for chat
model: dify 

configure for ios chatbox
API host: http yes, https not working
you need to check the checkbox-改善网络兼容性






