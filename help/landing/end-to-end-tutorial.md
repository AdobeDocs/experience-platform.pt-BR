---
keywords: Experience Platform, home, tópicos populares, CJA, análise de jornada, análise de jornada do cliente, orquestração de campanha, orquestração, jornada do cliente, jornada, orquestração de jornada, capacidade, região
title: Fluxo de trabalho de exemplo completo do Adobe Experience Platform
topic-legacy: getting started
description: Saiba mais sobre o fluxo de trabalho completo básico do Adobe Experience Platform em alto nível.
source-git-commit: 9ed521c4e2ebcd20da662e93b9591ef690f51c5e
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 2%

---

# Fluxo de trabalho de exemplo completo do Adobe Experience Platform

O Adobe Experience Platform é o sistema mais eficiente, flexível e aberto do mercado para criar e gerenciar soluções completas que impulsionam a experiência do cliente. A Platform permite que as organizações centralizem e padronizem dados e conteúdo de clientes de qualquer sistema e apliquem a ciência de dados e o aprendizado de máquina para melhorar o design e o delivery de experiências personalizadas.

Baseada em RESTful APIs, a Platform expõe a funcionalidade completa do sistema para os desenvolvedores, suportando a fácil integração de soluções corporativas usando ferramentas conhecidas. A Platform permite derivar uma visualização holística dos clientes, assimilando os dados dos clientes, segmentando os dados para os públicos-alvo que deseja direcionar e ativando esses públicos-alvo para um destino externo. O tutorial a seguir mostra um fluxo de trabalho completo, mostrando todas as etapas da assimilação por meio de fontes para a ativação do público-alvo por destinos.

