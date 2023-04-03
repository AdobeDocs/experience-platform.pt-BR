---
title: Uso do Adobe Experience Platform Assurance
description: Este guia explica como usar o Adobe Experience Platform Assurance depois de ter sido instalado e implementado.
source-git-commit: 24f452bdb923179eefe53fdb28d3a92d43e533cd
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Uso do Adobe Experience Platform Assurance

Este tutorial explica como usar o Adobe Experience Platform Assurance. Para obter instruções sobre como instalar e implementar a extensão Adobe Experience Platform Assurance, leia o tutorial em [implementação da extensão Assurance](./implement-assurance.md).

## Criar sessões

Depois de fazer logon na [Interface de usuário de garantia](https://experience.adobe.com/assurance), você pode selecionar **[!UICONTROL Criar sessão]** para começar a criar uma sessão.

![O botão Criar sessão é realçado, mostrando onde você pode criar uma sessão.](./images/using-assurance/create-session.png)

O **[!UICONTROL Criar nova sessão]** será exibida. Revise as instruções fornecidas e continue selecionando **[!UICONTROL Iniciar]**.

![A caixa de diálogo Criar nova sessão é exibida, exibindo instruções sobre como usar o Controle.](./images/using-assurance/create-new-session.png)

Agora você pode inserir um nome para identificar a sessão e, em seguida, fornecer um **[!UICONTROL URL básica]** (URL de deep linking para seu aplicativo). Após fornecer esses detalhes, selecione **[!UICONTROL Próximo]**.

>[!INFO]
>
>O URL base é a definição raiz usada para iniciar seu aplicativo a partir de um URL. Um URL de sessão é gerado pelo qual você pode iniciar a sessão de Controle. Um exemplo de valor pode ser: `myapp://default` No **[!UICONTROL URL básica]** digite a definição do deep link básico do seu aplicativo.

![O fluxo de trabalho completo da criação de uma nova sessão é exibido.](./images/using-assurance/create-session.gif)

## Conectar-se a uma sessão

Depois de criar uma sessão, verifique se é possível visualizar o **[!UICONTROL Criar nova sessão]** agora mostra um link, um código QR e um PIN.

![Uma caixa de diálogo que mostra as opções para se conectar à sua sessão de Controle é exibida.](./images/using-assurance/create-new-session-pin.png)

Se esta caixa de diálogo for exibida, você pode usar o aplicativo de câmera do seu dispositivo para digitalizar o código QR e abrir seu aplicativo ou copiar o link e abrir em seu aplicativo. Quando seu aplicativo é iniciado, a tela de entrada do PIN deve ser exibida sobreposta. Digite o PIN na etapa anterior e pressione **[!UICONTROL Connect]**.

Você pode verificar se o aplicativo está conectado ao Controle quando o ícone do Adobe Experience Platform (Adobe vermelho &quot;A&quot;) é exibido no aplicativo.

![O fluxo de trabalho completo de conexão do aplicativo a uma sessão de Controle é exibido.](./images/using-assurance/connect-session.gif)

## Exportar uma sessão

Para exportar uma sessão de Controle, na página de detalhes das sessões do seu aplicativo, selecione **[!UICONTROL Exportar para JSON]** em uma sessão:

![Exportar uma sessão](./images/using-assurance/export-session.png)

A opção de exportação respeita os resultados do filtro de pesquisa e apenas exporta os eventos exibidos na visualização de evento. Por exemplo, se você pesquisou eventos de &quot;rastreamento&quot; e, em seguida, selecionou **[!UICONTROL Exportar para JSON]**, somente os resultados do evento &quot;track&quot; são exportados.
