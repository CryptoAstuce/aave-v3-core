# Chapitre 9 — Le facteur de sante et le risque utilisateur

`GenericLogic.calculateUserAccountData` parcourt toutes les reserves d'un utilisateur pour calculer trois totaux exprimes dans une devise de base commune (generalement le dollar, via l'oracle de prix) : la valeur totale de son collateral, la valeur totale de sa dette, et un seuil de liquidation pondere par la part de chaque actif dans le collateral.

Le facteur de sante (`healthFactor`) en decoule : `collateral total * seuil de liquidation pondere / dette totale`. Un facteur de sante superieur a 1 signifie une position saine ; en dessous de 1, la position devient liquidable par n'importe quel liquidateur externe.

`calculateAvailableBorrows` utilise le meme calcul sous-jacent mais avec le LTV (loan-to-value, plus prudent que le seuil de liquidation) pour determiner combien un utilisateur peut encore emprunter avant d'atteindre la limite d'emprunt — une marge deliberement plus stricte que la limite de liquidation, pour laisser un coussin de securite.

Un actif en mode isole (verifie via `IsolationModeLogic`) ou hors de la categorie eMode active de l'utilisateur peut etre exclu de ce calcul ou plafonne differemment : le facteur de sante n'est donc pas une simple somme, il depend du mode dans lequel l'utilisateur se trouve.

[Chapitre suivant : les liquidations](10-liquidations.md)
