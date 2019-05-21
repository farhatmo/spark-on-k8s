# Submitting Applications to minikube

## Docker Images

Kubernetes requires users to supply images that can be deployed into containers within pods. The images are built to be run in a container runtime environment that Kubernetes supports. Docker is a container runtime environment that is frequently used with Kubernetes. Spark (starting with version 2.3) ships with a Dockerfile that can be used for this purpose, or customized to match an individual application’s needs. It can be found in the kubernetes/dockerfiles/ directory.

Spark also ships with a bin/docker-image-tool.sh script that can be used to build and publish the Docker images to use with the Kubernetes backend.

Example usage is:


```
cd /usr/local/Cellar/apache-spark/2.4.0/libexec
./bin/docker-image-tool.sh -m -t v2.4.0 build
```

## Submit spark app on kubernetes on cluster mode

To get cluster infos, 
```
kubectl cluster-info
```

To launch Spark Pi in cluster mode,

```
spark-submit \
--master k8s://https://192.168.99.100:8443 \
--deploy-mode cluster \
--name spark-pi \
--class org.apache.spark.examples.SparkPi \
--conf spark.executor.instances=3 \
--conf spark.kubernetes.container.image=spark:v2.4.0 \
local:///opt/spark/examples/jars/spark-examples_2.11-2.4.0.jar
```

# Submitting Applications to Google Kubernetes Engine (GKE)

