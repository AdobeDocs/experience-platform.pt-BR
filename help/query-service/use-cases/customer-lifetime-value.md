---
title: Rastrear sinais de dados para gerar o valor vitalício do cliente
description: Este guia fornece uma demonstração completa sobre como usar o Data Distiller e painéis definidos pelo usuário com o Real-time Customer Data Platform para medir e visualizar o valor vitalício do cliente.
source-git-commit: 2346f2d9450bc24e10419c09ee3dbcfb35bd5778
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 0%

---

# Rastrear sinais de dados para gerar o valor vitalício do cliente

Você pode usar o Real-time Customer Data Platform para rastrear o valor da vida útil do cliente (CLV) e visualizar essa métrica com painéis definidos pelo usuário. Com o uso do Data Distiller e painéis definidos pelo usuário, você pode medir o valor de um cliente para sua empresa em toda a sua relação. Conhecer o CLV pode ajudar você a desenvolver as estratégias de sua empresa para adquirir novos clientes, além de manter os existentes e as margens de lucro.

O infográfico a seguir descreve o ciclo de coleta, manipulação, análise e atuação de dados que gera dados de alto desempenho para melhorar suas campanhas de marketing.

![O infográfico de ida e volta dos dados da observação para a análise para a ação.](../images/use-cases/infographic-use-case-cycle.png)

Esse caso de uso completo demonstra como os sinais de dados podem ser capturados e modificados para calcular o atributo derivado do valor vitalício do cliente. Esses atributos derivados podem ser aplicados aos dados de perfil do Real-Time CDP e estão disponíveis para uso com painéis definidos pelo usuário para criar um painel para análise de insight. Por meio do Data Distiller, você pode estender o modelo de dados do Real-Time CDP insights e usar o atributo derivado do CLV e os insights do painel para criar um novo segmento e ativá-lo para um destino desejado. Esses segmentos podem ser usados para criar públicos de alto desempenho para potencializar sua próxima campanha de marketing.

Este guia foi projetado para ajudá-lo a entender melhor a experiência do cliente, medindo sinais de dados nos principais pontos de contato que impulsionam o CLV e implementando um caso de uso semelhante em seu ambiente. Todo o processo é resumido na imagem abaixo.

![Um infográfico das etapas amplas necessárias para utilizar o valor vitalício do cliente.](../images/use-cases/implementation-steps.png)

## Introdução {#getting-started}

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Serviço de query](../home.md): Fornece uma interface de usuário e uma RESTful API, onde você pode usar consultas SQL para analisar e enriquecer seus dados.
* [Serviço de segmentação](../../segmentation/home.md): Permite criar segmentos e gerar públicos-alvo a partir dos dados do Perfil do cliente em tempo real.

## Pré-requisitos

Este guia requer que você [Distiller de dados](../data-distiller/overview.md) SKU como parte da oferta do seu pacote. Se não tiver certeza se tem isso, fale com o representante do serviço da Adobe.

## Criar um atributo derivado {#create-derived-attribute}

O primeiro passo para estabelecer seu CLV é criar um atributo derivado dos sinais de dados capturados das ações do usuário. Este caso de uso específico é capturado em um documento separado sobre um esquema de fidelidade da companhia aérea. Consulte o guia para saber como [use o Serviço de query para criar atributos derivados baseados em decilis para usar com os dados do seu perfil](./deciles-use-case.md). Exemplos completos e explicações são fornecidos no documento que explicam as seguintes etapas:

* Crie um esquema para permitir a segmentação de decilis.
* Use o Serviço de Consulta para criar deciles.
* Gere conjuntos de dados do decile.
* Ative o esquema para usar no Perfil do cliente em tempo real.
* Crie um namespace de identidade e o marque como o identificador principal.
* Crie uma query para calcular decodificações em um período de lookback.

## Estender o modelo de dados de insights e agendar atualizações {#extend-data-model-and-set-refresh-schedule}

