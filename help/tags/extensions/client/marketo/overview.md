---
title: Visão geral da extensão do Marketo Munchkin
description: Saiba mais sobre a extensão de tag Marketo Munchkin na Adobe Experience Platform.
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 97%

---

# Visão geral da extensão do Marketo Munchkin

Use essa extensão para integrar o código de rastreamento JavaScript [!DNL Marketo Munchkin] com sua propriedade. O JavaScript [!DNL Marketo Munchkin] permite rastrear as visitas da página do usuário final e os cliques nas páginas de destino do Marketo e páginas da Web externas.

## Instalar a extensão do Marketo Munchkin

Se a extensão [!DNL Marketo Munchkin] ainda não tiver sido instalada, abra a propriedade e selecione **[!UICONTROL Extensions > Catalog]**, passe o mouse sobre a extensão [!DNL Marketo Munchkin] e selecione **[!UICONTROL Install]**.

Esta extensão não tem a configuração necessária.

## Tipos de ação da extensão do Marketo Munchkin

Esta seção descreve os tipos de ação disponíveis na extensão [!DNL Marketo Munchkin].

### Inicializar

![](../../../images/munchkin-Init.png)

**Munchkin ID: (obrigatória)** ID da conta do Munchkin encontrada no menu Admin > Integração > Munchkin.

**Configurations:** todos os parâmetros configuráveis estão documentados [aqui](https://developers.marketo.com/javascript-api/lead-tracking/configuration/).

### Visitar página da Web

![](../../../images/munchkin-visit-page.png)

**url: (obrigatório)** o caminho de arquivo do URL usado para registrar uma visita de página.

**params:** uma string de consulta dos parâmetros desejados a serem registrados.

**name:** o nome personalizado do ativo da página da Web.

### Clicar no link

![](../../../images/munchkin-click-link.png)

**href: (obrigatório)** o caminho de arquivo do URL usado para registrar uma seleção de link.
