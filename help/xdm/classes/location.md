---
title: Classe de localização
description: Saiba mais sobre a classe Localização no Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 7%

---

# Classe [!UICONTROL Location]

No Experience Data Model (XDM), a classe [!UICONTROL Location] captura informações do local do evento ao vivo, como um hall de viagem ou uma arena esportiva.

![Estrutura de classe de localização](../images/classes/location.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Identificador] | `_id` | [!UICONTROL String] | Um identificador de sequência de caracteres exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, impedir a duplicação de dados e pesquisar esse registro nos serviços downstream.<br><br>Como este campo é gerado pelo sistema, ele não precisa receber um valor explícito durante a assimilação de dados. No entanto, você ainda pode optar por fornecer seus próprios valores de ID exclusivos, se desejar. |
| [!UICONTROL Identificador de local] | `locationID` | [!UICONTROL String] | Um identificador exclusivo da localização. |
| [!UICONTROL Nome do local] | `locationName` | [!UICONTROL String] | O nome do local. |

A classe pode ser estendida com o grupo de campos [[!UICONTROL Local]](../field-groups/location/healthcare-location.md) para descrever mais detalhes sobre um local.
