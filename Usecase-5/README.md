# kube-ansible is to install and configure kubernetes with ansible
### How to run playbook
### To setup k8s master and slave please select t2.medium instance
ansible-playbook -i hosts main.yml


### How to verify nodes
kubectl get nodes
