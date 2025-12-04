+++
title = 'Hello world Kubernetes with Nginx on Minikube'
date = 2023-08-18T00:00:00+00:00
draft = false
tags = ['kubernetes', 'nginx', 'minikube', 'devops', 'tutorial']
+++

Kubernetes gives you the ability to deploy your app in a highly available way, and it has provisioning features that you can use to avoid manual tasks.

There are tons of tutorials about Kubernetes out there, but in this simple post, I just want to give you the simplest deployment ever in Kubernetes. You will see how to deploy nginx with Kubernetes and access it easily.

Before deployment, make sure you have properly installed kubectl and minikube, and remove any old stuff from minikube using the `delete` and `start` commands.

```bash
minikube delete
minikube start
```

If it works, everything is fine. Let's go ahead. The main part is the `deployment.yaml` file. Write it in a file and apply it.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

And then apply it with:

```bash
kubectl apply -f deployment.yaml
```

Now if you check the deployments:

```bash
kubectl get deployments
```

You should see something like this:

```
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment   2/2     2            2           29s
```

As you can see, there is an Nginx deployment with 2 replicas. In order to verify if it is actually working, we should check port 80 of the pods. Therefore, we need to find the IP of each pod by simply using this command:

```bash
kubectl get pods -o wide
```

And it should give you something similar to this:

```
NAME                                READY   STATUS     RESTARTS   AGE     IP            NODE       NOMINATED NODE   READINESS GATES
nginx-deployment-57d84f57dc-6wk4h   1/1     Running    0          3m22s   10.244.0.10   minikube   <none>           <none>
...
```

In my case, the IP of the Pod is `10.244.0.10`, which I should connect to the cluster and check port `80` of that. In Minikube, we can SSH to the cluster simply with:

```bash
minikube ssh
```

Now check the `<IP>:<PORT>` with this command:

```bash
curl 10.244.0.10
```

If you get an output like this:

```html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

It means your Nginx is working properly on the specified port. So you have a cluster with two Pods, each running an Nginx service.

## Expose Nginx to the world

If you want to expose your service to the outside to see it in the browser, you can use a `LoadBalancer` service like this:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-load-balancer
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
```

Apply it with:

```bash
kubectl apply -f load-balancer.yaml
```

And you should see an Nginx default page in your IP address.

![Nginx welcome page](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/z2ouvqa7uqauiucft7ao.png)

This was the most basic deployment on Kubernetes, but every big thing is made up of small pieces. In the next posts, I will try to delve deeper into Kubernetes. Have a good time! :)
