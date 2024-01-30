# Digital Post Komponent
Github repository som dokumenterer opsætningen af den digitale post komponent.

## Projekt Arkitektur
[![](https://mermaid.ink/img/pako:eNqNU8tugzAQ_BXLp1aKkzuHSknJo22kIszN5ODAEqyAQWZpVUX5nH5Jf6zOq5CURPHJ7M6MZnbNhkZFDNShjLFQBwozcIirVgplRryiQvJW5GWhQWOo95gkKz6jVBokcz_UxJ6hCIxMEhUtDt9VvVwZWaZXdcjxjIQ_5gHhYD5UBAvGyKs7eiaMPe0YKwNVg30WrqpKiVEK5pLRTbDNqe_t5cbizEqjtOjGTwTHn-8sKUzVDXaF507-bDT1cUvEbcqT7vJUjLUpsiwHvG8IM-FDBKq8E36qiIfTjbgS5VJW8Hg0DTq-sbRW4JcpD86nyLXCJJPxef4-mQWBx0nfJt1xWmlv9GZXev_tcTRS7jfTHm-LzQN_OJxP3n1ul2iOW7xMO7QDIyliWTmDQXxIxUqbiq1Pz7Qfrwe7sZIR7dEcTC5VbP-TzU4gpJhCDiF17DWGRNYZhjTUWwuVNRb8S0fUQVNDj9ZlLBFcJa3__FDc_gJ5yAti?type=png)](https://mermaid.live/edit#pako:eNqNU8tugzAQ_BXLp1aKkzuHSknJo22kIszN5ODAEqyAQWZpVUX5nH5Jf6zOq5CURPHJ7M6MZnbNhkZFDNShjLFQBwozcIirVgplRryiQvJW5GWhQWOo95gkKz6jVBokcz_UxJ6hCIxMEhUtDt9VvVwZWaZXdcjxjIQ_5gHhYD5UBAvGyKs7eiaMPe0YKwNVg30WrqpKiVEK5pLRTbDNqe_t5cbizEqjtOjGTwTHn-8sKUzVDXaF507-bDT1cUvEbcqT7vJUjLUpsiwHvG8IM-FDBKq8E36qiIfTjbgS5VJW8Hg0DTq-sbRW4JcpD86nyLXCJJPxef4-mQWBx0nfJt1xWmlv9GZXev_tcTRS7jfTHm-LzQN_OJxP3n1ul2iOW7xMO7QDIyliWTmDQXxIxUqbiq1Pz7Qfrwe7sZIR7dEcTC5VbP-TzU4gpJhCDiF17DWGRNYZhjTUWwuVNRb8S0fUQVNDj9ZlLBFcJa3__FDc_gJ5yAti)

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
