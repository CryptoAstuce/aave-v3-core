# Chapitre 11 — Le mode isole et le mode d'efficacite (eMode)

Le mode isole (`IsolationModeLogic.sol`) restreint un actif juge plus risque : quand un utilisateur n'a que cet actif comme collateral, il ne peut emprunter que des actifs explicitement autorises en isolation, et jusqu'a un plafond de dette total exprime en dollars (`debtCeiling`), pas en quantite de l'actif. `updateIsolatedDebtIfIsolated` decremente ce plafond a chaque remboursement ou liquidation. Ce mecanisme permet a Aave de lister des actifs plus volatils ou plus recents sans exposer l'ensemble du protocole a leur risque.

Le mode d'efficacite, ou eMode (`EModeLogic.sol`), fait l'inverse pour des actifs fortement correles entre eux, par exemple plusieurs stablecoins ou plusieurs versions d'ETH liquide. `executeSetUserEMode` place un utilisateur dans une categorie eMode ; a l'interieur de cette categorie, le LTV et le seuil de liquidation sont bien plus genereux que les valeurs par defaut, parce que le risque de desynchronisation de prix entre les actifs de la categorie est juge faible.

`isInEModeCategory` verifie qu'un actif appartient a la categorie active de l'utilisateur avant de lui appliquer ces parametres avantageux ; en dehors de sa categorie, ou pour un utilisateur sans eMode actif, les parametres standard de la reserve s'appliquent. Un utilisateur ne peut avoir qu'une seule categorie eMode active a la fois.

[Chapitre suivant : les flash loans](12-flash-loans.md)
