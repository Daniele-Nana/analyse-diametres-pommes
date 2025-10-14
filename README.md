# Test de conformité des diamètres d'un échantillon des pommes

## Objectif
Un producteur de pommes impose la clause suivante dans son cahier des charges :  
> *"Le diamètre d'une pomme dans chaque lot fourni devra avoir une moyenne égale à 10 cm."*

À partir d’un échantillon de **8 pommes**, on cherche à :
1. Décrire le jeu de données par des paramètres et des graphiques pertinents.  
2. Vérifier si la variable aléatoire \( X \) (diamètre) suit une loi normale.  
3. Tester, au risque de **1%**, si le cahier des charges est respecté (test de Student).

---

## Données

Échantillon :  
\[
X = [9.35, 10.14, 11.31, 8.97, 8.51, 9.92, 9.43, 10.81]
\]

---

## Étape 1 : Statistiques descriptives

```python
X = np.array([9.35, 10.14, 11.31, 8.97, 8.51, 9.92, 9.43, 10.81])

m = np.mean(X)   # Moyenne des diamètres
s = np.std(X, ddof=1) # Écart-type des diamètres de l'échantillon, ddof = 1 pour corriger le biais car on n'a pas toute la population 

print(f"Moyenne : {m}")
print(f"Écart-type : {s}")
```

### Résultat :

```text
- Moyenne : 9.805 cm

- Écart-type : 0.935 cm
```

---

## Étape 2 : Visualisation

```python
plt.hist(X, color="pink", edgecolor="black", density=True)
t = np.linspace(np.min(X), np.max(X), 1001)
plt.plot(t, stat.norm.pdf(t, m, s), color="brown", label="Densité normale")
plt.axvline(m, color="orange", linestyle="dashed", label=f"Moyenne = {m}")
plt.title("Distribution des diamètres des pommes")
plt.xlabel("Diamètre (cm)")
plt.ylabel("Densité")
plt.legend()
plt.show()

plt.boxplot(X)
plt.title("Diagramme en boîte des diamètres des pommes")
plt.ylabel("Diamètre (cm)")
plt.xticks([1], ["Échantillon extrait au hasard"])
plt.show()
```
### Graphiques obtenus :

---

## Étape 3 : Test de normalité (Shapiro-Wilk)

```python
shap_stat, shap_p_valeur = stat.shapiro(X)
print(f"p-valeur = {shap_p_valeur}")
```

### Résultat :

```text
- Statistique de test = 0.974

- p-valeur = 0.9286
```
### Interprétation :

H₀ : X suit une loi normale   
H₁ : X ne suit pas une loi normale   
Comme p = 0.9286 > 0.05, on ne rejette pas H₀.   
Les diamètres peuvent être considérés comme suivant une loi normale.

---

## Étape 4 : Test de Student (risque α = 1%)

```python
t_stat, t_p_valeur = stat.ttest_1samp(X, 10)
print(f"t = {t_stat}, p-valeur = {t_p_valeur}")
```

### Résultat :

```text
- Statistique t = -0.5897

- p-valeur = 0.5739
```

### Hypothèses :

- H₀ : μ = 10 (le cahier des charges est respecté)

- H₁ : μ ≠ 10 (le cahier des charges n’est pas respecté)

### Décision :

Comme p = 0.5739 > 0.01, on ne rejette pas H₀.   
La moyenne des diamètres n’est pas significativement différente de 10 cm.

---

## Conclusion générale :

Les diamètres des pommes sont compatibles avec une moyenne de 10 cm.   
Le cahier des charges du producteur est donc respecté.
