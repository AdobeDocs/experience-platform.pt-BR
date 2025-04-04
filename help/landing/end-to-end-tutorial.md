---
keywords: Experience Platform;página inicial;tópicos populares;CJA;análise de jornada;análise de jornada do cliente;orquestração de campanhas;orquestração;jornada do cliente;jornada;orquestração de jornadas;capacidade;região
title: Exemplo de fluxo de trabalho de ponta a ponta do Adobe Experience Platform
description: Conheça o fluxo de trabalho básico completo do Adobe Experience Platform em alto nível.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 1%

---

# Fluxo de trabalho de exemplo completo do Adobe Experience Platform

A Adobe Experience Platform é o sistema mais poderoso, flexível e aberto do mercado para criar e gerenciar soluções completas que impulsionam a experiência do cliente. O Experience Platform permite que as organizações centralizem e padronizem dados e conteúdo de clientes de qualquer sistema e apliquem a ciência de dados e o aprendizado de máquina para melhorar o design e o delivery de experiências personalizadas.

Baseado em APIs RESTful, o Experience Platform expõe a funcionalidade completa do sistema para os desenvolvedores, oferecendo suporte à fácil integração de soluções corporativas usando ferramentas familiares. O Experience Platform permite obter uma visualização integral dos clientes ao assimilar os dados deles, segmentar os dados para os públicos que deseja direcionar e ativar esses públicos para um destino externo. O tutorial a seguir mostra um fluxo de trabalho completo, mostrando todas as etapas, desde a assimilação por meio de fontes até a ativação de público-alvo por meio de destinos.

