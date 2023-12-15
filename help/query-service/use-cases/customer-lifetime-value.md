---
title: Rastrear sinais de dados para gerar o valor vitalício do cliente
description: Este guia fornece uma demonstração completa sobre como usar o Data Distiller e painéis definidos pelo usuário com o Real-time Customer Data Platform para medir e visualizar o valor vitalício do cliente.
exl-id: c74b5bff-feb2-4e21-9ee4-1e0973192570
source-git-commit: 18c1d32bbc2732c38a9c37ee8fb9d36a23d4e515
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 0%

---

# Rastrear sinais de dados para gerar o valor vitalício do cliente

Você pode usar o Real-time Customer Data Platform para rastrear o valor vitalício do cliente (CLV) e visualizar essa métrica com painéis definidos pelo usuário. Com o uso do Data Distiller e de painéis definidos pelo usuário, você pode medir o valor de um cliente para sua empresa em todo o relacionamento. Conhecer o CLV pode ajudar você a desenvolver as estratégias da sua empresa para adquirir novos clientes, mantendo os existentes e as margens de lucro.

O infográfico a seguir descreve o ciclo de coleta, manipulação, análise e atuação de dados que gera dados de alto desempenho para melhorar suas campanhas de marketing.

![O infográfico de ida e volta de dados, da observação à análise e à ação.](../images/use-cases/infographic-use-case-cycle.png)

Este caso de uso completo demonstra como os sinais de dados podem ser capturados e modificados para calcular o atributo derivado de valor do tempo de vida do cliente. Esses conjuntos de dados derivados podem ser aplicados aos dados de perfil do Real-Time CDP e estão disponíveis para uso com painéis definidos pelo usuário para criar um painel para análise de insight. Por meio do Data Distiller, é possível estender o modelo de dados do Real-Time CDP Insights e usar os conjuntos de dados derivados do CLV e insights do painel para criar um novo público-alvo e ativá-lo para um destino desejado. Esses públicos-alvo de alto desempenho podem ser usados para potencializar sua próxima campanha de marketing.

Este guia foi projetado para ajudar você a entender melhor a experiência do cliente, medindo sinais de dados nos principais pontos de contato que impulsionam o CLV e implementam um caso de uso semelhante em seu ambiente. Todo o processo está resumido na imagem abaixo.

![Um infográfico das etapas amplas necessárias para utilizar o valor vitalício do cliente.](../images/use-cases/implementation-steps.png)

## Introdução {#getting-started}

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Serviço de consulta](../home.md): fornece uma interface de usuário e uma API RESTful, onde você pode usar consultas SQL para analisar e enriquecer seus dados.
* [Serviço de segmentação](../../segmentation/home.md): permite gerar públicos a partir dos dados do Perfil do cliente em tempo real.

## Pré-requisitos

Este guia requer que você tenha a [Distiller de dados](../data-distiller/overview.md) SKU como parte de sua oferta de pacote. Se não tiver certeza se tem essa informação, entre em contato com o representante de serviços da Adobe.

## Criar um conjunto de dados derivado {#create-derived-dataset}

A primeira etapa no estabelecimento do CLV é criar um conjunto de dados derivado dos sinais de dados capturados das ações do usuário. Esse caso de uso específico é registrado em um documento separado sobre um esquema de fidelidade de uma companhia aérea. Consulte o guia para saber como [use o Serviço de consulta para criar conjuntos de dados derivados baseados em decile para usar com os dados do seu perfil](./deciles-use-case.md). Exemplos completos e explicações são fornecidos no documento que explica as seguintes etapas:

* Crie um esquema para permitir a segmentação de decis.
* Use o Serviço de consulta para criar decis.
* Gerar conjuntos de dados decis.
* Ativar o esquema para uso no Perfil de cliente em tempo real.
* Crie um namespace de identidade e marque-o como o identificador principal.
* Crie uma consulta para calcular decis durante um período de pesquisa.

## Estender o modelo de dados do Insights e agendar atualizações {#extend-data-model-and-set-refresh-schedule}

