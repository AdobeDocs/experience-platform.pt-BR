---
title: Criar Uma Conexão De Transmissão E Um Fluxo De Dados Do Shopify Na Interface Do Usuário
description: Saiba como criar uma conexão de origem e fluxo de dados de transmissão do Shopify usando a interface do usuário da Platform
badge: Beta
exl-id: d53f4ab5-8bdc-4647-83d5-ee898abda0f2
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 1%

---

# Criar uma conexão de origem e um fluxo de dados para dados do [!DNL Shopify Streaming] usando a interface

Este tutorial fornece etapas para criar uma conexão de origem e um fluxo de dados do [!DNL Shopify Streaming] usando a interface do usuário da Platform.

## Introdução {#getting-started}

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

>[!IMPORTANT]
>
>Este tutorial requer que você tenha concluído a configuração de pré-requisito da sua conta [!DNL Shopify Streaming]. Para obter as etapas de configuração da sua conta, leia a [[!DNL Shopify Streaming] visão geral](../../../../connectors/ecommerce/shopify-streaming.md).

## Conectar sua conta do [!DNL Shopify Streaming]

Na interface da Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **comércio eletrônico**, selecione [!DNL Shopify Streaming] e **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes de Experience Platform](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## Selecionar dados

A etapa **[!UICONTROL Selecionar dados]** é exibida, fornecendo uma interface para que você selecione os dados que trará para a Platform.

* A parte esquerda da interface é um navegador que permite visualizar os fluxos de dados disponíveis em sua conta;
* A parte direita da interface permite visualizar até 100 linhas de dados de um arquivo JSON.

Selecione **[!UICONTROL Carregar arquivos]** para carregar um arquivo JSON do sistema local. Como alternativa, você pode arrastar e soltar o arquivo JSON que deseja carregar no painel [!UICONTROL Arrastar e soltar arquivos].

![A etapa para adicionar dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/shopify-streaming/select-data.png)

Depois que o arquivo for carregado, a interface de visualização será atualizada para exibir uma visualização do esquema carregado. A interface de visualização permite inspecionar o conteúdo e a estrutura de um arquivo. Você também pode usar o utilitário [!UICONTROL Campo de pesquisa] para acessar itens específicos de dentro do esquema.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de visualização do fluxo de trabalho de fontes.](../../../../images/tutorials/create/shopify-streaming/preview.png)

## Detalhes do fluxo de dados

A etapa **Detalhes do fluxo de dados** é exibida, fornecendo opções para usar um conjunto de dados existente ou estabelecer um novo para o fluxo de dados, bem como uma oportunidade de fornecer um nome e uma descrição para o fluxo de dados. Durante essa etapa, você também pode definir configurações para Assimilação de perfil, diagnóstico de erro, assimilação parcial e alertas.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de detalhes do fluxo de dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## Mapeamento

A etapa [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

A Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso. Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre como usar a interface do mapeador e campos calculados, consulte o [Guia da Interface do Preparo de Dados](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Depois que os dados de origem forem mapeados com êxito, selecione **[!UICONTROL Próximo]**.

![A etapa de mapeamento do fluxo de trabalho de origens.](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## Revisar

A etapa **[!UICONTROL Revisão]** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e o número de colunas nesse arquivo de origem.
* **[!UICONTROL Atribuir campos de conjunto de dados e mapa]**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados pertence.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados seja criado.

![A etapa de revisão do fluxo de trabalho de fontes.](../../../../images/tutorials/create/shopify-streaming/review.png)

## Obter o URL do ponto de extremidade de streaming

Com o fluxo de dados de transmissão criado, agora é possível recuperar o URL do ponto de extremidade de transmissão. Esse endpoint será usado para assinar seu webhook, permitindo que a fonte de streaming se comunique com o Experience Platform.

Para recuperar o ponto de extremidade de streaming, vá para a página [!UICONTROL Atividade de fluxo de dados] do fluxo de dados que você acabou de criar e copie o ponto de extremidade da parte inferior do painel [!UICONTROL Propriedades].

![A extremidade de streaming na atividade de fluxo de dados.](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão de origem e um fluxo de dados para sua conta do [!DNL Shopify Streaming]. Para obter instruções sobre como conectar sua conta do [!DNL Shopify Streaming] usando a API, leia o tutorial em [criando uma conexão de origem e um fluxo de dados para transmitir dados [!DNL Shopify] usando a API de Serviço de Fluxo](../../../api/create/ecommerce/shopify-streaming.md).
