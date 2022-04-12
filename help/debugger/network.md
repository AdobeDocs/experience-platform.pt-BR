---
title: Guia Rede
description: Saiba como usar a guia Rede no Adobe Experience Platform Debugger.
keywords: depurador, extensão do Experience Platform Debugger, chrome, extensão, rede, informações
seo-description: Experience Platform Debugger Network screen
seo-title: Network Tab
uuid: 839686c9-6e4f-4661-acf6-150ea24dc47f
exl-id: ed0579ef-ec26-43df-9453-a395c105038a
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 58%

---

# Guia Rede

O **Rede** A guia agrega todas as chamadas da solução da Adobe Experience Cloud feitas na página e as exibe em ordem da esquerda para a direita. Os parâmetros padrão são identificados automaticamente com nomes familiares e organizados para agrupar parâmetros comuns na mesma função.

![](images/network.jpg)

Essa tela é útil para comparar pares de valores importantes entre ocorrências. É possível confirmar se os parâmetros usados para integrações, como a ID de visitante da Experience Cloud ou a ID de dados complementares, são consistentes em todas as integrações.

>[!NOTE]
>
>No momento, nem todos os parâmetros transmitidos nas chamadas da solução (por exemplo, variáveis de contexto do Analytics, parâmetros personalizados do Target ou IDs do cliente do serviço da Experience Cloud ID) estão visíveis na tela Rede.

Para alterar as informações por solução, selecione a solução que deseja exibir na lista da navegação à esquerda. O exemplo a seguir for filtrado para mostrar somente o Analytics:

![](images/network-analytics.jpg)

Para voltar a exibir todas as soluções, selecione **[!UICONTROL Rede]**

Selecione um item na exibição Rede para ver uma exibição expandida. Na janela de exibição expandida, é possível copiar as informações mostradas para a Área de transferência.

![](images/network-expand.jpg)

<!--Use the icon at the top of each column to copy the server call URL to your clipboard, where you can paste it into another document for reference or debugging purposes.

![](images/copy.jpg)-->

Para limpar a lista, selecione **[!UICONTROL Remover eventos]**.

Para baixar um arquivo do Excel que contém as informações nesta tela, selecione **[!UICONTROL Baixar]**.
