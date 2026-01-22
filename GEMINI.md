# Documentation Projet

> Documentation pour l'autocomplétion et le développement d'un projet Hugolify utilisant Medicalify

## Stack Technique

### Hugo

* **Version**: Go 1.21
* **Modules Hugo**:
  * `github.com/hugolify/medicalify-theme` - Thème principal Medicalify
  * `github.com/hugolify/hugolify-theme@v1.26.32` - Thème de base Hugolify
  * `github.com/hugolify/hugolify-admin@v0.9.1` - Interface d'administration
* **Documentation**: https://www.hugolify.io/docs/

### Dépendances JavaScript

* **Bootstrap**: v5.3.8 (via Hugo modules)
* **Popper.js**: v2 (pour les composants Bootstrap)
* **Splide**: v4.1.3 (carrousels)
* **Rellax**: Effets parallax
* **Tobii**: v3.1.1 (lightbox)
* **Cookie Consent**: v3.1.0 (gestion des cookies)
* **Bootstrap Icons**: v1.13.1

---

## Structure du Projet

### Assets
```
assets/
├── js/
│   ├── components/
│   └── features/
└── sass/
    ├── abstracts/         # Variables et mixins personnalisés
    │   └── _variables-site.sass
    ├── base/              # Styles de base
    │   ├── _fonts.sass
    │   └── _icons.sass
    ├── site/              # Styles spécifiques au site
    │   ├── components/    # Composants réutilisables
    │   │   ├── blocks/    # Blocs de contenu
    │   │   └── _hero.sass
    │   └── layout/        # Mise en page
    │       ├── _footer.sass
    │       └── _header.sass
    └── site.sass          # Point d'entrée principal
```

### Layouts
```
layouts/
```

### Configuration
```
config/
├── _default/              # Configuration par défaut
├── production/            # Configuration production
└── staging/               # Configuration staging
```

---

## SASS

### Framework & Guidelines

* **Framework**: Bootstrap v5.3.8 - https://github.com/twbs/bootstrap/tree/v5.3.8/scss
* **Guidelines**: Sass Guidelines - https://sass-guidelin.es/
* **Syntaxe**: SASS (indentation), pas SCSS

### Ressources Bootstrap

* **Variables**: https://github.com/twbs/bootstrap/tree/v5.3.8/scss/_variables.scss
* **Mixins**: https://github.com/twbs/bootstrap/tree/v5.3.8/scss/_mixins.scss
* **Functions**: https://github.com/twbs/bootstrap/tree/v5.3.8/scss/_functions.scss

### Ressources Hugolify

* **Variables**: https://github.com/Hugolify/hugolify-theme/blob/main/assets/sass/abstracts/_variables.default.sass
* **Mixins**: https://github.com/Hugolify/hugolify-theme/blob/main/assets/sass/abstracts/_mixins.default.sass

### Conventions SASS (`.sass-lint.yml`)

* **Indentation**: 4 espaces
* **Hex colors**: Format long, majuscules (ex: `#FFFFFF`)
* **Ordre des propriétés**: Alphabétique
* **Ordre des déclarations**:
  1. `@extend`
  2. `@include` (mixins)
  3. Propriétés CSS
  4. Règles imbriquées
* **Mixins exclus de l'ordre**: Les mixins de breakpoints Bootstrap peuvent être utilisés après les propriétés
  * `breakpoint`, `mq`, `media-breakpoint-up`, `media-breakpoint-down`, etc.

### Structure des Fichiers SASS

* **Point d'entrée**: `assets/sass/site.sass`
* **Imports**: Utiliser des chemins absolus depuis `/` (ex: `@import "/site/components/hero"`)
* **Fichiers partiels**: Préfixés par `_` (ex: `_variables-site.sass`)

---

## JavaScript

### Configuration ESLint (`.eslintrc.yml`)

* **Environnement**: Browser, ES6
* **Modules**: ES6 modules (`import`/`export`)
* **Indentation**: 4 espaces
* **Quotes**: Simple quotes (`'`)
* **Semi-colons**: Obligatoires
* **Naming**: camelCase
* **Max params**: 4 paramètres par fonction
* **Brace style**: 1tbs (one true brace style)

### Conventions JavaScript

* **Variables**: `const` par défaut, `let` si réassignation nécessaire
* **Functions**: Expression de fonction préférée (ex: `const myFunc = function () {}`)
* **Spacing**: Espaces autour des opérateurs et mots-clés
* **Comments**: Au-dessus du code, pas en ligne
* **Consistent this**: Utiliser `that` pour les références `this`

