# TI202 - Algorithmique et Structures de Données 1

Cours Magistraux 2025-2026 - Présentations Slidev

## 📚 Contenu

- **CM1** : Base du langage C
- **CM2** : Tableau et chaîne de caractères (à venir)
- **CM3** : Pointeurs et Allocation dynamique (à venir)
- **CM4** : Les fonctions en C (à venir)
- **CM5** : Types structurés (à venir)
- **CM6** : Listes chaînées (à venir)

## 🚀 Développement Local

### Installation

```bash
npm install
```

### Développer une présentation

```bash
# CM1 - Base du langage C
npm run dev:cm1

# CM2 - Tableau et chaîne de caractères
npm run dev:cm2

# CM3 - Pointeurs et Allocation dynamique
npm run dev:cm3

# CM4 - Les fonctions en C
npm run dev:cm4

# CM5 - Types structurés
npm run dev:cm5

# CM6 - Listes chaînées
npm run dev:cm6
```

### Build pour production

```bash
# Toutes les présentations
npm run build

# Une seule présentation
npm run build:cm1
npm run build:cm2
npm run build:cm3
npm run build:cm4
npm run build:cm5
npm run build:cm6
```

### Exporter en PDF

```bash
npm run export:cm2
npm run export:cm3
npm run export:cm4
npm run export:cm5
npm run export:cm6
# Toutes les présentations
npm run export

# Une seule présentation
npm run export:cm1
```

## 📦 Déploiement

Le déploiement sur GitHub Pages se fait automatiquement via GitHub Actions lors d'un push sur la branche `main`.


## 🛠️ Technologies

- [Slidev](https://sli.dev/) - Presentation slides for developers
- [Vue 3](https://vuejs.org/) - Progressive JavaScript framework
- [Vite](https://vitejs.dev/) - Next generation frontend tooling
- [UnoCSS](https://unocss.dev/) - Instant on-demand atomic CSS engine

## 📄 License

MIT
