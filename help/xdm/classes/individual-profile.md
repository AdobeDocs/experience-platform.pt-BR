---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: Classe de Perfil individual XDM
topic: overview
description: Este documento fornece uma visão geral da classe de Perfil individual XDM.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# [!DNL XDM Individual Profile] classe

[!DNL XDM Individual Profile] é uma classe XDM padrão que forma uma representação singular (ou &quot;perfil&quot;) dos atributos e interesses de indivíduos identificados e parcialmente identificados.

Os perfis podem variar desde sinais comportamentais anônimos (como cookies do navegador) até perfis altamente identificados que contêm informações detalhadas como nome, data de nascimento, local e endereço de email. À medida que um perfil cresce, ele se torna um repositório robusto de informações pessoais, identidades, detalhes de contato e preferências de comunicação para um indivíduo. Para obter mais informações de alto nível sobre o uso dessa classe no ecossistema da plataforma, consulte a visão geral [do](../home.md#data-behaviors)XDM.

A própria [!DNL XDM Individual Profile] classe fornece vários valores gerados pelo sistema que são automaticamente preenchidos quando os dados são ingeridos, enquanto todos os outros campos devem ser adicionados por meio do uso de combinações [](#mixins)compatíveis:

![](../images/classes/individual-profile.png)

| Propriedade | Descrição |
| --- | --- |
| `_repo` | Um objeto que contém os seguintes campos [!UICONTROL DateTime] : <ul><li>`createDate`: A data e a hora em que o recurso foi criado no armazenamento de dados, como quando os dados foram ingeridos pela primeira vez.</li><li>`modifyDate`: A data e a hora em que o recurso foi modificado pela última vez.</li></ul> |
| `_id` | Um identificador de string exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a singularidade de um registro individual, evitar a duplicação de dados e procurar esse registro em serviços de downstream. Como esse campo é gerado pelo sistema, ele não deve receber um valor explícito durante a ingestão dos dados.<br><br>É importante distinguir que este campo **não** representa uma identidade relacionada com uma pessoa individual, mas sim o registro dos dados propriamente ditos. Os dados de identidade relativos a uma pessoa devem ser relegados para campos [de](../schema/composition.md#identity) identidade. |
| `createdByBatchID` | A ID do lote ingerido que fez com que o registro fosse criado. |
| `modifiedByBatchID` | A ID do último lote ingerido que fez com que o registro fosse atualizado. |
| `repositoryCreatedBy` | A ID do usuário que criou o registro. |
| `repositoryLastModifiedBy` | A ID do usuário que modificou o registro pela última vez. |

## Misturas compatíveis {#mixins}

>[!NOTE]
>
>Os nomes de várias misturas mudaram. Consulte o documento sobre atualizações [de nome de](../mixins/name-updates.md) mixin para obter mais informações.

Adobe fornece várias combinações padrão para uso com a [!DNL XDM Individual Profile] classe. A seguir está uma lista das combinações mais usadas para a classe:

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Detalhes demográficos]](../mixins/profile/person-details.md)
* [[!UICONTROL Detalhes do contato pessoal]](../mixins/profile/personal-details.md)
* [[!UICONTROL Detalhes do contato de trabalho]](../mixins/profile/work-details.md)
* [[!UICONTROL Detalhes da associação ao segmento]](../mixins/profile/segmentation.md)