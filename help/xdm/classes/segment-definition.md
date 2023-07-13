---
solution: Experience Platform
title: Classe de definição de segmento
description: Este documento fornece uma visão geral da classe de definição de segmento no Experience Data Model (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: 55f86fdd4fd36d21dcbd575d6da83df18abb631d
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# [!UICONTROL Definição de segmento] classe

&quot;[!UICONTROL Definição de segmento]&quot; é uma classe padrão do Experience Data Model (XDM) que captura os detalhes de uma definição de segmento. A classe inclui campos obrigatórios, como a ID e o nome de um público-alvo, além de outros atributos opcionais. Essa classe deve ser usada se você estiver trazendo definições de segmento de sistemas externos para o Adobe Experience Platform.

>[!NOTE]
>
>Esta classe só deve ser usada para registrar informações sobre as próprias definições de segmento. Para capturar as informações de associação do público-alvo nos dados do perfil, use o [Grupo de campos Detalhes da Associação do Segmento](../field-groups/profile/segmentation.md) no seu [!UICONTROL Perfil individual XDM] esquema.

![](../images/classes/segment-definition.png)

| Propriedade | Descrição |
| --- | --- |
| `_repo` | Um objeto que contém o seguinte [!UICONTROL DateTime] campos: <ul><li>`createDate`: a data e a hora em que o recurso foi criado no armazenamento de dados, como quando os dados foram assimilados pela primeira vez.</li><li>`modifyDate`: a data e a hora da última modificação do recurso.</li></ul> |
| `_id` | Um identificador de sequência de caracteres exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, impedir a duplicação de dados e pesquisar esse registro nos serviços downstream.<br><br>Como esse campo é gerado pelo sistema, ele não recebe um valor explícito durante a assimilação de dados. No entanto, você ainda pode optar por fornecer seus próprios valores de ID exclusivos, se desejar.<br><br>É importante distinguir que esse campo **não** representam uma identidade relacionada a uma pessoa individual, mas sim o registro dos próprios dados. Os dados de identidade relativos a uma pessoa devem ser [campos de identidade](../schema/composition.md#identity) em vez disso. |
| `createdByBatchID` | A ID do lote assimilado que causou a criação do registro. |
| `description` | Uma descrição para a definição do segmento. |
| `identityMap` | Um campo de mapa que contém um conjunto de identidades com namespace para os indivíduos aos quais o público se aplica. Consulte a seção sobre mapas de identidade na [noções básicas da composição do esquema](../schema/composition.md#identityMap) para obter mais informações sobre o caso de uso. |
| `modifiedByBatchID` | A ID do último lote assimilado que causou a atualização do registro. |
| `repositoryCreatedBy` | A ID do usuário que criou o registro. |
| `repositoryLastModifiedBy` | A ID do usuário que modificou o registro pela última vez. |
| `segmentName` | **(Obrigatório)** Um nome para a definição de segmento. |
| `segmentStatus` | O status do público-alvo do sistema externo. Os seguintes valores são aceitos: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | O número da versão mais recente da definição de segmento. |

{style="table-layout:auto"}
