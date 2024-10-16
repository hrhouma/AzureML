# **Guide - Création d'un Datastore avec Azure ML SDK**

## **Table des Matières**
1. [Introduction](#section1)
2. [Installation et Configuration](#section2)
   - 2.1 [Installation du SDK Azure ML](#section21)
   - 2.2 [Accès à l'Espace de Travail Azure](#section22)
3. [Création d'un Datastore](#section3)
   - 3.1 [Importation de la classe `Datastore`](#section31)
   - 3.2 [Création du Datastore avec Azure Blob Storage](#section32)
4. [Conclusion](#section4)

---

<a id="section1"></a>
## 1. Introduction

Dans cette deuxième leçon, nous allons apprendre à créer un **Datastore** dans Azure Machine Learning à l'aide du SDK Azure ML. Un Datastore est utilisé pour connecter vos espaces de travail à des ressources de stockage dans Azure, telles que Azure Blob Storage, Azure Data Lake, ou d'autres services de stockage cloud.

---

<a id="section2"></a>
## 2. Installation et Configuration

Avant de créer un Datastore, vous devez installer et configurer le SDK Azure ML ainsi qu'accéder à votre espace de travail Azure.

<a id="section21"></a>
### 2.1 Installation du SDK Azure ML

Si ce n'est pas déjà fait, installez le SDK Azure ML pour permettre l'interaction avec les services Azure. Exécutez la commande suivante :

```bash
! pip install -q azureml-sdk
```

Cela téléchargera et installera le SDK nécessaire pour interagir avec Azure Machine Learning.

---

<a id="section22"></a>
### 2.2 Accès à l'Espace de Travail Azure

Pour interagir avec un Datastore, vous devez d'abord accéder à votre espace de travail Azure. Si vous avez déjà configuré votre espace de travail (voir *Lecture 1*), vous pouvez l'importer à l'aide du fichier de configuration `config.json` situé dans votre répertoire de travail.

```python
from azureml.core import Workspace
ws = Workspace.from_config(path='/content/config.json')
```

Cette commande récupère l'espace de travail à partir du fichier `config.json`. Assurez-vous que le chemin vers le fichier est correct et que le fichier contient les informations nécessaires.

---

<a id="section3"></a>
## 3. Création d'un Datastore

Une fois connecté à votre espace de travail, nous allons créer un Datastore, qui stocke les informations de connexion à un compte de stockage Azure.

<a id="section31"></a>
### 3.1 Importation de la classe `Datastore`

Pour travailler avec les Datastores, vous devez importer la classe `Datastore` du SDK Azure ML. Cette classe fournit des méthodes pour créer, enregistrer et gérer les datastores dans Azure Machine Learning.

```python
from azureml.core import Datastore
```

Si vous avez besoin de plus d'informations sur cette classe et ses méthodes, vous pouvez utiliser la fonction `help()` :

```python
# help(Datastore)
```

---

<a id="section32"></a>
### 3.2 Création du Datastore avec Azure Blob Storage

Dans cet exemple, nous allons créer un Datastore qui se connecte à un conteneur Azure Blob Storage. Nous utilisons la méthode `Datastore.register_azure_blob_container()` pour enregistrer le datastore dans l'espace de travail.

```python
az_dstore = Datastore.register_azure_blob_container(
    workspace=ws, 
    datastore_name='azureml_sdk_blob', 
    account_name='azuremlsdkst',
    container_name='azureml-blob-container',
    account_key='ydvDRe71rAO+gcWZz4DESU9Y87Qvnekge/Li8cwCusB/BqhEewPN840W3kw2GSfdtG8z+rpNov9l+ASt1WiAWg==')
```

Les paramètres requis sont :
- **workspace** : L'objet `Workspace` où le Datastore sera enregistré.
- **datastore_name** : Le nom que vous attribuez au Datastore, ici `azureml_sdk_blob`.
- **account_name** : Le nom du compte Azure Storage, ici `azuremlsdkst`.
- **container_name** : Le nom du conteneur Blob dans Azure, ici `azureml-blob-container`.
- **account_key** : La clé d'accès au compte de stockage Azure Blob.

> **Note** : Assurez-vous que les informations d'identification comme `account_key` et `account_name` sont correctes et sécurisées. Ne partagez pas ces informations sensibles dans des environnements publics.

---

<a id="section4"></a>
## 4. Conclusion

- Dans cette deuxième leçon, vous avez appris à installer le SDK Azure ML, à accéder à votre espace de travail, et à créer un Datastore connecté à Azure Blob Storage. 
- Ce Datastore peut maintenant être utilisé pour charger et sauvegarder des données dans votre environnement de machine learning. 
- Vous pouvez adapter cette configuration pour d'autres types de stockage en fonction de vos besoins.
- Ce guide détaillé vous permet de comprendre et de créer un Datastore avec Azure Machine Learning, étape par étape. 
- Vous pouvez ensuite utiliser ce Datastore dans vos expériences et pipelines de machine learning pour accéder à vos données en toute sécurité et efficacité.



