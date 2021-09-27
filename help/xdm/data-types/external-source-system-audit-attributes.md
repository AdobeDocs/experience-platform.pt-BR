---
title: Tipo de dados de atributos de auditoria do sistema de fonte externa
description: Este documento fornece uma visão geral do tipo de dados do Modelo de dados de experiência (XDM) de atributos de auditoria do sistema de fonte externa.
source-git-commit: 8bf0c63f33ae9cbfb01d4db9e5220c6762575c5b
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 3%

---

# [!UICONTROL Tipo de dados de ] Atributos de Auditoria de Sistema de Origem Externa

>[!NOTE]
>
>Esse tipo de dados só está disponível para organizações que têm acesso à edição B2B da Plataforma de dados do cliente em tempo real.

[!UICONTROL Os ] atributos de auditoria do sistema de fonte externa são um tipo de dados padrão do Experience Data Model (XDM) que captura detalhes de auditoria sobre um sistema de fonte externa.

![](../images/data-types/external-source-system-audit-attributes.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL Origem B2B]](./b2b-source.md) | Um identificador composto para a fonte usada para auditoria. |
| `createdBy` | String | O nome do usuário que criou este registro. |
| `createdDate` | DateTime | A data de criação deste registro. |
| `externalID` | String | Identificador exclusivo externo para a origem. Esse valor é usado para ajudar a identificar e desduplicar, se necessário. |
| `lastActivityDate` | DateTime | A última data de atividade do sistema de origem. |
| `lastReferencedDate` | DateTime | A última data referenciada para o sistema de origem. |
| `lastUpdatedBy` | String | O nome da pessoa que atualizou este registro pela última vez. |
| `lastUpdatedDate` | DateTime | A última data atualizada para o sistema de origem. |
| `lastViewedDate` | DateTime | A última data exibida para o sistema de origem. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
