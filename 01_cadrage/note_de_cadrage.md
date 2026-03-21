# Note de cadrage — Projet de surveillance prix & OOS - Amazon Vendor
## Edgard & Cooper — Canal Amazon E-commerce

## 1. Contexte & enjeux
E&C est une entreprise belge de Pet Food fondée en 2014. La marque commercialise des croquettes, aliments humides et friandises pour chiens et chats.
Elle est présente sur plusieurs pays Européen comprenant la France, L'Allemagne, l'Espagne, l'Italie, et l'Angleterre. L'entreprise a une plateforme DtoC mais travaille énormément avec Amazon Vendor et Seller. En 2025, Le CA du e-commerce avec Amazon Vendor était de 14,5M€. 

## 2. Problèmes identifiés
Problème 1 — Détection tardive des ruptures de stock (OOS)

L'information OOS circule manuellement et avec retard. Les décisions correctives sont prises trop tard, avec un impact potentiel sur les ventes et le ranking Amazon.

Problème 2 — Absence de visibilité sur les variations de prix

E&C n'a aucun historique ni suivi des dérives de prix sur ses ASINs. Des produits peuvent être bradés pendant des semaines sans que l'équipe le sache, ce qui empêche toute décision macro (bascule Vendor → Seller, renégociation, retrait).

## 3. Parties prenantes
Partie prenante |	Rôle |	Intérêt dans le projet |	Niveau d'influence
|---|---|---|---|
| Directeur e-commerce	|	Responsable du bon fonctionnement du pôle e-commerce	|	Veut s'assurer que tous les produits Amazon sont en ligne, vendables et au meilleur prix. 	| Elevé |
| Directrice marketing	|	Responsable du marketing, promotion, pub, mise en avant des produits…	|	Elle veut s'assurer que le budget marketing n'est pas utilisé pour un produit invendable.	Baisse de convertion et du ROAS.	|	Moyenne |
| Responsable commerce 	|	S'occupe du bon fonctionnement de tout étant liés aux chiffres de nos clients(Amazon, Zooplus…)	|	Veut le plus vite possible connaître les produits OOS, leur durée d'OOS et si les prix sont corrélés au listing price.	|	Moyenne |
| Supply Chain	|	S'occupe de l'envoie des produits dans les différents entrepôt. Afin de réguler les stocks.	|	Avoir une vue sur des produits OOS si ils ne l'ont pas remarqués avant leur permettant de réagir plus rapidement.	|	Moyenne |
| Country Manager France |	Responsable des ventes France (je le prend en exemple comme je suis Francais) veut s'assurer que chaque produit est vendu au bon prix et vendable. |	Veut le plus de CA possible.	Veut le bon fonctionnement du e-commerce pour porter les ventes au sommet	|	Elevé |


## 4. Périmètre du projet
IN
•	Suivi hebdomadaire des variations du prix affiché consommateur sur Amazon Vendor, par ASIN, sur les 5 marchés (UK, FR, DE, IT, ES)
•	Détection et alerte des produits en rupture de stock (OOS) par marché
•	Diffusion des alertes à l'équipe e-commerce (canal et fréquence à définir)
•	Sauvegarde de l'historique des prix afin de déceler si certains produits doivent être basculés sur Seller
•	Visualisation des tendances prix et OOS via un dashboard consolidé
OUT
•	Comptes non-Amazon : Zooplus, Pets at Home, Medpets NL
•	Réapprovisionnement automatique
•	Gestion des campagnes publicitaires Amazon AMS
•	Recommandations de réapprovisionnement à destination de la Supply Chain
•	Décision de bascule Vendor → Seller (le projet fournit les données, pas la décision)

## 5. Objectifs mesurables 

- Réduire le délai de détection d'un produit OOS de 7 jours à 1 jour ouvré grâce à une alerte hebdomadaire automatisée.
- Créer une réelle capacité de surveillance des variations de prix des produits Amazon Vendor sur le long terme d’ici 1 mois.
- Augmenter notre surveillance de tous les produits OOS sur Vendor et sur tous les marchés d’ici 1 mois avec un suivi hebdomadaire.

## 6. Contraintes & hypothèses

Contraintes
•	Aucun budget alloué — le projet est réalisé dans le cadre de l'alternance
•	Accès aux données limité — les données Amazon (prix, OOS) ne sont pas nativement exportables sans outil tiers payant
•	Projet mené en solo sans équipe dédiée
Hypothèses
•	Le coût des données Keepa reste accessible ou une alternative gratuite est identifiée
•	Les données Keepa sont suffisamment précises et exhaustives pour couvrir les 5 marchés
•	L'outil final sera adopté et consulté régulièrement par l'équipe e-commerce

## 7. Échéance
Projet réalisé dans le cadre de l'alternance — livraison estimée dans 1 mois.
