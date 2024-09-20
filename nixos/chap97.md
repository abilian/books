# Nix, le language

## References:

https://zero-to-nix.com/concepts/nix-language

## Dans ce chapitre

- Aperçu du langage de programmation Nix
- Les constructions du langage : littéraux, opérateurs, variables et fonctions
- Gestion conditionnelle et utilisation des mots-clés `inherit` et `with`
- Importation et chemins dans Nix
- Bibliothèques standard de Nix
- Fonctionnement des dérivations
- Idiomes courants dans Nix

## Introduction au Langage Nix

Le gestionnaire de paquets Nix repose sur un langage de programmation éponyme. Ce langage est essentiel pour la définition, la construction, et la gestion des paquets ainsi que de leurs dépendances. Nix, le langage, est un langage fonctionnel, purement destiné à la gestion des paquets et des configurations de systèmes.

### Caractéristiques Principales du Langage Nix

Nix est conçu spécifiquement pour répondre aux besoins du gestionnaire de paquets Nix et offre des concepts uniques :

1. **Fonctionnel pur** : Chaque expression Nix est immuable et ne produit pas d'effets de bord. Cela garantit que l'évaluation d'une expression avec les mêmes arguments retournera toujours le même résultat, essentiel pour la reproductibilité des systèmes.

2. **Évaluation paresseuse** : Nix n'évalue les expressions que lorsque leur résultat est explicitement demandé. Cela permet une gestion optimisée des ressources, et une flexibilité accrue pour gérer des configurations complexes.

3. **Spécifique à son domaine** : Contrairement aux langages de programmation généralistes, Nix est entièrement dédié à la gestion des paquets et des environnements de développement. Il n'est pas conçu pour d'autres usages en dehors de ce contexte.

## Constructions du Langage

### Littéraux et Types de Données

Le langage Nix comporte plusieurs types de données, représentés par des littéraux dans le code source.

```nix
# Exemples de types de données
42                # Nombre entier
1.72394           # Nombre flottant
"hello"           # Chaîne de caractères
./fichier.json    # Chemin relatif vers un fichier

# Listes
[ 1 2 3 ]

# Ensembles d'attributs
{ a = 15; b = "autre chose"; }

# Ensembles d'attributs récursifs
rec { a = 15; b = a * 2; }
```

### Opérateurs

Nix comprend plusieurs opérateurs communs à de nombreux langages de programmation. Voici quelques exemples :

| Syntaxe                  | Description                                    |
|--------------------------|------------------------------------------------|
| `+`, `-`, `*`, `/`       | Opérations numériques                          |
| `++`                     | Concatenation de listes                        |
| `==`, `>`, `>=`, `<`, `<=`| Comparateurs d'égalité et d'ordre              |
| `&&`, <code>&vert;&vert;</code>| Opérateurs logiques                       |
| `!`                      | Négation logique                               |
| `//`                     | Fusion d'ensembles d'attributs                 |

#### L'opérateur `//` (Fusion)

L'opérateur `//` est utilisé pour fusionner deux ensembles d'attributs, le second prenant la priorité en cas de conflit.

```nix
{ a = 1; } // { b = 2; }
# Résultat : { a = 1; b = 2; }

{ a = "gauche"; } // { a = "droite"; }
# Résultat : { a = "droite"; }
```

### Liens de Variables

Nix utilise les expressions `let ... in` pour créer des variables locales dans un certain contexte :

```nix
let
  a = 15;
  b = 2;
in a * b
# Résultat : 30
```

Les variables sont immuables, et leurs valeurs ne peuvent être modifiées une fois définies.

### Fonctions

Les fonctions dans Nix sont des lambdas anonymes et prennent un seul argument par défaut (les fonctions à arguments multiples sont simulées par *currying* ou en utilisant des ensembles d'attributs).

```nix
name: "Bonjour ${name}"
```

#### Currying (Fonctions à plusieurs arguments)

Nix utilise le currying pour traiter plusieurs arguments :

```nix
name: age: "${name} a ${toString age} ans"
```

Il est aussi possible d'utiliser des ensembles d'attributs pour accepter plusieurs arguments :

```nix
{ name, age }: "${name} a ${toString age} ans"
```

## Gestion Conditionnelle et Héritage

### `if ... then ... else ...`

Les conditions dans Nix sont des expressions qui nécessitent à la fois une branche "vraie" et "fausse" :

```nix
if condition
then "c'est vrai"
else "c'est faux"
```

### Mot-clé `inherit`

Le mot-clé `inherit` permet d'hériter des variables ou des attributs d'un contexte parent :

```nix
let
  name = "Alice";
in {
  inherit name;  # Equivalent à name = name;
}
```

### Les blocs `with`

`with` permet d'importer tous les attributs d'un ensemble dans le scope :

```nix
let attrs = { a = 15; b = 2; };
in with attrs; a + b
# Résultat : 17
```

## Importation et Chemins

Les fichiers Nix peuvent s'importer entre eux avec la fonction `import`. Le système de chemins Nix (`NIX_PATH`) permet d'accéder à des alias de chemins définis globalement.

```nix
let pkgs = import <nixpkgs> {};
in pkgs.hello
```

## Bibliothèques Standard

Nix comprend plusieurs bibliothèques standard importantes :

1. **`builtins`** : Contient les fonctions de base du langage, comme `toString`, `fetchGit`, ou `derivation`.
2. **`pkgs.lib`** : Inclut de nombreuses fonctions utilitaires pour manipuler des listes, ensembles d'attributs, et chaînes.
3. **`pkgs`** : Représente l'ensemble des paquets disponibles dans Nixpkgs, incluant des fonctions de construction comme `writeText`.

## Les Dérivations

Une dérivation dans Nix décrit une action de construction. C'est un élément fondamental du modèle de gestion des paquets dans Nix.

```nix
derivation {
  name = "hello";
  builder = "bash";
  args = [ "-c" "echo Hello, world!" ];
}
```

Les dérivations peuvent être générées via des fonctions de plus haut niveau comme `stdenv.mkDerivation`.

## Idiomes de Nix

### Lamba de Fichier

Il est courant d'utiliser une entête de fonction pour passer les dépendances dans les fichiers Nix, afin de permettre une modularité et une flexibilité accrues :

```nix
{ pkgs ? import <nixpkgs> {} }:
```

### `callPackage`

Nixpkgs utilise la fonction `callPackage` pour importer des fichiers avec leurs dépendances, en passant automatiquement les arguments requis :

```nix
let my-package = pkgs.callPackage ./mon-paquet.nix {};
in my-package
```

### Overrides et Overlays

Nix permet d'écraser ou de modifier des paquets en utilisant des *overrides* ou des *overlays*, ce qui facilite l'adaptation et l'extension des paquets existants.

```nix
somePackage.overrideAttrs (old: {
  configureFlags = old.configureFlags or [] ++ ["--nouveau-flag"];
})
```

## En Résumé

Le langage Nix, bien que simple, offre une approche puissante et flexible pour la gestion des paquets et des environnements logiciels. Avec ses concepts de pureté fonctionnelle, d'évaluation paresseuse, et d'isolation des dépendances, il permet de construire des systèmes reproductibles, robustes et adaptables. En maîtrisant ses idiomes et constructions, les utilisateurs de Nix peuvent créer et gérer des environnements complexes avec une grande facilité.
