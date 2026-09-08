# Chapitre 12 — Les flash loans

`FlashLoanLogic.executeFlashLoan` et `executeFlashLoanSimple` permettent d'emprunter un ou plusieurs actifs sans garantie, a condition de les rembourser avec une prime avant la fin de la meme transaction.

Le mecanisme : les actifs demandes sont transferes immediatement au contrat appelant, qui doit implementer une interface de rappel (`executeOperation`). Une fois ce rappel execute, `_handleFlashLoanRepayment` verifie que le solde du pool a bien retrouve son niveau plus la prime (`FLASHLOAN_PREMIUM_TOTAL`) ; sinon toute la transaction, y compris le transfert initial, est annulee.

Une variante existe : au lieu de rembourser immediatement, l'emprunteur peut choisir de convertir le flash loan en emprunt classique ouvert (`mintUnbacked`/le flag correspondant), ce qui evite le remboursement dans la meme transaction mais cree une position de dette normale, soumise aux memes regles de collateral que n'importe quel emprunt.

La prime se partage entre les fournisseurs de liquidite de la reserve et le protocole (`FLASHLOAN_PREMIUM_TO_PROTOCOL`) : c'est une source de revenu pour le protocole independante des interets d'emprunt classiques, utile pour l'arbitrage, la liquidation en un bloc ou le refinancement de position sans capital prealable.

[Chapitre suivant : limites et perimetre](13-limites-et-perimetre.md)
