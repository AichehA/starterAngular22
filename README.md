# Starter Angular 22 avec VScode

Ce projet permet d'expliquer comment installer et configurer un projet Angular 22.

- [Starter Angular 22 avec VScode](#starter-angular-22-avec-vscode)
  - [Prérequis](#prérequis)
  - [Création du projet](#création-du-projet)
  - [Explication de la structure de l'application](#explication-de-la-structure-de-lapplication)
  - [Configuration des plugins dans Vscode](#configuration-des-plugins-dans-vscode)
  - [Installation et configuration de Eslint / Prettier](#installation-et-configuration-de-eslint--prettier)
  - [Choix et installation une librairie de composant UI](#choix-et-installation-une-librairie-de-composant-ui)
  - [Conclusion](#conclusion)

## Prérequis

- Node 22 avec NVM
- Vscode

## Création du projet

Utilisation de la commande :

```cmd
npx -p @angular/cli ng new starterAngular22
```

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

## Configuration des plugins dans Vscode

Le fichier extensions.json permet de contenir toutes la liste des extensions partager avec son équipe qui sont recommander à installer.

Pour les retrouver facilement, il faut aller dans l'onglet extension et tape `@recommended`

```json
{
  "recommendations": [
    // Obligatoire pour Angular
    "angular.ng-template", // Permet d'aider l'IDE a comprendre la langue Angular
    "esbenp.prettier-vscode", // Plugin pour le formattage du code
    "dbaeumer.vscode-eslint", // Plugin pour définir des règles de codage
    "ms-vscode.vscode-typescript-next", // Plugin pour le langage TS et JS
    "formulahendry.auto-close-tag", // Permet la création de la balise fermante
    // Confort de vie
    "PKief.material-icon-theme", // Avoir des belles icons pour se retrouver facilement
    "usernamehw.errorlens", // Permet d'afficher les erreurs directement dans le code sans passer la souris dessus.    
    "christian-kohler.path-intellisense", // Permet d'avoir des recommandations de fichier
    "steoates.autoimport" // Aide à l'import de fichier
    // TODO le schématique
  ]
}
```

## Installation et configuration de Eslint / Prettier

## Choix et installation une librairie de composant UI

## Conclusion
