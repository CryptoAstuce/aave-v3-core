# Chapitre 6 — Les index normalises et les interets composes

`ReserveLogic.getNormalizedIncome` et `getNormalizedDebt` renvoient les facteurs multiplicatifs par lesquels tout solde scale doit etre multiplie pour obtenir le solde reel courant, en unite ray (27 decimales). Une valeur de `1e27` signifie aucun interet accumule ; `2e27` signifie que l'interet accumule egale le capital initial.

Deux formules distinctes sont utilisees. `MathUtils.calculateLinearInterest` calcule l'interet cote offre (liquidityIndex) : `RAY + taux * temps_ecoule / SECONDS_PER_YEAR`, une approximation lineaire simple. `calculateCompoundedInterest` calcule l'interet cote dette variable (variableBorrowIndex) via une approximation binomiale des trois premiers termes de `(1+x)^n` : suffisant pour approcher un interet compose sans recourir a une exponentiation couteuse en gaz, au prix d'une legere sous-estimation qui favorise le protocole.

`_updateIndexes`, dans `ReserveLogic.sol`, applique ces facteurs aux index stockes chaque fois qu'une action touche la reserve, avant tout calcul de solde. `getNormalizedIncome` court-circuite le calcul si l'index a deja ete mis a jour dans le meme bloc (`timestamp == block.timestamp`), pour eviter un travail redondant.

`WadRayMath` fournit `rayMul` et `rayDiv`, les deux operations centrales de toute cette arithmetique, avec arrondi au plus proche implemente en assembly Yul pour economiser du gaz.

[Chapitre suivant : le modele de taux a deux pentes](07-modele-de-taux.md)
