---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Monitorar os fluxos de contas e de conjunto de dados
topic: overview
translation-type: tm+mt
source-git-commit: fc0a406bdea7b31e046d02427805a9deba557e93

---


# Monitorar os fluxos de contas e de conjunto de dados

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para exibir contas e fluxos de conjunto de dados existentes da área de trabalho *Fontes* .

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

- [Sistema](../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   - [Noções básicas da composição](../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [Perfil](../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

## Monitorar contas

Faça logon na <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **Fontes** na barra de navegação esquerda para acessar a área de trabalho *Fontes* . A tela *Catálogo* exibe várias fontes com as quais você pode criar fluxos de conjunto de dados de contas. Cada fonte mostra o número de contas e fluxos de conjunto de dados existentes associados a elas.

Selecione *Contas* no cabeçalho superior para visualização contas existentes.

![catálogo](../../images/tutorials/monitor/catalog.png)

As páginas *Contas* são exibidas. Nesta página há uma lista de contas visualizáveis, incluindo informações sobre sua origem, nome de usuário, número de fluxos de conjunto de dados e data de criação.

Selecione o ícone na parte superior esquerda para abrir a janela de classificação.

![account](../../images/tutorials/monitor/accounts-list.png)

O painel de classificação permite acessar contas de uma fonte específica. Selecione a fonte com a qual deseja trabalhar e selecione a conta na lista à direita.

![selecionar contas](../../images/tutorials/monitor/accounts-sort.png)

Na página *Contas* , é possível visualização uma lista dos fluxos existentes do conjunto de dados associados à conta acessada. Selecione o fluxo do conjunto de dados que deseja visualização.

![página de contas](../../images/tutorials/monitor/dataset-flows.png)

A tela atividade *do fluxo do* Conjunto de dados é exibida. Esta página exibe a taxa de mensagens que estão sendo consumidas na forma de um gráfico.

![dataset-flow-atividade](../../images/tutorials/monitor/dataset-flows-activity.png)

## Monitorar fluxos de conjunto de dados

Os fluxos de conjunto de dados podem ser acessados diretamente da página *Catálogo* sem exibir *Contas*. Selecione Fluxos *de conjunto de* dados do cabeçalho superior para visualização de uma lista de fluxos de conjunto de dados existentes.

![fluxos de conjunto de dados](../../images/tutorials/monitor/dataset-flows-list.png)

Semelhante às contas, você pode classificar a lista de fluxos de conjunto de dados usando o ícone de classificação na parte superior esquerda. Selecione a fonte que deseja visualização e selecione o fluxo do conjunto de dados na lista à direita.

![select-dataset-flows](../../images/tutorials/monitor/dataset-flows-sort.png)

A tela atividade *do fluxo do* Conjunto de dados é exibida. Esta página exibe a taxa de mensagens que estão sendo consumidas na forma de um gráfico.

![dataset-flow-atividade](../../images/tutorials/monitor/dataset-flows-activity.png)

Para obter mais informações sobre monitoramento de conjuntos de dados e ingestão, consulte o tutorial sobre [monitoramento de fluxos de dados](../../../ingestion/quality/monitor-data-flows.md)de fluxo contínuo.

## Próximas etapas

Ao seguir este tutorial, você acessou com êxito contas e fluxos de conjunto de dados existentes da área de trabalho *Fontes* . Os dados recebidos agora podem ser usados pelos serviços de plataforma downstream, como o Perfil do cliente em tempo real e a Área de trabalho de análise de dados. Consulte os seguintes documentos para obter mais detalhes:

- [Visão geral do Perfil do cliente em tempo real](../../../profile/home.md)
- [Visão geral da Análise do espaço de trabalho da Data Science](../../../data-science-workspace/home.md)