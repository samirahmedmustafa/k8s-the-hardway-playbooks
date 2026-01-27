# k8s-the-hardway-playbooks
Execute all playbooks using the below

```
	ansible-playbook -i inventories/home-env01.yaml site.yaml
```

```
	ansible-playbook -i inventories/home-env01.yaml site.yaml --tags cilium
```

```
	ansible-playbook -i inventories/home-env01.yaml site.yaml --tags coredns
```
