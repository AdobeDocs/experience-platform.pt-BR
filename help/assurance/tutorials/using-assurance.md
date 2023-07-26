---
title: Utilização do Adobe Experience Platform Assurance
description: Este guia explica como usar o Adobe Experience Platform Assurance após sua instalação e implementação.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '402'
ht-degree: 100%

---

# Utilização do Adobe Experience Platform Assurance

Este tutorial explica como usar o Adobe Experience Platform Assurance. Para obter instruções sobre como instalar e implementar a extensão do Adobe Experience Platform Assurance, leia o tutorial sobre [implementação da extensão do Assurance](./implement-assurance.md).

## Criar sessões

Depois de fazer logon na [interface do Assurance](https://experience.adobe.com/assurance), você pode selecionar **[!UICONTROL Criar sessão]** para começar a criar uma sessão.

![O botão Criar sessão é realçado, mostrando onde você pode criar uma sessão.](./images/using-assurance/create-session.png)

A caixa de diálogo **[!UICONTROL Criar nova sessão]** é exibida. Revise as instruções fornecidas e continue selecionando **[!UICONTROL Iniciar]**.

![A caixa de diálogo Criar nova sessão será exibida, mostrando instruções sobre como usar o Assurance.](./images/using-assurance/create-new-session.png)

Agora você pode inserir um nome para identificar a sessão e fornecer um **[!UICONTROL URL base]** (URL de link profundo do seu aplicativo). Após fornecer esses detalhes, selecione **[!UICONTROL Próximo]**.

>[!INFO]
>
>O URL base é a definição raiz usada para iniciar seu aplicativo a partir de um URL. Um URL de sessão é gerado, a partir do qual você pode iniciar a sessão do Assurance. Um exemplo de valor pode ser: `myapp://default`. No campo **[!UICONTROL URL base]**, digite a definição do link profundo de base do seu aplicativo.

![O fluxo de trabalho completo de criação de uma nova sessão é exibido.](./images/using-assurance/create-session.gif)

## Conectar-se a uma sessão

Depois de criar uma sessão, verifique se a caixa de diálogo **[!UICONTROL Criar nova sessão]** mostra um link, um código QR e um PIN.

![Uma caixa de diálogo mostrando as opções para se conectar à sua sessão do Assurance é exibida.](./images/using-assurance/create-new-session-pin.png)

Se esta caixa de diálogo for exibida, você pode usar a câmera do dispositivo para digitalizar o código QR e abrir o aplicativo ou copiar o link e abri-lo no aplicativo. Quando o aplicativo for iniciado, você verá a tela de entrada do PIN sobreposta. Digite o PIN da etapa anterior e pressione **[!UICONTROL Conectar]**.

Você pode conferir se seu aplicativo está conectado ao Assurance observando se o ícone da Adobe Experience Platform (“A” vermelho de Adobe) está sendo exibido no aplicativo.

![O fluxo de trabalho completo de conexão do aplicativo a uma sessão do Assurance é exibido.](./images/using-assurance/connect-session.gif)

## Exportar uma sessão

Para exportar uma sessão do Assurance, selecione **[!UICONTROL Exportar para JSON]** em uma sessão na página de detalhes das sessões do aplicativo:

![Exportar uma sessão](./images/using-assurance/export-session.png)

A opção de exportação respeita os resultados do filtro de pesquisa e exporta somente os eventos mostrados na exibição de evento. Por exemplo, se você pesquisou por eventos de “rastreio” e depois selecionou **[!UICONTROL Exportar para JSON]**, somente os resultados do evento de “rastreio” serão exportados.
