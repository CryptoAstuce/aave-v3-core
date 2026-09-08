# Chapitre 5 — L'emprunt et les jetons de dette

Emprunter via `borrow` fait frapper a l'emprunteur un jeton de dette non transferable, en variante variable (`VariableDebtToken`) ou stable (`StableDebtToken`), qui represente ce qu'il doit.

`VariableDebtToken` reutilise exactement le meme mecanisme de solde mis a l'echelle que `AToken` : le solde affiche croit avec `variableBorrowIndex` de la reserve, de la meme facon que le solde de aToken croit avec `liquidityIndex`. C'est la meme bibliotheque `ScaledBalanceTokenBase` qui sert aux deux, cote actif comme cote passif.

`StableDebtToken` fonctionne differemment : chaque emprunt stable fixe un taux au moment de l'emprunt, et le contrat maintient une moyenne ponderee des taux de tous les emprunts stables en cours (`_calculateGlobalRate` dans le meme fichier). Ce taux n'est pas fige a vie ; `rebalanceStableBorrowRate` dans `Pool.sol` permet, sous conditions precises d'ecart au taux du marche, de le realigner.

Ces jetons de dette n'ont pas de fonction `transfer` operante : la dette d'un utilisateur ne peut pas etre cedee a un autre en dehors du protocole lui-meme (liquidation, remboursement pour compte d'autrui).

[Chapitre suivant : les index normalises et les interets composes](06-index-et-interets.md)
