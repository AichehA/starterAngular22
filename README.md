# Starter Angular 22 avec VScode

Ce projet permet d'expliquer comment installer et configurer un projet Angular 22.

- [Starter Angular 22 avec VScode](#starter-angular-22-avec-vscode)
  - [Prérequis](#prérequis)
  - [Création du projet](#création-du-projet)
  - [Explication de la structure de l'application](#explication-de-la-structure-de-lapplication)
  - [Configuration des extensions dans VS Code](#configuration-des-extensions-dans-vs-code)
  - [Installation et configuration de Eslint / Prettier](#installation-et-configuration-de-eslint--prettier)
  - [Choix et installation une librairie de composant UI](#choix-et-installation-une-librairie-de-composant-ui)
  - [i18n](#i18n)
  - [Conclusion](#conclusion)

## Prérequis

- Node 22 avec NVM
- Vscode

## Création du projet

Utilisation de la commande :

```bash
npx -p @angular/cli@22 ng new starterAngular22
```

Cette commande permet la création d'un projet Angular en version 22. On utilise le mode `npx` qui permet d'exécuté une commande a distance sans avoir besoin d'installer `ng` sur notre poste.

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
      favicon.ico ## icone affichee dans l'onglet du navigateur
    src/
      app/
        app.config.ts ## fournisseurs globaux, gestion des erreurs et routeur Angular
        app.css ## styles du composant racine, fichier actuellement vide
        app.html ## template HTML du composant racine
        app.routes.ts ## définition des routes, actuellement vide
        app.spec.ts ## tests unitaires de création du composant et du titre affiché
        app.ts ## composant racine
      index.html ## document HTML hôte qui contient app-root
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
    // TODO le schématique

    // Extensions de confort de vie
    "PKief.material-icon-theme", // Icônes de fichiers et de dossiers
    "usernamehw.errorlens", // Affiche les diagnostics près du code concerné
    "formulahendry.auto-close-tag", // Ferme automatiquement les balises HTML
    "christian-kohler.path-intellisense", // Complète les chemins de fichiers
    "steoates.autoimport" // Facilite l'ajout d'imports
  ]
}
```

## Installation et configuration de Eslint / Prettier

```bash
npm run ng add @angular-eslint/schematics@22
```

> [!TIP]
> On utilise la commande `npm run ng` pour utiliser le binaire du projet dans le dossier `node_modules` sans avoir besoin d'installer globalement la version Angular 22 sur notre machine.

Cette commande va ajouter et installer des nouveaux fichiers et dépendances pour la configuration de eslint.

Toute la configuration est dans le fichier `eslint.config.ts`.

Il est possible de retrouver la liste de la configuration en lien avec angular sur leur [github du plugin angular-eslint](https://github.com/angular-eslint/angular-eslint/tree/v22.5.0/packages/eslint-plugin/docs/rules). Il indique comment utiliser les différents règles de code avec les cas passants et d'erreur. 

## Choix et installation une librairie de composant UI

## i18n

## Conclusion
