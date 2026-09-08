# Chapitre 3 — Le pool central et ses actions

`Pool.sol` expose les actions que peut effectuer un utilisateur : `supply` (deposer), `withdraw` (retirer), `borrow` (emprunter), `repay` (rembourser), `liquidationCall` (liquider une position sous-collateralisee), `flashLoan` et `flashLoanSimple` (emprunt eclair), `setUserUseReserveAsCollateral` (activer ou desactiver un actif comme garantie).

Chaque fonction publique est courte : elle recupere l'etat de la reserve concernee (`_reserves[asset]`), puis appelle la bibliotheque de logique correspondante (`SupplyLogic.executeSupply`, `BorrowLogic.executeBorrow`, etc.) en lui passant le stockage par reference. `Pool.sol` ne fait quasiment aucun calcul lui-meme.

`getUserAccountData` et `getReserveData` sont les fonctions de lecture principales : la premiere renvoie la synthese de risque d'un utilisateur (collateral total, dette totale, facteur de sante), la seconde l'etat complet d'une reserve (index, taux courants, configuration).

Le contrat est deploye derriere un proxy amenant sa propre gestion de version (`getRevision`), un choix standard chez Aave pour permettre les mises a niveau sans changer l'adresse publique du pool.

[Chapitre suivant : l'apport de liquidite et le aToken](04-apport-et-atoken.md)
