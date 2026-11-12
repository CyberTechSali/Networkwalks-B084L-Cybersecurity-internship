
# 🕵️ Maltego : Installation, activation et première investigation OSINT

> Module : Reconnaissance / OSINT
> Outil : **Maltego Graph (Desktop) 4.14.0**
> Plateforme : Windows (.exe + Java x64)

## 📌 Présentation

**Maltego** est un outil d'investigation OSINT (Open Source Intelligence) qui représente les informations sous forme de **graphes**. Il relie des entités (domaines, emails, personnes, IP, etc.) grâce à des **Transforms**, des requêtes automatisées vers des sources de données.

Ce document explique :
1. Le téléchargement et l'installation
2. L'activation avec un Maltego ID
3. La configuration des sources de données
4. Une première investigation : trouver les adresses email liées à un domaine

---

## 1. Téléchargement

1. Aller sur la page officielle : https://www.maltego.com/downloads/
2. Choisir le système d'exploitation **Windows** et l'extension **.exe + Java (x64)**
3. Cliquer sur **Download Maltego Graph** (version 4.14.0)

![Téléchargement](images/1.png)

## 2. Installation

1. Lancer l'installeur téléchargé
2. Fermer les autres applications, puis cliquer sur **Next >**
3. Suivre l'assistant jusqu'à la fin de l'installation

![Installation](images/2.png)

## 3. Activation du produit

### 3.1 Choix du mode d'activation

Au premier lancement, sélectionner **MALTEGO ID** (pour un nouvel utilisateur), puis **Next**.

![Options d'activation](images/3.png)

Choisir **Online Activation (Default)**, puis **Next**.

![Activation en ligne](images/4.png)

### 3.2 Contrat de licence

Lire et cocher **Accept**, puis **Next**.

![Licence](images/05-licence.png)

### 3.3 Connexion via le navigateur

Cliquer sur **Browser Login** : la page de connexion s'ouvre dans le navigateur.

![Login link options](images/06-login-link.png)

Le client Maltego attend alors le signal d'authentification du navigateur.

![Attente de connexion](images/07-attente-login.png)

### 3.4 Création du Maltego ID (si pas de compte)

1. Sur la page de connexion, cliquer sur **CREATE ID**

![Page de login](images/08-page-login.png)

2. Remplir l'email (valide), le prénom et le nom, puis cliquer sur **CONTINUE**

![Création du compte](images/09-creation-id.png)

3. Après validation, le message **Authentication complete** apparaît : fermer le navigateur et revenir à l'application.

![Authentification terminée](images/10-auth-complete.png)

### 3.5 Activation réussie

Le message **Activation Successful!** confirme l'activation. Cliquer sur **Next**.

![Activation réussie](images/11-activation-ok.png)

## 4. Configuration des sources de données

1. **Select Data Sources** : laisser **Utilities** coché, puis **Next**

![Sources de données](images/12-select-data-sources.png)

2. **Download Data Sources** : Maltego télécharge les transforms (ex. 238 Transforms, 245 Entities, 79 Transform Sets, 14 Machines)

![Téléchargement des sources](images/13-download-data-sources.png)

3. Poursuivre l'assistant (T&Cs, options du navigateur, mode de confidentialité) jusqu'à **Finish**.

## 5. Interface de Maltego

Après la configuration, l'espace de travail s'ouvre avec :
- **Entity Palette** : la liste des types d'entités
- **Graph** : la zone centrale où se construit l'investigation
- **Run View / Transforms** : lancement des transforms et des machines
- **Detail View / Properties** : détails de l'entité sélectionnée
- **Overview** : vue globale du graphe

![Interface](images/14-interface.png)

## 6. Première investigation : emails d'un domaine

### Étape 1 : Ajouter une entité Domain
1. Dans l'**Entity Palette**, rechercher `dom` et glisser l'entité **Domain** dans le graphe
2. Double-cliquer dessus et renseigner le **Domain Name** (ex. `networkwalks.com`)
3. Valider avec **OK**

![Entité Domain](images/15-entite-domain.png)

### Étape 2 : Lancer un transform
1. Clic droit sur l'entité, puis ouvrir **Run Transforms**
2. Choisir **Email addresses from Domain**

![Run Transforms](images/16-run-transforms.png)

### Étape 3 : Analyser le résultat
Le graphe affiche le domaine relié à l'adresse email trouvée (ex. `info@networkwalks.com`). La fenêtre **Output - Transform Output** montre l'exécution des transforms et la consommation de crédits.

![Résultat](images/17-resultat.png)

## 📝 Ce qu'il faut retenir

| Notion | Description |
|---|---|
| **Entity** | Un élément d'information (domaine, email, personne, etc.) |
| **Transform** | Une requête automatisée qui produit de nouvelles entités à partir d'une entité |
| **Machine** | Une suite de transforms automatisée |
| **Maltego ID** | Compte nécessaire pour activer et utiliser le logiciel |
| **Crédits** | Chaque transform consomme des crédits selon le plan utilisé |

## ⚠️ Avertissement légal et éthique

Maltego doit être utilisé uniquement sur des cibles pour lesquelles vous avez une **autorisation** (audit, pentest, formation) ou sur des données publiques et dans le respect de la loi (RGPD, lois locales sur la protection des données). L'auteur décline toute responsabilité en cas d'usage abusif.

## 📚 Ressources

- Site officiel : https://www.maltego.com
- Téléchargement : https://www.maltego.com/downloads/
