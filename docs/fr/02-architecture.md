# Chapitre 2 — Architecture du depot

`contracts/protocol/pool/` contient le contrat central `Pool.sol`, point d'entree de toutes les actions utilisateur (`supply`, `borrow`, `repay`, `withdraw`, `liquidationCall`, `flashLoan`), ainsi que `PoolConfigurator.sol` qui gere les parametres de risque et `DefaultReserveInterestRateStrategy.sol` qui calcule les taux.

`contracts/protocol/libraries/logic/` porte la logique metier, decoupee par domaine : `SupplyLogic`, `BorrowLogic`, `LiquidationLogic`, `FlashLoanLogic`, `EModeLogic`, `IsolationModeLogic`, `ValidationLogic`, `ReserveLogic`, `GenericLogic`. `Pool.sol` reste volontairement mince ; il delegue l'essentiel a ces bibliotheques via `using ... for`, un choix qui contourne la limite de taille de bytecode d'un contrat Solidity.

`contracts/protocol/libraries/math/` fournit les primitives numeriques : `WadRayMath` (virgule fixe 18 et 27 decimales) et `MathUtils` (interets lineaires et composes).

`contracts/protocol/libraries/configuration/` contient `ReserveConfiguration` et `UserConfiguration`, deux bibliotheques qui compressent l'ensemble des parametres d'une reserve ou d'un utilisateur dans un seul entier 256 bits.

`contracts/protocol/tokenization/` contient les jetons emis par le protocole : `AToken` (le recu de depot), `VariableDebtToken` et `StableDebtToken` (la dette).

[Chapitre suivant : le pool central](03-le-pool-central.md)
