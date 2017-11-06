# Tp_Ansible @Propriété de Victor Moreau

 <victor.moreau@ynov.com> 


Server SSH Ansible Nginx Docker
Creation des 3 containers récupérant un server ssh gérer par Ansible


- #1 -> Se connecter au hub privé : - 

	docker login registry.mrzee.fr
		-> Id : ynov

		-> mdp: DevOps123!


#2 -> Récupérer l'image du server ssh 

	docker pull registry.mrzee.fr/ynov/ssh-server:0.1


#3-> Création des servers : 

	docker run -d --name="ssh-server-1" registry.mrzee.fr/ynov/ssh-server:0.1
	docker run -d --name="ssh-server-2" registry.mrzee.fr/ynov/ssh-server:0.1
	docker run -d --name="ssh-server-3" registry.mrzee.fr/ynov/ssh-server:0.1

#4 -> Création de la clé ssh

	récupérer la clé sur : https://git.mrzee.fr/ynov/devops-ssh-server/raw/master/id_rsa
	
	éxecuter les commandes suivantes : 
		cp chemin/cle/enregistrée .ssh/id_rsa
		ssh-add .ssh/id_rsa
	verifier la présence de la clé:
		ssh-add l
	vérifier root sur les containers validé avec la clé
		ssh root@IP container ( connaitre Ip container : -> docker inspect server-ssh-1)
	

#5 Installer ansible sur votre machine

#6 Modifier le fichier /etc/ansible/hosts

	-> Créé un grp : Exemple [MONGROUPEDESERVER]
	suivis a ligne pour chacune de vos Ip de vos containers précédemment récupérés

#7 Vérifier la connexion ansible sur vos containers 

	-> ansible all -m ping -vvv

#8 Lancer le playbook depuis votre dossier

	->ansible-playbook chemin/de/votre/playbook.yml

#9 Si Crash

	-> Décommentez la task -name="restart pm2"
				shell: pm2 stop /var/www/my-node-project/myapp/bin/myapp	