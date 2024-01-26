# Digitale Post Komponent
Github repository som dokumenterer opsætningen af den digitale post komponent.

## Projekt Arkitektur
[![](https://mermaid.ink/img/pako:eNqFktFugjAYhV-l6dWWyLwniwkO0GUmM-Bd8aLSH2mElpSfLYvxcfYke7GVoaLOaK_K4fvbc066pakWQF2aFfozzblBMosSRezy2MLwLJPpsvuum9Xa8ConvlxL5AWZ6xrJmy4rrUBhB7VrzAIlKi0VkhjMh0xh6Tijll4bqHvuhfmyrjimOZgj-XwdtWrAgpXe1KQfWp4DIYvx57vItLkB-Wzuh8fb-n8Ta9rooigB73iZsghSkNWddAeFPRx2xOfIV7yGx_29oMSNavuj_NdJvGBntcdKYlZwcRohcJ5svpY9iXVFm15o_23EaDj_K7KfCtupeBF53ix8j2LbtdmXfZnGI45DcsSqdodD0bl2Kuva2Rwey5PYDC01ImM6oCWYkkthH-G2PSChmEMJCXXtVkDGmwITmqidRXmDOv5SKXXRNDCgTSU4gi-59V124u4XXBriaw?type=png)](https://mermaid.live/edit#pako:eNqFktFugjAYhV-l6dWWyLwniwkO0GUmM-Bd8aLSH2mElpSfLYvxcfYke7GVoaLOaK_K4fvbc066pakWQF2aFfozzblBMosSRezy2MLwLJPpsvuum9Xa8ConvlxL5AWZ6xrJmy4rrUBhB7VrzAIlKi0VkhjMh0xh6Tijll4bqHvuhfmyrjimOZgj-XwdtWrAgpXe1KQfWp4DIYvx57vItLkB-Wzuh8fb-n8Ta9rooigB73iZsghSkNWddAeFPRx2xOfIV7yGx_29oMSNavuj_NdJvGBntcdKYlZwcRohcJ5svpY9iXVFm15o_23EaDj_K7KfCtupeBF53ix8j2LbtdmXfZnGI45DcsSqdodD0bl2Kuva2Rwey5PYDC01ImM6oCWYkkthH-G2PSChmEMJCXXtVkDGmwITmqidRXmDOv5SKXXRNDCgTSU4gi-59V124u4XXBriaw)

## DPK-Projekter
- [Endpoint-Service](https://github.com/trifork/dpk-docs): Service som udstiller den offentlige snitflade til udsendelse af post
- [PDF-Service](https://github.com/trifork/dpk-docs): Service som skaber PDF til afsending ud fra et template og data fra snitflade/dispatcher
- [Dispatcher-Service](https://github.com/trifork/dpk-docs): (Cron/Batch) Service som delegerer viderere til "subservices" der enten sender til digital post eller fysisk post
- [Eboks-Dispatcher-Service](https://github.com/trifork/dpk-docs): Service som sender et brev til eboks/digital post til digital forsendelse
- [Strålfors-Dispatcher-Service](https://github.com/trifork/dpk-docs): Service som sender et brev til Strålfors til fysisk forsendelse
- [Enrollment-Service](https://github.com/trifork/dpk-docs) - (Cron/Batch) Service som vedligholder en liste af personer tilmeldt digital post
- [Receipt-Service](https://github.com/trifork/dpk-docs) - (Cron/Batch) Service som indhenter kvitteringer fra Digital Post / Strålfors

## Udviklingsprocess

## Opstart af komponent
### Docker
TODO: direkte kørsel af `docker-compose`
