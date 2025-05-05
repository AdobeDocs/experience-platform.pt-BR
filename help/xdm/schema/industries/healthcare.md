---
title: ERD do modelo de dados do setor de saúde
description: Exibir um diagrama de relacionamento de entidade (ERD) que descreva um modelo de dados padronizado para o setor de saúde. Esse modelo de dados é compatível com o Experience Data Model (XDM) para uso no Adobe Experience Platform.
exl-id: ebcf97ec-f5a4-46e5-b1ad-c80d55aa2c6e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# ERD do modelo de dados do setor de [!UICONTROL Saúde]

O diagrama de relacionamento de entidade (ERD) a seguir representa um modelo de dados padronizado para o setor de saúde. O ERD é intencionalmente apresentado de forma desnormalizada e considerando a forma como os dados são armazenados no Adobe Experience Platform.

>[!NOTE]
>
>O ERD, conforme descrito, é uma recomendação sobre como você deve modelar seus dados para esse caso de uso do setor. Para usar esse modelo de dados no Experience Platform, você deve criar os esquemas recomendados e seus relacionamentos sozinho. Consulte os guias sobre gerenciamento de [esquemas](../../ui/resources/schemas.md) e [relações](../../tutorials/relationship-ui.md) na interface do usuário para obter mais informações.

Use a seguinte legenda para interpretar este ERD:

* Cada entidade mostrada no é baseada em uma [classe do Experience Data Model (XDM)](../composition.md#class) subjacente.
* Os campos recuados em um campo pai representam um campo filho, ou subcampo, que pertence ao grupo de campos do pai.
* Os campos mais importantes para uma determinada entidade são destacados em vermelho.
* Todas as propriedades que poderiam ser usadas para identificar clientes individuais são marcadas como &quot;identidade&quot;, com uma dessas propriedades marcada como &quot;identidade principal&quot;.
* Os relacionamentos de entidade são marcados como não dependentes, já que os eventos baseados em cookies geralmente não podem determinar a pessoa ou indivíduo que fez a transação.

![Um exemplo de ERD para um modelo de dados do setor de saúde](../../images/industries/healthcare.png)

>[!NOTE]
>
>Cada entidade inclui um campo &quot;_ID&quot;, que representa o atributo de identificador de sequência de caracteres exclusivo (`_id`) para o registro ou evento em questão. Este campo é usado para rastrear a exclusividade do registro ou evento individual, evitar a duplicação de dados e pesquisar esses dados nos serviços downstream. Em alguns casos, `_id` pode ser um [Identificador exclusivo universal (UUID)](https://tools.ietf.org/html/rfc4122) ou [Identificador exclusivo global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>É importante distinguir que **este campo não representa uma identidade relacionada a uma pessoa individual**, mas o próprio registro de dados. Os dados de identidade relacionados a uma pessoa, evento ou entidade de negócios devem ser relegados a [campos de identidade](../composition.md#identity) fornecidos por grupos de campos compatíveis.

## Casos de uso de [!UICONTROL Assistência médica]

A tabela a seguir descreve as classes recomendadas e os grupos de campos de esquema para vários casos de uso comuns do sistema de saúde.

| Caso de uso | Classes e grupos de campos recomendados |
| --- | --- |
| Melhore a aquisição digital e a experiência entre os consumidores que compram seguros. São exemplos: <ul><li>Quando as pessoas acessam uma página contendo informações gerais (como planos, nomes/níveis de planos, medicaid, programas de bem-estar e assim por diante), entendem seu comportamento e o que estão procurando para enviar emails promocionais ou direcioná-los em plataformas de terceiros com anúncios.</li><li>Quando as pessoas buscam informações sobre a saúde cardíaca e a vacina, envie a elas informações relacionadas à vacina sobre a saúde cardíaca para criar uma percepção da marca ou peça para agendar vacinas.</li></ul> | <ul><li>**[[!UICONTROL Perfil Individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do membro da área de saúde]](../../field-groups/profile/healthcare-member-details.md)</li><li>Campos de relacionamento estabelecidos entre `planID` atributos e esquemas que usam a classe [!UICONTROL Plan].</li></ul></li><li>**[[!UICONTROL Pagador]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plano]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalhes do plano de saúde]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes do aplicativo]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Detalhes De Sitetool]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL &#x200B; Detalhes de marketing da campanha]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| Aumentar a aquisição digital de pacientes por meio de anúncios direcionados com base no comportamento online anterior e nos dados de saúde. | <ul><li>**[[!UICONTROL Perfil Individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do membro da área de saúde]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Provedor]](../../classes/provider.md)**:<ul><li>[[!UICONTROL Prestador de serviços de saúde]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes da Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalhes do Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Melhore a inscrição e a criação de contas em planos de saúde rastreando o marketing de seguros por diferentes canais, a fim de entender como um cliente descobriu sobre uma empresa de seguros. | <ul><li>**[[!UICONTROL Perfil Individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do membro da área de saúde]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Pagador]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plano]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalhes do plano de saúde]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes da Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalhes do Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Evite lapsos na cobertura do seguro médico. | <ul><li>**[[!UICONTROL Perfil Individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do membro da área de saúde]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Plano]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalhes do plano de saúde]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| Promover informações sobre medicamentos para fornecedores usando anúncios diretos ao cliente (DTC). | <ul><li>**[[!UICONTROL Perfil Individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do membro da área de saúde]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Medicação]](../../classes/medication.md)**:<ul><li>[[!UICONTROL Medicamentos para a área de saúde]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes da Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalhes do Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |

