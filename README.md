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
