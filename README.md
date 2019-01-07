# dual-welcome

CND example with multiple cnd up on the same k8s deployment

*Prerequisites: you need to have a kubernetes cluster running and `kubectl` pointing to it.*

Clone this repo:

```console
git clone https://github.com/okteto/welcome-double
cd welcome-double
```

Deploy the welcome service by running the following command.
```console
$ kubectl create -f manifests 
deployment.apps/welcome created
service/welcome1 created
service/welcome2 created

$ kubectl get service welcome1 welcome2
NAME       TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)          AGE
welcome1   LoadBalancer   10.15.253.35    35.204.72.236    8080:30217/TCP   19h
welcome2   LoadBalancer   10.15.246.131   35.204.124.187   8081:32092/TCP   19h
```
It might take a minute or two for the services to expose the external ips depending on your cluster.

*If you're using minikube, you'll need to either change the services to use a NodePort, or enable load balancers in your instance.*

Open your browser and hit the external-ips. You should see our welcome services, a place to vote on whether you prefer dogs or cats. Go ahead and place a few votes on your preferred species. 

Now that your service is running, it's time to do some **cloud native development**. Run the following command on your terminal

```console
$ cd welcome1
$ cnd up
Activating your cloud native development environment...
Linking '/Users/ramiro/okteto/welcome1' to ramiro/welcome...
Ready! Go to your local IDE and continue coding!
```

Open your favorite IDE, go to `welcome1/app.py` and change the value of  `option_a` (line 7) from `Cats1` to `Otters1` and save the file. Go to the browser, reload the page, and check the label on the first button. Your changes were applied instantly and automatically!

Now open s new terminal and run the following command on your terminal

```console
$ cd welcome2
$ cnd up
Activating your cloud native development environment...
Linking '/Users/ramiro/okteto/welcome2' to ramiro/welcome...
Ready! Go to your local IDE and continue coding!
```

Open your favorite IDE, go to `welcome2/app.py` and change the value of  `option_a` (line 7) from `Cats2` to `Otters2` and save the file. Go to the browser, reload the page, and check the label on the first button. Your changes were applied instantly and automatically!

Congratulations, you're now a **cloud native developer** 😎.

## Known issues

- If you terminate the execution of any of the `cnd up` commands, you will need to kill both of them, execute `cnd down`, and execute `cnd up` again in one of the folders (or on both of them)

- Before executing the second `cnd up` command, you need to wait for the first one to finish.
