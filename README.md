# Digital Post Komponent
Github repository som dokumenterer opsætningen af den digitale post komponent.

## Projekt Arkitektur
[![](https://mermaid.ink/img/pako:eNqFktFugjAYhV-l6dWWiN6TxQQH6DKTGepd8aLSH2kESsrPlsX4OHuSvdjKUFFnXK_K4fvbc066o4mWQF2a5vojyYRBMo_iktjl8aURaaqSVfddN-uNEVVGfLVRKHKy0DWSV11UuoQSO6hdEx4FbEkYmHeVwMpxxi25MVD3zDP3VV0JTDIwJ_LpNmrVgAdrva1JP7S6BELO8PsrT7W5A_l84Yen2_p_Ux6URud5AfiPlxmPIAFV4f10R4U_HHfEFyjWoobHw71Qyju19kf5L1O25BeVs1Jhmgt5HiFwhjZfy57FuqHNrrS_NhgaIX6L7KfCdootI8-bh28Rs12bQ9nXaTziOCRDrGp3NJKda6eyrp3t8aEM5XZkqTGZ0AEtwBRCSfsAd-0BMcUMCoipa7cSUtHkGNO43FtUNKjZZ5lQF00DA9pUUiD4SljfRSfufwDwReBo?type=png)](https://mermaid.live/edit#pako:eNqFktFugjAYhV-l6dWWiN6TxQQH6DKTGepd8aLSH2kESsrPlsX4OHuSvdjKUFFnXK_K4fvbc066o4mWQF2a5vojyYRBMo_iktjl8aURaaqSVfddN-uNEVVGfLVRKHKy0DWSV11UuoQSO6hdEx4FbEkYmHeVwMpxxi25MVD3zDP3VV0JTDIwJ_LpNmrVgAdrva1JP7S6BELO8PsrT7W5A_l84Yen2_p_Ux6URud5AfiPlxmPIAFV4f10R4U_HHfEFyjWoobHw71Qyju19kf5L1O25BeVs1Jhmgt5HiFwhjZfy57FuqHNrrS_NhgaIX6L7KfCdootI8-bh28Rs12bQ9nXaTziOCRDrGp3NJKda6eyrp3t8aEM5XZkqTGZ0AEtwBRCSfsAd-0BMcUMCoipa7cSUtHkGNO43FtUNKjZZ5lQF00DA9pUUiD4SljfRSfufwDwReBo)

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

## Opstart af komponent
### Docker
TODO: direkte kørsel af `docker-compose`