Em seguida, você deve criar um modelo de dados personalizado ou estender um modelo de dados existente do Adobe Real-Time CDP para interagir com seus insights de relatórios CLV. Consulte a documentação para saber como [criar um modelo de dados de insights de relatórios por meio do Serviço de consulta para uso com dados de armazenamento acelerados e painéis definidos pelo usuário](../data-distiller/customizable-insights/reporting-insights-data-model.md#build-a-reporting-insights-data-model). O tutorial aborda as seguintes etapas:

* Crie um modelo para relatar insights com o Data Distiller.
* Criar tabelas, relações e preencher dados.
* Consulte o modelo de dados de insight de relatórios.
* Estenda seu modelo de dados com o modelo de dados do Real-Time CDP Insights.
* Crie tabelas de dimensão para estender seu modelo de insights de relatórios.
* Consulte seu modelo de dados de insights de relatório de armazenamento acelerado estendido

Consulte a documentação do Modelo de dados do Real-time Customer Data Platform Insights para saber como [personalizar seus modelos de consulta SQL para criar relatórios do Real-Time CDP para seus casos de uso de marketing e KPI (indicador principal de desempenho)](../../dashboards/cdp-insights-data-model.md).

Defina um agendamento para atualizar seu modelo de dados personalizado regularmente. Isso garante que os dados retornem como parte do pipeline de assimilação, conforme necessário, e preenche os painéis definidos pelo usuário. Consulte a [guia de agendamento de consultas](../ui/query-schedules.md#create-schedule) para saber como configurar sua programação.

## Crie um painel para capturar insights {#build-a-custom-dashboard}

Agora que criou seu modelo de dados personalizado, você está pronto para visualizar seus dados com consultas personalizadas e painéis definidos pelo usuário. Consulte a visão geral dos painéis definidos pelo usuário para obter orientação completa sobre como [criar um painel personalizado](../../dashboards/user-defined-dashboards.md). O guia da interface do usuário inclui detalhes sobre:

* Como criar um widget.
* Como usar o compositor de widgets.

Exemplos de widgets CLV personalizados que usam intervalos de decis podem ser vistos abaixo.

![Uma coleção de widgets CLTV personalizados baseados em decil.](../images/use-cases/deciles-user-defined-dashboard.png)

## Criar e ativar públicos-alvo de alto desempenho {#create-and-activate-audiences}

A próxima etapa é criar uma definição de segmento e gerar públicos-alvo a partir dos dados do Perfil do cliente em tempo real. Consulte o guia da interface do construtor de segmentos para saber como [criar e ativar públicos na Platform](../../segmentation/ui/segment-builder.md). O guia fornece seções sobre como:

* Crie definições de segmento usando uma combinação de atributos, eventos e públicos-alvo existentes como blocos de construção.
* Use a tela e os contêineres do construtor de regras para controlar a ordem em que as regras de segmentação são executadas.
* Visualize estimativas de seu público-alvo em potencial, permitindo ajustar as definições de segmento, conforme necessário.
* Ative todas as definições de segmento para a segmentação programada.
* Ative as definições de segmento especificadas para a segmentação por transmissão.

Em alternativa, existe também uma [tutorial em vídeo do construtor de segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-segments.html) disponível para obter mais informações.

## Ativar o público-alvo para uma campanha por email {#activate-audience-for-campaign}

Depois de criar o público-alvo, você estará pronto para ativá-lo para um destino. A Platform é compatível com diversos Provedores de serviços de email (ESPs) que permitem gerenciar suas atividades de marketing por email, como enviar campanhas promocionais por email.

Verifique a [visão geral de destinos de marketing por email](../../destinations/catalog/email-marketing/overview.md#connect-destination) para obter uma lista dos destinos suportados para os quais você deseja exportar dados (por exemplo, os [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) página).

## Veja os dados de análise retornados de sua campanha {#post-campaign-data-analysis}

Os dados de fontes agora podem ser [processado incrementalmente](../key-concepts/incremental-load.md) como parte de uma atualização agendada para seu modelo de dados no armazenamento de dados acelerado. Qualquer evento de resposta de clientes pode ser assimilado na Adobe Experience Platform à medida que ocorre ou em lotes. Seu modelo de dados pode ser atualizado uma ou várias vezes por dia, dependendo das configurações ou dos conectores de origem. Consulte a [visão geral da API de assimilação em lote](../../ingestion/batch-ingestion/api-overview.md) ou o [visão geral da assimilação por transmissão](../../ingestion/streaming-ingestion/overview.md) para obter mais informações.

Depois que seu modelo de dados é atualizado, seus widgets de painel personalizados fornecem sinais significativos que permitem medir e visualizar o valor vitalício do cliente.

![Um widget personalizado para mostrar o número de emails abertos de acordo com o público-alvo e a campanha de email.](../images/use-cases/post-activation-and-email-response-kpis.png)

Uma variedade de opções de visualização é fornecida para sua análise personalizada.

![O widget email aberto pelos buckets de campanha.](../images/use-cases/email-opened-by-campaign-buckets.png)

Esses insights podem, por sua vez, ajudar você a desenvolver suas estratégias de negócios para campanhas subsequentes.

![Uma coleção de quatro widgets personalizados que detalham os resultados da campanha de email.](../images/use-cases/example-widgets.png)

## Próximas etapas

Ao ler este documento, você deve entender melhor como usar o Real-time Customer Data Platform para rastrear e visualizar a métrica do valor vitalício do cliente (CLV). Para saber mais sobre os vários casos de uso de negócios atendidos pelo Serviço de query e Experience Platform, é recomendável ler os seguintes documentos:

* [Um exemplo completo de um caso de uso de navegador abandonado que demonstra a versatilidade e os benefícios do Serviço de consulta.](./abandoned-browse.md)
* [Como usar o Serviço de consulta e o aprendizado de máquina para determinar e filtrar a atividade de bot a partir do tráfego de visitante genuíno do site online](./bot-filtering.md)
* [Como fazer uma correspondência nos dados da Platform que combina resultados de vários conjuntos de dados correspondendo aproximadamente a uma string de sua escolha.](./fuzzy-match.md)

<!-- "Data signals are actions taken by consumers while online that offer clues about intent that can be acted upon. This includes anything from visiting a website to filling out a change of address or clicking an ad."  -->

<!-- "Customer touchpoints are your brand's points of customer contact, from start to finish." -->
