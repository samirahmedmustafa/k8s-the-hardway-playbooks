# k8s-the-hardway-playbooks

- I'm keeping the certificates in the repository to make testing easier(in case you don't want to generate the certs yourself) they are valid certificates as of before 2037
- I kept the compressed packages as download takes time and ansible collection for download has some python upgrade requirements

Installation steps:

Execute all playbooks in the below order

1. Deploy loadbalancer, kubeconfig accounts, kube-apiserver, kube-scheduler, kube-controller-manager
```
	ansible-playbook -i inventories/home-env01.yaml site.yaml
```

2. Deploy cilium for network
```
	ansible-playbook -i inventories/home-env01.yaml site.yaml --tags cilium
```

3. Deploy the coredns
```
	ansible-playbook -i inventories/home-env01.yaml site.yaml --tags coredns
```

4. Approve pending CSRs
```
	ansible-playbook -i inventories/home-env01.yaml site.yaml --tags csr
```
