# Tp_Ansible @Propri�t� de Victor Moreau

 <victor.moreau@ynov.com> 


Server SSH Ansible Nginx Docker
Creation des 3 containers r�cup�rant un server ssh g�rer par Ansible


- #1 -> Se connecter au hub priv� : - 

	docker login registry.mrzee.fr
		-> Id : ynov

		-> mdp: DevOps123!


#2 -> R�cup�rer l'image du server ssh 

	docker pull registry.mrzee.fr/ynov/ssh-server:0.1


#3-> Cr�ation des servers : 

	docker run -d --name="ssh-server-1" registry.mrzee.fr/ynov/ssh-server:0.1
	docker run -d --name="ssh-server-2" registry.mrzee.fr/ynov/ssh-server:0.1
	docker run -d --name="ssh-server-3" registry.mrzee.fr/ynov/ssh-server:0.1

#4 -> Cr�ation de la cl� ssh

	r�cup�rer la cl� sur : https://git.mrzee.fr/ynov/devops-ssh-server/raw/master/id_rsa
	
	�xecuter les commandes suivantes : 
		cp chemin/cle/enregistr�e .ssh/id_rsa
		ssh-add .ssh/id_rsa
	verifier la pr�sence de la cl�:
		ssh-add l
	v�rifier root sur les containers valid� avec la cl�
		ssh root@IP container ( connaitre Ip container : -> docker inspect server-ssh-1)
	

#5 Installer ansible sur votre machine

#6 Modifier le fichier /etc/ansible/hosts

	-> Cr�� un grp : Exemple [MONGROUPEDESERVER]
	suivis a ligne pour chacune de vos Ip de vos containers pr�c�demment r�cup�r�s

#7 V�rifier la connexion ansible sur vos containers 

	-> ansible all -m ping -vvv

#8 Lancer le playbook depuis votre dossier

	->ansible-playbook chemin/de/votre/playbook.yml

#9 Si Crash

	-> D�commentez la task -name="restart pm2"
				shell: pm2 stop /var/www/my-node-project/myapp/bin/myapp	