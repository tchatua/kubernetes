# HPA (Horizontal Pod Autoscaler)
- In Kubernetes, I can scale my deployments **manually** or **automatically** using **Horizontal Pod Autoscaler** (**HPA**) *based on metrics* like **CPU utilization** or **custom metrics**. 

## Here's how I can perform scaling:
1. **Manual Scaling**:
- Scale Up:
To manually scale up a deployment named **app-deploy**, I can use the **kubectl scale** command:

```sh
kubectl scale --replicas=5 deployment/app-deploy
```
This command will scale the deployment to have 5 replicas.

2. **Scale Down**:
To manually scale down a deployment:

```sh
kubectl scale --replicas=3 deployment/app-deploy
```
This command will scale the deployment down to have 3 replicas.

## Autoscaling with Horizontal Pod Autoscaler (HPA):

### CPU-based Autoscaling:

- I can set up Horizontal Pod Autoscaler (HPA) to automatically scale my deployment based on CPU utilization. 
- Here's how I can create an HPA:

1. **Enable Metrics Server**: 
    - Ensure that Metrics Server is installed in my cluster. 
    - Metrics Server collects resource usage metrics from pods and nodes.
2. **Create HPA**:
   - Create an HPA using kubectl autoscale command. For example, to autoscale a deployment named *app-deploy* to maintain an **average CPU utilization of 50%** across all pods:

```sh
kubectl autoscale deployment app-deploy --cpu-percent=50 --min=2 --max=10
```
This command will create an HPA for the deployment, **targeting a CPU utilization of 50%**, with a **minimum of 2 replicas** and a **maximum of 10 replicas**.

### Custom Metrics-based Autoscaling:

- To use custom metrics for autoscaling, I need to set up custom metric APIs and corresponding HPA configurations. 
- This involves:

1. **Implement Custom Metrics API**: I need to expose custom metrics through a Metrics API. This can be done using tools like *Prometheus*, Stackdriver, or other monitoring solutions.
2. **Configure HPA**: Once you have custom metrics available, you can create an HPA targeting those metrics. 
For example:
```sh
kubectl autoscale deployment app-deploy --cpu-percent=50 --min=2 --max=10 --custom-metrics=custom.metric/api
```
Replace **custom.metric/api** with the **custom metric API path**.

- I need to ensure that your **Kubernetes cluster is properly configured to support autoscaling**, and that the necessary metrics APIs and monitoring solutions are set up and integrated with my cluster. 
- Additionally, **always monitor the performance and behavior of autoscaled deployments** to ensure they meet your application's requirements.
