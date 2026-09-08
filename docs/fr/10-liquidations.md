# Chapitre 10 — Les liquidations

`LiquidationLogic.executeLiquidationCall` permet a n'importe quelle adresse de rembourser une partie de la dette d'un utilisateur dont le facteur de sante est descendu sous 1, en echange d'une partie de son collateral a un prix escompte (la prime de liquidation).

`_calculateDebt` fixe combien de dette peut etre remboursee en une seule liquidation via le "close factor". Par defaut (`DEFAULT_LIQUIDATION_CLOSE_FACTOR`), 50% de la dette peut etre liquidee en une fois. Mais si le facteur de sante est deja tres bas, sous `CLOSE_FACTOR_HF_THRESHOLD` (0.95), le close factor passe a 100% (`MAX_LIQUIDATION_CLOSE_FACTOR`) : une position dangereusement sous-collateralisee peut etre entierement liquidee d'un coup plutot que par etapes, pour limiter le risque de creance irrecouvrable pour le protocole.

`_calculateAvailableCollateralToLiquidate` convertit le montant de dette rembourse en montant de collateral a transferer, majore de la prime de liquidation propre a cet actif. `_burnCollateralATokens` et `_liquidateATokens` gerent les deux issues possibles : le collateral saisi est soit brule et transfere en actif sous-jacent au liquidateur, soit transfere directement sous forme de aToken si le liquidateur choisit de le garder dans le protocole.

`_burnDebtTokens` reduit enfin la dette de l'utilisateur liquide, en respectant l'ordre stable puis variable si les deux coexistent.

[Chapitre suivant : le mode isole et le mode d'efficacite](11-modes-isole-et-efficacite.md)
