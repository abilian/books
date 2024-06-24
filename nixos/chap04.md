# Installation et Configuration

## Dans ce chapitre

- Étapes pour installer Nix sur Linux ou macOS
- Configuration de base après l'installation de Nix
- Activation des fonctionnalités expérimentales de Nix
- Gestion et utilisation des canaux Nix
- Utilisation du garbage collector de Nix

## Installation de Nix

L'installation de Nix marque le premier pas vers l'adoption de cette puissante plateforme de gestion de paquets. Ce processus a été conçu pour être aussi simple et indolore que possible, que vous soyez sous Linux, macOS, ou même dans certaines configurations plus exotiques. Dans cette section, nous allons vous guider à travers les étapes essentielles pour installer Nix sur votre système.

### Prérequis

Avant de commencer, assurez-vous que votre système répond aux exigences minimales. Vous aurez besoin :

- D'un système d'exploitation basé sur Linux ou macOS.
- D'une connexion Internet pour télécharger Nix et les paquets nécessaires.
- Des droits d'administrateur sur votre système, ou au moins la capacité d'accéder au mode `sudo` pour l'installation.

### Étape 1 : Téléchargement du script d'installation

Nix est installé en utilisant un script shell qui prend en charge la majeure partie du processus. Pour commencer, ouvrez un terminal sur votre système et exécutez la commande suivante :

```bash
sh <(curl -L https://nixos.org/nix/install) --daemon
```

Cette commande télécharge le script d'installation depuis le site officiel de Nix et l'exécute. L'option `--daemon` installe Nix en mode multi-utilisateurs, ce qui est recommandé pour la plupart des configurations car cela permet une utilisation plus flexible de Nix entre différents utilisateurs sur le même système.

### Étape 2 : Exécution du script d'installation

Une fois le script téléchargé, il se lance automatiquement et commence le processus d'installation. Pendant l'installation, le script vous informera de ce qu'il est en train de faire et peut vous demander de confirmer certaines actions. Voici quelques-unes des tâches réalisées par le script :

- Création d'un répertoire `nix` à la racine de votre système pour stocker tous les paquets et leurs dépendances.
- Installation du logiciel Nix et configuration du système pour utiliser le dépôt Nix.
- Configuration des chemins d'accès et des variables d'environnement nécessaires.

Si l'installation se termine avec succès, vous verrez un message indiquant que Nix a été correctement installé et configuré.

### Étape 3 : Configuration de l'environnement

Après l'installation, vous devrez redémarrer votre terminal ou recharger votre fichier de configuration shell (par exemple, `.bashrc` ou `.zshrc`) pour que les modifications prennent effet. Vous pouvez faire cela en exécutant :

```bash
source ~/.bashrc
```

Remplacez `.bashrc` par le fichier de configuration de votre interpréteur de commandes si vous utilisez un shell différent.

### Étape 4 : Vérification de l'installation

Pour vérifier que Nix a été installé correctement, vous pouvez exécuter la commande :

```bash
nix --version
```

Si l'installation a réussi, cette commande affichera la version de Nix installée sur votre système.

### Installations alternatives

Sous Ubuntu, vous pouvez utiliser le paquet `nix-bin` pour installer Nix via `apt` (ou `apt-get`, ou `aptitude`, etc.):

```bash
sudo apt update
sudo apt install nix-bin
```


## Configuration de Base

Après avoir installé Nix, la prochaine étape cruciale est de configurer votre environnement pour tirer le meilleur parti de cet outil puissant. La configuration de base de Nix est relativement simple, mais elle jette les bases pour une gestion des paquets efficace et flexible.

### Configuration du Profile Nix

Lorsque vous installez Nix pour la première fois, un profil utilisateur est automatiquement créé. Ce profil est le point central de gestion de vos paquets Nix. Il se trouve généralement dans `/nix/var/nix/profiles/per-user/<votre_nom_utilisateur>/profile`. Pour vérifier si votre profil est correctement configuré, vous pouvez exécuter :

```sh
echo $NIX_PATH
```

Cette commande devrait retourner le chemin vers votre profil Nix. Si ce n'est pas le cas, assurez-vous que Nix est correctement installé et que votre environnement de shell est configuré pour inclure le chemin Nix.

### Configuration de l'Environnement Shell

