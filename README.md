# Digital Post Komponent
Github repository som dokumenterer opsætningen af den digitale post komponent.

## Projekt Arkitektur
[![](https://mermaid.ink/img/pako:eNqNU8tuwjAQ_BXLp1bCcM-hEjQB2iIVxbk5HEyyIRaJHTmbVhXic_ol_bGaVwkUED45uzOTnZ1kRROTAvUoYyzWkcICPOKrhUJZkKmpkbyZsjIaNMZ6i8kK85nk0iKZhLEm7vRFZGWWqWS2e66b-cLKKr-qQ_ZnIMKAR4SD_VAJzBgjr_7gmTD2tGEsLNRH7LPwVV1JTHKw54zLBNcchdOtXCCCuVnW5CgxuwwcCo4_30Vm7BWwL6b-8O_9x3rQEvGP5eHl8kgE2pqiKAHvcz8WISSgqjvhh4p4ONyIL1HOZQ2P-6FBpzfSahl-GfFInCTJtcKskOmp_y4ZR9GUk65zuuG03N7oja_0_o_H0Uq5Taa93habR2G_Pxm-h9yFaPcpnrvtu4WRHLGqvV4v3blilXPFlofvs5sue5u1kgHt0BJsKVXqfpDVRiCmmEMJMfXcNYVMNgXGNNZrB5UNGv6lE-qhbaBDmyqVCL6Sbv5yV1z_Avo4CNI?type=png)](https://mermaid.live/edit#pako:eNqNU8tuwjAQ_BXLp1bCcM-hEjQB2iIVxbk5HEyyIRaJHTmbVhXic_ol_bGaVwkUED45uzOTnZ1kRROTAvUoYyzWkcICPOKrhUJZkKmpkbyZsjIaNMZ6i8kK85nk0iKZhLEm7vRFZGWWqWS2e66b-cLKKr-qQ_ZnIMKAR4SD_VAJzBgjr_7gmTD2tGEsLNRH7LPwVV1JTHKw54zLBNcchdOtXCCCuVnW5CgxuwwcCo4_30Vm7BWwL6b-8O_9x3rQEvGP5eHl8kgE2pqiKAHvcz8WISSgqjvhh4p4ONyIL1HOZQ2P-6FBpzfSahl-GfFInCTJtcKskOmp_y4ZR9GUk65zuuG03N7oja_0_o_H0Uq5Taa93habR2G_Pxm-h9yFaPcpnrvtu4WRHLGqvV4v3blilXPFlofvs5sue5u1kgHt0BJsKVXqfpDVRiCmmEMJMfXcNYVMNgXGNNZrB5UNGv6lE-qhbaBDmyqVCL6Sbv5yV1z_Avo4CNI)

## DPK-Projekter
- [REST-Service](https://github.com/trifork/dpk-docs): Service som udstiller den offentlige snitflade til udsendelse af post
  - Go Service?
- [PDF-Service](https://github.com/trifork/dpk-docs): Service som skaber PDF til afsending ud fra et template og data fra snitflade/dispatcher
  - Java/Kotlin Service?
- [Dispatcher-Service](https://github.com/trifork/dpk-docs): (Cron/Batch) Service som delegerer viderere til "subservices" der enten sender til digital post eller fysisk post
  - Java/Kotlin Service? 
- [Eboks-Dispatcher-Service](https://github.com/trifork/dpk-docs): Service som får skabt et digitalt brev og sender brevet til eboks/digital post til digital forsendelse
  - Java Service 
- [Strålfors-Dispatcher-Service](https://github.com/trifork/dpk-docs): Service som får skabt et PDF brev og sender det brev til Strålfors til fysisk forsendelse
  - Java Service
- [Enrollment-Service](https://github.com/trifork/dpk-docs) - (Cron/Batch) Service som vedligholder liste af personer tilmeldt digital post
  - Java Service: Kopi/opgradering af tilsvarende [Bulk-Notify service](https://github.com/trifork/bulk-notification/tree/master/poll-eboks-enrollment-lists)
- [Receipt-Service](https://github.com/trifork/dpk-docs) - (Cron/Batch) Service som indhenter kvitteringer fra Digital Post / Strålfors
  - Java Service: Kopi/opgradering af tilsvarende [Bulk-Notify service](https://github.com/trifork/bulk-notification/tree/master/poll-eboks-acknowledgements)
- [Common-Submodule](https://github.com/trifork/dpk-docs) - Github submodul med indhold som skal bruges af to eller flere services
  - Protobuf, SQL
- [Flux](https://github.com/trifork/dpk-docs) - TCS dev/test repository

## Snitflade
Følgende snitflade funktioner kan kaldes hvoraf data forventes at være i json format:

> # /api/v1/sendPDF
>
> *Påbegynder udsendelse af en PDF til de angivne modtagere*
> | Query Parameter             | Beskrivelse                                                                         | Obligatorisk |
> |-----------------------------|-------------------------------------------------------------------------------------|:------------:|
> | recipientList               | Liste af modtagere                                                                  | X            |
> | templateDigital             | PDF template til digital forsendelse                                                | X            |
> | templatePhysical            | PDF template til fysisk forsendelse, ved udeladelse kan der kun sendes digital post |              |
> | templateSubstitutionValues  | Key-Value mapning til substituering af generiske værdier i et PDF template          |              |
>
> *Eksempel på Json:*
> ```json
> {
>  "recipientList": [
>   {
>    "uuid": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
>    "identifier": "1111111118",
>    "identifierSource": "CPR",
>    "name": "Jens Jensen",
>    "address": "Jensenvej 11, 8000",
>    "city": "Testby",
>    "substitutionValues": {
>     "age": "31"    
>    }
>   }
>  ],
>  "templateDigital": "Genoplivning_paamindelse_2024q4_digital",
>  "templatePhysical": "Genoplivning_paamindelse_2024q4_fysisk",
>  "templateSubstitutionValues": {
>   "date": "2023-01-29"    
>  } 
> }
> ```
> *Hvoraf uuid er messageId for den enkelte forsendelse*

## Database
Der arbejdes med en Postgres (Forhåbentligt) database i alle miljøer (Forhåbentligt) med følgende ER diagram:
![dpk_db.png not found!](assets/dpk_db.png "ER Diagram")

## Udviklingsprocess

## Opstart af komponent
### Docker
TODO: direkte kørsel af `docker-compose` ?
