# **Guide - Création d'un Espace de Travail avec Azure ML SDK**

## **Table des Matières**
1. [Introduction](#section1)
2. [Installation et Configuration](#section2)
   - 2.1 [Installation du SDK Azure ML](#section21)
   - 2.2 [Vérification de la version de Python](#section22)
   - 2.3 [Vérification de la version du SDK Azure ML](#section23)
   - 2.4 [Détails sur le SDK Azure ML](#section24)
3. [Création de l'Espace de Travail](#section3)
   - 3.1 [Importation de la classe `Workspace`](#section31)
   - 3.2 [Création de l'espace de travail](#section32)
4. [Conclusion](#section4)

---

<a id="section1"></a>
## 1. Introduction

Dans ce guide, vous apprendrez à configurer un environnement de travail pour Azure Machine Learning et à créer un espace de travail (Workspace) pour gérer vos ressources Azure. Ce guide est particulièrement utile pour ceux qui travaillent avec des notebooks comme Jupyter ou Google Colab et souhaitent configurer rapidement un environnement Azure ML SDK.

---

<a id="section2"></a>
## 2. Installation et Configuration

Avant de commencer à travailler avec Azure Machine Learning, vous devez installer et configurer l'outil SDK Azure ML.

<a id="section21"></a>
### 2.1 Installation du SDK Azure ML

Le SDK Azure ML fournit tous les outils nécessaires pour interagir avec les services Azure Machine Learning. Pour installer le SDK, exécutez la commande suivante :

```bash
! pip install -q azureml-sdk
```

Cette commande télécharge et installe le package `azureml-sdk` avec toutes les dépendances nécessaires.

---

<a id="section22"></a>
### 2.2 Vérification de la version de Python

Avant de commencer, il est important de vérifier la version de Python que vous utilisez, car Azure Machine Learning SDK requiert certaines versions de Python pour fonctionner correctement.

```bash
! python --version
```

Assurez-vous que la version de Python est compatible avec Azure ML SDK, idéalement une version 3.6 ou supérieure.

---

<a id="section23"></a>
### 2.3 Vérification de la version du SDK Azure ML

Après l'installation du SDK, vérifiez la version installée du package pour vous assurer que vous utilisez une version à jour et compatible avec les dernières fonctionnalités d'Azure Machine Learning.

```python
import azureml.core
print(azureml.core.VERSION)
```

Cela affichera la version du SDK Azure ML installé sur votre environnement.

---

<a id="section24"></a>
### 2.4 Détails sur le SDK Azure ML

Si vous souhaitez obtenir plus d'informations sur le package installé, y compris sa version, son emplacement et ses dépendances, utilisez la commande suivante :

```bash
! pip show azureml-core
```

Cela vous donnera tous les détails sur le package `azureml-core`, qui est la base du SDK Azure ML.

---

<a id="section3"></a>
## 3. Création de l'Espace de Travail

Une fois le SDK installé et configuré, vous pouvez créer un espace de travail (Workspace) Azure, qui servira à centraliser toutes vos ressources liées à vos projets de machine learning.

<a id="section31"></a>
### 3.1 Importation de la classe `Workspace`

La classe `Workspace` d'Azure ML permet de créer et gérer les espaces de travail. Vous devez d'abord l'importer dans votre notebook pour pouvoir l'utiliser.

```python
from azureml.core import Workspace
```

La classe `Workspace` vous permet de créer, récupérer, et gérer vos espaces de travail Azure.

---

<a id="section32"></a>
### 3.2 Création de l'espace de travail

Pour créer un nouvel espace de travail, vous devez utiliser la méthode `Workspace.create()` et fournir les informations nécessaires comme le nom de l'espace de travail, l'ID d'abonnement, le groupe de ressources, et la localisation. Voici un exemple de code pour créer un espace de travail :

```python
ws = Workspace.create(name='azureml-sdk-ws', 
                      subscription_id='remplacer-moi125-4ef8-a883-jeneserasrien',
                      resource_group='azureml-sdk-rg', 
                      create_resource_group=True,
                      location='westus')
```

- **name** : Le nom de l'espace de travail, ici `azureml-sdk-ws`.
- **subscription_id** : L'ID d'abonnement Azure. Assurez-vous d'utiliser votre propre identifiant d'abonnement.
- **resource_group** : Le groupe de ressources où l'espace de travail sera créé. S'il n'existe pas, il sera créé automatiquement avec `create_resource_group=True`.
- **location** : La région Azure où les ressources seront déployées, ici `westus`.

> **Note** : Vous devez avoir un compte Azure valide avec un abonnement actif pour exécuter cette commande. Vous pouvez récupérer votre ID d'abonnement depuis le portail Azure.

---

<a id="section4"></a>
## 4. Conclusion

Dans ce guide, nous avons vu comment installer et configurer le SDK Azure ML, ainsi que les étapes pour créer un espace de travail Azure. Cet espace de travail servira de base à la gestion de vos projets de machine learning, vos modèles et vos expériences. Vous êtes maintenant prêt à explorer les services offerts par Azure Machine Learning pour accélérer le développement de vos modèles d'IA.
