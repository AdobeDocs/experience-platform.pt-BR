---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;perfil individual;campos;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;união schema;união
solution: Experience Platform
title: Classe de Perfil Individual XDM
topic: overview
description: Este documento fornece uma visão geral da classe de Perfil individual XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# [!DNL XDM Individual Profile] classe

[!DNL XDM Individual Profile] é uma classe XDM padrão que forma uma representação singular (ou &quot;perfil&quot;) dos atributos e interesses de indivíduos identificados e parcialmente identificados.

Os perfis podem variar desde sinais comportamentais anônimos (como cookies do navegador) até perfis altamente identificados que contêm informações detalhadas como nome, data de nascimento, local e endereço de email. À medida que um perfil cresce, ele se torna um repositório robusto de informações pessoais, identidades, detalhes de contato e preferências de comunicação para um indivíduo. Para obter mais informações de alto nível sobre o uso dessa classe no ecossistema da plataforma, consulte a [visão geral do XDM](../home.md#data-behaviors).

A classe [!DNL XDM Individual Profile] em si fornece vários valores gerados pelo sistema que são automaticamente preenchidos quando os dados são ingeridos, enquanto todos os outros campos devem ser adicionados por meio do uso de [mixins compatíveis](#mixins):

![](../images/classes/individual-profile.png)

| Propriedade | Descrição |
| --- | --- |
| `_repo` | Um objeto que contém os seguintes campos [!UICONTROL DateTime]: <ul><li>`createDate`: A data e a hora em que o recurso foi criado no armazenamento de dados, como quando os dados foram ingeridos pela primeira vez.</li><li>`modifyDate`: A data e a hora em que o recurso foi modificado pela última vez.</li></ul> |
| `_id` | Um identificador de string exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a singularidade de um registro individual, evitar a duplicação de dados e procurar esse registro em serviços de downstream. Como esse campo é gerado pelo sistema, ele não deve receber um valor explícito durante a ingestão dos dados.<br><br>É importante distinguir que este campo  **não** representa uma identidade relacionada com uma pessoa individual, mas sim o registro dos próprios dados. Os dados de identidade relacionados a uma pessoa devem ser relegados para [campos de identidade](../schema/composition.md#identity). |
| `createdByBatchID` | A ID do lote ingerido que fez com que o registro fosse criado. |
| `modifiedByBatchID` | A ID do último lote ingerido que fez com que o registro fosse atualizado. |
| `repositoryCreatedBy` | A ID do usuário que criou o registro. |
| `repositoryLastModifiedBy` | A ID do usuário que modificou o registro pela última vez. |

## Misturas compatíveis {#mixins}

>[!NOTE]
>
>Os nomes de várias misturas mudaram. Consulte o documento em [mixin name updates](../mixins/name-updates.md) para obter mais informações.

O Adobe fornece várias combinações padrão para uso com a classe [!DNL XDM Individual Profile]. A seguir está uma lista das combinações mais usadas para a classe:

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Detalhes demográficos]](../mixins/profile/person-details.md)
* [[!UICONTROL Detalhes do contato pessoal]](../mixins/profile/personal-details.md)
* [[!UICONTROL Detalhes do contato de trabalho]](../mixins/profile/work-details.md)
* [[!UICONTROL Detalhes da associação ao segmento]](../mixins/profile/segmentation.md)