![Fluxo de trabalho completo do Experience Platform](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Introdução

Esse fluxo de trabalho completo usa vários serviços da Adobe Experience Platform. Veja a seguir uma lista dos serviços usados neste fluxo de trabalho com links para suas visões gerais:

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente. Para melhor usar a Segmentação, verifique se seus dados são assimilados como perfis e eventos de acordo com as [práticas recomendadas para modelagem de dados](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md): fornece uma visão abrangente dos clientes e do comportamento deles ao unir as identidades de vários dispositivos e sistemas.
- [Fontes](../sources/home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] permite dividir os dados armazenados em [!DNL Experience Platform] que se relacionam a indivíduos (como clientes, clientes potenciais, usuários ou organizações) em grupos menores.
- [[!DNL Real-Time Customer Profile]](../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [Conjuntos de dados](../catalog/datasets/overview.md): a construção de armazenamento e gerenciamento para a persistência de dados em [!DNL Experience Platform].
- [Destinos](../destinations/home.md): os destinos são integrações pré-criadas com aplicativos usados com frequência que permitem a ativação contínua de dados do Experience Platform para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

## Criar um esquema do XDM

Antes de assimilar dados na Experience Platform, primeiro você deve criar um esquema XDM para descrever a estrutura desses dados. Ao assimilar seus dados na próxima etapa, você mapeará os dados recebidos para esse esquema. Para saber como criar um exemplo de esquema XDM, leia o tutorial sobre [criação de um esquema usando o Editor de esquemas](../xdm/tutorials/create-schema-ui.md).

O tutorial acima mostra como definir campos de identidade para seus esquemas. Um campo de identidade representa um campo que pode ser usado para identificar uma pessoa individual relacionada a um registro ou evento de série temporal. Os campos de identidade são um componente essencial na forma como os gráficos de identidade do cliente são construídos no Experience Platform, o que afeta como o Perfil do cliente em tempo real mescla fragmentos de dados diferentes para obter uma visão completa do cliente. Para obter mais detalhes sobre como visualizar gráficos de identidade no Experience Platform, consulte o tutorial sobre [como usar o visualizador de gráficos de identidade](../identity-service/features/identity-graph-viewer.md).

Você precisa ativar seu esquema para usar no Perfil do cliente em tempo real para que os perfis do cliente possam ser construídos a partir dos dados baseados no seu esquema. Consulte a seção sobre [habilitação de um esquema para o Perfil](../xdm/ui/resources/schemas.md#profile) no guia de interface do usuário de esquemas para obter mais informações.

## Assimilar seus dados na Experience Platform

Depois de criar um esquema XDM, você pode começar a trazer seus dados para o sistema.

Todos os dados trazidos para a Experience Platform são armazenados em conjuntos de dados individuais após a assimilação. Um conjunto de dados é uma coleção de registros de dados que mapeiam para um esquema XDM específico. Antes que seus dados possam ser usados pelo [!DNL Real-Time Customer Profile], o conjunto de dados em questão deve ser configurado especificamente. Para obter instruções completas sobre como habilitar um conjunto de dados para o Perfil, consulte o [guia da interface do usuário de conjuntos de dados](../catalog/datasets/user-guide.md#enable-profile) e o [tutorial da API de configuração de conjunto de dados](../profile/tutorials/dataset-configuration.md). Após configurar o conjunto de dados, você pode começar a assimilar dados nele.

O Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamentos baseados em nuvem, bancos de dados e muitas outras. Por exemplo, você pode assimilar seus dados usando o [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). Uma lista completa de origens disponíveis pode ser encontrada na [visão geral dos conectores de origem](../sources/home.md).

Se você usar o Amazon S3 como conector de origem, poderá seguir as instruções no tutorial da API em [criação de um conector Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md) ou no tutorial da interface do usuário em [criação de um conector Amazon S3](../sources/tutorials/ui/create/cloud-storage/s3.md) para saber como criar, conectar e assimilar dados no conector.

Para obter instruções mais detalhadas sobre conectores de origem, leia a [visão geral sobre conectores de origem](../sources/home.md). Para saber mais sobre o Serviço de Fluxo, a API da qual as fontes se baseiam, leia a [Referência da API do Serviço de Fluxo](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Depois que os dados forem trazidos para a Experience Platform por meio do conector de origem e armazenados em seu conjunto de dados habilitado para perfil, os perfis do cliente serão criados automaticamente com base nos dados de identidade configurados no esquema XDM.

Ao fazer upload dos dados para um novo conjunto de dados pela primeira vez ou ao configurar um novo processo ETL ou fonte de dados, é recomendável verificar cuidadosamente os dados para garantir que tenham sido carregados corretamente e que os perfis gerados contenham os dados esperados. Para obter mais informações sobre como acessar perfis de clientes na interface do usuário do Experience Platform, consulte o [Guia da interface do usuário do perfil do cliente em tempo real](../profile/ui/user-guide.md). Para obter detalhes sobre como acessar perfis usando a API de Perfil do cliente em tempo real, consulte o manual sobre [uso do ponto de extremidade de entidades](../profile/api/entities.md).

## Avalie seus dados

Depois de gerar perfis com sucesso a partir dos dados assimilados, você pode avaliar os dados usando a segmentação. A segmentação é o processo de definir atributos ou comportamentos específicos compartilhados por um subconjunto de indivíduos da loja de Perfis para distinguir um grupo comercializável de pessoas da sua base de clientes. Para saber mais sobre segmentação, leia a [visão geral do serviço de segmentação](../segmentation/home.md).

### Criar uma definição de segmento

Para começar, você deve criar uma definição de segmento para agrupar seus clientes e criar seu público-alvo. Uma definição de segmento é uma coleção de regras que você pode usar para definir o público-alvo que deseja direcionar. Para criar uma definição de segmento, siga as instruções no guia da interface do usuário sobre como usar o [Construtor de segmentos](../segmentation/ui/segment-builder.md) ou o tutorial da API sobre como [criar um segmento](../segmentation/tutorials/create-a-segment.md).

Depois de criar uma definição de segmento, anote a ID de definição de segmento.

### Avaliar a definição do segmento

Depois de criar a definição do segmento, você pode criar um job de segmento para avaliá-lo como uma instância única ou criar uma programação para avaliá-lo de forma contínua.

Para avaliar uma definição de segmento sob demanda, você pode criar um trabalho de segmento. Um trabalho de segmento é um processo assíncrono que cria um novo segmento de público-alvo com base na definição do segmento referenciado e nas políticas de mesclagem. Uma política de mesclagem é um conjunto de regras que a Experience Platform usa para determinar quais dados serão usados para criar perfis de clientes e quais dados serão priorizados quando houver discrepâncias entre fontes. Para saber como trabalhar com políticas de mesclagem, consulte o [guia da interface de políticas de mesclagem](../profile/merge-policies/ui-guide.md).

Depois que o trabalho de segmento é criado e avaliado, você pode obter informações sobre o segmento, como o tamanho do público-alvo ou erros que podem ter ocorrido durante o processamento. Para saber como criar um trabalho de segmento, incluindo todos os detalhes que você precisa fornecer, leia o [guia do desenvolvedor do trabalho de segmento](../segmentation/api/segment-jobs.md).

Para avaliar uma definição de segmento de forma contínua, você pode criar e ativar uma programação. Uma programação é uma ferramenta que pode ser usada para executar automaticamente um trabalho de segmento uma vez por dia em um horário especificado. Para saber como criar e habilitar um agendamento, siga as instruções no guia de API no [endpoint de agendamentos](../segmentation/api/schedules.md).

## Exportar os dados avaliados

Depois de criar seu trabalho de segmento único ou sua programação contínua, você pode criar um trabalho de exportação de segmento para exportar os resultados para um conjunto de dados ou exportá-los para um destino. As seções a seguir fornecem orientação sobre essas duas opções.

### Exportar os dados avaliados para um conjunto de dados

Após criar o job de segmento ocasional ou a programação contínua, você pode exportar os resultados criando um job de exportação de segmento. Um trabalho de exportação de segmento é uma tarefa assíncrona que envia informações sobre o público-alvo avaliado para um conjunto de dados.

Antes de criar um trabalho de exportação, primeiro crie um conjunto de dados para o qual exportar os dados. Para saber como criar um conjunto de dados, leia a seção sobre [criação de um conjunto de dados de destino](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) no tutorial sobre avaliação de um segmento, certificando-se de anotar a ID do conjunto de dados após a criação. Depois de criar um conjunto de dados, você pode criar um trabalho de exportação. Para saber como criar um trabalho de exportação, siga as instruções no guia da API no [ponto de extremidade de trabalhos de exportação](../segmentation/api/export-jobs.md).

### Exportar os dados avaliados para um destino

Como alternativa, depois de criar seu trabalho de segmento único ou sua programação contínua, você pode exportar os resultados para um destino. Um destino é um endpoint, como um aplicativo do Adobe em um serviço externo, em que um público-alvo pode ser ativado e entregue. Uma lista completa de destinos disponíveis pode ser encontrada no [catálogo de destinos](../destinations/catalog/overview.md).

Para obter instruções sobre como ativar dados para destinos de marketing em lote ou por email, consulte o tutorial sobre [como ativar dados de público-alvo para destinos de exportação de perfil em lote usando a interface do usuário do Experience Platform](../destinations/ui/activate-batch-profile-destinations.md) e o [guia sobre como se conectar a destinos em lote e ativar dados usando a API do Serviço de Fluxo](../destinations/api/connect-activate-batch-destinations.md).

## Monitorar suas atividades de dados do Experience Platform

O Experience Platform permite rastrear como os dados estão sendo processados por meio do uso de fluxos de dados, que são representações de trabalhos que movem dados entre os vários componentes do Experience Platform. Esses fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para os conjuntos de dados de destino, onde são utilizados por [!DNL Identity Service] e [!DNL Real-Time Customer Profile] antes de serem ativados para os destinos. O painel de monitoramento fornece uma representação visual da jornada de um fluxo de dados. Para saber como monitorar fluxos de dados na interface do Experience Platform, consulte os tutoriais em [monitoramento de fluxos de dados de fontes](../dataflows/ui/monitor-sources.md) e [monitoramento de fluxos de dados de destinos](../dataflows/ui/monitor-destinations.md).

Você também pode monitorar as atividades do Experience Platform usando métricas estatísticas e notificações de eventos com o [!DNL Observability Insights]. Você pode assinar notificações de alerta por meio da interface do usuário do Experience Platform ou enviá-las para um webhook configurado. Para obter mais detalhes sobre como exibir, habilitar, desabilitar e assinar alertas disponíveis na interface do usuário do Experience Platform, consulte o [[!UICONTROL Guia de Interface do Usuário de Alertas]](../observability/alerts/ui.md). Para obter detalhes sobre como receber alertas por meio de webhooks, consulte o manual sobre [assinatura de notificações de eventos do Adobe I/O](../observability/alerts/subscribe.md).

## Próximas etapas

Ao ler este tutorial, você recebeu uma introdução básica a um fluxo simples de ponta a ponta para o Experience Platform. Para saber mais sobre o Adobe Experience Platform, leia a [visão geral do Experience Platform](./home.md). Para saber mais sobre como usar a interface do usuário do Experience Platform e a API do Experience Platform, leia o [guia da interface do usuário do Experience Platform](./ui-guide.md) e o [guia da API do Experience Platform](./api-guide.md), respectivamente.
