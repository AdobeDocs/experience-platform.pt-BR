---
keywords: Experience Platform;home;popular topics;conexão de fluxo;criar conexão de fluxo;uguide;tutorial;criar uma conexão de fluxo;ingestão de fluxo;;home;popular topics;streaming connection;create streaming connection;ui guide;tutorial;create a streaming connection;streaming ingestion;ingestion;ingestão;
solution: Experience Platform
title: Criar uma conexão de transmissão usando a interface do usuário
topic: tutorial
type: Tutorial
description: Este guia de interface de usuário o ajudará a criar uma conexão de streaming usando o Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a4019227abaddd9dbe143899d273580ebf21849e
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---


# Criar uma conexão de streaming usando a interface do usuário

Este guia de interface de usuário o ajudará a criar uma conexão de streaming usando o Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

## Criar uma conexão de streaming

Depois de fazer logon na interface do usuário [!DNL Experience Platform], selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catalog]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Streaming]**, selecione **[!UICONTROL API HTTP]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector de streaming HTTP.

![](../../../../images/tutorials/create/http/catalog.png)

A página **[!UICONTROL Connect HTTP API account]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome de conta e uma descrição opcional. Você também terá a opção de fornecer as seguintes propriedades de configuração:

- **[!UICONTROL Autenticação]:** Essa propriedade determina se a conexão de streaming exige ou não autenticação. A autenticação garante que os dados sejam coletados de fontes confiáveis. Se você estiver lidando com Informações pessoais identificáveis (PII), essa propriedade deverá ser ativada. Por padrão, essa propriedade está desativada.
- **[!UICONTROL Compatibilidade] do Schema XDM:** essa propriedade indica se essa conexão de streaming enviará eventos compatíveis com schemas XDM. Por padrão, essa propriedade está ativada.

Quando terminar, selecione **[!UICONTROL Ligar à origem]**, seguido por **[!UICONTROL Seguinte]** para prosseguir.

![](../../../../images/tutorials/create/http/new-account.png)

### Conta existente

Para conectar-se usando credenciais existentes, selecione a conexão da API HTTP que deseja usar e, em seguida, selecione **[!UICONTROL Próximo]** para continuar.

![](../../../../images/tutorials/create/http/existing-account.png)

## Selecionar dados

Depois de criar a conexão da API HTTP, a etapa **[!UICONTROL Selecionar dados]** é exibida, fornecendo uma interface para escolher o conjunto de dados com o qual se conectar. Você tem a opção de criar um novo conjunto de dados ou se conectar a um conjunto de dados existente.

### Criar um novo conjunto de dados

Para criar um novo conjunto de dados, selecione **[!UICONTROL Novo conjunto de dados]**. No formulário exibido, forneça o nome, uma descrição opcional, bem como o schema do público alvo para o conjunto de dados. Se você selecionar um schema habilitado para Perfis, poderá escolher se o conjunto de dados também deve estar habilitado para Perfis.

![](../../../../images/tutorials/create/http/new-dataset.png)

### Usar um conjunto de dados existente

Para usar um conjunto de dados existente, selecione **[!UICONTROL Conjunto de dados existente]**. No formulário exibido, selecione o conjunto de dados que deseja usar. Depois de selecionar um conjunto de dados, você pode escolher se o conjunto de dados deve estar habilitado para Perfil.

![](../../../../images/tutorials/create/http/existing-dataset.png)

## Detalhe do fluxo de dados

A etapa **[!UICONTROL Dataflow detail]** é exibida. Nesta página, você pode fornecer detalhes para o fluxo de dados criado, fornecendo um nome e uma descrição opcional.

Depois de fornecer detalhes para o fluxo de dados, selecione **[!UICONTROL Next]**.

![](../../../../images/tutorials/create/http/dataflow-detail.png)

## Revisão

A etapa **[!UICONTROL Revisar]** é exibida, permitindo que você analise os detalhes do seu fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

- **[!UICONTROL Conexão]**: Mostra o nome da conta, a plataforma de origem e o nome de origem.
- **[!UICONTROL Atribuir campos]** de conjunto de dados e mapa: Mostra o conjunto de dados do público alvo e o schema ao qual o conjunto de dados adere.

Depois de confirmar se os detalhes estão corretos, selecione **[!UICONTROL Concluir]**.

![](../../../../images/tutorials/create/http/review.png)

## Obter URL de ponto de extremidade de streaming

Com a conexão criada, a página de detalhes das fontes é exibida. Esta página mostra detalhes da conexão recém-criada, incluindo fluxos de dados executados anteriormente, ID e URL de ponto de extremidade de streaming.

![](../../../../images/tutorials/create/http/get-streaming-url.png)

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão HTTP de streaming, permitindo que você use o terminal de streaming para acessar várias APIs [!DNL Data Ingestion]. Para obter instruções para criar uma conexão de streaming na API, leia o tutorial [criação de uma conexão de streaming](../../../api/create/streaming/http.md).

Para saber como transmitir dados para a Plataforma, leia o tutorial em [streaming time series data](../../../../../ingestion/tutorials/streaming-time-series-data.md) ou o tutorial em [streaming record data](../../../../../ingestion/tutorials/streaming-record-data.md).
