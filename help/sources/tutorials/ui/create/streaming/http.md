---
title: Criar uma conexão de transmissão da API HTTP usando a interface
description: Este guia de interface ajudará você a criar uma conexão de transmissão usando o Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: de721d204cda8e55c72ac5f530b89b2275d94306
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---


# Criar um [!DNL HTTP API] conexão de transmissão usando a interface

Este tutorial fornece etapas para criar uma conexão de origem de transmissão usando o [!UICONTROL Origens] espaço de trabalho.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   - [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

## Criar uma conexão de streaming

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No **[!UICONTROL Streaming]** categoria, selecione **[!UICONTROL API HTTP]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/http/catalog.png)

A variável **[!UICONTROL Conectar conta de API HTTP]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta da API HTTP com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próxima]** para continuar.

![conta existente](../../../../images/tutorials/create/http/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome de conta e uma descrição opcional. Você também terá a opção de fornecer as seguintes propriedades de configuração:

- **[!UICONTROL Autenticação]:** Essa propriedade determina se a conexão de streaming requer ou não autenticação. A autenticação garante que os dados sejam coletados de fontes confiáveis. Se você estiver lidando com Informações de identificação pessoal (PII), essa propriedade deve ser ativada. Por padrão, essa propriedade está desativada.
- **[!UICONTROL Compatível com XDM]:** Essa propriedade indica se essa conexão de transmissão enviará eventos compatíveis com esquemas XDM. Por padrão, essa propriedade está desativada.

Quando terminar, selecione **[!UICONTROL Conectar à origem]** e selecione **[!UICONTROL Próxima]** para continuar.

![nova conta](../../../../images/tutorials/create/http/new.png)

## Selecionar dados

Depois de criar a conexão da API HTTP, a variável **[!UICONTROL Selecionar dados]** é exibida, fornecendo uma interface para carregar e visualizar seus dados.

Selecionar **[!UICONTROL Fazer upload de arquivos]** para carregar seus dados. Como alternativa, você pode arrastar e soltar seus dados na [!UICONTROL Arrastar e soltar arquivos] seção da interface.

![add-data](../../../../images/tutorials/create/http/add-data.png)

Com os dados carregados, você pode usar o lado direito da interface para visualizar a hierarquia de arquivos. Selecionar **[!UICONTROL Próxima]** para continuar.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## Mapear campos de dados para um esquema XDM

A variável [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os dados de origem para um conjunto de dados da Platform.

A variável [!DNL HTTP API] A fonte oferece suporte à assimilação de arquivos JSON. Os arquivos JSON não exigem configuração manual se estiverem marcados como reclamação XDM. Caso contrário, você deve configurar explicitamente o mapeamento.

Escolha um conjunto de dados para os dados de entrada que serão assimilados. Você pode usar um conjunto de dados existente ou criar um novo.

### Criar um novo conjunto de dados

Para criar um novo conjunto de dados, selecione **[!UICONTROL Novo conjunto de dados]**. No formulário exibido, forneça o nome, uma descrição opcional, bem como o schema de destino para o conjunto de dados. Se você selecionar um [!DNL Profile]esquema habilitado para, você pode escolher se o conjunto de dados também deve ser [!DNL Profile]-habilitado.

![novo conjunto de dados](../../../../images/tutorials/create/http/new-dataset.png)

### Usar um conjunto de dados existente

Para usar um conjunto de dados existente, selecione **[!UICONTROL Conjunto de dados existente]**. No formulário exibido, selecione o conjunto de dados que deseja usar. Após selecionar um conjunto de dados, você pode escolher se ele deve ser [!DNL Profile]-habilitado.

![conjunto de dados existente](../../../../images/tutorials/create/http/existing-dataset.png)

### Mapear campos padrão

Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre o uso da interface do mapeador e campos calculados, consulte o [Guia da interface de preparação de dados](../../../../../data-prep/ui/mapping.md).

Para adicionar um novo campo de origem, selecione **[!UICONTROL Adicionar novo mapeamento]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Um novo emparelhamento de campo de origem e campo de destino é exibido. Para adicionar um novo campo de origem, selecione o ícone de seta ao lado do [!UICONTROL Selecionar campo de origem] barra de entrada.

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

A variável [!UICONTROL Selecionar atributos] permite explorar a hierarquia de arquivos e selecionar um campo de origem específico para mapear para um campo XDM de destino. Depois de selecionar o campo de origem que deseja mapear, selecione **[!UICONTROL Selecionar]** para continuar.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

Com um campo de origem selecionado, agora é possível identificar o campo XDM de destino apropriado para o qual mapear. Selecione o ícone do schema na seção target field.

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

A variável [!UICONTROL Mapear campo de origem para campo de destino] é exibida, fornecendo uma interface para explorar o esquema do conjunto de dados de destino. Selecione o campo de destino que corresponde ao campo de origem e selecione **[!UICONTROL Selecionar]** para continuar.

![mapear para campo de destino](../../../../images/tutorials/create/http/map-to-target-field.png)

Depois que todos os campos de origem forem mapeados para os campos XDM de destino apropriados, selecione **[!UICONTROL Próxima]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Detalhes do fluxo de dados

A variável **[!UICONTROL Detalhes do fluxo de dados]** é exibida. Nesta página, você pode fornecer detalhes sobre o fluxo de dados criado fornecendo um nome e uma descrição opcional.

Depois de fornecer detalhes para o fluxo de dados, selecione **[!UICONTROL Próxima]**.

![detalhes do fluxo de dados](../../../../images/tutorials/create/http/dataflow-detail.png)

## Consulte a seção

A variável **[!UICONTROL Revisão]** é exibida, permitindo que você revise os detalhes do fluxo de dados antes que ele seja criado. Os detalhes estão agrupados nas seguintes categorias:

- **[!UICONTROL Conexão]**: mostra o nome da conta, a plataforma de origem e o nome da origem.
- **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: mostra o conjunto de dados de destino e o esquema ao qual o conjunto de dados pertence.

Depois de confirmar que os detalhes estão corretos, selecione **[!UICONTROL Concluir]**.

![revisão](../../../../images/tutorials/create/http/review.png)

## Obter URL de ponto de extremidade de streaming

Com a conexão criada, a página de detalhes das origens é exibida. Esta página mostra detalhes da conexão recém-criada, incluindo fluxos de dados executados anteriormente, ID e URL do ponto de extremidade de streaming.

![endpoint](../../../../images/tutorials/create/http/endpoint.png)

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão HTTP de transmissão, permitindo usar o endpoint de transmissão para acessar uma variedade de [!DNL Data Ingestion] APIs. Para obter instruções sobre como criar uma conexão de transmissão na API, leia o [tutorial de criação de uma conexão de transmissão](../../../api/create/streaming/http.md).

Para saber como transmitir dados para a Platform, leia o tutorial sobre [transmissão de dados de série temporal](../../../../../ingestion/tutorials/streaming-time-series-data.md) ou o tutorial em [dados de registro de transmissão](../../../../../ingestion/tutorials/streaming-record-data.md).
