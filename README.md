# Projet BA — Système de détection prix & OOS | Edgard & Cooper

## Contexte
Edgard & Cooper est une marque belge de pet food présente sur Amazon 
Vendor dans 5 pays (FR, DE, UK, IT, ES) avec un CA de 14,5M€. 
Ce projet a été réalisé dans le cadre de mon alternance en tant que 
Data Analyst au pôle e-commerce.

## Problématique
L'équipe e-commerce n'avait aucune visibilité en temps réel sur :
- Les produits en rupture de stock (OOS) sur Amazon
- Les variations anormales de prix sur les 476 ASINs Vendor

## Ce que le dashboard détecte
- Les produits OOS par marché et par semaine
- Les baisses de prix supérieures à 10% entre deux périodes
- Les alertes prix filtrées sur un minimum de 10 ASINs actifs 
  pour garantir la fiabilité statistique

## Stack technique
- **Données** : Export Keepa (Excel) — 10 094 lignes, 26 semaines
- **Nettoyage** : Power Query (locale, erreurs, lignes corrompues)
- **Modélisation** : DAX (mesures de variation, détection d'anomalies)
- **Visualisation** : Power BI Desktop

## Structure du repo
- `01_cadrage/` — Note de cadrage
- `02_besoins/` — Compte-rendu d'atelier + Backlog MoSCoW
- `03_data/` — Dictionnaire de données
- `04_dashboard/` — Plan dashboard + Documentation technique
- `05_recommandations/` — Note de recommandations
- `06_portfolio/` — Synthèse portfolio