![Fluxo de trabalho Experience Platform end-to-end](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Introdução

Esse fluxo de trabalho completo usa vários serviços da Adobe Experience Platform. Esta é uma lista dos serviços usados neste workflow com links para suas visões gerais:

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): O quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente. Para utilizar melhor a Segmentação, verifique se os dados são assimilados como perfis e eventos de acordo com a variável [práticas recomendadas para modelagem de dados](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md): Fornece uma visão abrangente de seus clientes e seu comportamento ao unir identidades em dispositivos e sistemas.
- [Fontes](../sources/home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] permite dividir os dados armazenados em [!DNL Experience Platform] que se relaciona a indivíduos (como clientes, clientes potenciais, usuários ou organizações) em grupos menores.
- [[!DNL Real-time Customer Profile]](../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
- [Conjuntos de dados](../catalog/datasets/overview.md): A construção de armazenamento e gerenciamento para a persistência de dados em [!DNL Experience Platform].
- [Destinos](../destinations/home.md): Os destinos são integrações pré-criadas com aplicativos comumente usados que permitem a ativação simplificada de dados da Platform para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

## Criar um esquema do XDM

Antes de assimilar dados na Platform, primeiro você deve criar um esquema XDM para descrever a estrutura desses dados. Ao assimilar seus dados na próxima etapa, você mapeará seus dados recebidos para esse esquema. Para saber como criar um esquema XDM de exemplo, leia o tutorial em [criação de um esquema usando o Editor de esquemas](../xdm/tutorials/create-schema-ui.md).

O tutorial acima mostra como definir campos de identidade para seus esquemas. Um campo de identidade representa um campo que pode ser usado para identificar uma pessoa relacionada a um registro ou evento de série de tempo. Os campos de identidade são um componente essencial na forma como os gráficos de identidade do cliente são construídos na plataforma, o que afeta o modo como o Perfil do cliente em tempo real mescla fragmentos de dados diferentes para obter uma visualização completa do cliente. Para obter mais detalhes sobre como visualizar gráficos de identidade na Platform, consulte o tutorial em [como usar o visualizador de gráfico de identidade](../identity-service/ui/identity-graph-viewer.md).

É necessário ativar o esquema para usar no Perfil do cliente em tempo real para que os perfis do cliente possam ser construídos a partir dos dados com base no esquema. Consulte a seção sobre [ativar um esquema para o Perfil](../xdm/ui/resources/schemas.md#profile) no guia da interface do usuário do schemas para obter mais informações.

## Assimilar seus dados na Platform

Depois de criar um esquema XDM, você pode começar a trazer seus dados para o sistema.

Todos os dados trazidos para a Platform são armazenados em conjuntos de dados individuais após a assimilação. Um conjunto de dados é uma coleção de registros de dados que mapeiam para um esquema XDM específico. Antes que os dados possam ser usados pelo [!DNL Real-time Customer Profile], o conjunto de dados em questão deve ser configurado especificamente. Para obter instruções completas sobre como ativar um conjunto de dados para o Perfil, consulte o [Guia da interface do usuário de conjuntos de dados](../catalog/datasets/user-guide.md#enable-profile) e [tutorial da API de configuração do conjunto de dados](../profile/tutorials/dataset-configuration.md). Após configurar o conjunto de dados, você pode começar a assimilar dados nele.

A Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamentos baseados em nuvem, bancos de dados e muitas outras. Por exemplo, é possível assimilar seus dados usando [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). Uma lista completa das fontes disponíveis pode ser encontrada no [visão geral dos conectores de origem](../sources/home.md).

Se você usar o Amazon S3 como conector de origem, poderá seguir as instruções no tutorial de API em [criação de um conector Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md) ou o tutorial da interface do usuário em [criação de um conector Amazon S3](../sources/tutorials/ui/create/cloud-storage/s3.md) para saber como criar, conectar e assimilar dados no conector.

Para obter instruções mais detalhadas sobre conectores de origem, leia o [visão geral dos conectores de origem](../sources/home.md). Para saber mais sobre o Serviço de Fluxo, consulte a API em que as fontes se baseiam. [Referência da API do Serviço de Fluxo](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Quando os dados são trazidos para a Platform pelo conector de origem e armazenados em seu conjunto de dados habilitado para perfil, os perfis do cliente são criados automaticamente com base nos dados de identidade configurados no esquema XDM.

Ao carregar dados em um novo conjunto de dados pela primeira vez ou ao configurar um novo processo ETL ou fonte de dados, é recomendável verificar cuidadosamente os dados para garantir que eles foram carregados corretamente e que os perfis gerados contêm os dados que você espera. Para obter mais informações sobre como acessar perfis de clientes na interface do usuário da plataforma, consulte o [Guia da interface do usuário do perfil do cliente em tempo real](../profile/ui/user-guide.md). Para obter detalhes sobre como acessar perfis usando a API de perfil do cliente em tempo real, consulte o guia em [uso do endpoint de entidades](../profile/api/entities.md).

## Avaliar seus dados

Depois de gerar perfis com sucesso a partir dos dados assimilados, você pode avaliar seus dados usando a segmentação. A segmentação é o processo de definição de atributos ou comportamentos específicos compartilhados por um subconjunto de indivíduos da loja de perfis, a fim de distinguir um grupo comercializável de pessoas da base de clientes. Para saber mais sobre a segmentação, leia o [visão geral do serviço de segmentação](../segmentation/home.md).

### Criar uma definição de segmento

Para começar, você deve criar uma definição de segmento para agrupar seus clientes e criar seu público-alvo. Uma definição de segmento é uma coleção de regras que pode ser usada para definir o público-alvo que deseja direcionar. Para criar uma definição de segmento, você pode seguir as instruções no guia da interface do usuário sobre como usar o [Construtor de segmentos](../segmentation/ui/segment-builder.md) ou o tutorial da API em [criação de um segmento](../segmentation/tutorials/create-a-segment.md).

Depois de criar uma definição de segmento, anote a ID de definição de segmento.

### Avaliar a definição do segmento

Depois de criar a definição de segmento, você pode criar um trabalho de segmento para avaliar o segmento como uma instância única ou criar um agendamento para avaliar o segmento de forma contínua.

Para avaliar uma definição de segmento sob demanda, você pode criar um trabalho de segmento. Um trabalho de segmento é um processo assíncrono que cria um novo segmento de público-alvo com base na definição do segmento referenciado e nas políticas de mesclagem. Uma política de mesclagem é um conjunto de regras que a Platform usa para determinar quais dados serão usados para criar perfis de clientes e quais dados serão priorizados quando houver discrepâncias entre as fontes. Para saber como trabalhar com políticas de mesclagem, consulte o [guia da interface do usuário de políticas de mesclagem](../profile/merge-policies/ui-guide.md).

Depois que o trabalho do segmento é criado e avaliado, você pode obter informações sobre o segmento, como o tamanho do público-alvo ou erros que podem ter ocorrido durante o processamento. Para saber como criar um trabalho de segmento, incluindo todos os detalhes que você precisa fornecer, leia o [guia do desenvolvedor de trabalhos do segmento](../segmentation/api/segment-jobs.md).

Para avaliar uma definição de segmento de forma contínua, você pode criar e ativar uma programação. Um agendamento é uma ferramenta que pode ser usada para executar automaticamente um trabalho de segmento uma vez por dia em um horário especificado. Para saber como criar e habilitar um cronograma, siga as instruções no guia da API no [endpoint de agendamentos](../segmentation/api/schedules.md).

## Exportar os dados avaliados

Depois de criar o trabalho de segmento único ou o agendamento contínuo, você pode criar um trabalho de exportação de segmento para exportar os resultados para um conjunto de dados ou exportar os resultados para um destino. As seções a seguir fornecem orientação sobre essas duas opções.

### Exportar os dados avaliados para um conjunto de dados

Após criar o trabalho de segmento único ou o agendamento contínuo, é possível exportar os resultados criando um trabalho de exportação de segmento. Um trabalho de exportação de segmento é uma tarefa assíncrona que envia informações sobre o público avaliado para um conjunto de dados.

Antes de criar um trabalho de exportação, primeiro crie um conjunto de dados para o qual exportar os dados. Para saber como criar um conjunto de dados, leia a seção sobre [criação de um conjunto de dados de target](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) no tutorial sobre avaliação de um segmento, certifique-se de anotar a ID do conjunto de dados após a criação. Depois de criar um conjunto de dados, você pode criar um trabalho de exportação. Para saber como criar um trabalho de exportação, siga as instruções no guia da API no [ponto de extremidade de tarefas de exportação](../segmentation/api/export-jobs.md).

### Exportar os dados avaliados para um destino

Como alternativa, depois de criar o trabalho de segmento único ou o agendamento contínuo, você pode exportar os resultados para um destino. Um destino é um terminal, como um aplicativo Adobe em um serviço externo, em que um público-alvo pode ser ativado e entregue. Uma lista completa de destinos disponíveis pode ser encontrada no [catálogo de destinos](../destinations/catalog/overview.md).

Para obter instruções sobre como ativar dados para destinos de marketing em lote ou por email, consulte o tutorial em [como ativar os dados do público-alvo para exportar perfis em lote usando a interface do usuário da plataforma](../destinations/ui/activate-batch-profile-destinations.md) e [guia sobre como se conectar a destinos em lote e ativar dados usando a API do Serviço de Fluxo](../destinations/api/connect-activate-batch-destinations.md).

## Monitore atividades de dados da plataforma

A Platform permite rastrear como os dados estão sendo processados por meio do uso de fluxos de dados, que são representações de trabalhos que movem dados pelos vários componentes da plataforma. Esses fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de destino, onde são utilizados por [!DNL Identity Service] e [!DNL Real-time Customer Profile] antes de ser ativado para destinos. O painel de monitoramento fornece uma representação visual da jornada de um fluxo de dados. Para saber como monitorar fluxos de dados na interface do usuário da plataforma, consulte os tutoriais em [monitoramento de fluxos de dados para fontes](../dataflows/ui/monitor-sources.md) e [monitoramento de fluxos de dados para destinos](../dataflows/ui/monitor-destinations.md).

Você também pode monitorar as atividades da Platform por meio do uso de métricas estatísticas e notificações de eventos usando [!DNL Observability Insights]. Você pode assinar notificações de alerta por meio da interface do usuário da plataforma ou enviá-las para um webhook configurado. Para obter mais detalhes sobre como visualizar, ativar, desativar e assinar alertas disponíveis na interface do usuário do Experience Platform, consulte o [[!UICONTROL Alertas] Guia da interface do usuário](../observability/alerts/ui.md). Para obter detalhes sobre como receber alertas por meio de webhooks, consulte o guia sobre [assinando notificações de Adobe I/O Event](../observability/alerts/subscribe.md).

## Próximas etapas

Ao ler este tutorial, você recebeu uma introdução básica a um fluxo completo simples para a Platform. Para saber mais sobre o Adobe Experience Platform, leia o [Visão geral da plataforma](./home.md). Para saber mais sobre como usar a interface do usuário da plataforma e a API da plataforma, leia o [Guia da interface do usuário da plataforma](./ui-guide.md) e [Guia da API da plataforma](./api-guide.md) respectivamente.