# Digital Post Komponent
Github repository som dokumenterer opsætningen af den digitale post komponent.

## Projekt Arkitektur
[![](https://mermaid.ink/img/pako:eNqNU9FugjAU_ZWmT1ti9Z2HJSig20xGKG_FhwoXaYRCStmyGD9nX7IfW9E50KGxT-Xec0_OObfscFwmgC1MCIlkKHQOFnLERmieI7-sNXoti6qUIHUkD5g0Lz_ijCuNlkEkkTk2CxVPUxGvjt91s94oXmVXedDvmbLApSGioN5FDCtC0IsznSFCntqJjYK6w86YI-qK6zgDdTkxPGCa88A_0LnsTErHtBrGe4xq9f2Vp6Wqh9EO8x3vT0dXd3ssTlf2hstz5kpV5nkB-r4UFiyAGER1J_xUYQ-nG3K45mtew-OvaJDJja31DD_PaXgW45nrMVqEoU_R2PhrkT2PN3qLK73_osw-OD_sox9qb5qGgW0vvbeA9nZ36dE2MaFM66q2JpPk6IVUxgvZnl7nONlO2jDRFI9wAargIjG_x64liLDOoIAIW-aaQMqbXEc4knsD5Y0u6aeMsaVVAyPcVAnX4Ahu9BfYSnlew_4HlvkIZQ?type=png)](https://mermaid.live/edit#pako:eNqNU9FugjAU_ZWmT1ti9Z2HJSig20xGKG_FhwoXaYRCStmyGD9nX7IfW9E50KGxT-Xec0_OObfscFwmgC1MCIlkKHQOFnLERmieI7-sNXoti6qUIHUkD5g0Lz_ijCuNlkEkkTk2CxVPUxGvjt91s94oXmVXedDvmbLApSGioN5FDCtC0IsznSFCntqJjYK6w86YI-qK6zgDdTkxPGCa88A_0LnsTErHtBrGe4xq9f2Vp6Wqh9EO8x3vT0dXd3ssTlf2hstz5kpV5nkB-r4UFiyAGER1J_xUYQ-nG3K45mtew-OvaJDJja31DD_PaXgW45nrMVqEoU_R2PhrkT2PN3qLK73_osw-OD_sox9qb5qGgW0vvbeA9nZ36dE2MaFM66q2JpPk6IVUxgvZnl7nONlO2jDRFI9wAargIjG_x64liLDOoIAIW-aaQMqbXEc4knsD5Y0u6aeMsaVVAyPcVAnX4Ahu9BfYSnlew_4HlvkIZQ)

## DPK-Projekter
- [REST-Service](https://github.com/trifork/dpk-rest-service): Service som udstiller den offentlige snitflade til udsendelse af post
- [PDF-Service](https://github.com/trifork/dpk-pdf-service): Service som skaber PDF til afsending ud fra et template og data fra snitflade/dispatcher
- [Dispatcher-Service](https://github.com/trifork/dpk-docs): (Cron/Batch) Service som finder ud af hvilke breve der skal sendes og delegerer viderere til "subservices" der enten sender til digital post eller fysisk post
- [Strålfors-Dispatcher-Service](https://github.com/trifork/dpk-straalfors): Service som får skabt et PDF brev og sender det brev til Strålfors til fysisk forsendelse
- [Digital-Post-Services](https://github.com/trifork/dpk-digital-post): Repository som samler services der skal interagere med Digital Post
  - [Digital-Post-Dispatcher-Service](https://github.com/trifork/dpk-digital-post): Service som får skabt et digitalt brev og sender brevet til Digital Post til digital forsendelse
  - [Enrollment-Service](https://github.com/trifork/dpk-digital-post) - (Cron/Batch) Service som vedligholder liste af personer tilmeldt digital post
  - [Receipt-Service](https://github.com/trifork/dpk-digital-post) - (Cron/Batch) Service som indhenter kvitteringer fra Digital Post / Strålfors
- [Common-Submodule](https://github.com/trifork/dpk-common-submodule) - Github submodul med indhold som skal bruges af to eller flere services
- [Flux](https://github.com/trifork/dpk-docs) - TCS dev/test repository
- [Docker](https://github.com/trifork/dpk-docker) - Repository hosting a docker-compose setup

## Teknologi-Stak
* **Git** for source control, and **Github** as source repository
* **Github Workflow** for continuous integration
* **Java 21**, **Kotlin 1.9.22** and **Go 1.22** as programming language
* **Maven** for building the Java/Kotlin services
* **Makefile** for easy scripting of Go build and run targets
* **Docker** for containerization
* **Github Container Registry** as docker image repository
* **PostgresDB** for persistence
* **SpringBoot** for Java/Kotlin projects
* **protobuf** and **gRPC** for communication
* **Kubernetes** as the infrastructure environment (hosted at Netic)
* **kubectl** CLI for accessing the Kubernetes cluster and viewing logs

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
> [
>  {
>   "message_id": "UUID som identificerer requestet",
>   "status": "OK/Error",
>   "error_code": "Fejlkode, hvis der opstod en fejl",
>   "error_description": "Beskrivelse af fejlen, hvis der opstod en fejl"
>  }
> ]
> ```

## Database
Der arbejdes med en Postgres (Forhåbentligt) database i alle miljøer (Forhåbentligt) med følgende ER diagram:
![dpk_db.png not found!](assets/dpk_db.png "ER Diagram")

## Udviklingsprocess

## Opstart af komponent
### Docker
TODO: direkte kørsel af `docker-compose` ?
