# Chapitre 7 — Le modele de taux d'interet a deux pentes

`DefaultReserveInterestRateStrategy.calculateInterestRates` fixe le taux d'emprunt variable en fonction du taux d'utilisation de la reserve, `borrowUsageRatio = total emprunte / total disponible`.

Le modele a deux segments lineaires, separes par `OPTIMAL_USAGE_RATIO` (typiquement 80 ou 90%). En dessous de ce seuil, le taux croit doucement : `_baseVariableBorrowRate + _variableRateSlope1 * ratio / OPTIMAL_USAGE_RATIO`. Au-dessus, la pente change brutalement pour `_variableRateSlope2`, beaucoup plus raide, appliquee a l'exces au-dela du seuil.

L'intention economique : maintenir l'utilisation pres du seuil optimal. En dessous, un taux d'emprunt modere encourage a emprunter et decourage a retirer sa liquidite. Au-dessus, un taux qui grimpe tres vite decourage rapidement de nouveaux emprunts et incite les emprunteurs existants a rembourser, ce qui protege la reserve contre l'illiquidite (le risque qu'un deposant ne puisse plus retirer faute de liquidite disponible).

Le taux paye aux deposants, `currentLiquidityRate`, n'est pas fixe independamment : `_getOverallBorrowRate` calcule le taux d'emprunt moyen pondere entre dette stable et variable, puis ce taux est redistribue aux deposants au prorata de l'utilisation et net de la part reservee au protocole (`reserveFactor`).

[Chapitre suivant : la configuration bitmap des reserves](08-configuration-bitmap.md)
