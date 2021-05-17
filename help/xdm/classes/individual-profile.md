---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, perfil individual, campos, esquemas, esquemas, Esquemas, identityMap, mapa de identidade, mapa de identidade, design de esquema, mapa, mapa, mapa, esquema de união, união
solution: Experience Platform
title: Classe de Perfil Individual XDM
topic-legacy: overview
description: Este documento fornece uma visão geral da classe Perfil individual XDM.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 9fbb40a401250496761dcce63a3f033a8746ae7e
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] classe

[!DNL XDM Individual Profile] é uma classe padrão do Experience Data Model (XDM) que forma uma representação singular (ou &quot;perfil&quot;) de uma pessoa individual. Especificamente, a classe (e suas combinações compatíveis) captura os atributos e interesses de indivíduos identificados e parcialmente identificados que interagem com sua marca.

Os perfis podem variar de sinais comportamentais anônimos (como cookies do navegador) a perfis altamente identificados que contêm informações detalhadas, como nome, data de nascimento, local e endereço de email. À medida que um perfil cresce, ele se torna um repositório robusto de informações pessoais, identidades, detalhes de contato e preferências de comunicação para um indivíduo. Para obter mais informações de alto nível sobre o uso dessa classe no ecossistema da plataforma, consulte a [Visão geral do XDM](../home.md#data-behaviors).

A própria classe [!DNL XDM Individual Profile] fornece vários valores gerados pelo sistema que são automaticamente preenchidos quando os dados são assimilados, enquanto todos os outros campos devem ser adicionados por meio do uso de [grupos de campos de esquema compatíveis](#field-groups):

![](../images/classes/individual-profile.png)

| Propriedade | Descrição |
| --- | --- |
| `_repo` | Um objeto que contém os seguintes campos [!UICONTROL DateTime]: <ul><li>`createDate`: A data e a hora em que o recurso foi criado no armazenamento de dados, como quando os dados foram assimilados pela primeira vez.</li><li>`modifyDate`: A data e a hora em que o recurso foi modificado pela última vez.</li></ul> |
| `_id` | Um identificador exclusivo para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, evitar a duplicação de dados e buscar esse registro em serviços downstream.<br><br>É importante distinguir que este campo  **não** representa uma identidade relacionada a uma pessoa, mas sim o registro dos dados propriamente ditos. Os dados de identidade relacionados a uma pessoa devem ser relegados para [campos de identidade](../schema/composition.md#identity). |
| `createdByBatchID` | A ID do lote assimilado que fez com que o registro fosse criado. |
| `modifiedByBatchID` | A ID do último lote ingerido que fez com que o registro fosse atualizado. |
| `personID` | Um identificador exclusivo para a pessoa a que este registro se refere. Este campo não representa necessariamente uma identidade relacionada à pessoa, a menos que também seja designado como um [campo de identidade](../schema/composition.md#identity). |
| `repositoryCreatedBy` | A ID do usuário que criou o registro. |
| `repositoryLastModifiedBy` | A ID do usuário que modificou o registro pela última vez. |

## Grupos de campos compatíveis {#field-groups}

>[!NOTE]
>
>Os nomes de vários grupos de campos foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../field-groups/name-updates.md) para obter mais informações.

O Adobe fornece vários grupos de campos padrão para uso com a classe [!DNL XDM Individual Profile] . Esta é uma lista de alguns grupos de campos comumente usados para a classe :

* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Detalhes demográficos]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL Detalhes de contato pessoal]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Detalhes do Contato do Trabalho]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL Detalhes da associação ao segmento]](../field-groups/profile/segmentation.md)

Para obter uma lista completa de todos os grupos de campos compatíveis para [!DNL XDM Individual Profile], consulte o [XDM GitHub repo](https://github.com/adobe/xdm/tree/master/components/mixins/profile).
