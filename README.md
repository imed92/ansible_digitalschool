# Ansible

## On va etablir la connexion au serveur AWS en :
### Ajoutant ca dans le fichier /etc/ansible/hosts
```yaml
# ci dessous c'est le nom du groupe d'hôtes dans cet inventaire. Les crochets [aws] indiquent qu'il s'agit d'un groupe d'hôtes et aws est le nom du groupe. Vous pouvez utiliser ce nom pour spécifier ce groupe dans vos playbooks Ansible.
[aws]
# test : C'est le nom de l'hôte. Dans cet exemple, l'hôte est nommé test.
#ansible_ssh_host=test ansible_ssh_host=ec2-34-226-155-165.compute-1.amazonaws.com : C'est une variable d'inventaire qui spécifie l'adresse IP de l'hôte. Dans ce cas, ansible_ssh_host est utilisé pour spécifier l'adresse IP de l'hôte, qui est 3.80.77.108. Cette variable est utilisée par Ansible pour se connecter à l'hôte via SSH.
test ansible_ssh_host=ec2-34-226-155-165.compute-1.amazonaws.com
# ansible_ssh_user username du user sur l'hote
test ansible_ssh_user=ubuntu
## fonctionne aussi comme ca
## test ansible_ssh_host=ubuntu@ec2-34-226-155-165.compute-1.amazonaws.com
```

ensuite on fait cette commande :
```bash
# c'est pour pinger le serveur et ca retourne success si ca a marcher
ansible -m ping all
```

## Ensuite créer un playbook dédié au fait d'executer un script sur le serveur
Apelle le playbook comme tu veux et mets ca dedans :
```yaml
---
- name: Exécuter un script bash sur le serveur slave
  hosts: aws   # Remplacez par le nom de votre groupe d'hôtes contenant le serveur slave
  tasks:
    - name: Exécuter le script bash
      script: ./test.sh
```
Et ici le test.sh va s'executer dans le serveur, le test.sh c'est le script qu'on veux executer sur le serveur.
Ensuite on execute :
```bash
ansible-playbook -i hosts install_app.yml
```

