# Digital Post Komponent
Github repository som dokumenterer opsætningen af den digitale post komponent.

## Projekt Arkitektur
[![](https://mermaid.ink/img/pako:eNqNU8tuwjAQ_BXLp1bCcM-hEjQB2iIVxbk5HEyyIRaJHTmbVhXic_ol_bGaVwkUED45uzOTnZ1kRROTAvUoYyzWkcICPOKrhUJZkKmpkbyZsjIaNMZ6i8kK85nk0iKZhLEm7vRFZGWWqWS2e66b-cLKKr-qQ_ZnIMKAR4SD_VAJzBgjr_7gmTD2tGEsLNRH7LPwVV1JTHKw54zLBNcchdOtXCCCuVnW5CgxuwwcCo4_30Vm7BWwL6b-8O_9x3rQEvGP5eHl8kgE2pqiKAHvcz8WISSgqjvhh4p4ONyIL1HOZQ2P-6FBpzfSahl-GfFInCTJtcKskOmp_y4ZR9GUk65zuuG03N7oja_0_o_H0Uq5Taa93habR2G_Pxm-h9yFaPcpnrvtu4WRHLGqvV4v3blilXPFlofvs5sue5u1kgHt0BJsKVXqfpDVRiCmmEMJMfXcNYVMNgXGNNZrB5UNGv6lE-qhbaBDmyqVCL6Sbv5yV1z_Avo4CNI?type=png)](https://mermaid.live/edit#pako:eNqNU8tuwjAQ_BXLp1bCcM-hEjQB2iIVxbk5HEyyIRaJHTmbVhXic_ol_bGaVwkUED45uzOTnZ1kRROTAvUoYyzWkcICPOKrhUJZkKmpkbyZsjIaNMZ6i8kK85nk0iKZhLEm7vRFZGWWqWS2e66b-cLKKr-qQ_ZnIMKAR4SD_VAJzBgjr_7gmTD2tGEsLNRH7LPwVV1JTHKw54zLBNcchdOtXCCCuVnW5CgxuwwcCo4_30Vm7BWwL6b-8O_9x3rQEvGP5eHl8kgE2pqiKAHvcz8WISSgqjvhh4p4ONyIL1HOZQ2P-6FBpzfSahl-GfFInCTJtcKskOmp_y4ZR9GUk65zuuG03N7oja_0_o_H0Uq5Taa93habR2G_Pxm-h9yFaPcpnrvtu4WRHLGqvV4v3blilXPFlofvs5sue5u1kgHt0BJsKVXqfpDVRiCmmEMJMfXcNYVMNgXGNNZrB5UNGv6lE-qhbaBDmyqVCL6Sbv5yV1z_Avo4CNI)

## DPK-Projekter
- [REST-Service](https://github.com/trifork/dpk-docs): Service som udstiller den offentlige snitflade til udsendelse af post
- [PDF-Service](https://github.com/trifork/dpk-docs): Service som skaber PDF til afsending ud fra et template og data fra snitflade/dispatcher
- [Dispatcher-Service](https://github.com/trifork/dpk-docs): (Cron/Batch) Service som delegerer viderere til "subservices" der enten sender til digital post eller fysisk post
- [Eboks-Dispatcher-Service](https://github.com/trifork/dpk-docs): Service som sender et brev til eboks/digital post til digital forsendelse
- [Strålfors-Dispatcher-Service](https://github.com/trifork/dpk-docs): Service som sender et brev til Strålfors til fysisk forsendelse
- [Enrollment-Service](https://github.com/trifork/dpk-docs) - (Cron/Batch) Service som vedligholder en liste af personer tilmeldt digital post
- [Receipt-Service](https://github.com/trifork/dpk-docs) - (Cron/Batch) Service som indhenter kvitteringer fra Digital Post / Strålfors
- [Common-Submodule](https://github.com/trifork/dpk-docs) - Github submodul med indhold som skal bruges af to eller flere services
- [Flux](https://github.com/trifork/dpk-docs) - TCS dev/test repository

## Udviklingsprocess

## Database
Der arbejdes med en Postgres (Forhåbentligt) database i alle miljøer (Forhåbentligt) med følgende ER diagram:
![dpk_db.png not found!](assets/dpk_db.png "ER Diagram")

## Opstart af komponent
### Docker
TODO: direkte kørsel af `docker-compose`
