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
4. Deploy the coredns
```
	ansible-playbook -i inventories/home-env01.yaml site.yaml --tags coredns
```
