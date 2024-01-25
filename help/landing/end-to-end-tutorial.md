---
keywords: Experience Platform;página inicial;tópicos populares;CJA;análise de jornada;análise de jornada do cliente;orquestração de campanhas;orquestração;jornada do cliente;jornada;orquestração de jornadas;capacidade;região
title: Exemplo de fluxo de trabalho de ponta a ponta do Adobe Experience Platform
description: Conheça o fluxo de trabalho básico completo do Adobe Experience Platform em alto nível.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: f9917d6a6de81f98b472cff9b41f1526ea51cdae
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 1%

---

# Fluxo de trabalho de exemplo completo do Adobe Experience Platform

A Adobe Experience Platform é o sistema mais poderoso, flexível e aberto do mercado para criar e gerenciar soluções completas que impulsionam a experiência do cliente. A Platform permite que as organizações centralizem e padronizem dados e conteúdo de clientes de qualquer sistema e apliquem a ciência de dados e o aprendizado de máquina para melhorar o design e o delivery de experiências personalizadas.

Criada com APIs RESTful, a Platform expõe a funcionalidade completa do sistema para os desenvolvedores, oferecendo suporte à fácil integração de soluções empresariais usando ferramentas familiares. A Platform permite obter uma visualização integral dos clientes assimilando os dados deles, segmentando os dados para os públicos que você deseja direcionar e ativando esses públicos para um destino externo. O tutorial a seguir mostra um fluxo de trabalho completo, mostrando todas as etapas, desde a assimilação por meio de fontes até a ativação de público-alvo por meio de destinos.

