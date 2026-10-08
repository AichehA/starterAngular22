# Starter Angular 22 avec VS Code

Ce projet permet d'expliquer comment installer et configurer un projet Angular 22.

- [Starter Angular 22 avec VS Code](#starter-angular-22-avec-vs-code)
  - [Prérequis](#prérequis)
  - [Création du projet](#création-du-projet)
  - [Explication de la structure de l'application](#explication-de-la-structure-de-lapplication)
  - [Configuration des extensions dans VS Code](#configuration-des-extensions-dans-vs-code)
    - [Le système de schematics dans Angular](#le-système-de-schematics-dans-angular)
  - [Installation et configuration de ESLint / Prettier](#installation-et-configuration-de-eslint--prettier)
    - [Installation de ESLint](#installation-de-eslint)
    - [À quoi sert la configuration ?](#à-quoi-sert-la-configuration-)
    - [Règles importantes dans le projet](#règles-importantes-dans-le-projet)
    - [Installation de Prettier](#installation-de-prettier)
    - [Pourquoi utiliser Prettier ?](#pourquoi-utiliser-prettier-)
    - [Mise à jour de la configuration VS Code partagée](#mise-à-jour-de-la-configuration-vs-code-partagée)
    - [Mise à jour de la config de "package.json"](#mise-à-jour-de-la-config-de-packagejson)
    - [Lancement des commandes](#lancement-des-commandes)
  - [Choix et installation d'une librairie de composants UI](#choix-et-installation-dune-librairie-de-composants-ui)
    - [Point important](#point-important)
  - [i18n](#i18n)
    - [À quoi sert l'i18n ?](#à-quoi-sert-li18n-)
  - [Conclusion TODO](#conclusion-todo)

## Prérequis

- Node 22 avec NVM
- VS Code

## Création du projet

Utilisation de la commande :

```bash
npx -p @angular/cli@22 ng new starterAngular22
```

Cette commande permet de créer un projet Angular en version 22. On utilise le mode `npx`, qui permet d'exécuter une commande à distance sans avoir besoin d'installer `ng` sur notre poste.

## Explication de la structure de l'application

```mermaid
---
config:
    treeView:
        rowIndent: 20
        lineThickness: 2
    themeVariables:
        treeView:
            labelFontSize: '18px'
            labelColor: '#FFFFFF'
            lineColor: '#a2a2a2'
---
treeView-beta
  starterAngular22/
    .vscode/ ## configuration partagée de VS Code
      extensions.json ## extensions recommandées pour le projet
      launch.json ## configurations de lancement et de débogage Chrome
      mcp.json ## configuration du serveur MCP Angular CLI
      tasks.json ## tâches VS Code pour démarrer et tester l'application
    public/
      favicon.ico ## icône affichée dans l'onglet du navigateur
    src/
      app/
        app.config.ts ## fournisseurs globaux, gestion des erreurs et routeur Angular
        app.css ## styles du composant racine, fichier actuellement vide
        app.html ## template HTML du composant racine
        app.routes.ts ## définition des routes, actuellement vide
        app.spec.ts ## tests unitaires de création du composant et du titre affiché
        app.ts ## composant racine
      index.html ## document HTML hôte contenant app-root
      main.ts ## point d'entrée qui initialise et démarre le composant racine `app.ts`
      styles.css ## styles globaux et import de Tailwind CSS
    .editorconfig ## règles partagées de formatage des fichiers
    .gitignore ## fichiers et dossiers exclus du suivi Git
    .postcssrc.json ## configuration PostCSS avec le plugin Tailwind CSS
    .prettierrc ## règles de formatage Prettier
    AGENTS.md ## consignes de développement pour l'assistant de code
    angular.json ## configuration Angular CLI des compilations, tests et ressources
    package-lock.json ## versions exactes et arbre résolu des dépendances npm
    package.json ## dépendances du projet et commandes npm
    tsconfig.app.json ## configuration TypeScript de l'application, hors tests
    tsconfig.json ## options TypeScript partagées et références aux configurations
    tsconfig.spec.json ## configuration TypeScript des fichiers de test
```

## Configuration des extensions dans VS Code

Le fichier `.vscode/extensions.json` partage avec l'équipe une liste d'extensions recommandées pour ce projet. Ces recommandations ne sont pas obligatoires : VS Code propose de les installer lorsqu'on ouvre le projet.

Pour les afficher, ouvrez la vue **Extensions** et recherchez `@recommended`.

```jsonc
{
  "recommendations": [
    // Obligatoire pour Angular
    "angular.ng-template", // Angular Language Service : complétion et diagnostics dans les templates Angular
    "esbenp.prettier-vscode", // Formatage du code avec Prettier
    "dbaeumer.vscode-eslint", // Diagnostics ESLint, une fois ESLint configuré dans le projet
    "imgildev.vscode-angular-generator", // Schematics de génération de code pour Angular

    // Extensions de confort de vie
    "PKief.material-icon-theme", // Icônes de fichiers et de dossiers
    "usernamehw.errorlens", // Affiche les diagnostics près du code concerné
    "formulahendry.auto-close-tag", // Ferme automatiquement les balises HTML
    "christian-kohler.path-intellisense", // Complète les chemins de fichiers
    "steoates.autoimport", // Facilite l'ajout d'imports
  ],
}
```

### Le système de schematics dans Angular

Angular met à disposition un système de schémas ("schematics") qui permet de générer automatiquement des fichiers et une structure de code selon des modèles prédéfinis. Cela permet de créer rapidement des composants, des services, des directives, des routes et d'autres éléments du projet sans avoir à tout écrire à la main.

Par exemple, la commande suivante :

```bash
ng generate component mon-composant
```

crée automatiquement le composant, son template, son style et ses tests associés, en respectant les conventions du projet.

Ce mécanisme est très utile pour standardiser le code et gagner du temps lors du développement. Il repose sur des schémas officiels fournis par Angular, mais il est aussi possible d'ajouter des schémas personnalisés.

> [!WARNING]
> Je ne recommande pas l'extension `cyrilletuzi.angular-schematics`, car elle est payante et il n'est pas possible de la personnaliser facilement.

Je recommande l'extension `imgildev.vscode-angular-generator` car elle permet de créer des commandes personnalisées.

Dans le fichier `.vscode/settings.json`, il est possible d'ajouter des commandes personnalisées pour générer des composants, des services ou autres via le plugin.

Exemple de configuration :

```jsonc
{
  "angular.submenu.customCommands": [
    {
      "name": "Creation component pour starterAngular22",
      "command": "npm run ng g -- c",
      "args": "--project starterAngular22",
    },
    {
      "name": "Creation service pour starterAngular22",
      "command": "npm run ng g -- s",
      "args": "--project starterAngular22",
    },
  ],
  ...
}
```

> [!TIP]
> On utilise `npm run ng` pour appeler le binaire Angular du projet depuis `node_modules`, sans devoir installer Angular CLI globalement sur la machine.

Pour lancer la génération, il faut juste faire un clic droit sur le dossier où on veut faire une génération.
Puis "Angular File Generator" > "Generate Custom Element with CLI" > "Taper le nom du fichier" puis choisir entre composant ou service.

L'avantage avec cette façon de faire, c'est que l'on peut personnaliser facilement la génération.

## Installation et configuration de ESLint / Prettier

### Installation de ESLint

Pour installer et préparer la validation du code Angular, on utilise la commande suivante :

```bash
npm run ng add @angular-eslint/schematics@22
```

Cette commande ajoute les dépendances et génère la configuration ESLint du projet. Dans cette version d'Angular, le fichier généré est `eslint.config.js`.

### À quoi sert la configuration ?

Le fichier `eslint.config.js` regroupe plusieurs ensembles de règles :

- `eslint.configs.recommended` : règles de base recommandées par ESLint.
- `tseslint.configs.recommended` : bonnes pratiques pour TypeScript.
- `tseslint.configs.stylistic` : règles de style et de lisibilité.
- `angular.configs.tsRecommended` : recommandations Angular pour les fichiers TypeScript.
- `angular.configs.templateRecommended` : règles pour les templates Angular.
- `angular.configs.templateAccessibility` : vérification de l'accessibilité HTML et Angular.

### Règles importantes dans le projet

Le fichier contient aussi des règles personnalisées concernant les sélecteurs Angular :

Ces règles imposent que :

- les attributs Angular utilisent le préfixe `app` en camelCase, par exemple `appUserCard` ;
- les composants HTML utilisent le préfixe `app` en kebab-case, par exemple `app-user-card`.

Cela permet de garder une convention de nommage cohérente et d'éviter les collisions avec les balises HTML standard.

Il est possible de retrouver la liste complète des règles Angular ESLint sur le lien [GitHub du plugin angular-eslint](https://github.com/angular-eslint/angular-eslint/tree/v22.5.0/packages/eslint-plugin/docs/rules).

### Installation de Prettier

```bash
npm i prettier -D
```

> [!NOTE]
> Dans cette commande, on utilise le paramètre `i`, qui est un alias de `install`, puis on indique le paramètre `-D` pour ajouter la dépendance dans la partie `devDependencies` du fichier `package.json`.

### Pourquoi utiliser Prettier ?

Prettier sert à uniformiser le format du code (indentation, guillemets, virgules, sauts de ligne, etc.). Il est complémentaire à ESLint :

- ESLint valide la qualité et la cohérence du code.
- Prettier s'occupe du rendu visuel et du formatage.

Le projet contient déjà un fichier `.prettierrc`, mais il faut lui ajouter de nouvelles règles.

```jsonc
{
  "printWidth": 120, // Permet de définir la longueur de ligne à partir de laquelle Prettier tentera de renvoyer le code à la ligne pour en préserver la lisibilité.
  "tabWidth": 2, // Nombre d'espaces par niveau d'indentation
  "useTabs": false, // Pour ne pas indenter les lignes avec des tabulations, mais avec des espaces
  "singleQuote": true, // Pour formater le code avec des guillemets simples au lieu de guillemets doubles
  "semi": true, // Pour afficher des points-virgules à la fin des instructions
  "bracketSpacing": true, // Pour formater le code avec des espaces autour des accolades dans les objets ou les tableaux
  "arrowParens": "avoid", // Pour éviter les parenthèses autour d'un paramètre unique de fonction fléchée.
  "trailingComma": "es5", // Utilise des virgules de fin dans les paramètres de type en TypeScript et Flow lorsqu'elles sont valides en ES5 (objets, tableaux, etc.).
  "bracketSameLine": true, // Place le « > » d'un élément HTML multiligne (HTML, JSX, Vue, Angular) à la fin de la dernière ligne au lieu de le placer seul sur la ligne suivante (ne s'applique pas aux éléments auto-fermants).
  "overrides": [
    {
      "files": "*.html",
      "options": {
        "parser": "angular", // Pour avoir le formatage Angular sur les contrôles de flux (@if, @for, ...)
      },
    },
  ],
}
```

### Mise à jour de la configuration VS Code partagée

Maintenant que la configuration est en place, il faut modifier le fichier nommé `.vscode/settings.json`.

Ce fichier contient toutes les configurations que l'on veut partager. Dans notre cas, on va ajouter la configuration pour lancer le formatage Prettier au moment de la sauvegarde du fichier.

Voici la configuration :

```jsonc
{
  "files.autoSave": "onFocusChange",
  "editor.formatOnSave": true,
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
  },
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
  },
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
  },
  "[jsonc]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
  },
  "[markdown]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
  },
}
```

### Mise à jour de la config de "package.json"

Il faut ajouter quelques commandes dans notre configuration.

```jsonc
  "scripts": {
    ...
    "lint": "ng lint", // Permet de lister les erreurs d'écriture
    "lint:fix": "ng lint --fix", // Permet de corriger automatiquement le code si possible, sinon il faut le faire manuellement
    "prettier": "prettier --write ." // Permet de formater tous les fichiers du projet
  },
```

### Lancement des commandes

Pour commencer, lancez le formatage du code avec la commande Prettier :

```bash
npm run prettier
```

Suite à cela, il faudra commiter les changements.

Ensuite, il faudra lancer la commande pour corriger les erreurs de code :

```bash
npm run lint:fix
```

Ensuite, il faudra aussi commiter les modifications.

À partir de ce moment-là, l'environnement Prettier et ESLint est configuré. À chaque modification de fichier, le formatage sera lancé et tout le monde aura la même configuration sur son poste de travail.

## Choix et installation d'une librairie de composants UI

Pour accélérer le développement d'une interface moderne et cohérente, il est souvent utile d'ajouter une librairie de composants. Pour un projet Angular, l'option la plus naturelle reste Angular Material, car elle est officiellement maintenue par Google et pensée pour fonctionner nativement avec le framework.

Voici une liste des librairies populaires :

- Angular Material
- PrimeNG
- NG Bootstrap
- Taiga UI
- Zard/ui (qui correspond à un Shadcn/ui de React)

### Point important

Ces librairies apportent des composants prêts à l'emploi, mais elles ne remplacent pas le bon usage de l'architecture et du design system. Le plus important reste de choisir une librairie adaptée aux besoins du projet, puis de garder une cohérence visuelle dans l'application.

## i18n

L'internationalisation est une fonctionnalité native d'Angular qu'il faut activer avec l'installation du package `ng add @angular/localize`. Elle permet de préparer une application pour plusieurs langues sans dupliquer toute la logique de l'interface.

Il est aussi possible d'utiliser d'autres librairies comme `Transloco de jsverse`.

J'ai surtout utilisé la librairie Transloco, car elle permet une utilisation assez simple.

### À quoi sert l'i18n ?

L'i18n permet de :

- Traduire les libellés affichés à l'utilisateur dans d'autres langues comme `fr`, `en`, `es`
- Centraliser les libellés dans des fichiers pour une meilleure maintenance dans le temps.

## Conclusion TODO

Ce starter Angular 22 permet de poser les bases d'un projet moderne et bien structuré :

- création de projet Angular 22 avec le bon outil CLI
- organisation claire du code et des ressources
- configuration de VS Code pour gagner en productivité
- installation d'ESLint et Prettier pour la qualité et le formatage
- préparation du projet avec des composants UI
- support de l'i18n pour des applications multilingues

En somme, ce starter sert de fondation solide pour démarrer un projet Angular avec des conventions lisibles, des outils pertinents et une structure facilement extensible.