Em seguida, você deve criar um modelo de dados personalizado ou estender um modelo de dados Adobe Real-Time CDP existente para se envolver com seus insights de relatórios do CLV. Consulte a documentação para saber como [criar um modelo de dados de insights de relatórios por meio do Serviço de query para uso com dados de armazenamento acelerados e painéis definidos pelo usuário](../data-distiller/query-accelerated-store/reporting-insights-data-model.md#build-a-reporting-insights-data-model). O tutorial aborda as seguintes etapas:

* Crie um modelo para relatórios de insights com o Data Distiller.
* Crie tabelas, relações e preencha dados.
* Consulte o modelo de dados de insight do relatório.
* Estenda seu modelo de dados com o modelo de dados do Real-Time CDP insights.
* Crie tabelas de dimensão para estender seu modelo de insights de relatórios.
* Consulte o modelo de dados de insights de relatório de loja acelerada estendida

Consulte a documentação do Modelo de dados do Real-time Customer Data Platform Insights para saber como [personalize seus modelos de consulta SQL para criar relatórios do Real-Time CDP para seus casos de uso de indicador de desempenho principal (KPI) de marketing](../../dashboards/cdp-insights-data-model.md).

Certifique-se de definir um agendamento para atualizar seu modelo de dados personalizado em uma cadência regular. Isso garante que os dados retornem como parte do pipeline de assimilação, conforme necessário, e preencha seus painéis definidos pelo usuário. Consulte a [guia de agendamento de consultas](../ui/query-schedules.md#create-schedule) para saber como configurar seu cronograma.

## Criar um painel para capturar insights {#build-a-custom-dashboard}

Agora que você criou seu modelo de dados personalizado, está pronto para visualizar seus dados com consultas personalizadas e painéis definidos pelo usuário. Consulte a visão geral dos painéis definidos pelo usuário para obter orientação completa sobre como [criar um painel personalizado](../../dashboards/user-defined-dashboards.md). O guia da interface do usuário inclui detalhes sobre:

* Como criar um widget.
* Como usar o compositor de widgets.

Exemplos de widgets CLV personalizados que usam buckets de decillo podem ser vistos abaixo.

![Uma coleção de widgets CLTV personalizados e baseados em decis.](../images/use-cases/deciles-user-defined-dashboard.png)

## Criar e ativar segmentos para criar públicos de alto desempenho {#create-and-activate-segments}

A próxima etapa é criar segmentos e gerar públicos-alvo a partir dos dados do Perfil do cliente em tempo real. Consulte o guia da interface do usuário do Construtor de segmentos para saber como [criar e ativar segmentos na Platform](../../segmentation/ui/segment-builder.md). O guia fornece seções sobre como:

* Crie definições de segmento usando uma combinação de atributos, eventos e públicos-alvo existentes como blocos de construção.
* Use a tela e os contêineres do construtor de regras para controlar a ordem em que as regras de segmento são executadas.
* Visualize estimativas do seu público-alvo potencial, permitindo ajustar as definições do segmento, conforme necessário.
* Ativar todas as definições de segmento para segmentação agendada.
* Ativar definições de segmento especificadas para a segmentação de fluxo.

Como alternativa, há também um [tutorial em vídeo do construtor de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) disponível para obter mais informações.

## Ativar seu segmento para uma campanha de email {#activate-segment-for-campaign}

Depois de criar seu segmento, você está pronto para ativá-lo em um destino. A plataforma oferece suporte a uma variedade de provedores de serviços de email (ESPs) que permitem gerenciar suas atividades de marketing por email, como enviar campanhas promocionais por email.

Verifique a [visão geral de destinos de marketing por email](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/overview.html?lang=en#connect-destination) para obter uma lista dos destinos compatíveis para os quais você deseja exportar dados (por exemplo, a variável [Oracle Eloqua](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/oracle-eloqua-api.html?lang=en) página).

## Veja os dados de análise retornados de sua campanha {#post-campaign-data-analysis}

Os dados das fontes agora podem ser [processado gradualmente](../essential-concepts/incremental-load.md) como parte de uma atualização programada para o modelo de dados no armazenamento de dados acelerado. Qualquer evento de resposta de clientes pode ser assimilado no Adobe Experience Platform conforme ocorre ou em lotes. O modelo de dados pode ser atualizado uma ou várias vezes por dia, dependendo das configurações ou conectores de origem. Consulte a [visão geral da API de assimilação de lote](../../ingestion/batch-ingestion/api-overview.md) ou [visão geral da assimilação de streaming](../../ingestion/streaming-ingestion/overview.md) para obter mais informações.

Depois que seu modelo de dados é atualizado, seus widgets de painel personalizados fornecem sinais significativos que permitem medir e visualizar o valor vitalício do cliente.

![Um widget personalizado para mostrar o número de emails abertos de acordo com seu segmento e campanha de email.](../images/use-cases/post-activation-and-email-response-kpis.png)

Várias opções de visualização são fornecidas para a análise personalizada.

![O email aberto pelo widget de buckets da campanha.](../images/use-cases/email-opened-by-campaign-buckets.png)

Esses insights podem, por sua vez, ajudar você a desenvolver suas estratégias de negócios para campanhas subsequentes.

![Uma coleção de quatro widgets personalizados que detalham os resultados da campanha de email.](../images/use-cases/example-widgets.png)

## Próximas etapas

Ao ler este documento, você deve ter uma melhor compreensão de como pode usar o Real-time Customer Data Platform para rastrear e visualizar a métrica de valor vitalício do cliente (CLV). Para saber mais sobre os muitos casos de uso comercial encontrados por meio do Serviço de query e do Experience Platform, é recomendável ler os seguintes documentos:

* [Um exemplo completo de um caso de uso de navegação abandonado que demonstra a versatilidade e os benefícios do Serviço de query.](./abandoned-browse.md)
* [Como usar o Serviço de query e o aprendizado de máquina para determinar e filtrar a atividade de bot do tráfego online genuíno de visitantes](./bot-filtering.md)
* [Como executar uma correspondência nos dados da plataforma que combina resultados de vários conjuntos de dados, correspondendo aproximadamente a uma string de sua escolha.](./fuzzy-match.md)

<!-- "Data signals are actions taken by consumers while online that offer clues about intent that can be acted upon. This includes anything from visiting a website to filling out a change of address or clicking an ad."  -->

<!-- "Customer touchpoints are your brand's points of customer contact, from start to finish." -->
