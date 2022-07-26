---
title: ERD do Modelo de Dados do Setor de Saúde
description: Exibir um diagrama de relacionamento de entidade (ERD) que descreve um modelo de dados padronizado para o setor de saúde. Esse modelo de dados é compatível com o Experience Data Model (XDM) para uso no Adobe Experience Platform.
source-git-commit: 721059a87347e371228d00edeac141afa894af47
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 1%

---

# [!UICONTROL Saúde] ERD do modelo de dados do setor

O diagrama de relacionamento de entidade (ERD) a seguir representa um modelo de dados padronizado para o setor de saúde. O ERD é intencionalmente apresentado de forma desnormalizada e considerando como os dados são armazenados no Adobe Experience Platform.

>[!NOTE]
>
>O ERD conforme descrito é uma recomendação sobre como você deve modelar seus dados para este caso de uso do setor. Para usar esse modelo de dados no Platform, você deve construir os esquemas recomendados e seus relacionamentos sozinho. Consulte os guias sobre gerenciamento [esquemas](../../ui/resources/schemas.md) e [relações](../../tutorials/relationship-ui.md) na interface do usuário do para obter mais informações.

Use a seguinte legenda para interpretar este ERD:

* Cada entidade mostrada no é baseada em um [Classe do Experience Data Model (XDM)](../composition.md#class).
* Para uma determinada entidade, cada linha marcada em **bold** representa um grupo de campos ou um tipo de dados, com os campos relevantes fornecidos listados abaixo em texto não em negrito.
* Os campos mais importantes para uma determinada entidade são destacados em vermelho.
* Todas as propriedades que podem ser usadas para identificar clientes individuais são marcadas como &quot;identidade&quot;, com uma dessas propriedades marcadas como &quot;identidade primária&quot;.
* Os relacionamentos de entidade são marcados como não dependentes, já que os eventos baseados em cookies geralmente não podem determinar a pessoa ou o indivíduo que fez a transação.

![Imagem que mostra o diagrama de relacionamento da entidade para o modelo de dados do setor de saúde](../../images/industries/healthcare.png)

>[!NOTE]
>
>Cada entidade inclui um campo &quot;_ID&quot;, que representa o identificador de sequência exclusivo (`_id`) para o registro ou evento em questão. Este campo é usado para rastrear a exclusividade do registro ou evento individual, evitar duplicação de dados e buscar esses dados em serviços downstream. Em alguns casos, `_id` pode ser um [Identificador universal exclusivo (UUID)](https://tools.ietf.org/html/rfc4122) ou [Identificador único global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>É importante distinguir que **este campo não representa uma identidade relacionada a uma pessoa**, mas o registro dos dados em si. Os dados de identidade relativos a uma pessoa, evento ou entidade empresarial devem ser relegados para [campos de identidade](../composition.md#identity) fornecido por grupos de campos compatíveis.

## [!UICONTROL Saúde] casos de uso

A tabela a seguir descreve as classes recomendadas e os grupos de campos de esquema para vários casos comuns de uso de assistência médica.

| Caso de uso | Classes e grupos de campos recomendados |
| --- | --- |
| Melhorar a aquisição digital e a experiência entre os consumidores que compram seguros. São exemplos: <ul><li>Quando as pessoas acessam uma página contendo informações gerais (como planos, nomes/níveis de plano, medicamentos, programas de bem-estar, etc.), compreendem seu comportamento e o que estão procurando para enviar emails promocionais ou direcioná-los em plataformas de terceiros com anúncios.</li><li>Quando as pessoas procuram informação sobre saúde cardíaca e vacinas, enviam-lhes informação sobre saúde cardíaca relacionada com a vacina para criar conhecimento sobre a marca ou pedem-lhes que programem vacinas.</li></ul> | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do Membro da Saúde]](../../field-groups/profile/healthcare-member-details.md)</li><li>Campo(s) de relacionamento estabelecido(s) entre `planID` atributos e esquemas que usam o [!UICONTROL Plano] classe .</li></ul></li><li>**[[!UICONTROL Pagador]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plano]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalhes do Plano de Saúde]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL ExperiênciaEvento XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes do aplicativo]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Detalhes da Sitecool]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  Detalhes de marketing da campanha]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| Aumente a aquisição digital de pacientes por meio de anúncios direcionados com base no comportamento online anterior e em dados de saúde. | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do Membro da Saúde]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Provedor]](../../classes/provider.md)**:<ul><li>[[!UICONTROL Provedor de saúde]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL ExperiênciaEvento XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes da Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalhes da publicidade]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Melhore a inscrição e a criação de contas em planos de saúde, rastreando o marketing de seguros por meio de diferentes canais, para entender como um cliente descobriu sobre uma empresa de seguros. | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do Membro da Saúde]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Pagador]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plano]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalhes do Plano de Saúde]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL ExperiênciaEvento XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes da Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalhes da publicidade]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Evite falhas na cobertura do seguro médico. | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do Membro da Saúde]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Plano]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalhes do Plano de Saúde]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| Promover informações sobre drogas para provedores usando anúncios de DTC (direct-to-customer). | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do Membro da Saúde]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Medicação]](../../classes/medication.md)**:<ul><li>[[!UICONTROL Medicamentos para a saúde]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL ExperiênciaEvento XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes da Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalhes da publicidade]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
