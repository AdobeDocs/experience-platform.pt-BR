---
title: Extensão do Marketo Munchkin Visão geral
description: Saiba mais sobre a extensão de tag do Marketo Munchkin no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 80%

---

# Visão geral da extensão do Marketo Munchkin

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Use essa extensão para integrar o código de rastreamento JavaScript [!DNL Marketo Munchkin] com sua propriedade. O JavaScript [!DNL Marketo Munchkin] permite rastrear as visitas da página do usuário final e os cliques nas páginas de aterrissagem do Marketo e páginas da Web externas.

## Instalar a extensão do Marketo Munchkin

Se a extensão [!DNL Marketo Munchkin] ainda não estiver instalada, abra a propriedade e selecione **[!UICONTROL Extensões > Catálogo]**, passe o mouse sobre a extensão [!DNL Marketo Munchkin] e selecione **[!UICONTROL Instalar]**.

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

**params:** uma sequência de consulta dos parâmetros desejados a serem registrados.

**name:** o nome personalizado do ativo da página da Web.

### Clicar no link

![](../../../images/munchkin-click-link.png)

**href: (obrigatório)** o caminho de arquivo do URL usado para registrar uma seleção de link.
