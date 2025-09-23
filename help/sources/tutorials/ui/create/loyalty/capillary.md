---
title: Conectar o Capilar ao Experience Platform usando a interface
description: Saiba como conectar o Capilary ao Experience Platform usando a interface do usuário
hide: true
hidefromtoc: true
source-git-commit: 7b733831932c48240340b0a2136e15f5d2144635
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 5%

---

# Conectar o [!DNL Capillary] ao Experience Platform usando a interface

Leia este guia para saber como conectar seu banco de dados do [!DNL Capillary] ao Adobe Experience Platform usando o espaço de trabalho de origens na interface do usuário do Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

## Navegar pelo catálogo de origens

Na interface do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho *[!UICONTROL Fontes]*. Selecione a categoria apropriada no painel *[!UICONTROL Categorias]* Como alternativa, use a barra de pesquisa para navegar até a fonte específica que deseja usar.

Para usar [!DNL Capillary], selecione o cartão de origem **[!UICONTROL Eventos Capilares de Streaming]** em *[!UICONTROL Fidelidade]* e selecione **[!UICONTROL Adicionar dados]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Configurar]** quando uma determinada origem ainda não tem uma conta autenticada. Após a criação de uma conta autenticada, esta opção será alterada para **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes na interface do usuário com o cartão Eventos de Transmissão Capilares selecionado.](../../../../images/tutorials/create/capillary/catalog.png)

## Selecionar dados

Em seguida, use a interface *[!UICONTROL Selecionar dados]* para carregar um arquivo JSON de amostra para definir seu esquema de origem. Durante essa etapa, é possível usar a interface de pré-visualização para exibir a estrutura de arquivo do payload. Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de seleção de dados do fluxo de trabalho de fontes](../../../../images/tutorials/create/capillary/select-data.png)

## Detalhes do fluxo de dados

Em seguida, você deve fornecer informações sobre o conjunto de dados e o fluxo de dados.

### Detalhes do conjunto de dados

Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas). Os dados assimilados com sucesso na Experience Platform são mantidos no data lake como conjuntos de dados.

Durante essa etapa, é possível usar um conjunto de dados existente ou criar um novo.

>[!NOTE]
>
>Independentemente de você usar um conjunto de dados existente ou criar um novo, você deve garantir que seu conjunto de dados esteja **habilitado para assimilação do Perfil**.

+++Selecione para obter as etapas para ativar a Assimilação de perfil, Diagnóstico de erro e Assimilação parcial.

Se o seu conjunto de dados estiver habilitado para o Perfil de cliente em tempo real, durante essa etapa você poderá alternar para **[!UICONTROL o conjunto de dados do perfil]** para habilitar seus dados para assimilação de perfil. Você também pode usar esta etapa para habilitar o **[!UICONTROL Diagnóstico de erro]** e a **[!UICONTROL Assimilação parcial]**.

* **[!UICONTROL Diagnóstico de erro]**: selecione **[!UICONTROL Diagnóstico de erro]** para instruir a origem a produzir o diagnóstico de erro que você poderá consultar posteriormente ao monitorar a atividade do conjunto de dados e o status do fluxo de dados.
* **[!UICONTROL Assimilação parcial]**: a assimilação parcial de lotes é a capacidade de assimilar dados que contêm erros, até um determinado limite configurável. Esse recurso permite assimilar com sucesso todos os seus dados precisos na Experience Platform, enquanto todos os seus dados incorretos são armazenados em lote separadamente com informações sobre por que são inválidos.

+++

### Detalhes do fluxo de dados

Depois que o conjunto de dados é configurado, você deve fornecer detalhes sobre o fluxo de dados, incluindo um nome, uma descrição opcional e configurações de alerta.

![A interface de detalhes do fluxo de dados](../../../../images/tutorials/create/capillary/dataflow-detail.png)

| Configurações de fluxo de dados | Descrição |
| --- | --- |
| Nome do fluxo de dados | O nome do fluxo de dados.  Por padrão, esse campo usará o nome do arquivo que está sendo importado. |
| Descrição | (Opcional) Uma breve descrição do fluxo de dados. |
| Alertas | O Experience Platform pode produzir alertas baseados em eventos, nos quais os usuários podem assinar. Todas essas opções dependem de um fluxo de dados em execução para acioná-los.  Para obter mais informações, leia a [visão geral dos alertas](../../alerts.md) <ul><li>**Início da Execução do Fluxo de Dados de Fontes**: selecione este alerta para receber uma notificação quando a execução do fluxo de dados começar.</li><li>**Êxito na Execução do Fluxo de Dados de Fontes**: selecione este alerta para receber uma notificação se o fluxo de dados terminar sem erros.</li><li>**Falha na execução do fluxo de dados de fontes**: selecione este alerta para receber uma notificação se a execução do fluxo de dados terminar com erros.</li></ul> |

{style="table-layout:auto"}

## Mapeamento

Use a interface de mapeamento para mapear os dados de origem para os campos de esquema apropriados antes de assimilar dados na Experience Platform.  Para obter mais informações, leia o [guia de mapeamento na interface](../../../../../data-prep/ui/mapping.md).

![A interface de mapeamento para Capilar.](../../../../images/tutorials/create/capillary/mappings.png)

## Revisar

A etapa *[!UICONTROL Revisar]* é exibida, permitindo que você revise os detalhes do fluxo de dados antes que ele seja criado. Os detalhes estão agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra o nome da conta, a plataforma de origem e o nome de origem.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: mostra o conjunto de dados de destino e o esquema ao qual o conjunto de dados pertence.

Depois de confirmar que os detalhes estão corretos, selecione **[!UICONTROL Concluir]**.

![A etapa de revisão no fluxo de trabalho de fontes.](../../../../images/tutorials/create/capillary/review.png)

## Recuperar o URL do ponto de extremidade de streaming

Com a conexão criada, a página de detalhes das origens é exibida. Esta página mostra detalhes da conexão recém-criada, incluindo fluxos de dados executados anteriormente, ID e URL do ponto de extremidade de streaming.

![A URL da extremidade de streaming.](../../../../images/tutorials/create/capillary/endpoint-url.png)