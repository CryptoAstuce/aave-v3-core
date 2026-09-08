# Chapitre 8 — La configuration bitmap des reserves

`ReserveConfiguration.sol` stocke tous les parametres de risque d'une reserve (LTV, seuil de liquidation, prime de liquidation, decimales, actif actif/gele/en pause, plafonds d'emprunt et de depot, categorie eMode, plafond de dette en isolation...) dans un seul `uint256`, decoupe en tranches de bits contigues.

Chaque parametre a un masque (`LTV_MASK`, `LIQUIDATION_THRESHOLD_MASK`, etc.) et une position de depart en bits (`LIQUIDATION_THRESHOLD_START_BIT_POSITION = 16`, etc.). Lire un champ revient a appliquer le masque inverse puis a decaler ; ecrire revient a effacer les bits concernes avec le masque puis a inserer la nouvelle valeur decalee.

Cette compression n'est pas cosmetique : elle fait tenir toute la configuration d'une reserve dans un seul slot de stockage (`SSTORE`/`SLOAD`), ce qui reduit fortement le cout en gaz de chaque lecture ou ecriture de configuration comparee a des champs separes. `UserConfiguration.sol` applique la meme idee au niveau utilisateur : deux bits par reserve indiquent si elle sert de garantie et si elle est empruntee.

Cette technique de bitmap packe est courante dans les protocoles DeFi a forte activite on-chain ; elle a pour contrepartie un code de bas niveau, difficile a lire sans les constantes de position, que ce depot documente abondamment en commentaires.

[Chapitre suivant : le facteur de sante et le risque utilisateur](09-facteur-de-sante.md)
