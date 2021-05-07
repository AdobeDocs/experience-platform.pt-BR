---
solution: Experience Platform
title: Classe de definição de segmento
topic-legacy: overview
description: Este documento fornece uma visão geral da classe de definição de segmento no Experience Data Model (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# [!UICONTROL Segment definition] classe

&quot;[!UICONTROL Segment definition]&quot; é uma classe padrão do Experience Data Model (XDM) que captura os detalhes de uma definição de segmento. A classe inclui campos obrigatórios, como a ID e o nome de um segmento, juntamente com outros atributos opcionais. Essa classe deve ser usada se você estiver trazendo definições de segmento de sistemas externos para o Adobe Experience Platform.

>[!NOTE]
>
>Essa classe só deve ser usada para capturar informações sobre as próprias definições de segmento. Para capturar informações de associação de segmento nos dados do perfil, você deve usar o [grupo de campos Detalhes de associação de segmento](../field-groups/profile/segmentation.md) no esquema [!UICONTROL XDM Individual Profile].

![](../images/classes/segment-definition.png)

| Propriedade | Descrição |
| --- | --- |
| `_repo` | Um objeto que contém os seguintes campos [!UICONTROL DateTime]: <ul><li>`createDate`: A data e a hora em que o recurso foi criado no armazenamento de dados, como quando os dados foram assimilados pela primeira vez.</li><li>`modifyDate`: A data e a hora em que o recurso foi modificado pela última vez.</li></ul> |
| `_id` | Um identificador de string exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, evitar a duplicação de dados e buscar esse registro em serviços downstream.<br><br>Como esse campo é gerado pelo sistema, ele não recebe um valor explícito durante a assimilação de dados. No entanto, ainda é possível optar por fornecer seus próprios valores de ID exclusivos.<br><br>É importante distinguir que este campo  **não** representa uma identidade relacionada a uma pessoa, mas sim o registro dos dados propriamente ditos. Os dados de identidade relacionados a uma pessoa devem ser relegados para [campos de identidade](../schema/composition.md#identity). |
| `createdByBatchID` | A ID do lote assimilado que fez com que o registro fosse criado. |
| `description` | Uma descrição para a definição de segmento. |
| `identityMap` | Campo de mapa que contém um conjunto de identidades namespacadas para os indivíduos aos quais o segmento se aplica. Este campo é atualizado automaticamente pelo sistema conforme os dados de identidade são assimilados.<br /><br />Consulte a seção sobre mapas de identidade nas  [noções básicas da ](../schema/composition.md#identityMap) composição do schema para obter mais informações sobre seu caso de uso. |
| `modifiedByBatchID` | A ID do último lote ingerido que fez com que o registro fosse atualizado. |
| `repositoryCreatedBy` | A ID do usuário que criou o registro. |
| `repositoryLastModifiedBy` | A ID do usuário que modificou o registro pela última vez. |
| `segmentName` | **(Obrigatório)** Um nome para a definição de segmento. |
| `segmentStatus` | O status do segmento no sistema externo. Os seguintes valores são aceitos: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | O número da versão mais recente da definição de segmento. |
