# Analyse des diamètres de pommes – Test de Student

## Contexte

Dans l'industrie agroalimentaire, le respect des spécifications contractuelles est essentiel. Un producteur de pommes doit garantir que le diamètre moyen de chaque lot est égal à 10 cm, conformément à son cahier des charges. Ce projet met en œuvre une démarche statistique inférentielle pour juger objectivement de la conformité d'un lot à partir d'un échantillon.

## Structure du projet
```text
analyse-diametres-pommes/
├── analyse-diametres-pommes.Rmd   # Script R Markdown
├── .gitignore                     # Fichiers à ignorer
└── README.md                      # Ce fichier
```

## Technologies utilisées

- **R** (version ≥ 4.0)
- Packages de base : `stats`, `graphics`
- **ggplot2** *(optionnel pour des graphiques plus élaborés)*
- **R Markdown** – pour générer un rapport automatisé

## Prérequis

- R installé ([CRAN](https://cran.r-project.org/))
- *(Windows)* Rtools pour compiler certains packages
- Un IDE (RStudio, VS Code avec extension R) ou un terminal

## Installation et exécution

### 1. Cloner le dépôt
```bash
git clone https://github.com/Daniele-Nana/analyse-diametres-pommes.git
cd analyse-diametres-pommes
```

### 2. Exécuter le script

- Ouvrez `analyse-diametres-pommes.Rmd` dans RStudio et cliquez sur **Knit** pour générer le rapport HTML.
- Ou lancez le code R ligne par ligne dans la console.

## Résultats obtenus

### Données

Échantillon de 8 pommes (diamètres en cm) : `9.35, 10.14, 11.31, 8.97, 8.51, 9.92, 9.43, 10.81`

### Statistiques descriptives

- **Moyenne** : 9,805 cm
- **Écart-type** : 0,935 cm
- **Étendue** : 8,51 – 11,31 cm

### Vérification de la normalité (Shapiro‑Wilk)

- W = 0,974
- p‑value = 0,9286 → L'hypothèse de normalité n'est pas rejetée.

### Test de Student bilatéral (H₀ : μ = 10 cm, α = 1 %)

- t = –0,5898 (ddl = 7)
- p‑value = 0,5739
- Intervalle de confiance à 99 % : [8,65 ; 10,96]

### Conclusion

La p‑value étant largement supérieure à 0,01, on ne rejette pas H₀. Le lot est conforme au cahier des charges.

## Hypothèses testées

- **H₀** : le diamètre moyen de la population est égal à 10 cm.
- **H₁** : le diamètre moyen de la population est différent de 10 cm.

Le test de Student a été choisi car l'échantillon est de petite taille, la variance inconnue, et la condition de normalité vérifiée.

## Pistes d'amélioration

- Augmenter la taille de l'échantillon pour une puissance statistique plus élevée.
- Utiliser un test non paramétrique (Wilcoxon) en cas de non‑normalité.
- Générer automatiquement un rapport avec R Markdown (déjà fait).
- Créer un tableau de bord interactif avec Shiny pour visualiser dynamiquement les résultats.
- Étendre le contrôle à d'autres critères (fermeté, calibre) ou à plusieurs lots.
- Intégrer le script dans un pipeline CI/CD pour exécuter les tests automatiquement.

## Auteur

Daniele-Nana