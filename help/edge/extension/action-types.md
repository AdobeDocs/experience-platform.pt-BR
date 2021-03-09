---
title: Tipos de ação na extensão SDK da Web da Adobe Experience Platform
description: Saiba mais sobre os diferentes tipos de ação fornecidos pela extensão Adobe Experience Platform Web SDK no Adobe Experience Platform Launch.
translation-type: tm+mt
source-git-commit: ff261c507d310b8132912680b6ddd1e7d5675d08
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 6%

---


# Tipos de ação

Depois de configurar a [extensão do SDK da Web da Adobe Experience Platform](web-sdk-extension.md) para [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configure os tipos de ação.

Esta página descreve os tipos de ação disponíveis.

## Enviar evento

Envia um evento para a Adobe [!DNL Experience Platform] para que a Adobe Experience Platform possa coletar os dados enviados e agir de acordo com essas informações. Selecione uma instância (caso tenha mais de uma). Se o evento ocorrer no início de um carregamento de página ou durante uma alteração de exibição em um aplicativo de página única, selecione **[!UICONTROL Ocorre no início de uma exibição]**.

Todos os dados que deseja enviar podem ser enviados no campo **[!UICONTROL Dados XDM]**. Use um objeto JSON que esteja em conformidade com a estrutura do esquema XDM. Esse objeto pode ser criado na página ou por meio de um **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

## Definir consentimento

Após receber o consentimento do usuário, ele deve ser comunicado ao SDK da Web da Adobe Experience Platform usando o tipo de ação &quot;Definir consentimento&quot;. Atualmente, há suporte para dois tipos de padrões: &quot;Adobe&quot; e &quot;IAB TCF&quot;. Consulte [Suporte a preferências de consentimento do cliente](../consent/supporting-consent.md). Ao usar o Adobe versão 2.0, somente um valor de elemento de dados é suportado. Será necessário criar um elemento de dados que resolva o objeto de consentimento.

Nesta ação, você também recebe um campo opcional para incluir um Mapa de identidade para que as identidades possam ser sincronizadas após o recebimento do consentimento. A sincronização é útil quando o consentimento é configurado como &quot;Pendente&quot; ou &quot;Fora&quot;, pois a chamada de consentimento é provavelmente a primeira chamada a ser acionada.

## Redefinir ID de mesclagem de eventos

Se você quiser redefinir a ID da mesclagem de eventos na página, é possível fazê-lo com esta ação. Para redefinir sua ID, selecione a ID de mesclagem que deseja redefinir e acione a ação conforme necessário.

## O que vem a seguir

Depois de definir os tipos de ação, [configure os tipos de elemento de dados](data-element-types.md).