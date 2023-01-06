# the_red_infra
the red infra

# FAQ
* An EC2 VPC Not Found error occurs.
  * Occurs when:
    * If the VPC is randomly created, rather than the VPC that AWS generates by default.
    * In this case, if you enter VPC id explicitly, it works.
    * Please try changing it to the part processed with the comment "#".

# Q/A
* Create a question in Issue.

# setup

* Basic tests have been done on ubuntu 20.04.(18.04 works as well.)
* Update apt to use the apt properly.

```
sudo apt update
```

* Install the package essential for python installation.

```
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl
```

* git clone the_red_infra and run ./install_pyenv.sh. If you use bash, source ~/.bashrc, if you use zsh, source ~/.zshrc

```
	git clone https://github.com/charsyam/the_red_infra
	./install_pyenv.sh
	source ~/.bashrc
	./install_python.sh
    install_ansible_password.sh    
	install_terraform.sh	
```

* Run terraform 
```
    cd terraform/ec2/ap-northeast-2
    terraform init
    terraform plan -out "output"
    terraform apply "output"
```

* The following is how to run ansible. Before writing, destination host settings must be configured on the aws/hosts file.

apply ansible: geoip
```
    ansible-playbook -i aws the_red_1_base.yml
    ansible-playbook -i aws the_red_2_geoip.yml
    ansible-playbook -i aws the_red_2_lb.yml
```

apply ansible: monitor(prometheus + grafana)
```
    ansible-playbook -i aws the_red_1_base.yml
    ansible-playbook -i aws the_red_2_monitor.yml
```

apply ansible: ngrinder
```
    ansible-playbook -i aws the_red_1_jvm.yml
    ansible-playbook -i aws the_red_2_ngrinder.yml
```

# Ansile Reference
* For basic Ansible reference, refer to the following.
 * [https://docs.google.com/presentation/d/1xYQ2i2lWbu4dJNW8g_6xhMhrbHMF_lnI/edit?usp=sharing&ouid=105217181260208837838&rtpof=true&sd=true]