---

## Scripts NPM

### Développement
* `yarn watch` - Lance le serveur de développement Hugo
* `yarn cms` - Lance Decap CMS en local
* `yarn cms:decapcms` - Lance le serveur proxy Decap CMS
* `yarn cms:netlifycms` - Lance le serveur proxy Netlify CMS

### Build
* `yarn build` - Build de production avec minification
* `yarn build:search` - Build + génération de l'index de recherche (Pagefind)
* `yarn build:icons` - Génération des icônes Bootstrap
* `yarn build:config:pagescms` - Génération de la config PagesCMS

### Maintenance
* `yarn clean` - Nettoie le cache des modules Hugo
* `yarn clean:all` - Nettoie tout le cache Hugo
* `yarn tidy` - Nettoie go.mod et go.sum
* `yarn update` - Met à jour les modules Hugo
* `yarn update:all` - Met à jour tous les modules (Hugo + npm)

---

## PostCSS

### Plugins (`postcss.config.js`)

* **autoprefixer** - Ajoute les préfixes vendeurs automatiquement
* **cssnano** - Minification CSS (production)
* **postcss-purgecss** - Suppression du CSS non utilisé (production)
* **postcss-sass** - Support SASS

### Browserslist (`.browserslistrc`)

Configuration des navigateurs cibles pour autoprefixer

---

## 📝 Conventions de Code

### Nommage

* **Fichiers SASS**: kebab-case avec underscore pour les partiels (ex: `_variables-site.sass`)
* **Classes CSS**: Suivre les conventions Bootstrap et Hugolify
* **Variables SASS**: kebab-case (ex: `$primary-color`)
* **Fonctions/Mixins**: kebab-case (ex: `@mixin custom-button`)

### Organisation du Code

1. **Abstracts**: Variables, mixins, fonctions globales
2. **Base**: Reset, typographie, éléments HTML de base
3. **Site**: Styles spécifiques au projet
   * **Components**: Composants réutilisables
   * **Layout**: Structure de page (header, footer, etc.)

### Surcharge des Styles Hugolify

* Créer des fichiers dans `assets/sass/site/` pour les styles personnalisés
* Utiliser `assets/sass/abstracts/_variables-site.sass` pour surcharger les variables
* Ne jamais modifier directement les fichiers du thème (Hugo modules)

---

## Outils de Qualité

### Linting

* **SASS**: `.sass-lint.yml` - Génère un rapport HTML dans `linters/sass-lint.html`
* **JavaScript**: `.eslintrc.yml` - Configuration ESLint stricte
* **Prettier**: `.prettierrc` - Formatage automatique du code

### Configuration Prettier

* Config: `@hugolify/prettier-config@^0.3.1`
* Ignore: `.prettierignore`

---

## Déploiement

### Netlify

* **Configuration**: `netlify.toml`
* **Plugin**: `netlify-plugin-hugo-cache-resources` - Cache des ressources Hugo

### Environnements

* **Production**: Configuration dans `config/production/`
* **Staging**: Configuration dans `config/staging/`

---

## Ressources Complémentaires

### Documentation Officielle

* **Hugo**: https://gohugo.io/documentation/
* **Hugolify**: https://www.hugolify.io/docs/
* **Bootstrap 5**: https://getbootstrap.com/docs/5.3/
* **Medicalify**: https://www.medicalify.io

### Thèmes GitHub

* **Medicalify Theme**: https://github.com/hugolify/medicalify-theme
* **Hugolify Theme**: https://github.com/hugolify/hugolify-theme

### CMS

* **Hugolify Admin**: https://github.com/hugolify/hugolify-admin

---

## Bonnes Pratiques

### Performance

* Utiliser les mixins de breakpoints Bootstrap pour le responsive
* Éviter les sélecteurs trop profonds (max 3-4 niveaux)
* Privilégier les classes utilitaires Bootstrap quand c'est pertinent

### Maintenance

* Documenter les surcharges importantes dans les commentaires
* Garder les fichiers SASS modulaires et focalisés
* Tester sur plusieurs navigateurs (voir `.browserslistrc`)

### Hugo Modules

* Ne jamais modifier directement les modules dans `resources/_gen/`
* Utiliser `yarn update` pour mettre à jour les modules
* Utiliser `yarn tidy` après les mises à jour pour nettoyer