Pour que Nix fonctionne correctement dans votre shell, il doit être initialisé à chaque démarrage de session. Cela est généralement géré par le script d'initialisation de Nix, qui doit être inclus dans le fichier de configuration de votre shell (par exemple, `.bashrc` ou `.zshrc` pour Bash et Zsh, respectivement).

Si Nix a été installé correctement, il devrait avoir ajouté automatiquement les lignes nécessaires à votre fichier de configuration de shell. Pour Bash, cela ressemblerait à :

```bash
if [ -e /nix/store/*-nix-*/etc/profile.d/nix.sh ]; then . /nix/store/*-nix-*/etc/profile.d/nix.sh; fi
```

Pour Zsh, l'ajout serait similaire mais dans `.zshrc`. Vérifiez que ces lignes sont présentes pour vous assurer que Nix est correctement initialisé.

Bien sûr, ajoutons cette section importante concernant l'utilisation des fonctionnalités expérimentales dans Nix.

### Activation des Fonctionnalités Expérimentales

Nix continue d'évoluer avec l'introduction de nouvelles fonctionnalités expérimentales. Ces fonctionnalités peuvent offrir des avantages significatifs en termes de performance, d'expérience utilisateur ou de nouvelles capacités, mais elles ne sont pas activées par défaut. Pour les utiliser sans avoir à spécifier l'option `--extra-experimental-features` à chaque commande, suivez ces étapes :

#### Configuration Globale

1. **Modifier le fichier de configuration Nix** : Ouvrez le fichier de configuration global de Nix, `/etc/nix/nix.conf`, avec un éditeur de texte en tant qu'administrateur ou en utilisant `sudo`.

2. **Ajouter les fonctionnalités expérimentales** : Ajoutez la ligne suivante au fichier :
   ```
   experimental-features = nix-command flakes
   ```
   Cette ligne active les commandes Nix de nouvelle génération ainsi que le support pour Flakes, une méthode pour gérer les projets Nix de manière reproductible. Vous pouvez ajuster cette ligne pour inclure d'autres fonctionnalités expérimentales selon vos besoins.

#### Configuration Utilisateur

Si vous préférez activer les fonctionnalités expérimentales uniquement pour votre utilisateur plutôt que globalement, ou si vous n'avez pas les droits d'administrateur, vous pouvez modifier le fichier de configuration dans votre dossier personnel :

1. **Créer ou ouvrir le fichier de configuration utilisateur** : Le fichier se trouve dans `~/.config/nix/nix.conf`. Si le dossier ou le fichier n'existe pas, créez-les.

2. **Ajouter les fonctionnalités expérimentales** : Comme pour la configuration globale, ajoutez la ligne pour activer les fonctionnalités souhaitées.

#### Vérification

Après avoir modifié la configuration, redémarrez votre terminal ou rechargez votre fichier de configuration shell pour appliquer les modifications. Vous pouvez vérifier que les fonctionnalités expérimentales sont activées en exécutant une commande qui les utilise, sans avoir à spécifier l'option `--extra-experimental-features`, par exemple

```bash
nix search nixpkgs firefox
```


### Mise en Place des Canaux (Channels)

Les canaux Nix fournissent un moyen simple de s'abonner à des collections de paquets Nix. Par défaut, lors de l'installation, vous êtes abonné au canal `nixpkgs`, qui contient une vaste collection de paquets Nix. Pour lister les canaux auxquels vous êtes abonné, utilisez :

```sh
nix-channel --list
```

Si vous souhaitez ajouter un nouveau canal, par exemple pour accéder à des versions plus récentes ou à des paquets expérimentaux, vous pouvez le faire avec :

```sh
nix-channel --add <url_du_canal> <nom_du_canal>
nix-channel --update
```

Remplacez `<url_du_canal>` par l'URL du dépôt de paquets et `<nom_du_canal>` par un nom d'identification pour le canal.

### Configuration du Garbage Collector

Nix gère les paquets et leurs dépendances de manière isolée, ce qui peut rapidement utiliser un espace disque substantiel. Heureusement, Nix fournit un "garbage collector" pour supprimer les paquets et les versions non utilisés.

Pour exécuter le garbage collector manuellement et libérer de l'espace, utilisez :

```sh
nix-collect-garbage -d
```

