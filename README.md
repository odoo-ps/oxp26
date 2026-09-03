# 🛠️ Cheat Sheet `odev` : Gestion de Base de Données

Ce guide regroupe les commandes essentielles pour créer, lancer, sauvegarder et restaurer une base de données Odoo via l'outil `odev`.

> 💡 **À NOTER AVANT DE COMMENCER :**
> Les noms utilisés dans ce guide sont purement indicatifs. Vous êtes totalement libres (et encouragés) de les remplacer par les noms de votre choix selon vos projets :
> * `mon_dossier` ➡️ Choisissez un nom de dossier pertinent (ex: `dossier_client_x`).
> * `ma_db` ➡️ Remplacez par le nom que vous souhaitez donner à votre base de données.
> * `mon_back_up.dump.sql` ➡️ Nommez votre fichier de sauvegarde pour qu'il soit facilement identifiable.

---

## 1. Préparation de l'environnement
Avant de commencer, il est utile de créer un dossier dédié à votre projet pour y centraliser votre travail (notamment vos sauvegardes), puis de vous y rendre.

```bash
# Créer un nouveau dossier (remplacez "mon_dossier" par le nom souhaité)
mkdir mon_dossier

# Se déplacer à l'intérieur de ce nouveau dossier
cd mon_dossier/
```

## 2. Création de la base de données
Utilisez la commande `create` en spécifiant le nom de la base et la version souhaitée (ici, la version *master*, mais cela peut changer selon le projet).

```bash
# Créer la base de données
odev create ma_db -V master
```

## 3. Lancement de l'instance
Une fois la base de données créée, vous pouvez lancer le serveur pour y accéder depuis votre navigateur.

```bash
# Lancer l'instance liée à votre base de données
odev run ma_db
```
*(Pour couper l'instance plus tard, utilisez généralement `Ctrl+C` dans le terminal).*

## 4. Sauvegarde (Dump) de la base de données
Pour créer une copie de sécurité de votre base (par exemple avant de faire des tests ou de valider une étape de configuration), utilisez la commande `dump`. 

```bash
# Exécuter la sauvegarde
odev dump ma_db 

# L'outil confirmera la création avec un chemin par défaut :
# [i] Database 'ma_db' dumped to /home/odoo/odoo/dumps/20260903-ma_db.dump.sql 
```

Le fichier est créé dans un dossier global de Odoo. Pour ne pas le perdre de vue, il est recommandé de le déplacer vers votre dossier de travail actuel et de le renommer plus clairement.

```bash
# 1. Vérifier dans quel dossier vous vous trouvez actuellement (pour être sûr)
pwd
# Résultat attendu : /home/odoo/mon_dossier

# 2. Déplacer et renommer le fichier généré vers votre dossier
# Attention à bien adapter la date et le nom selon ce que "odev dump" vous a retourné !
mv /home/odoo/odoo/dumps/20260903-ma_db.dump.sql /home/odoo/mon_dossier/mon_back_up.dump.sql

# 3. Vérifier que le fichier a bien été déplacé
ls
# Résultat attendu : mon_back_up.dump.sql
```

## 5. Restauration d'une sauvegarde
Si vous souhaitez réinitialiser votre base avec des données précédemment sauvegardées (ou charger le dump d'un collègue), utilisez la commande `restore`.

```bash
# Restaurer le fichier de sauvegarde sur la base
odev restore ma_db mon_back_up.dump.sql 
```

Une fois la restauration terminée, vous n'avez plus qu'à relancer votre instance pour retrouver vos données :

```bash
# Relancer l'instance avec les données restaurées
odev run ma_db
```

## 6. Accéder à l'interface Odoo
Une fois votre instance lancée (avec la commande odev run), vous pouvez y accéder directement depuis votre navigateur web.

👉 Cliquez sur ce lien pour ouvrir la page : http://localhost:8069

(Ou tapez simplement http://localhost:8069 dans la barre d'adresse de votre navigateur).

> 🔐 **Identifiants de connexion :**
> Lors de votre arrivée sur la page de connexion de votre nouvelle base de données, utilisez les accès par défaut :
> * **Email / Utilisateur :** `admin`
> * **Mot de passe :** `admin`


## 7. Arrêter l'instance de Odoo

```bash
# Dans la console
ctrl + c
```
