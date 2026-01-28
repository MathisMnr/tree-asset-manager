# Tree Asset Manager

## Description
Le projet consiste a créer un site web repertoriant les arbres de la ville de Saint-Qentin, et ainsi de pouvoir les consulter, les visualiser sur une carte, les modifier ou bien les supprimer.
Le projet vise également à faire de l'analyse sur une base de donnée massive, en devant filtrer les données erronées, trier celles corrects pour ensuite pouvoir les traiter. Une fois propre, ces données nous permettent d'entraîner des IA via divers modèles d'apprentissage (Clustering et Classifiers) pour parvenir à prédire des caractéristiques sur des arbres tel que leur âge, couleur, taille, etc... L'accent a notamment été mit sur l'étude des corrélations, de la pertinence des données traités selon le tri, la provenance et les relations de causalité, via des études graphiques de Big Data. 

## Installation
### Technologie
- Python 3.8
- Php 8.3
- Postgresql 15
- Apache 2.4

#### Packages
```bash
sudo apt-get install python3-pip php postgresql apache2 libapache2-mod-php php-pgsql postgresql-contrib postgresql-server python3-asyncpg python3-pandas python3-sklearn -y
```

### Configuration Apache
VirtualHost exemple:
```apache
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName api.arbre.com
    DocumentRoot /var/www/projetA3

    <Directory /var/www/projetA3>
        Options -Indexes +FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
```bash
sudo a2ensite projetA3.conf
```
```bash
sudo service apache2 reload
```

Cette configuration permet de rediriger les requetes vers le dossier /var/www/projetA3    
Lorsque qu'un autre virtual host par default est configuré, il est necessaire de sois le desactivé ou changer votre fichier hosts sur votre OS pour rediriger les requetes vers le bon virtual host.  

### Configuration de la base de donnée
Pour configurer la base de donnée, il est necessaire de créer un user et une base donnée sur postgresql.
```bash
sudo -u postgres psql
```
```sql
CREATE USER
    tree
WITH
    PASSWORD 'tree';
```
```sql
CREATE DATABASE
    tree
WITH
    OWNER = tree
```
```sql
GRANT ALL PRIVILEGES ON DATABASE tree TO tree;
```

#### Remplir la base de donnée
Table de la base
```bash
cd 'root du projet'
psql -U tree -d tree -f sql/tables.sql
psql -U tree -d tree -f sql/data.sql
```
Remplir la base de donnée avec les données du fichier csv Data_arbre.csv
```bash
cd IA && python3 load_data.py
```

### Configuration du projet
Pour configurer le projet, il est nécessaire de renomer le fichier hidden.constants.php dans le dossier database en constants.php et de le remplir avec les informations de la base de donnée.  

### Lancement du projet
Pour lancer le projet, il est necessaire de lancer le serveur apache et de lancer le service postgresql.  
Pour lancer le serveur apache:
```bash
sudo service apache2 reload
```
Pour lancer le service postgresql:
```bash
sudo service postgresql restart
```

## Utilisation
Aller sur le site web et naviguer sur les différentes pages. And Enjoy !!
