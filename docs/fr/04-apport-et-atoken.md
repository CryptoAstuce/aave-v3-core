# Chapitre 4 — L'apport de liquidite et le aToken

Deposer un actif via `supply` fait frapper au deposant un `AToken` en proportion 1:1 au moment du depot : deposer 100 USDC donne 100 aUSDC.

Le mecanisme interessant est que le solde de aToken affiche par `balanceOf` n'est pas stocke tel quel. En interne, `ScaledBalanceTokenBase` stocke un solde mis a l'echelle, `scaledBalanceOf`, qui ne bouge pas avec le temps. `balanceOf` le multiplie a la volee par l'index de liquidite normalise de la reserve : `super.balanceOf(user).rayMul(POOL.getReserveNormalizedIncome(asset))`. Comme cet index ne fait que croitre, le solde affiche croit lui aussi tout seul, sans qu'aucune transaction ne soit necessaire pour distribuer l'interet a chaque detenteur.

`_mintScaled`, dans `ScaledBalanceTokenBase.sol`, fait la conversion inverse a l'entree : `amountScaled = amount.rayDiv(index)`. Elle calcule aussi `balanceIncrease`, l'interet deja accumule depuis la derniere interaction de l'utilisateur, pour l'inclure dans l'evenement `Mint` emis (le solde ERC-20 logique augmente de `amount + balanceIncrease`, mais seul `amountScaled` est reellement frappe).

`_burnScaled` fait l'operation symetrique au retrait. Cette architecture ("rebasement par index" plutot que "rebasement par frappe repetee") est ce qui permet a un aToken de rester un ERC-20 standard tout en distribuant l'interet en continu a tous les detenteurs simultanement.

[Chapitre suivant : l'emprunt et les jetons de dette](05-emprunt-et-dette.md)
