# Starter Angular 22 avec VScode

Ce projet permet d'expliquer comment installer et configurer un projet Angular 22.

- [Starter Angular 22 avec VScode](#starter-angular-22-avec-vscode)
  - [Prérequis](#prérequis)
  - [Création du projet](#création-du-projet)
  - [Explication de la structure de l'application](#explication-de-la-structure-de-lapplication)
  - [Configuration des plugins dans Vscode](#configuration-des-plugins-dans-vscode)
  - [Installation et configuration de eslint / prettier](#installation-et-configuration-de-eslint--prettier)
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
    .vscode ## configuration partager pour l'ide
    public/
      favicon.ico
    src/
      app/
        app.config.ts ## configuration des providers Angular
        app.css ## styles du composant racine
        app.html ## template du composant racine
        app.routes.ts ## table des routes, actuellement vide
        app.spec.ts ## tests du composant racine
        app.ts ## composant racine
      index.html
      main.ts ## point d'entree et bootstrap de l'application
      styles.css ## styles globaux
    .editorconfig ## 
    .gitignore ## 
    .postcssrc.json ## 
    .prettierrc ## 
    AGENTS.md ## décrit comment fonctionne le projet pour l'IA
    angular.json ## configuration Angular CLI
    package-lock.json ## dependances vérrouiller à un instant T
    package.json ## dependances et scripts npm
    tsconfig.app.json
    tsconfig.json
    tsconfig.spec.json
```

## Configuration des plugins dans Vscode
## Installation et configuration de eslint / prettier
## Choix et installation une librairie de composant UI
## Conclusion
