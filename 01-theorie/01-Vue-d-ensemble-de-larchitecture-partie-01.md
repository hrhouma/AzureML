# **Cours sur l'Architecture et la Configuration d'un Espace de Travail Azure ML**
---
# Architecture Azure ML :

```
                         +---------------------------------------+
                         |     Dépendances de l'Espace de        |
                         |           Travail Azure ML            |
                         +---------------------------------------+
                          |            |           |            |
                          v            v           v            v
+-------------------+ +--------------------+ +-----------------+ +---------------------+
| Azure Storage     | | Azure Container     | | Azure Key Vault | | Azure Application    |
| Account           | | Registry            | |                 | | Insights             |
+-------------------+ +--------------------+ +-----------------+ +---------------------+
                          |            |           |            |
                          v            v           v            v
+-----------------------------------------------------------------------------------------+
|                                   Espace de Travail                                     |
|                                                                                         |
|    +----------------+                      +------------------------+                  |
|    | Services Liés   |                      |   Ressources Gérées    |                  |
|    | (Linked         |                      |  (Managed Resources)   |                  |
|    | Services)       |                      +------------------------+                  |
|    +----------------+                      | +--------------------+ |                  |
|    |                |                      | | Instances de Calcul | |                  |
|    | +-------------+|                      | +--------------------+ |                  |
|    | | Datastores  ||                      | | Clusters de Calcul  | |                  |
|    | +-------------+|                      | +--------------------+ |                  |
|    | +-------------+|                      +------------------------+                  |
|    | | Cibles de   ||                                                                 |
|    | | Calcul      ||                                                                 |
|    | +-------------+|                                                                 |
|    +----------------+                                                                 |
+-----------------------------------------------------------------------------------------+
                          |            |           |            |           |
                          v            v           v            v           v
+---------------+ +--------------+ +------------------+ +---------------+ +------------+
| Environnements| | Expériences  | | Pipelines         | | Ensembles de  | | Modèles    |
|               | |              | |                  | | Données       | |            |
+---------------+ +--------------+ +------------------+ +---------------+ +------------+
                                                                              |
                                                                              v
                                                                     +----------------+
                                                                     | Points de      |
                                                                     | Terminaison    |
                                                                     | (Endpoints)    |
                                                                     +----------------+
```

### Explication :
- **Espace de Travail (Workspace)** : C'est le hub central. Il gère des ressources comme des **instances de calcul** et des **clusters**.
- **Dépendances** : Ce sont des services comme **Azure Storage Account**, **Azure Container Registry**, **Azure Key Vault**, et **Azure Application Insights** qui fournissent les bases nécessaires à l'espace de travail.
- **Services Liés (Linked Services)** : Comme les **datastores** et les **cibles de calcul**, ils sont liés à l'espace de travail pour la gestion des données et des ressources de calcul.
- **Ressources Gérées** : Elles incluent les **instances de calcul** et les **clusters de calcul** pour exécuter les expériences et les modèles.
- **Actifs (Assets)** : Les éléments comme les **environnements**, **expériences**, **pipelines**, **ensembles de données**, et **modèles** qui sont créés, suivis, et versionnés dans l'espace de travail.

Le diagramme résume comment chaque composant interagit dans un projet Azure ML, en mettant en lumière les dépendances, services liés, ressources gérées, et actifs utilisés pour la gestion des expériences et des modèles.