![fluxo de trabalho completo do Experience Platform](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Introdução

Esse fluxo de trabalho completo usa vários serviços da Adobe Experience Platform. Veja a seguir uma lista dos serviços usados neste fluxo de trabalho com links para suas visões gerais:

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): o quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente. Para melhor usar a segmentação, verifique se seus dados são assimilados como perfis e eventos de acordo com a [práticas recomendadas para modelagem de dados](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md): fornece uma visualização abrangente dos clientes e do comportamento deles ao unir as identidades de vários dispositivos e sistemas.
- [Origens](../sources/home.md): [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços.
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] permite dividir os dados armazenados no [!DNL Experience Platform] que se relaciona a indivíduos (como clientes, clientes potenciais, usuários ou organizações) em grupos menores.
- [[!DNL Real-Time Customer Profile]](../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [Conjuntos de dados](../catalog/datasets/overview.md): a construção de armazenamento e gerenciamento para a persistência de dados no [!DNL Experience Platform].
- [Destinos](../destinations/home.md): os destinos são integrações pré-criadas com aplicativos de uso comum que permitem a ativação contínua de dados da Platform para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

## Criar um esquema do XDM

Antes de assimilar dados na Platform, primeiro você deve criar um esquema XDM para descrever a estrutura desses dados. Ao assimilar seus dados na próxima etapa, você mapeará os dados recebidos para esse esquema. Para saber como criar um exemplo de esquema XDM, leia o tutorial em [criação de um esquema usando o Editor de esquemas](../xdm/tutorials/create-schema-ui.md).

O tutorial acima mostra como definir campos de identidade para seus esquemas. Um campo de identidade representa um campo que pode ser usado para identificar uma pessoa individual relacionada a um registro ou evento de série temporal. Os campos de identidade são um componente essencial em como os gráficos de identidade do cliente são construídos na Platform, o que afeta como o Perfil do cliente em tempo real mescla fragmentos de dados diferentes para obter uma visão completa do cliente. Para obter mais detalhes sobre como visualizar gráficos de identidade na Platform, consulte o tutorial em [como usar o visualizador de gráficos de identidade](../identity-service/features/identity-graph-viewer.md).

Você precisa ativar seu esquema para usar no Perfil do cliente em tempo real para que os perfis do cliente possam ser construídos a partir dos dados baseados no seu esquema. Consulte a seção sobre [ativar um esquema para Perfil](../xdm/ui/resources/schemas.md#profile) no guia da interface de schemas para obter mais informações.

## Assimilar seus dados na plataforma

Depois de criar um esquema XDM, você pode começar a trazer seus dados para o sistema.

Todos os dados trazidos para a Platform são armazenados em conjuntos de dados individuais após a assimilação. Um conjunto de dados é uma coleção de registros de dados que mapeiam para um esquema XDM específico. Antes que seus dados possam ser usados pelo [!DNL Real-Time Customer Profile], o conjunto de dados em questão deve ser configurado especificamente. Para obter instruções completas sobre como ativar um conjunto de dados para o Perfil, consulte [Guia da interface do usuário de conjuntos de dados](../catalog/datasets/user-guide.md#enable-profile) e a variável [tutorial da API de configuração do conjunto de dados](../profile/tutorials/dataset-configuration.md). Após configurar o conjunto de dados, você pode começar a assimilar dados nele.

A Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Platform. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamentos baseados em nuvem, bancos de dados e muitas outras. Por exemplo, você pode assimilar seus dados usando [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). Uma lista completa de fontes disponíveis pode ser encontrada no [visão geral dos conectores de origem](../sources/home.md).

Se você usar o Amazon S3 como conector de origem, poderá seguir as instruções no tutorial da API em [criação de um conector do Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md) ou o tutorial da interface do usuário no [criação de um conector do Amazon S3](../sources/tutorials/ui/create/cloud-storage/s3.md) para saber como criar, conectar e assimilar dados no conector.

Para obter instruções mais detalhadas sobre conectores de origem, leia o [visão geral dos conectores de origem](../sources/home.md). Para saber mais sobre o Serviço de fluxo, a API da qual as fontes se baseiam, leia a [Referência da API do serviço de fluxo](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Depois que os dados forem trazidos para a Platform por meio do conector de origem e armazenados em seu conjunto de dados habilitado para perfil, os perfis do cliente serão criados automaticamente com base nos dados de identidade configurados no esquema XDM.

Ao fazer upload dos dados para um novo conjunto de dados pela primeira vez ou ao configurar um novo processo ETL ou fonte de dados, é recomendável verificar cuidadosamente os dados para garantir que tenham sido carregados corretamente e que os perfis gerados contenham os dados esperados. Para obter mais informações sobre como acessar perfis de clientes na interface do usuário da Platform, consulte [Guia da interface do usuário do Perfil do cliente em tempo real](../profile/ui/user-guide.md). Para obter detalhes sobre como acessar perfis usando a API de perfil do cliente em tempo real, consulte o guia em [uso do endpoint de entidades](../profile/api/entities.md).

## Avalie seus dados

Depois de gerar perfis com sucesso a partir dos dados assimilados, você pode avaliar os dados usando a segmentação. A segmentação é o processo de definir atributos ou comportamentos específicos compartilhados por um subconjunto de indivíduos da loja de perfis, a fim de distinguir um grupo comercializável de pessoas da sua base de clientes. Para saber mais sobre segmentação, leia o [visão geral do serviço de segmentação](../segmentation/home.md).

### Criar uma definição de segmento

Para começar, você deve criar uma definição de segmento para agrupar seus clientes e criar seu público-alvo. Uma definição de segmento é uma coleção de regras que você pode usar para definir o público-alvo que deseja direcionar. Para criar uma definição de segmento, siga as instruções no guia da interface sobre como usar o [Construtor de segmentos](../segmentation/ui/segment-builder.md) ou o tutorial da API em [criação de um segmento](../segmentation/tutorials/create-a-segment.md).

Depois de criar uma definição de segmento, anote a ID de definição de segmento.

### Avaliar a definição do segmento

Depois de criar a definição do segmento, você pode criar um job de segmento para avaliá-lo como uma instância única ou criar uma programação para avaliá-lo de forma contínua.

Para avaliar uma definição de segmento sob demanda, você pode criar um trabalho de segmento. Um trabalho de segmento é um processo assíncrono que cria um novo segmento de público-alvo com base na definição do segmento referenciado e nas políticas de mesclagem. Uma política de mesclagem é um conjunto de regras que a Platform usa para determinar quais dados serão usados para criar perfis de clientes e quais dados serão priorizados quando houver discrepâncias entre as fontes. Para saber como trabalhar com políticas de mesclagem, consulte [guia da interface do usuário de políticas de mesclagem](../profile/merge-policies/ui-guide.md).

Depois que o trabalho de segmento é criado e avaliado, você pode obter informações sobre o segmento, como o tamanho do público-alvo ou erros que podem ter ocorrido durante o processamento. Para saber como criar um trabalho de segmento, incluindo todos os detalhes que você precisa fornecer, leia o [guia do desenvolvedor do trabalho de segmento](../segmentation/api/segment-jobs.md).

Para avaliar uma definição de segmento de forma contínua, você pode criar e ativar uma programação. Uma programação é uma ferramenta que pode ser usada para executar automaticamente um trabalho de segmento uma vez por dia em um horário especificado. Para saber como criar e habilitar um agendamento, siga as instruções no guia da API na [ponto de extremidade de agendamentos](../segmentation/api/schedules.md).

## Exportar os dados avaliados

Depois de criar seu trabalho de segmento único ou sua programação contínua, você pode criar um trabalho de exportação de segmento para exportar os resultados para um conjunto de dados ou exportá-los para um destino. As seções a seguir fornecem orientação sobre essas duas opções.

### Exportar os dados avaliados para um conjunto de dados

Após criar o job de segmento ocasional ou a programação contínua, você pode exportar os resultados criando um job de exportação de segmento. Um trabalho de exportação de segmento é uma tarefa assíncrona que envia informações sobre o público-alvo avaliado para um conjunto de dados.

Antes de criar um trabalho de exportação, primeiro crie um conjunto de dados para o qual exportar os dados. Para saber como criar um conjunto de dados, leia a seção sobre [criação de um conjunto de dados de destino](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) no tutorial sobre avaliação de um segmento, certifique-se de anotar a ID do conjunto de dados após a criação. Depois de criar um conjunto de dados, você pode criar um trabalho de exportação. Para saber como criar um trabalho de exportação, siga as instruções no guia da API na guia [exportar ponto de extremidade de trabalhos](../segmentation/api/export-jobs.md).

### Exportar os dados avaliados para um destino

Como alternativa, depois de criar seu trabalho de segmento único ou sua programação contínua, você pode exportar os resultados para um destino. Um destino é um endpoint, como um aplicativo Adobe em um serviço externo, em que um público-alvo pode ser ativado e entregue. Uma lista completa dos destinos disponíveis pode ser encontrada no [catálogo de destinos](../destinations/catalog/overview.md).

Para obter instruções sobre como ativar dados para destinos de marketing em lote ou por email, consulte o tutorial em [como ativar dados de público-alvo para destinos de exportação de perfil em lote usando a interface do usuário da Platform](../destinations/ui/activate-batch-profile-destinations.md) e a variável [guia sobre como se conectar a destinos em lote e ativar dados usando a API do Serviço de fluxo](../destinations/api/connect-activate-batch-destinations.md).

## Monitorar suas atividades de dados da plataforma

A Platform permite rastrear como os dados estão sendo processados por meio do uso de fluxos de dados, que são representações de trabalhos que movem dados entre os vários componentes da Platform. Esses fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para os conjuntos de dados de destino, onde são utilizados pelo [!DNL Identity Service] e [!DNL Real-Time Customer Profile] antes de serem ativados para destinos. O painel de monitoramento fornece uma representação visual da jornada de um fluxo de dados. Para saber como monitorar fluxos de dados na interface do Platform, consulte os tutoriais em [monitoramento de fluxos de dados para origens](../dataflows/ui/monitor-sources.md) e [monitoramento de fluxos de dados para destinos](../dataflows/ui/monitor-destinations.md).

Você também pode monitorar as atividades da Platform usando métricas estatísticas e notificações de evento [!DNL Observability Insights]. Você pode assinar notificações de alerta por meio da interface do usuário da Platform ou enviá-las para um webhook configurado. Para obter mais detalhes sobre como exibir, ativar, desativar e assinar alertas disponíveis na interface do Experience Platform, consulte [[!UICONTROL Alertas] Guia da interface do usuário](../observability/alerts/ui.md). Para obter detalhes sobre como receber alertas por meio de webhooks, consulte o manual sobre [assinatura de notificações de Adobe I/O Event](../observability/alerts/subscribe.md).

## Próximas etapas

Ao ler este tutorial, você recebeu uma introdução básica a um fluxo simples de ponta a ponta para a Platform. Para saber mais sobre o Adobe Experience Platform, leia o [Visão geral da plataforma](./home.md). Para saber mais sobre como usar a interface do usuário da plataforma e a API da plataforma, leia o [Guia da interface do usuário da Platform](./ui-guide.md) e a variável [Guia da API da plataforma](./api-guide.md) respectivamente.
