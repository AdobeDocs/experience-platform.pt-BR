---
title: ERD do modelo de dados do setor de saúde
description: Exibir um diagrama de relacionamento de entidade (ERD) que descreva um modelo de dados padronizado para o setor de saúde. Esse modelo de dados é compatível com o Experience Data Model (XDM) para uso no Adobe Experience Platform.
exl-id: ebcf97ec-f5a4-46e5-b1ad-c80d55aa2c6e
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 1%

---

# [!UICONTROL Assistência médica] ERD do modelo de dados do setor

O diagrama de relacionamento de entidade (ERD) a seguir representa um modelo de dados padronizado para o setor de saúde. O ERD é intencionalmente apresentado de forma desnormalizada e considerando a forma como os dados são armazenados no Adobe Experience Platform.

>[!NOTE]
>
>O ERD, conforme descrito, é uma recomendação sobre como você deve modelar seus dados para esse caso de uso do setor. Para usar esse modelo de dados na Platform, você deve criar os esquemas recomendados e seus relacionamentos sozinho. Consulte os guias sobre gerenciamento [schemas](../../ui/resources/schemas.md) e [relacionamentos](../../tutorials/relationship-ui.md) na interface para obter mais informações.

Use a seguinte legenda para interpretar este ERD:

* Cada entidade mostrada no é baseada em um subjacente [Classe do Experience Data Model (XDM)](../composition.md#class).
* Para uma determinada entidade, cada linha marcada em **negrito** representa um grupo de campos ou um tipo de dados, com os campos relevantes fornecidos listados abaixo em texto não negrito.
* Os campos mais importantes para uma determinada entidade são destacados em vermelho.
* Todas as propriedades que poderiam ser usadas para identificar clientes individuais são marcadas como &quot;identidade&quot;, com uma dessas propriedades marcada como &quot;identidade principal&quot;.
* Os relacionamentos de entidade são marcados como não dependentes, já que os eventos baseados em cookies geralmente não podem determinar a pessoa ou indivíduo que fez a transação.

![Imagem mostrando o diagrama de relacionamento da entidade para o modelo de dados do setor de saúde](../../images/industries/healthcare.png)

>[!NOTE]
>
>Cada entidade inclui um campo &quot;_ID&quot;, que representa o identificador exclusivo da string (`_id`) para o registro ou evento em questão. Este campo é usado para rastrear a exclusividade do registro ou evento individual, evitar a duplicação de dados e pesquisar esses dados nos serviços downstream. Em alguns casos, `_id` pode ser um [Identificador exclusivo universal (UUID)](https://tools.ietf.org/html/rfc4122) ou [Identificador exclusivo global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>É importante distinguir esse **este campo não representa uma identidade relacionada a uma pessoa individual**, mas sim o próprio registro dos dados. Dados de identidade relacionados a uma pessoa, evento ou entidade comercial devem ser relegados a [campos de identidade](../composition.md#identity) fornecido por grupos de campos compatíveis.

## [!UICONTROL Assistência médica] casos de uso

A tabela a seguir descreve as classes recomendadas e os grupos de campos de esquema para vários casos de uso comuns do sistema de saúde.

| Caso de uso | Classes e grupos de campos recomendados |
| --- | --- |
| Melhore a aquisição digital e a experiência entre os consumidores que compram seguros. São exemplos: <ul><li>Quando as pessoas acessam uma página contendo informações gerais (como planos, nomes/níveis de planos, medicaid, programas de bem-estar e assim por diante), entendem seu comportamento e o que estão procurando para enviar emails promocionais ou direcioná-los em plataformas de terceiros com anúncios.</li><li>Quando as pessoas buscam informações sobre a saúde cardíaca e a vacina, envie a elas informações relacionadas à vacina sobre a saúde cardíaca para criar uma percepção da marca ou peça para agendar vacinas.</li></ul> | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do membro da área de saúde]](../../field-groups/profile/healthcare-member-details.md)</li><li>Campos de relacionamento estabelecidos entre `planID` atributos e esquemas que usam a variável [!UICONTROL Plano] classe.</li></ul></li><li>**[[!UICONTROL Pagador]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plano]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalhes do plano de saúde]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes do aplicativo]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Detalhes do sitetool]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  Detalhes de marketing da campanha]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| Aumentar a aquisição digital de pacientes por meio de anúncios direcionados com base no comportamento online anterior e nos dados de saúde. | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do membro da área de saúde]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Provedor]](../../classes/provider.md)**:<ul><li>[[!UICONTROL Provedor de assistência médica]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes da Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalhes de publicidade]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Melhore a inscrição e a criação de contas em planos de saúde rastreando o marketing de seguros por diferentes canais, a fim de entender como um cliente descobriu sobre uma empresa de seguros. | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do membro da área de saúde]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Pagador]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plano]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalhes do plano de saúde]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes da Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalhes de publicidade]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Evite lapsos na cobertura do seguro médico. | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do membro da área de saúde]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Plano]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Detalhes do plano de saúde]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| Promover informações sobre medicamentos para fornecedores usando anúncios diretos ao cliente (DTC). | <ul><li>**[[!UICONTROL Perfil individual XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Detalhes do membro da área de saúde]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Medicação]](../../classes/medication.md)**:<ul><li>[[!UICONTROL Medicação para tratamento de saúde]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Detalhes da Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Detalhes de publicidade]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
