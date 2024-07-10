# Introduction aux Flakes dans Nix

(Draft 1 - à réviser)

## Dans ce chapitre

- Introduction aux flakes dans Nix
- Définition d'un flake et sa structure de base
- Description des attributs des flakes
- Création et utilisation des flakes dans vos projets
- Gestion des dépendances avec les flakes
- Définition et utilisation des sorties des flakes (packages, devShells, checks, etc.)
- Avantages et limitations des flakes


## Qu'est-ce qu'un Flake ?

Les flakes représentent une évolution significative dans l'écosystème Nix, apportant une nouvelle approche pour structurer, gérer et partager des projets. Introduits pour répondre aux défis de la gestion des dépendances et de la reproductibilité des environnements, les flakes offrent une manière modulaire et déclarative de décrire les composants d'un projet Nix, en définissant clairement les entrées et les sorties d'un projet. Bien qu'encore expérimentaux, les flakes ont rapidement gagné en popularité parmi les utilisateurs avancés de Nix pour leur capacité à simplifier et à standardiser de nombreuses tâches courantes.

## Définition d'un Flake

Un flake est essentiellement une fonction qui prend des entrées (inputs) et produit des sorties (outputs). Les entrées peuvent être des références valides, telles que d'autres flakes ou des chemins de fichiers, et les sorties doivent suivre un schéma défini. Voici un exemple simple de définition d'un flake :

```nix
{
  description = "Description de mon flake";
  outputs = { self, nixpkgs }: {
    packages.x86_64-linux.default = nixpkgs.legacyPackages.x86_64-linux.hello;
  };
}
```

## Structure et Syntaxe des Flakes

### Description

La description d'un flake est généralement une courte explication de son objectif. Bien qu'elle soit optionnelle, elle est utile pour fournir un contexte sur le flake lors de l'affichage des métadonnées.

### Inputs

Les entrées d'un flake peuvent inclure d'autres flakes ou des chemins de fichiers. Les entrées sont définies dans l'attribut `inputs`. Par exemple :

```nix
{
  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-unstable";
    myProject.url = "path:/mon/projet";
  };
}
```

### Outputs

Les sorties d'un flake sont définies dans l'attribut `outputs`. Elles peuvent inclure des paquets, des configurations NixOS, des shells de développement, etc. Voici une illustration des différents types de sorties possibles :

- **Packages** : Paquets spécifiques à un système.
- **Apps** : Applications exécutables.
- **DevShells** : Environnements de développement.
- **Checks** : Tests d'intégration et vérifications.
- **NixOS Configurations** : Configurations complètes pour NixOS.

Exemple de sorties avec des paquets et un shell de développement :

```nix
{
  outputs = { self, nixpkgs }: {
    packages.x86_64-linux.default = nixpkgs.legacyPackages.x86_64-linux.hello;
    devShells.x86_64-linux.default = pkgs.mkShell {
      nativeBuildInputs = [ pkgs.hello ];
    };
  };
}
```

## 18.4 Utilisation des Flakes

### 18.4.1 Créer un Flake

Pour créer un flake, il suffit de définir un fichier `flake.nix` dans le répertoire de votre projet avec la structure de base décrite ci-dessus. Ensuite, vous pouvez initialiser et verrouiller les dépendances avec les commandes suivantes :

```bash
nix flake init
nix flake lock
```

### 18.4.2 Exécuter et Tester des Flakes

Pour exécuter une application définie dans un flake, utilisez `nix run` :

```bash
nix run .#default
```

Pour tester les sorties d'un flake, vous pouvez utiliser `nix flake check` qui exécutera tous les tests définis sous l'attribut `checks`.

## 18.5 Exemples Pratiques

### 18.5.1 Exemple de Flake Simple

Un flake simple avec une description, des entrées et une sortie de paquet :

```nix
{
  description = "Exemple de flake simple";
  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-unstable";
  };
  outputs = { self, nixpkgs }: {
    packages.x86_64-linux.default = nixpkgs.legacyPackages.x86_64-linux.hello;
  };
}
```

### 18.5.2 Gestion des Dépendances avec les Flakes

Les flakes permettent de gérer facilement les dépendances de projet en déclarant des entrées spécifiques. Par exemple, pour utiliser une version particulière de `nixpkgs` :

```nix
{
  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/807c549feabce7eddbf259dbdcec9e0600a0660d";
  };
  outputs = { self, nixpkgs }: {
    packages.x86_64-linux.default = nixpkgs.legacyPackages.x86_64-linux.hello;
  };
}
```

## 18.6 Avantages et Limitations des Flakes

Les flakes offrent plusieurs avantages, notamment une meilleure gestion des dépendances, une reproductibilité améliorée et une modularité accrue des configurations. Cependant, étant encore expérimentaux, ils peuvent subir des modifications et certaines fonctionnalités pourraient évoluer dans les futures versions de Nix.

## En résumé

Les flakes représentent une avancée significative dans l'écosystème Nix, offrant une manière structurée et modulaire de gérer les projets et leurs dépendances. En comprenant et en utilisant les flakes, les utilisateurs de Nix peuvent créer des configurations plus robustes et maintenables, tout en tirant parti des puissantes fonctionnalités de ce gestionnaire de paquets unique.

## Références

- https://nixos.wiki/wiki/Flakes
- https://vtimofeenko.com/posts/practical-nix-flake-anatomy-a-guided-tour-of-flake.nix/
