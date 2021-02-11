---
title: Tipos de ação de extensão do SDK da Web da plataforma
description: Tipos de ação de extensão do Adobe Experience Platform Web SDK no Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 473cc1f7617f1d65cdb70ff0e758178ea0174f00
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Tipos de ação

Depois de configurar a [extensão do Adobe Experience Platform Web SDK](web-sdk-extension.md) para [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configure os tipos de ação.

Esta página descreve os tipos de ação disponíveis.

## Enviar evento

Envia um evento para Adobe [!DNL Experience Platform] para que a Adobe Experience Platform possa coletar os dados enviados e agir de acordo com essas informações. Você deve selecionar uma instância (se tiver mais de uma). Se o evento ocorrer no início de um carregamento de página ou durante uma alteração de visualização em um único aplicativo de página, selecione **[!UICONTROL Ocorre no start de uma visualização]**.

Todos os dados que você deseja enviar podem ser enviados no campo **[!UICONTROL Dados XDM]**. Esse deve ser um objeto JSON que esteja em conformidade com a estrutura do esquema XDM. Esse objeto pode ser criado na sua página ou por meio de um **[!UICONTROL Código personalizado]** **[!UICONTROL Elemento de dados]**.

## Definir consentimento

Depois de receber o consentimento do usuário, isso deve ser comunicado ao SDK da Web da Adobe Experience Platform. Para fazer isso, use o tipo de ação &quot;Definir consentimento&quot;. Atualmente, há suporte para dois tipos de padrões: &quot;Adobe&quot; e &quot;IAB TCF&quot;. Se estiver usando o padrão Adobe, você poderá definir o consentimento como &quot;Dentro&quot; ou &quot;Fora&quot; ou poderá fornecê-lo usando um elemento de dados. Se estiver usando o padrão TCF IAB, forneça a versão e o valor que você deseja usar, além de informações adicionais sobre o GDPR.

Nesta ação, você também recebe um campo opcional para incluir um Mapa de identidade, de modo que as identidades possam ser sincronizadas assim que o consentimento for recebido. Isso pode ser útil quando o consentimento é configurado como &quot;Pendente&quot;, pois a chamada de consentimento provavelmente será a primeira chamada a ser acionada.

## Redefinir ID de mesclagem de eventos

Se você deseja redefinir sua ID de mesclagem de eventos na página, é possível fazer isso com esta ação. Para redefinir sua ID, é necessário selecionar a ID de mesclagem que deseja redefinir e acionar a ação conforme necessário.

## O que vem a seguir

Depois de definir os tipos de ação, [configure os tipos de elementos de dados](data-element-types.md).