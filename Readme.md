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
Ainsi ils ont ete utilise pour B, D, et H

D'autre part, le service ClusterIP a été choisi pour le composant interne sensibles  la base de données F , afin de limiter son accessibilité uniquement à l'intérieur du cluster Kubernetes. Cela renforce la sécurité en empêchant tout accès externe non autorisé à ce service, tout en permettant aux autres composants de l'application d'interagir avec elle de manière sécurisée à l'intérieur du cluster.

voici la représentation de chaque lettre :

A, C et G ,  sont des nodePort
E est un clusterIp.
B, D, H et F representent respectivement ic-webapp, odoo, pgAdmin et la base de donnee de odoo. Il  sont de type deployments.

L'enssemble du manifest kubernetes se trouve dans le repertoire 'manifestes-k8s'.

### 3 Partie 3 
3) Pipeline CI/CD 



#### Partie CI Jenkins 

<div style="text-align:center;">
    <img src="https://github.com/MousMaster/ProjetFilRouge/blob/main/images/Jenkins.png" width="300">
</div>

# Pipeline CI/CD pour l'application Web

Ce pipeline Jenkins automatise le processus de développement logiciel, du build à la publication, en passant par les tests et le déploiement.

## Environnement

Les variables d'environnement sont définies pour faciliter le déploiement et la gestion du pipeline.

- `IMAGE_NAME`: Nom de l'image Docker.
- `APP_CONTAINER_PORT`: Port utilisé par le conteneur de l'application.
- `DOCKERHUB_ID`: Identifiant Docker Hub.
- `DOCKERHUB_PASSWORD`: Mot de passe Docker Hub.
- `ANSIBLE_IMAGE_AGENT`: Image Ansible utilisée pour les déploiements.
- `IC_WEBAPP_SERVER_DEV`: Adresse IP du serveur pour l'environnement DEV.

## Stages du pipeline

1. **Build de l'image**:
   - Construction de l'image Docker à partir du Dockerfile.

2. **Analyse de l'image avec Snyk**:
   - Analyse de l'image Docker pour détecter les vulnérabilités de sécurité.

3. **Exécution du conteneur basé sur l'image construite**:
   - Lancement d'un conteneur Docker pour effectuer des tests.

4. **Test de l'image**:
   - Vérification de l'accessibilité de l'application via curl.

5. **Nettoyage du conteneur**:
   - Arrêt et suppression du conteneur Docker après les tests.

6. **Connexion et publication de l'image sur Docker Hub**:
   - Publication de l'image construite sur Docker Hub.

7. **Construction d'une instance EC2 sur AWS avec Terraform**:
   - Création d'une instance EC2 sur AWS à l'aide de Terraform.

8. **Préparation de l'environnement Ansible**:
   - Configuration des clés et des variables pour Ansible.

9. **Déploiement de l'environnement DEV pour les tests**:
   - Déploiement de l'application dans l'environnement DEV avec Ansible.

10. **Suppression de l'environnement DEV**:
    - Destruction de l'environnement DEV une fois les tests terminés.

11. **Déploiement en PRODUCTION**:
    - Déploiement de l'application dans l'environnement de production avec Ansible.

## Notifications

Le résultat du pipeline est notifié via Slack pour une communication efficace au sein de l'équipe de développement.

---
Ce pipeline CI/CD automatisé garantit un déploiement fluide et sécurisé de l'application web, de la construction à la publication, en passant par les tests et le déploiement dans différents environnements.



#### Partie CD Ansible 
![project](https://github.com/MousMaster/ProjetFilRouge/blob/main/images/ansible.png)
 

# Guide de déploiement avec Ansible

Ce référentiel contient des configurations Ansible conçues pour le déploiement automatisé d'applications. Utilisant une approche modulaire, il est structuré en environnements, rôles, et playbooks, offrant ainsi une méthode de déploiement cohérente et réutilisable pour différents environnements tels que le développement, le test et la production.

## Configuration

Les fichiers de configuration principaux (`ansible.cfg`, `hosts.yml`) et les variables (`group_vars/`, `host_vars/`) définissent les paramètres globaux et spécifiques pour le déploiement.

## Rôles

Les rôles organisent les tâches, les variables, les valeurs par défaut et les templates pour déployer des composants spécifiques de manière autonome.

## Playbooks

Les playbooks (`playbooks/`) sont les scripts qui orchestrent le déploiement, faisant appel aux rôles et aux variables pour déployer les applications sur les hôtes ciblés.

## Usage

Pour déployer, exécutez :

```bash
ansible-playbook -i hosts.yml playbooks/<nom_du_playbook>.yml
