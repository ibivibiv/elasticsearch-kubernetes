# elasticsearch-kubernetes
simple files for making a kubernetes docker Elasticsearch deployment

create the docker file with the included docker folder.  It has the elasticsearch config and the Dockerfile.

There is also a shell script for clearing the conductor index.  It doesn't copy to the docker image but you can add it if you like to the dockerfile.  You will want to change the image name in the yaml's below to the one you create (it's currently ibivibiv/elasticsearch5 for the one I created)


Next create the deployment by using kubectl create -f <filename> in order for the following yaml's:
  
  1.  elasticsearchdiscoveryservice.yaml. (the service to make the nodes have a zen unicast discovery node)
  2.  elasticsearchdiscoverydeployment.yaml (the actual discovery node)
  3.  elasticdata.yaml (data node deployment, starts with scale of 2 but can be increased)
  
  
The order is important because the service is a common endpoint by hostname, the discovery deployment acts as the zen master and then the data nodes point to the zen master.

Things left to do:  I need to create scripts for automating the creation of default storage classes and then the claims.  For now these just default to "storage" which needs to be created by hand)


