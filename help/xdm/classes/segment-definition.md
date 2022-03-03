---
solution: Experience Platform
title: Classe de definição de segmento
topic-legacy: overview
description: Este documento fornece uma visão geral da classe de definição de segmento no Experience Data Model (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 2%

---

# [!UICONTROL Definição de segmento] classe

&quot;[!UICONTROL Definição de segmento]&quot; é uma classe padrão do Experience Data Model (XDM) que captura os detalhes de uma definição de segmento. A classe inclui campos obrigatórios, como a ID e o nome de um segmento, juntamente com outros atributos opcionais. Essa classe deve ser usada se você estiver trazendo definições de segmento de sistemas externos para o Adobe Experience Platform.

>[!NOTE]
>
>Essa classe só deve ser usada para capturar informações sobre as próprias definições de segmento. Para capturar informações de associação de segmento nos dados do perfil, você deve usar o [Grupo de campos Detalhes da associação ao segmento](../field-groups/profile/segmentation.md) em seu [!UICONTROL Perfil individual XDM] esquema.

![](../images/classes/segment-definition.png)

| Propriedade | Descrição |
| --- | --- |
| `_repo` | Um objeto contendo o seguinte [!UICONTROL DateTime] campos: <ul><li>`createDate`: A data e a hora em que o recurso foi criado no armazenamento de dados, como quando os dados foram assimilados pela primeira vez.</li><li>`modifyDate`: A data e a hora em que o recurso foi modificado pela última vez.</li></ul> |
| `_id` | Um identificador de string exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, evitar a duplicação de dados e buscar esse registro em serviços downstream.<br><br>Como esse campo é gerado pelo sistema, ele não recebe um valor explícito durante a assimilação de dados. No entanto, ainda é possível optar por fornecer seus próprios valores de ID exclusivos.<br><br>É importante distinguir que este campo **não** representar uma identidade relacionada a uma pessoa individual, mas sim o registro dos dados propriamente ditos. Os dados de identidade relativos a uma pessoa devem ser relegados para [campos de identidade](../schema/composition.md#identity) em vez disso. |
| `createdByBatchID` | A ID do lote assimilado que fez com que o registro fosse criado. |
| `description` | Uma descrição para a definição de segmento. |
| `identityMap` | Campo de mapa que contém um conjunto de identidades namespacadas para os indivíduos aos quais o segmento se aplica. Consulte a seção sobre mapas de identidade na [noções básicas da composição do schema](../schema/composition.md#identityMap) para obter mais informações sobre o caso de uso. |
| `modifiedByBatchID` | A ID do último lote ingerido que fez com que o registro fosse atualizado. |
| `repositoryCreatedBy` | A ID do usuário que criou o registro. |
| `repositoryLastModifiedBy` | A ID do usuário que modificou o registro pela última vez. |
| `segmentName` | **(Obrigatório)** Um nome para a definição do segmento. |
| `segmentStatus` | O status do segmento no sistema externo. Os seguintes valores são aceitos: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | O número da versão mais recente da definição de segmento. |

{style=&quot;table-layout:auto&quot;}
