---
title: Configurações de consentimento
description: Defina as configurações padrão de consentimento e privacidade para a extensão de tag.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Configurações de consentimento

A seção **[!UICONTROL Consent]** permite selecionar o nível padrão de consentimento que será presumido se nenhuma outra preferência de consentimento explícito for fornecida. O nível de consentimento padrão não é salvo em perfis de usuário.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensions]** e selecione **[!UICONTROL Configure]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role até a seção **[!UICONTROL Consent]**.

![Imagem mostrando as configurações de privacidade da extensão de marca do Web SDK na interface do usuário de Marcas](../assets/web-sdk-ext-privacy.png)

Esta seção contém um único conjunto de botões de opção que determina o nível de consentimento padrão:

* **[!UICONTROL In]**: Colete eventos que ocorrem antes que o usuário forneça preferências de consentimento.
* **[!UICONTROL Out]**: descartar eventos que ocorrem antes de o usuário fornecer preferências de consentimento.
* **[!UICONTROL Pending]**: enfileirar eventos que ocorrem antes que o usuário forneça preferências de consentimento. Quando o consentimento é concedido, os eventos em fila são enviados para a Adobe. Quando o consentimento é negado, os eventos em fila são descartados.
* **[!UICONTROL Provide a data element]**: Selecione um elemento de dados que determine uma das definições de configuração acima. Os valores válidos incluem as cadeias de caracteres `"in"`, `"out"` ou `"pending"`.

Se sua organização exigir o consentimento explícito do usuário para coletar dados, a Adobe recomenda definir o consentimento padrão para **[!UICONTROL Out]** ou **[!UICONTROL Pending]**.
