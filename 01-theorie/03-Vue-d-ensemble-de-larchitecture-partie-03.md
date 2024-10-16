# **Cours sur l'Architecture et la Configuration d'un Espace de Travail Azure ML**

# Introduction

Je vous présente une description détaillée, étape par étape, des actions que l'utilisateur doit entreprendre pour configurer un espace de travail Azure ML, ainsi que ce qui se passe en arrière-plan à chaque étape.



### **1. Créer un Espace de Travail Azure ML**

#### **Étape à réaliser :**
L'utilisateur doit créer un nouvel **espace de travail** Azure ML dans le portail Azure.

1. **Accéder au portail Azure** et aller dans "Machine Learning".
2. **Cliquer sur "Créer un espace de travail"**.
3. **Renseigner les informations suivantes :**
   - Nom de l’espace de travail.
   - Abonnement (choisir l’abonnement Azure où sera facturé l’espace de travail).
   - Groupe de ressources (créer un nouveau groupe ou en sélectionner un existant).
   - Région (choisir la région géographique la plus proche de vos ressources de calcul et de stockage).

#### **Ce qui se passe en arrière-plan :**
- Azure provisionne un **hub central** où toutes les ressources liées à vos projets de machine learning seront organisées.
- Azure génère des métadonnées et des configurations qui permettent à ce workspace de communiquer avec d'autres services Azure (ex. comptes de stockage, registres de conteneurs).
- Azure configure des liens vers des **dépendances essentielles** comme **Azure Storage**, **Key Vault**, **Container Registry** (qui sera utilisé pour stocker les images Docker nécessaires à l'entraînement et à l'inférence).

---

### **2. Configurer les Datastores (Sources de Données)**

#### **Étape à réaliser :**
L'utilisateur doit configurer des **datastores** pour indiquer à Azure ML où se trouvent les données utilisées pour entraîner les modèles.

1. **Accéder à l'espace de travail Azure ML** via le portail ou via le SDK.
2. **Configurer un datastore** en liant un service de stockage :
   - Par exemple, utiliser un **Azure Blob Storage** ou un **Azure Data Lake** pour stocker des fichiers CSV ou Parquet contenant des ensembles de données.
3. **Enregistrer le datastore** dans l'espace de travail pour qu'il soit disponible pour les expériences futures.

#### **Ce qui se passe en arrière-plan :**
- Azure ML lie l'espace de travail à un **service de stockage** pour permettre l'accès aux données pendant les expériences.
- Le **datastore** devient un lien logique entre l'espace de travail et un emplacement de stockage, vous permettant de charger facilement des données pour les expériences.
- Azure gère la **sécurité et les permissions** pour garantir que seules les ressources autorisées peuvent accéder aux données.

---

### **3. Créer des Cibles de Calcul (Compute Targets)**

#### **Étape à réaliser :**
L'utilisateur doit configurer des **cibles de calcul** pour exécuter ses expériences (entraînement de modèles, etc.).

1. **Accéder à l'onglet "Compute"** dans l'espace de travail.
2. **Créer une nouvelle cible de calcul** :
   - Choisir entre une **instance de calcul** (pour des tâches interactives) ou un **cluster de calcul** (pour des entraînements à grande échelle).
   - Configurer les ressources (nombre de CPU, GPU, taille des machines virtuelles).
3. **Démarrer l'instance de calcul** ou laisser le cluster se redimensionner automatiquement en fonction des besoins.

#### **Ce qui se passe en arrière-plan :**
- Azure provisionne une **machine virtuelle** (ou un cluster de VMs) basée sur les ressources choisies par l'utilisateur.
- Cette infrastructure de calcul est optimisée pour les tâches de machine learning, y compris la prise en charge de GPU pour l'entraînement accéléré.
- Azure ML gère le **scaling automatique** (en fonction de la demande pour les clusters de calcul), arrêtant ou démarrant des instances selon les besoins.

---

### **4. Créer et Charger des Ensembles de Données (Datasets)**

#### **Étape à réaliser :**
L'utilisateur doit charger ses ensembles de données dans Azure ML pour les utiliser dans les expériences d'entraînement.

1. **Accéder à l'onglet "Datasets"** dans l'espace de travail.
2. **Charger un dataset** depuis un datastore (comme Azure Blob Storage) ou directement depuis votre machine.
   - Choisir le format des données (CSV, Parquet, etc.).
3. **Versionner l'ensemble de données** afin de garantir la reproductibilité des expériences.

