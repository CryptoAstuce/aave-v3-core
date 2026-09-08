# Chapitre 13 — Limites connues et perimetre de ce parcours

Ce depot, `aave/aave-v3-core`, est marque DEPRECATED par ses propres murs : la suite active du developpement est `aave-dao/aave-v3-origin`. Le code ici correspond a la version V3.0.1 historique, largement auditee et deployee, mais fige.

La licence est Business Source License 1.1 : le `LICENSE.md` fixe une date de changement (27 janvier 2023) au-dela de laquelle la licence devient MIT. Cette date est deja passee, le code est donc de fait sous MIT au moment ou ce parcours est ecrit.

L'approximation binomiale de `calculateCompoundedInterest` sous-estime legerement l'interet reel, un choix documente et assume par Aave (leger avantage au protocole plutot qu'a l'emprunteur ou au preteur). Le modele de taux a deux pentes, la prime de liquidation, les seuils de close factor et les plafonds sont tous des parametres de gouvernance modifiables par `PoolConfigurator`, pas des constantes figees dans ce depot.

Ce parcours ne couvre ni l'oracle de prix (`contracts/misc` et les interfaces associees, dont l'implementation concrete vit hors de ce depot), ni la gouvernance Aave (module de securite, jeton AAVE, votes), ni les modules peripheriques comme les incitations ou le "portal" de bridge L2. Rien n'a ete installe, compile, deploye ni execute pour ecrire ces chapitres. Aucun test n'a ete lance ; ces chapitres decrivent ce que le code Solidity dit faire, en renvoyant aux fichiers cites. Le depot fournit sa propre suite de tests Hardhat pour verification independante.
