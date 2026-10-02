# Starter Angular 22 avec VScode

Ce projet permet d'expliquer comment installer et configurer un projet Angular 22.

- [Starter Angular 22 avec VScode](#starter-angular-22-avec-vscode)
  - [Prérequis](#prérequis)
  - [Création du projet](#création-du-projet)
  - [Explication de la structure de l'application](#explication-de-la-structure-de-lapplication)
  - [Configuration des extensions dans VS Code](#configuration-des-extensions-dans-vs-code)
  - [Installation et configuration de ESLint / Prettier](#installation-et-configuration-de-eslint--prettier)
    - [Installation de ESlint](#installation-de-eslint)
    - [À quoi sert la configuration ?](#à-quoi-sert-la-configuration-)
    - [Règles importantes dans le projet](#règles-importantes-dans-le-projet)
    - [Installation de Prettier](#installation-de-prettier)
    - [Pourquoi utiliser Prettier ?](#pourquoi-utiliser-prettier-)
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

## Installation et configuration de ESLint / Prettier

### Installation de ESlint

Pour installer et préparer la validation du code Angular, on utilise la commande suivante :

```bash
npm run ng add @angular-eslint/schematics@22
```

> [!TIP]
> On utilise `npm run ng` pour appeler le binaire Angular du projet depuis `node_modules`, sans devoir installer Angular CLI globalement sur la machine.

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

Le fichier contient aussi des règles personnalisées sur les sélecteurs Angular :

Ces règles imposent que :

- les attributs Angular utilisent le préfixe `app` en camelCase, par exemple `appUserCard` ;
- les composants HTML utilisent le préfixe `app` en kebab-case, par exemple `app-user-card`.

Cela permet de garder une convention de nommage cohérente et évite les collisions avec les balises HTML standards.

Il est possible de retrouver la liste complète des règles Angular ESLint sur leur [GitHub du plugin angular-eslint](https://github.com/angular-eslint/angular-eslint/tree/v22.5.0/packages/eslint-plugin/docs/rules).

### Installation de Prettier

```bash
npm i prettier -D
```

> [!NOTE]
> Dans cette commande on utilise le paramètre `i` qui est un alias de `install` puis on indique le paramètre `-D` pour ajouter la dépendance dans la partie `devDependencies`
> du fichier `package.json`.

### Pourquoi utiliser Prettier ?

Prettier sert à uniformiser le format du code (indentation, guillemets, virgules, sauts de ligne, etc.). Il est complémentaire à ESLint :

- ESLint valide la qualité et la cohérence du code
- Prettier s'occupe du rendu visuel et du formatage.

Le projet contient déjà un fichier `.prettierrc` mais il faut lui ajouter des nouvelles règles.

```jsonc
{
  "printWidth": 120, // Permet de définir la longueur de ligne à partir de laquelle Prettier tentera de renvoyer le code à la ligne pour en préserver la lisibilité.
  "tabWidth": 2, // Nombre d'espaces par niveau d'indentation
  "useTabs": false, // Pour ne pas indenter les lignes avec des tabulations, mais avec des espaces
  "singleQuote": true, // Pour formater le code avec des guillemets simples au lieu de guillemets doubles
  "semi": true, // Pour afficher des points-virgules à la fin des instructions
  "bracketSpacing": true, // Pour formater le code avec des espaces autour des accolades dans les objets ou les tableaux
  "arrowParens": "avoid", // Pour éviter les parenthèses autour d’un paramètre unique de fonction fléchée.
  "trailingComma": "es5", // Utilise des virgules de fin dans les paramètres de type en TypeScript et Flow lorsqu’elles sont valides en ES5 (objets, tableaux, etc.).
  "bracketSameLine": true, // Place le « > » d’un élément HTML multiligne (HTML, JSX, Vue, Angular) à la fin de la dernière ligne au lieu de le placer seul sur la ligne suivante (ne s’applique pas aux éléments auto-fermants).
  "overrides": [
    {
      "files": "*.html",
      "options": {
        "parser": "angular" // Pour avoir le formatage Anguler sur les contrôl flow (@if, @for, ...)
      }
    }
  ]
}
```

## Choix et installation une librairie de composant UI

## i18n

## Conclusion
