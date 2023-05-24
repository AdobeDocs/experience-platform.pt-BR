---
title: Utilização do Adobe Experience Platform Assurance
description: Este guia explica como usar o Adobe Experience Platform Assurance após sua instalação e implementação.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Utilização do Adobe Experience Platform Assurance

Este tutorial explica como usar o Adobe Experience Platform Assurance. Para obter instruções sobre como instalar e implementar a extensão Adobe Experience Platform Assurance, leia o tutorial sobre [implementação da extensão do Assurance](./implement-assurance.md).

## Criar sessões

Depois de fazer logon na [Interface do usuário do Assurance](https://experience.adobe.com/assurance), você pode selecionar **[!UICONTROL Criar sessão]** para começar a criar uma sessão.

![O botão criar sessão é realçado, mostrando onde você pode criar uma sessão.](./images/using-assurance/create-session.png)

A variável **[!UICONTROL Criar nova sessão]** será exibida. Revise as instruções fornecidas e continue selecionando **[!UICONTROL Início]**.

![A caixa de diálogo Criar nova sessão é exibida, mostrando instruções sobre como usar o Assurance.](./images/using-assurance/create-new-session.png)

Agora você pode inserir um nome para identificar a sessão e, em seguida, fornecer um **[!UICONTROL URL base]** (URL de deep linking do seu aplicativo). Após fornecer esses detalhes, selecione **[!UICONTROL Próxima]**.

>[!INFO]
>
>O URL base é a definição raiz usada para iniciar seu aplicativo a partir de um URL. Um URL de sessão é gerado pelo qual você pode iniciar a sessão do Assurance. Um exemplo de valor pode se parecer com: `myapp://default` No **[!UICONTROL URL base]** digite a definição base do deep link do seu aplicativo.

![O workflow completo da criação de uma nova sessão é exibido.](./images/using-assurance/create-session.gif)

## Conectar-se a uma sessão

Depois de criar uma sessão, verifique se **[!UICONTROL Criar nova sessão]** A caixa de diálogo agora mostra um link, um código QR e um PIN.

![Uma caixa de diálogo mostrando as opções para se conectar à sua sessão do Assurance é exibida.](./images/using-assurance/create-new-session-pin.png)

Se esta caixa de diálogo for exibida, você pode usar o aplicativo de câmera do dispositivo para digitalizar o código QR e abrir o aplicativo ou copiar o link e abrir no aplicativo. Quando o aplicativo for iniciado, você deverá ver a tela de entrada do PIN sobreposta. Digite o PIN da etapa anterior e pressione **[!UICONTROL Conectar]**.

Você pode verificar se seu aplicativo está conectado ao Assurance quando o ícone do Adobe Experience Platform (Adobe vermelho &quot;A&quot;) for exibido no aplicativo.

![O workflow completo de conexão do aplicativo a uma sessão do Assurance é exibido.](./images/using-assurance/connect-session.gif)

## Exportar uma sessão

Para exportar uma sessão do Assurance, na página de detalhes das sessões do aplicativo, selecione **[!UICONTROL Exportar para JSON]** em uma sessão:

![Exportar uma sessão](./images/using-assurance/export-session.png)

A opção de exportação respeita os resultados do filtro de pesquisa e exporta somente os eventos exibidos na visualização de evento. Por exemplo, se você pesquisou por eventos &quot;track&quot; e depois selecionou **[!UICONTROL Exportar para JSON]**, somente os resultados do evento &quot;rastrear&quot; serão exportados.