Pour configurer le garbage collector afin qu'il s'exécute automatiquement, vous pouvez définir des paramètres tels que l'âge maximal des paquets ou l'espace disque maximum utilisé dans le fichier de configuration Nix (`/etc/nix/nix.conf`).

## Utilisation de canaux (channels)

Les canaux (channels) jouent un rôle central dans l'écosystème Nix, facilitant la gestion des paquets et des configurations. Un canal dans Nix est essentiellement un pointeur vers une collection spécifique de paquets, leur permettant de rester à jour avec les dernières versions disponibles. Cette section vous guidera à travers les concepts clés de l'utilisation des canaux et vous montrera comment les configurer et les utiliser efficacement.

### Qu'est-ce qu'un Canal ?

Un canal dans Nix est une collection de paquets Nix et de configurations système, généralement hébergée sur un serveur distant. Chaque canal est associé à une branche spécifique de paquets et de configurations, permettant aux utilisateurs de s'abonner à différentes versions ou configurations en fonction de leurs besoins.

### Pourquoi Utiliser des Canaux ?

Les canaux offrent plusieurs avantages, notamment :

- **Mises à jour simplifiées** : Les canaux permettent aux utilisateurs de recevoir des mises à jour de paquets et de configurations de manière automatisée, sans nécessiter de recherches manuelles.
- **Stabilité** : En s'abonnant à un canal spécifique, vous pouvez vous assurer que votre système utilise un ensemble cohérent de paquets testés et validés ensemble, réduisant ainsi les risques d'incompatibilité.
- **Flexibilité** : Les canaux permettent de facilement basculer entre différentes versions de paquets ou configurations du système, facilitant les tests et l'évaluation de différentes configurations.

### Configuration des Canaux

Lors de l'installation de Nix, un canal par défaut est souvent configuré automatiquement pour vous. Cependant, vous pouvez souhaiter ajuster cette configuration pour répondre à vos besoins spécifiques.

**Ajout d'un canal** :

Pour ajouter un nouveau canal, utilisez la commande suivante dans votre terminal :

```shell
nix-channel --add <URL du canal> <nom du canal>
```

Par exemple, pour s'abonner au canal stable de NixOS 21.05, utilisez :

```shell
nix-channel --add https://nixos.org/channels/nixos-21.05 nixos
```

**Mise à jour des canaux** :

Pour mettre à jour tous les canaux auxquels vous êtes abonné, exécutez :

```shell
nix-channel --update
```

Cette commande télécharge et applique les dernières versions des paquets et configurations disponibles pour les canaux auxquels vous êtes abonné.

**Liste des canaux** :

Pour voir une liste de tous les canaux auxquels vous êtes actuellement abonné, utilisez :

```shell
nix-channel --list
```

### Exemple Pratique

Supposons que vous souhaitiez tester la dernière version instable de NixOS tout en conservant l'accès aux paquets de la version stable. Vous pouvez configurer votre système pour suivre à la fois les canaux stable et instable de la manière suivante :

1. Ajoutez le canal instable :

```shell
nix-channel --add https://nixos.org/channels/nixos-unstable \
  nixos-unstable
```

2. Mettez à jour vos canaux :

```shell
nix-channel --update
```

Avec cette configuration, vous pouvez choisir de quel canal installer des paquets en spécifiant le préfixe approprié lors de l'installation ou la mise à niveau des paquets.

## En résumé

Dans ce chapitre, nous avons parcouru le processus d'installation de Nix, grâce au script d'installation. les utilisateurs sont guidés à travers une série d'étapes claires pour configurer leur environnement. Cette configuration initiale inclut la mise en place des profils utilisateur Nix, l'ajustement des environnements shell pour l'initialisation de Nix, et la gestion des canaux pour l'accès aux paquets. De plus, nous avons discuté de l'importance de la configuration du garbage collector de Nix pour maintenir une utilisation efficace de l'espace disque.

Nous avons souligné le rôle essentiel des canaux dans la gestion des paquets Nix, offrant une flexibilité et des mises à jour simplifiées pour les utilisateurs. En suivant ces étapes, les utilisateurs peuvent s'assurer que leur système est à jour avec les dernières versions de paquets, en répondant de manière fine à leurs besoins spécifiques.
