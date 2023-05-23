# sit323-737-2023-t1-prac7p

## Starting application

Please not that the image `namanyash/sit323-737-2023-t1-prac7p` for Kubernetes deployment has been pushed to DockerHub.

To start a Kubernetes deployment use the following command:

`kubectl apply -f .\kubeDeploy.yaml`

> Wait for the Kubernetes pod to change its state to `Running` and then move on to the next steps. Get pod information using the `kubectl get pods` command.

To start a Kubernetes service for the deployment use the following command

`kubectl apply -f .\kubeService.yaml`

Get the IP address for the service using the following command

`kubectl get services`

> Access the Node application on the URL `http://<Service-IP-address>:8000/getToken`

## In case of connection timeout

> For Windows docker desktop users and in case of any issues when connecting to the service use the following command:

`kubectl port-forward service/node-app-service 8000`

Access the microservice on the url `http://localhost:8000/getToken`
