# Configuration de l'espace de travail local pour Azure

Si vous avez besoin de travailler localement, voici les étapes pour configurer un environnement Python virtuel sur votre machine et installer les outils nécessaires pour travailler avec Azure Machine Learning :

1. **Installer Virtualenv** :
   Utilisez la commande suivante pour installer virtualenv si ce n'est pas déjà fait :

   ```bash
   #! pip install virtualenv
   ```

2. **Créer un environnement virtuel avec Python 3.9** :
   Pour créer un environnement virtuel, exécutez les commandes suivantes :

   ```bash
   #python3.9 -m venv azureml_env
   ```

   Cela va créer un environnement nommé `azureml_env`.

3. **Activer l'environnement virtuel** :
   Activez l'environnement que vous venez de créer :

   ```bash
   #azureml_env\Scripts\activate
   ```

4. **Vérifier la version de Python** :
   Assurez-vous que vous utilisez la bonne version de Python :

   ```bash
   #python3.9 --version
   ```

   Vous pouvez également vérifier la version par défaut de Python avec :

   ```bash
   #python --version
   ```

5. **Installer Azure Machine Learning SDK** :
   Une fois l'environnement activé, installez le SDK Azure ML :

   ```bash
   #pip install azureml-sdk
   ```

6. **Installer IPython Kernel** :
   Pour garantir que vous pouvez utiliser cet environnement dans Jupyter ou d'autres interfaces, installez et réinstallez l'IPython Kernel :

   ```bash
   # azureml_env\Scripts\python.exe -m pip install ipykernel -U --force-reinstall
   ```


