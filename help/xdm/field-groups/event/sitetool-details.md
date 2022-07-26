---
title: Detalhes da Sitecool Grupo de Campos do Esquema
description: Este documento fornece uma visão geral do grupo de campos de esquema Detalhes da Ferramenta da Arquitetura.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 5%

---

# [!UICONTROL Detalhes da Sitecool] grupo de campos de esquema

[!UICONTROL Detalhes da Sitecool] é um grupo de campos de esquema padrão para a variável [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único `sitetool` objeto de um esquema, que captura informações coletadas por uma ferramenta.

![Estrutura do grupo de campos](../../images/field-groups/sitetool-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `dataGatheringEvent` | Objeto | Indica se esse evento é um evento de coleta de dados junto com outros detalhes relacionados. Contém as seguintes propriedades:<ul><li>`data`: (Mapa) Contém os dados JSON coletados e enviados como parte do evento de envio de pesquisa, questionário ou pesquisa.</li><li>`isTrue`: (Booleano) Indica se esse evento é um evento de coleta de dados como questionário, pesquisa ou pesquisa.</li><li>`score`: (Número inteiro) A pontuação protegida pelo ator com base nas respostas do evento.</li></ul> |
| `actor` | String | Uma pessoa/membro que fez a ação. |
| `actorID` | String | Um identificador exclusivo para pessoa/membro que executou a ação. |
| `isKeyEvent` | Booleano | Indica se esse evento é um evento principal. |
| `name` | String | O nome da ferramenta, como chatbot, pesquisa e assim por diante. |
| `section` | String | A seção relevante da arquitetura como principal ou subtítulo. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
