# Documentation technique — Page Prix
## Module de détection des variations de prix
**Auteur :** Joffray | **Date :** Avril 2026 | **Outil :** Power BI Desktop

---

## 1. Problèmes de qualité de données rencontrés

### Problème 1 — Colonne `Amazon Current` en type texte
Au chargement, la colonne `Amazon Current` était détectée en type texte (AB꜀) 
par Power Query, rendant tout calcul DAX impossible. La cause racine était un 
conflit de séparateur décimal : le fichier source utilisait le point comme 
séparateur (format en-US) alors que Power Query appliquait les paramètres 
régionaux français.

**Correction appliquée :** Conversion via "Change Type with Locale" 
(locale en-US, type Decimal Number), suivie d'un "Replace Errors → null" 
pour les 2% de valeurs résiduelles en erreur.

### Problème 2 — Ligne corrompue dans la colonne `Week`
Une ligne contenait la valeur `05/06/2025+B11569:B12985` dans la colonne 
`Week` — résultat d'une cellule Excel mal formée dans le fichier source 
(date collée avec une référence de plage Excel). Cette ligne provoquait 
une erreur de conversion de type sur l'ensemble de la colonne.

**Correction appliquée :** Ajout d'un filtre Power Query 
`Table.SelectRows(..., each not Text.Contains([Week], "+"))` 
avant l'étape de conversion, éliminant la ligne corrompue sans 
impacter les 10 093 lignes valides restantes.

### Problème 3 — Valeurs nulles sur `Amazon Current`
17% des lignes présentaient une valeur nulle sur `Amazon Current`. 
Après investigation, ces nulls correspondaient aux lignes où 
`Buy Box Seller` = "no Amazon offer exists" — c'est-à-dire les cas 
où Amazon n'est pas vendeur actif sur l'ASIN. Ces nulls sont donc 
métier significatifs et non de la saleté à corriger.

**Décision prise :** Aucun traitement supplémentaire. La fonction 
`AVERAGE()` en DAX ignore nativement les nulls, ce qui produit 
un comportement correct.

-- 

## 2. Décisions métier prises

### 1ère Décision - Le seuil de fiabilité du prix moyen
Il est important d'établir un seuil de fiabilité du prix moyen en corrélation avec le nombre d'ASINs.
Nous avons estimé qu'en dessous de ce seuil, la moyenne est calculée sur un volume trop faible et n'est pas représentative du marché.

### 2ème Décision - Le traitement des nulls sur Amazon Current
Un environ de 20% à été considéré comme null dans la base de données au niveau de Amazon Current Ce qui posait un problème.

### 3ème Décision - Le seuil d'alerte prix
Il était important de délimiter un seuil d'alerte prix pour ne pas recevoir trop d'alertes et d'être dépassé. Nous avons fixé
un seuil de 10% de baisse car cela semblait être une bonne limite en accord avec l'équipe e-commerce.

--

## 3. Mesures DAX créées

| Mesure | Formule | Description |
|---|---|---|
| Prix Moyen | `AVERAGE(Data[Amazon Current])` | Prix moyen brut par contexte de filtre |
| Prix Moyen Fiable | `IF(NbASINs >= 10, AVERAGE(...), BLANK())` | Prix moyen conditionné à un minimum de 10 ASINs actifs |
| Prix Semaine Precedente | `CALCULATE([Prix Moyen Fiable], Data[Week] = DatePrecedente)` | Prix de la période précédente sur dates irrégulières |
| Variation Prix % | `DIVIDE([Prix Moyen Fiable] - [Prix Semaine Precedente], [Prix Semaine Precedente])` | Variation relative entre deux périodes |
| Alerte Baisse Prix | `IF([Variation Prix %] < -0.10, "⚠️ ALERTE", BLANK())` | Déclenchement d'alerte si baisse supérieure à 10% |

--

## 4. Limites connues

### 1ère Limite - Les devises ne sont pas converties
Pour éviter toute confusion, les slicers Country permettent à l'utilisateur de filtrer par pays et donc de consulter 
chaque devise séparément. Une conversion GBP/EUR n'a pas été implémentée faute de taux historique disponible dans les 
données source.

### 2ème Limite - Le seuil de 10 ASINs est arbitraire
Ce seuil a été fixé empiriquement, on ne sait pas si c'est le meilleur seuil ou le plus exact selon notre projet.

### 3ème Limite - La détection ne couvre qu'une période
La détection compare uniquement J avec J-1. Elle ne détecte pas une baisse lente et progressive sur 4-5 semaines 
si chaque baisse individuelle est inférieure à 10%. C'est une vraie limite métier.


