#Setup the ansible server

-
```
	dnf install ansible-core-1:2.14.17-1.el9 -y -q
```

- Clone the repo
```
	git clone https://github.com/samirahmedmustafa/k8s-the-hardway-playbooks.git
```

- switch to the repo location and install collections
```
	cd k8s-the-hardway-playbooks
	cd collections/
	ansible-galaxy install -r requirements.yml	
	cd ..
```
