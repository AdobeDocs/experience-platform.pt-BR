---
solution: Experience Platform
title: Classe de definição de segmento
description: Saiba mais sobre a classe de definição de segmento no Experience Data Model (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 1%

---

# Classe [!UICONTROL Definição de segmento]

&quot;[!UICONTROL Definição de segmento]&quot; é uma classe padrão do Experience Data Model (XDM) que captura os detalhes de uma definição de segmento. A classe inclui campos obrigatórios, como a ID e o nome de um público-alvo, além de outros atributos opcionais. Essa classe deve ser usada se você estiver trazendo definições de segmento de sistemas externos para o Adobe Experience Platform.

>[!NOTE]
>
>Esta classe só deve ser usada para registrar informações sobre as próprias definições de segmento. Para capturar informações de associação de público nos dados do seu perfil, você deve usar o [grupo de campos Detalhes da associação do segmento](../field-groups/profile/segmentation.md) no seu esquema [!UICONTROL Perfil individual XDM].

![](../images/classes/segment-definition.png)

| Propriedade | Descrição |
| --- | --- |
| `_repo` | Um objeto contendo os seguintes campos [!UICONTROL DateTime]: <ul><li>`createDate`: a data e a hora em que o recurso foi criado no armazenamento de dados, como quando os dados foram assimilados pela primeira vez.</li><li>`modifyDate`: a data e a hora em que o recurso foi modificado pela última vez.</li></ul> |
| `_id` | Um identificador de sequência de caracteres exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, impedir a duplicação de dados e pesquisar esse registro nos serviços downstream.<br><br>Como este campo é gerado pelo sistema, ele não receberá um valor explícito durante a assimilação de dados. No entanto, você ainda pode optar por fornecer seus próprios valores de ID exclusivos, se desejar.<br><br>É importante distinguir que este campo **não** representa uma identidade relacionada a uma pessoa individual, mas sim o próprio registro de dados. Os dados de identidade relacionados a uma pessoa devem ser relegados a [campos de identidade](../schema/composition.md#identity). |
| `createdByBatchID` | A ID do lote assimilado que causou a criação do registro. |
| `description` | Uma descrição para a definição do segmento. |
| `identityMap` | Um campo de mapa que contém um conjunto de identidades com namespace para os indivíduos aos quais o público se aplica. Consulte a seção sobre mapas de identidade nas [noções básicas da composição de esquema](../schema/composition.md#identityMap) para obter mais informações sobre o caso de uso. |
| `modifiedByBatchID` | A ID do último lote assimilado que causou a atualização do registro. |
| `repositoryCreatedBy` | A ID do usuário que criou o registro. |
| `repositoryLastModifiedBy` | A ID do usuário que modificou o registro pela última vez. |
| `segmentName` | **(Obrigatório)** Um nome para a definição de segmento. |
| `segmentStatus` | O status do público-alvo do sistema externo. Os seguintes valores são aceitos: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | O número da versão mais recente da definição de segmento. |

{style="table-layout:auto"}