#### **Ce qui se passe en arrière-plan :**
- Azure ML vérifie la connexion avec le **datastore** et accède aux fichiers stockés dans le service de stockage.
- Le dataset est stocké de manière versionnée dans l'espace de travail, permettant une traçabilité des données utilisées pour chaque expérience.
- Azure gère la **validation des données** et leur accessibilité à partir des ressources de calcul pendant les expériences.

---

### **5. Créer des Expériences (Experiments)**

#### **Étape à réaliser :**
L'utilisateur doit organiser les runs d'entraînement en **expériences** dans Azure ML.

1. **Accéder à l'onglet "Experiments"** et créer une nouvelle expérience.
2. **Définir le script d'entraînement** (via un notebook ou un script Python).
3. **Lancer l'expérience** en spécifiant la cible de calcul et l'ensemble de données à utiliser.
4. **Suivre les métriques** (comme l'exactitude, la perte, etc.) en temps réel à mesure que l'entraînement progresse.

#### **Ce qui se passe en arrière-plan :**
- Azure ML soumet la tâche d'entraînement à la **cible de calcul** choisie (instance ou cluster).
- Azure suit les **métriques d'entraînement** et les enregistre dans l'expérience pour une analyse ultérieure.
- Le modèle est entraîné en utilisant les ressources de calcul, les données, et les scripts spécifiés par l'utilisateur.

---

### **6. Enregistrer et Versionner les Modèles**

#### **Étape à réaliser :**
Après l'entraînement, l'utilisateur doit **enregistrer** le modèle dans l'espace de travail pour le déploiement ou l'évaluation future.

1. **Après la fin de l'entraînement**, accéder à la section "Models".
2. **Enregistrer le modèle** :
   - Ajouter un nom et des tags pour identifier facilement la version du modèle.
   - Associer le modèle à l'expérience correspondante.
3. **Versionner le modèle** pour le comparer avec d'autres versions.

#### **Ce qui se passe en arrière-plan :**
- Azure ML enregistre le modèle en tant qu'artefact dans l'espace de travail.
- Le modèle est versionné, ce qui permet de garder une trace des itérations, facilitant la comparaison entre différentes versions.
- Azure conserve les informations sur les **hyperparamètres**, les données d'entraînement, et les métriques, vous permettant de reproduire exactement l'entraînement du modèle si nécessaire.

---

### **7. Déployer des Modèles sur des Points de Terminaison (Endpoints)**

#### **Étape à réaliser :**
L'utilisateur doit déployer les modèles pour les rendre accessibles via des **API REST** ou d'autres points de terminaison.

1. **Accéder à la section "Endpoints"** et créer un nouveau point de terminaison.
2. **Spécifier le modèle à déployer** (en utilisant le modèle versionné).
3. **Configurer les ressources de calcul** pour héberger l'API du modèle (CPU/GPU, taille de la machine).
4. **Déployer l'endpoint** pour le rendre disponible en production.

#### **Ce qui se passe en arrière-plan :**
- Azure ML crée une **API REST** pour que le modèle puisse être appelé via des requêtes HTTP.
- Le modèle est déployé sur une **cible de calcul** capable de gérer des requêtes en temps réel ou par lots.
- Azure configure les **points de terminaison sécurisés**, permettant aux utilisateurs autorisés d'accéder au modèle.

---

### **8. Surveiller les Modèles Déployés**

#### **Étape à réaliser :**
L'utilisateur doit configurer la **surveillance** pour suivre les performances des modèles déployés.

1. **Accéder à Azure Application Insights** via le portail Azure.
2. **Suivre les métriques** des endpoints (latence, taux de réussite des prédictions, erreurs).
3. **Analyser les journaux** pour identifier les problèmes ou les baisses de performance.
4. **Configurer des alertes** pour recevoir des notifications en cas de dérives dans les performances du modèle.

#### **Ce qui se passe en arrière-plan :**
- Azure ML envoie des **métriques de performance** (temps de réponse, erreurs, etc.) à Azure Application Insights pour une analyse continue.
- Les données de surveillance sont centralisées, ce qui permet de détecter rapidement les problèmes de performance ou de dérive des modèles.
- Azure aide à **optimiser les modèles** en identifiant les inefficacités dans les prévisions ou les temps de réponse.

---

## **Conclusion**

En suivant ces étapes méthodiques, l'utilisateur peut configurer, gérer et surveiller un environnement complet de machine learning dans Azure. Azure ML automatise de nombreuses tâches complexes (provisionnement, surveillance, gestion des ressources), permettant ainsi à l'utilisateur de se concentrer sur les aspects critiques de ses projets d'IA.
