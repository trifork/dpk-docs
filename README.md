# Digital Post Komponent
Github repository som dokumenterer opsætningen af den digitale post komponent.

## Projekt Arkitektur
[![](https://mermaid.ink/img/pako:eNqNU8tOwzAQ_BXLJ5Dq9p4DUkv6ACpRxbk5PSzJprHqOJGzASHE5_Al_BhuoTSFtqpPzu7saGbWeeNplSEPuBAisbEmgwEL9UoTGLaoGmIPVVlXFi0ldovJTfWSFuCIzaPEMn-GKnaQ5zpdfn837dPKQV2c5GE_Z6SisYyZRPesU1wKwe7D0S0T4mYzsXLY7LG3KtRNDZQW6P5OHB_wzWm02NKN1YGUPdPyOH6iJLnPD5NXrjmODtUinPzq2NfHHZZwX54cL0_V2LrKmBLpshRmKsIUdX0hfFdRV7sbC4HgCRq8_hGNNjuztY7hu6mMD2OUVlNuIDv032ezOF5I1vdONzMdt2d6sxO9__L8ZgC2m-nG25mWcTQcziePkexs8a_boQ-MFUR1EwwG2bcrUXtXYr17p_1sPdjEyka8x0t0JejM_yhvG4KEU4ElJjzw1wxzaA0lPLHvHgotVfLVpjwg12KPt3UGhKEGr7_kQQ6mwfcv6foMHw?type=png)](https://mermaid.live/edit#pako:eNqNU8tOwzAQ_BXLJ5Dq9p4DUkv6ACpRxbk5PSzJprHqOJGzASHE5_Al_BhuoTSFtqpPzu7saGbWeeNplSEPuBAisbEmgwEL9UoTGLaoGmIPVVlXFi0ldovJTfWSFuCIzaPEMn-GKnaQ5zpdfn837dPKQV2c5GE_Z6SisYyZRPesU1wKwe7D0S0T4mYzsXLY7LG3KtRNDZQW6P5OHB_wzWm02NKN1YGUPdPyOH6iJLnPD5NXrjmODtUinPzq2NfHHZZwX54cL0_V2LrKmBLpshRmKsIUdX0hfFdRV7sbC4HgCRq8_hGNNjuztY7hu6mMD2OUVlNuIDv032ezOF5I1vdONzMdt2d6sxO9__L8ZgC2m-nG25mWcTQcziePkexs8a_boQ-MFUR1EwwG2bcrUXtXYr17p_1sPdjEyka8x0t0JejM_yhvG4KEU4ElJjzw1wxzaA0lPLHvHgotVfLVpjwg12KPt3UGhKEGr7_kQQ6mwfcv6foMHw)

## DPK-Projekter
- [REST-Service](https://github.com/trifork/dpk-docs): Service som udstiller den offentlige snitflade til udsendelse af post
  - Go Service?
- [PDF-Service](https://github.com/trifork/dpk-docs): Service som skaber PDF til afsending ud fra et template og data fra snitflade/dispatcher
  - Java/Kotlin Service?
- [Dispatcher-Service](https://github.com/trifork/dpk-docs): (Cron/Batch) Service som delegerer viderere til "subservices" der enten sender til digital post eller fysisk post
  - Java/Kotlin Service?
- [Strålfors-Dispatcher-Service](https://github.com/trifork/dpk-docs): Service som får skabt et PDF brev og sender det brev til Strålfors til fysisk forsendelse
  - Java Service 
- [Digital-Post-ServiceS](https://github.com/trifork/dpk-docs): Service som får skabt et digitalt brev og sender brevet til eboks/digital post til digital forsendelse
  - [Digital-Post-Dispatcher-Service](https://github.com/trifork/dpk-docs): Service som får skabt et digitalt brev og sender brevet til Digital Post til digital forsendelse
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
> | Query Parameter             | Beskrivelse                                                                                                                               | Obligatorisk |
> |-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|:------------:|
> | recipientList               | Liste af modtagere                                                                                                                        | X            |
> | templateDigital             | PDF template til digital forsendelse                                                                                                      | X            |
> | templatePhysical            | PDF template til fysisk forsendelse, ved udeladelse sendes der kun digital post                                                           |              |
> | templateSubstitutionValues  | Key-Value mapning til substituering af generiske værdier i et PDF template                                                                |              |
> | sendDate                    | (Fremtidig) dato hvor servicen skal begynde at sende post fra, ved udeladelse begynder servicen at sende snarest muligt                   |              |
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
> *Hvoraf `uuid` er messageId for den enkelte forsendelse. `identifierSource` kan udelades, med antagelse om at der er tale om CPR. `substitutionValues` kan udelades.*
>
> Kaldet kvitteres med følgende json struktur
> ```json
> {
>  "request_id": "UUID som identificerer requestet",
>  "status": "OK/Error",
>  "error_code": "Fejlkode, hvis der opstod en fejl",
>  "error_description": "Beskrivelse af fejlen, hvis der opstod en fejl"
> }
> ```

## Database
Der arbejdes med en Postgres (Forhåbentligt) database i alle miljøer (Forhåbentligt) med følgende ER diagram:
![dpk_db.png not found!](assets/dpk_db.png "ER Diagram")

## Udviklingsprocess

## Opstart af komponent
### Docker
TODO: direkte kørsel af `docker-compose` ?
