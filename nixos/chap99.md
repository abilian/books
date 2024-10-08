# Appendice 1 : La thèse de Dolstra

La thèse d'Eelco Dolstra, intitulée **[The Purely Functional Software Deployment Model](https://edolstra.github.io/pubs/phd-thesis.pdf)** (PDF, 281 pages), constitue la principale référence académique pour comprendre Nix. Bien qu'écrite il y a presque 20 ans, elle reste étonnamment accessible et toujours pertinente, car une partie importante de son contenu est philosophique plutôt que technique. Ce résumé vise à condenser certaines des idées clés de la thèse, afin d'inciter à lire le texte complet ou, à défaut, fournir un aperçu rapide.

### Déploiement correct des logiciels

À la fin de sa thèse, Dolstra résume l'objectif de son projet : parvenir à un système de déploiement logiciel correct. La "correction" est atteinte par deux moyens principaux : un schéma de nommage précis utilisant des hachages cryptographiques pour résumer le logiciel de manière concise, et un modèle de déploiement purement fonctionnel. Ce dernier repose sur des artefacts de construction immuables, des processus de construction purs (dépendant uniquement de leurs entrées) sans effets secondaires, et une composition précise des composants logiciels.

Dolstra distingue les aspects philosophiques de sa thèse, tels qu'une ontologie du déploiement logiciel et la définition d'un déploiement correct, des techniques et implémentations guidées par cette théorie.

### La correction

La correction se résume par l'équation suivante : **correction = complétude + absence d'interférences**. La complétude implique la présence de toutes les dépendances nécessaires, tandis que l'absence d'interférences signifie qu'aucun composant logiciel différent n'occupe le même espace de noms, ce qui les rendrait indiscernables les uns des autres. Pour illustrer ces concepts, Dolstra utilise des exemples issus de la bijectivité en mathématiques discrètes.

### Déploiement des logiciels

Le déploiement logiciel inclut la distribution, l'acquisition, l'installation, la mise à jour et la désinstallation de logiciels. Les problèmes rencontrés peuvent être classés en deux catégories : gestion de l'environnement et correction d'une part, maniabilité et utilisabilité d'autre part. Les problèmes de correction incluent l'identification des dépendances, la compatibilité des logiciels avec les exigences des dépendances, et la distinction entre les dépendances de construction et d'exécution.

### Problèmes des solutions existantes

Dolstra analyse plusieurs systèmes de gestion de paquets et de déploiement logiciel existants, identifiant des problèmes tels que les mises à jour non atomiques, la nécessité d'applications monolithiques contenant toutes leurs dépendances, la composition manuelle des composants, et la difficulté à adapter les composants. Il conclut que le système le plus proche d'un déploiement correct n'est pas un système de déploiement classique, mais les outils de gestion de configuration logicielle côté développeur, comme les systèmes de contrôle de version.

### Les avantages de Nix

Nix apporte plusieurs avantages grâce à ses principes de base :

1. **Isolation des composants** dans un stockage centralisé.
2. **Schéma de nommage** utilisant des hachages cryptographiques.
3. **Modèle purement fonctionnel** où tous les logiciels sont immuables et où les processus de construction sont déterministes et sans effets secondaires.

Ces principes permettent des déploiements complets et sans interférences, des mises à jour atomiques, des retours en arrière en temps constant, et une distribution transparente des sources et des binaires.

### Détails d'implémentation

Le stockage Nix fonctionne en conservant les composants logiciels sous forme de répertoires nommés avec des hachages dans un répertoire racine (généralement `/nix/store`). Ce schéma de nommage évite les interférences et garantit la complétude. Les dépendances de construction sont identifiées à l'avance, et les dépendances d'exécution sont référencées dans le composant logiciel lui-même, ce qui permet de suivre toutes les dépendances nécessaires.

### Principe du modèle purement fonctionnel

Le modèle purement fonctionnel de Nix repose sur deux aspects principaux : l'immuabilité des chemins de stockage et la pureté des processus de construction, ce qui assure des constructions déterministes et sans effets secondaires.

### Principes de Nix

La thèse de Dolstra énonce plusieurs principes pour l'utilisation de Nix :

- **Les compositions statiques** sont préférables car elles garantissent la correction.
- **Les compositions statiques tardives** permettent de lier dynamiquement des composants via des wrappers.
- **Les environnements utilisateur ne doivent pas servir de mécanisme de composition**.
- **Les composants fins** sont préférables aux composants grossiers, car ils offrent une meilleure réutilisabilité et aident à éviter des clôtures inutilement larges.

### Sujets non couverts à l'époque

La thèse mentionne également plusieurs sujets intéressants pour de futurs travaux, tels que le modèle intentionnel vs extensional, le patching binaire, un langage pour les constructeurs, et un système de types pour le langage d'expression Nix.
