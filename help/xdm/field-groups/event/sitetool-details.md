---
title: Grupo De Campos De Esquema De Detalhes Do Sitetool
description: Saiba mais sobre o grupo de campos de esquema Detalhes da ferramenta de site.
exl-id: 472c0a3f-efda-49af-9490-f2de90b348c0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 5%

---

# [!UICONTROL Detalhes de Sitetool] grupo de campos de esquema

[!UICONTROL Detalhes de Sitetool] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único objeto `sitetool` a um esquema, que captura informações coletadas por uma ferramenta de site.

![Estrutura do grupo de campos](../../images/field-groups/sitetool-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `dataGatheringEvent` | Objeto | Indica se esse evento é um evento de coleta de dados juntamente com outros detalhes relacionados. Contém as seguintes propriedades:<ul><li>`data`: (Mapa) Contém os dados JSON coletados e enviados como parte de um questionário, pesquisa ou evento de envio de enquete.</li><li>`isTrue`: (Booleano) Indica se este evento é um evento de coleta de dados como questionário, pesquisa ou enquete.</li><li>`score`: (Número inteiro) a pontuação garantida pelo ator com base nas respostas do evento.</li></ul> |
| `actor` | String | Uma pessoa/membro que executou a ação. |
| `actorID` | String | Um identificador exclusivo da pessoa/membro que executou a ação. |
| `isKeyEvent` | Booleano | Indica se este evento é um evento chave. |
| `name` | String | O nome da ferramenta de site, como chatbot, pesquisa e assim por diante. |
| `section` | String | A seção relevante da ferramenta de site como main ou sub. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
