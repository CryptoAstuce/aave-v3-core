# Chapitre 1 — Presentation d'Aave v3

Aave est un protocole de pret decentralise et non custodial : les preteurs deposent des actifs dans des reserves communes pour toucher un interet, les emprunteurs empruntent contre une garantie surcollateralisee, en permanence, ou de facon non collateralisee pendant un seul bloc via un flash loan.

Ce depot, `aave-v3-core`, contient le coeur du protocole Aave version 3 : le contrat `Pool`, les jetons `aToken` et jetons de dette, les bibliotheques de calcul d'interet et de risque. Le code est en Solidity.

L'avertissement en tete du `README` de ce depot le signale comme archive : la suite active du developpement se trouve desormais dans `aave-v3-origin`. Ce parcours l'utilise malgre tout parce que c'est la version historique la plus largement auditee et documentee de la V3, et que son code n'a pas change depuis.

Ce parcours s'appuie sur `contracts/protocol/pool/Pool.sol`, les bibliotheques de `contracts/protocol/libraries/`, et les jetons de `contracts/protocol/tokenization/`.

Rien n'a ete installe, compile ni execute pour ecrire ces chapitres.

[Chapitre suivant : architecture du depot](02-architecture.md)
