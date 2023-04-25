---
title: Criar Uma Conexão De Transmissão Do Shopify E Um Fluxo De Dados Na Interface Do Usuário
description: Saiba como criar uma conexão de origem e fluxo de dados do Shopify Streaming usando a interface do usuário da plataforma
badge: Beta
exl-id: 3368ecf6-0c61-49ce-bc9c-29ee50b3f037
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# Criar uma conexão de origem e um fluxo de dados para [!DNL Shopify Streaming] dados que usam a interface do usuário

Este tutorial fornece etapas para criar um [!DNL Shopify Streaming] conexão de origem e fluxo de dados usando a interface do usuário da plataforma.

## Introdução {#getting-started}

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

>[!IMPORTANT]
>
>Este tutorial requer que você tenha concluído a configuração de pré-requisito para sua [!DNL Shopify Streaming] conta. Para obter as etapas sobre como configurar sua conta, leia o [[!DNL Shopify Streaming] visão geral](../../../../connectors/ecommerce/shopify-streaming.md).

## Conecte seu [!DNL Shopify Streaming] account

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **comércio eletrônico** categoria , selecione [!DNL Shopify Streaming]e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes de Experience Platform](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## Selecionar dados

O **[!UICONTROL Selecionar dados]** será exibida, fornecendo uma interface para selecionar os dados trazidos para a plataforma.

* A parte esquerda da interface é um navegador que permite visualizar os fluxos de dados disponíveis em sua conta;
* A parte direita da interface permite visualizar até 100 linhas de dados de um arquivo JSON.

Selecionar **[!UICONTROL Upload de arquivos]** para carregar um arquivo JSON do sistema local. Como alternativa, você pode arrastar e soltar o arquivo JSON que deseja fazer upload no [!UICONTROL Arrastar e soltar arquivos] painel.

![A etapa adicionar dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/shopify-streaming/select-data.png)

Depois que o arquivo é carregado, a interface de visualização é atualizada para exibir uma pré-visualização do esquema carregado. A interface de visualização permite inspecionar o conteúdo e a estrutura de um arquivo. Também é possível usar a variável [!UICONTROL Campo de pesquisa] para acessar itens específicos dentro do esquema.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de visualização do fluxo de trabalho de fontes.](../../../../images/tutorials/create/shopify-streaming/preview.png)

## Detalhes do fluxo de dados

O **Detalhes do fluxo de dados** é exibida, fornecendo opções para usar um conjunto de dados existente ou estabelecer um novo conjunto de dados para o fluxo de dados, bem como uma oportunidade de fornecer um nome e uma descrição para o fluxo de dados. Durante essa etapa, você também pode definir as configurações para assimilação de perfil, diagnóstico de erro, assimilação parcial e alertas.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de detalhes do fluxo de dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## Mapeamento

O [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

A Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema de destino ou conjunto de dados selecionado. Você pode ajustar manualmente as regras de mapeamento de acordo com seus casos de uso. Com base em suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem em valores calculados ou calculados. Para obter etapas abrangentes sobre o uso da interface do mapeador e dos campos calculados, consulte o [Guia da interface do usuário de preparação de dados](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Depois que os dados de origem forem mapeados com êxito, selecione **[!UICONTROL Próximo]**.

![A etapa de mapeamento do fluxo de trabalho de origens.](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## Consulte a seção

O **[!UICONTROL Revisão]** é exibida, permitindo que você revise o novo fluxo de dados antes de criá-lo. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: Mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e o número de colunas dentro desse arquivo de origem.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e permitir que o fluxo de dados seja criado.

![A etapa de revisão do fluxo de trabalho de fontes.](../../../../images/tutorials/create/shopify-streaming/review.png)

## Obter o URL do terminal de transmissão

Com o fluxo de dados criado, agora é possível recuperar o URL do terminal de transmissão. Esse terminal será usado para se inscrever no webhook, permitindo que sua fonte de transmissão se comunique com o Experience Platform.

Para recuperar o terminal de transmissão, acesse [!UICONTROL Atividade do fluxo de dados] página do fluxo de dados que você acabou de criar e copiar o ponto de extremidade da parte inferior do [!UICONTROL Propriedades] painel.

![O endpoint de transmissão na atividade de fluxo de dados.](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão de origem e um fluxo de dados para seu [!DNL Shopify Streaming] conta. Para obter instruções sobre como conectar seu [!DNL Shopify Streaming] leia o tutorial em [criar uma conexão de origem e um fluxo de dados para fluxo [!DNL Shopify] dados usando a API do Serviço de Fluxo](../../../api/create/ecommerce/shopify-streaming.md).
