# k8s-the-hardway-playbooks

- I'm keeping the certificates in the repository to make testing easier(in case you don't want to generate the certs yourself) they are valid certificates as of before 2037
- I kept the compressed packages as download takes time and ansible collection for download has some python upgrade requirements
- I have filebeats agents installation as I wanted to have the log in a centralized location, you can deploy it by filebeat tag and and updating the ELK elasticsearch creds 

Installation steps:

Execute all playbooks in the below order

1. Deploy loadbalancer, kubeconfig accounts, kube-apiserver, kube-scheduler, kube-controller-manager and kubelet
```
	ansible-playbook -i inventories/home-env01.yaml site.yaml
```

2. Approve pending CSRs
```
	ansible-playbook -i inventories/home-env01.yaml site.yaml --tags csr
```

3. Deploy cilium for network
	```
	ansible-playbook -i inventories/home-env01.yaml site.yaml --tags cilium
	```
	- Wait till nodes become ready
	```
	/usr/local/bin/kubectl get node
 	```
 	```
		NAME       STATUS   ROLES    AGE    VERSION
		worker-1   Ready    <none>   3m1s   v1.34.2
		worker-2   Ready    <none>   3m1s   v1.34.2
	```
  	```
   /usr/local/bin/kubectl get pods -A
   	```
   	```
	NAMESPACE     NAME                              READY   STATUS    RESTARTS   AGE
	kube-system   cilium-7fdht                      1/1     Running   0          2m
	kube-system   cilium-envoy-t9dbc                1/1     Running   0          2m
	kube-system   cilium-envoy-vwgsj                1/1     Running   0          2m
	kube-system   cilium-jdcdr                      1/1     Running   0          2m
	kube-system   cilium-operator-d5978dfc7-fwb5w   1/1     Running   0          2m
	kube-system   hubble-relay-54774bdddb-mvhnl     0/1     Running   0          2m
	kube-system   hubble-ui-576dcd986f-rhwdb        2/2     Running   0          2m
   	```
    *hubble-relay will come online once coredns is deployed*
   
4. Deploy the coredns
```
	ansible-playbook -i inventories/home-env01.yaml site.yaml --tags coredns
```
