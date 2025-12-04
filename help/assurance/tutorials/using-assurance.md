---
title: Utilização do Adobe Experience Platform Assurance
description: Este guia explica como usar o Adobe Experience Platform Assurance após sua instalação e implementação.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: f8576e7f7e1da7351f7860cba27d5d09d0161132
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 28%

---

# Utilização do Adobe Experience Platform Assurance

Este tutorial explica como usar o Adobe Experience Platform Assurance. Para obter instruções sobre como instalar e implementar a extensão do Adobe Experience Platform Assurance, leia o tutorial sobre [implementação da extensão do Assurance](./implement-assurance.md).

## Criar sessões

Depois de fazer logon na [interface do usuário do Assurance](https://experience.adobe.com/assurance), você pode selecionar **[!UICONTROL Create Session]** para começar a criar uma sessão.

![O botão Criar sessão é realçado, mostrando onde você pode criar uma sessão.](./images/using-assurance/create-session.png)

A caixa de diálogo **[!UICONTROL Create New Session]** é exibida com duas opções para criar uma sessão:

### Conexão de deep link

Selecione esta opção para gerar um URL, código QR e PIN exclusivo da sessão. Digitalize o código QR ou abra manualmente o link de sessão no aplicativo e insira o PIN para estabelecer a conexão.

Selecione **[!UICONTROL Deep link connect]** e prossiga selecionando **[!UICONTROL Start]**.

![A caixa de diálogo Criar Nova Sessão mostrando a opção de conexão Deep link selecionada.](./images/using-assurance/create-new-session-deep-link.png)

Agora você pode inserir um nome para identificar a sessão e fornecer um **[!UICONTROL Base URL]** (URL de deep linking do seu aplicativo). Depois de fornecer esses detalhes, selecione **[!UICONTROL Next]**.

>[!INFO]
>
>O URL base é a definição raiz usada para iniciar seu aplicativo a partir de um URL. Um URL de sessão é gerado, a partir do qual você pode iniciar a sessão do Assurance. Um exemplo de valor pode se parecer com: `myapp://default` No campo **[!UICONTROL Base URL]**, digite a definição base do deep link do seu aplicativo.

![Os campos de entrada Nome da sessão e URL Base são mostrados.](./images/using-assurance/create-session-form-deep-link.png)

### Conexão rápida

Acione uma conexão do aplicativo e seu dispositivo aparecerá em uma lista de dispositivos disponíveis. Selecione **[!UICONTROL Quick connect]** para criar a sessão do Assurance.

#### Pré-requisitos

Antes de usar a Conexão rápida, verifique se o aplicativo tem as versões e a implementação necessárias do SDK:

**Requisitos do Android SDK:**

- Mobile Core v3.1.0 ou posterior
- Adobe Journey Optimizer v3.1.0 ou posterior
- Adobe Experience Platform Assurance v3.0.4 ou posterior

**Requisitos do iOS SDK:**

- Mobile Core v5.2.0 ou posterior
- Adobe Journey Optimizer v5.1.1 ou posterior
- Adobe Experience Platform Assurance v5.0.0 ou posterior

**Implementação:**

Seu aplicativo deve implementar a API [`startSession` &#x200B;](https://developer.adobe.com/client-sdks/home/base/assurance/api-reference/#startsession-quick-connect) para acionar a conexão do Assurance. Normalmente, essa chamada de API é incluída em um conjunto de ações ou acionada no aplicativo.

#### Criando uma sessão de conexão rápida

![A caixa de diálogo Criar Nova Sessão mostrando a opção Conexão Rápida selecionada.](./images/using-assurance/create-new-session-quick-connect.png)

Selecione **[!UICONTROL Quick connect]** e prossiga selecionando **[!UICONTROL Start]**, você verá a interface do seletor de dispositivos:

1. **Acionar a conexão do Assurance** - No aplicativo móvel ou na implementação, acione a ação que inicia a conexão do Assurance usando a API `startSession`. Isso tornará seu dispositivo detectável.

2. **Selecione e conecte seu dispositivo** - Quando o dispositivo aparecer na lista de dispositivos disponíveis, selecione-o e clique em **[!UICONTROL Connect]**.

![A interface do seletor de dispositivos de Conexão Rápida mostrando os dispositivos disponíveis.](./images/using-assurance/quick-connect-device-picker.png)

## Conectar-se a uma sessão

As etapas para se conectar dependem do tipo de sessão que você está usando:

### Sessões de conexão de deep link

Para sessões criadas com **[!UICONTROL Deep Link Connect]**:

1. Navegue até a página de detalhes da sessão (para sessões existentes) ou prossiga da criação da sessão para ver o link, o código QR e o PIN
2. Use o aplicativo de câmera do dispositivo para digitalizar o código QR ou copie o link e abra-o no aplicativo
3. Quando o aplicativo for iniciado, você verá a tela de entrada do PIN sobreposta. Insira o PIN e pressione **[!UICONTROL Connect]**

![Uma caixa de diálogo mostrando as opções para se conectar à sua sessão do Assurance é exibida.](./images/using-assurance/deep-link-connection.png)

### Sessões de conexão rápida

Para sessões criadas com **[!UICONTROL Quick Connect]** (identificáveis por uma URL de sessão que começa com `adobeassurance://`), a conexão acontece automaticamente por meio da interface do seletor de dispositivos:

1. Navegue até a página de detalhes da sessão (para sessões existentes) ou continue a partir da criação da sessão
2. Na seção **[!UICONTROL Connect Device]**, você verá a interface do seletor de dispositivos
3. Acione o conjunto de ações no aplicativo para tornar o dispositivo detectável
4. Selecione seu dispositivo na lista e clique em **[!UICONTROL Connect]**

![A interface do seletor de dispositivos mostrando os dispositivos disponíveis para conexão.](./images/using-assurance/quick-connect-device-picker.png)

### Verificando conexão

Você pode conferir se seu aplicativo está conectado ao Assurance observando se o ícone da Adobe Experience Platform (“A” vermelho de Adobe) está sendo exibido no aplicativo.

## Exportar uma sessão

Para exportar uma sessão do Assurance, na página de detalhes das sessões do seu aplicativo, selecione **[!UICONTROL Export to JSON]** em uma sessão:

![Exportar uma sessão](./images/using-assurance/export-session.png)

A opção de exportação respeita os resultados do filtro de pesquisa e exporta somente os eventos mostrados na exibição de evento. Por exemplo, se você pesquisou por eventos &quot;track&quot; e depois selecionou **[!UICONTROL Export to JSON]**, somente os resultados do evento &quot;track&quot; são exportados.