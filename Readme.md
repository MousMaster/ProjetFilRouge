# PROJET FINAL DEVOPS. 

## 1 Ennonce : 
Lien : 
La société **IC GROUP** dans laquelle vous travaillez en tant qu’ingénieur Devops souhaite mettre sur pied un site web vitrine devant permettre d’accéder à ses 02 applications phares qui sont :  

## 2 Modele propose : 


### 1 Partie 1 :  
1) Dockeristaion du site vitrine 


L'application a été dockerisée en créant un fichier Dockerfile décrivant les dépendances et les étapes d'installation. Ensuite, Docker a été utilisé pour construire une image à partir de ce Dockerfile avec la commande docker build. Enfin, l'application a été exécutée dans un conteneur Docker isolé en utilisant la commande docker run.
Un apperçu de l'application est visble ci dessous.

![project](https://github.com/MousMaster/ProjetFilRouge/blob/main/images/ic-webapp.png)

### 2 Partie 2 :  
2) Déploiement des différentes applications dans un cluster Kubernetes

![project](https://github.com/MousMaster/ProjetFilRouge/blob/main/images/kubernetes.png)

Dans cette architecture Kubernetes, les choix des services ont été faits en tenant compte des exigences de sécurité et des bonnes pratiques. Les services NodePort ont été utilisés pour les applications nécessitant un accès externe, tout en garantissant une certaine sécurité grâce à la délimitation des ports exposés. Par exemple, les services NodePort sont appropriés pour des applications telles que les API ou les applications Web qui doivent être accessibles depuis l'extérieur du cluster.

D'autre part, le service ClusterIP a été choisi pour des composants internes sensibles comme la base de données, afin de limiter leur accessibilité uniquement à l'intérieur du cluster Kubernetes. Cela renforce la sécurité en empêchant tout accès externe non autorisé à ces services, tout en permettant aux autres composants de l'application d'interagir avec eux de manière sécurisée à l'intérieur du cluster.

voici la représentation où chaque lettre correspond à :

A, C et G ,  sont des nodePort

E est un clusterIp.

B, D, H et F representent respectivement ic-webapp, odoo, pgAdmin et la base de donnee de odoo. sont des deployments.


### 3 Partie 3 
3) Pipeline CI/CD 



#### Partie CI Jenkins 

<div style="text-align:center;">
    <img src="https://github.com/MousMaster/ProjetFilRouge/blob/main/images/Jenkins.png" width="300">
</div>


#### Partie CD Ansible 
![project](https://github.com/MousMaster/ProjetFilRouge/blob/main/images/ansible.png)
 

