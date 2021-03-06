---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 4956b940dfd25f55eaf67296f2cb31db65fac079
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 5%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 22 de junho de 2022**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[Coleta de dados]](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de query](#query-service)
- [Fontes](#sources)

## [!DNL Data Science Workspace] {#dsw}

O Data Science Workspace usa aprendizagem de máquina e inteligência artificial para liberar insights de seus dados. Integrado ao Adobe Experience Platform, o Data Science Workspace ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções de Adobe. Uma das maneiras como o Data Science Workspace consegue isso é usando o JupyterLab. O JupyterLab é uma interface de usuário baseada na Web para <a href="https://jupyter.org/" target="_blank">Jupyter do projeto</a> e é totalmente integrado ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para os cientistas de dados trabalharem com notebooks, códigos e dados do Júpiter.

| Recurso | Descrição |
| --- | --- |
| Iniciador do JupyterLab | O JupyterLab Launcher agora inclui iniciadores para notebooks Spark 3.2. As inicializações do notebook Spark 2.4 agora são substituídas pelos notebooks Spark 3.2 e farão parte desta versão. |
| Spark 3.2 | As novas receitas do Scala (Spark) e do PySpark agora usam o Spark 3.2 |
| Kernels | Os notebooks Scala (Spark) agora são criados por meio do kernel Scala. Os notebooks PySpark agora são criados por meio do kernel Python. Os kernel Spark e PySpark estão obsoletos e configurados para serem removidos em uma versão subsequente. |
| Receitas | As novas receitas PySpark e Spark agora seguem o fluxo de trabalho Docker semelhante às receitas Python e R. |

{style=&quot;table-layout:auto&quot;}

Para obter informações mais gerais sobre o Data Science Workspace, consulte o [documentação de visão geral](../../data-science-workspace/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ----------- | ----------- |
| Suporte ao Destination SDK (Beta) para [[!DNL Google Cloud Storage]](../../destinations/destination-sdk/server-and-file-configuration.md#gcs-example) destinos com base em arquivo e [nomes de arquivo configuráveis](../../destinations/destination-sdk/file-based-destination-configuration.md#file-name-configuration). | Agora você pode usar o Destination SDK para criar destinos de armazenamento da Google Cloud e definir nomes de arquivo personalizados para arquivos exportados, por meio de macros de nome de arquivo. <br><br> No momento, o suporte ao destino baseado em arquivo no Adobe Experience Platform Destination SDK está na versão beta. A documentação e a funcionalidade estão sujeitas a alterações. |
| A coluna Segmento no fluxo de dados é executada para destinos em lote | Para que o fluxo de dados seja executado para destinos em lote, a interface do usuário agora exibe o nome do segmento associado a cada execução do fluxo de dados. Leia mais sobre [o fluxo de dados é executado para destinos em lote](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations). |

{style=&quot;table-layout:auto&quot;}

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [(Beta) Google Ad Manager 360](../../destinations/catalog/advertising/google-ad-manager-360-connection.md) | O [!DNL Google Ad Manager 360] a conexão habilita o upload em lote para [!DNL publisher provided identifiers] (PPID) em [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage] <br><br>No momento, esse destino está na versão Beta e só está disponível para um número limitado de clientes. Para solicitar acesso à [!DNL Google Ad Manager 360] entre em contato com o representante do Adobe e forneça [!DNL IMS Organization ID]. |
| [[!DNL Medallia]](/help/destinations/catalog/voice/medallia-connector.md) | Ative perfis para pesquisas direcionadas da Medallia e coleta de feedback para entender melhor as necessidades e expectativas do cliente. |
| [[!DNL Adobe Advertising Cloud DSP]](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) | A Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) o destino permite compartilhar segmentos originais autenticados com anunciantes e usuários aprovados para ativação da campanha com o DSP. |

{style=&quot;table-layout:auto&quot;}

Para obter informações mais gerais sobre destinos, consulte [visão geral dos destinos](../../destinations/home.md).

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente e enviá-los para a Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não-Adobe.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| [Configuração de tipo de acesso para datastreams](../../edge/datastreams/overview.md#create) | Ao criar um novo armazenamento de dados, você pode selecionar o tipo de solicitações que deseja que a Rede de Borda aceite: <ul><li>**[!UICONTROL Autenticação mista]**: Quando essa opção é selecionada, a Edge Network aceita solicitações autenticadas e não autenticadas. Selecione essa opção quando planeja usar o SDK da Web ou [SDK móvel](https://aep-sdks.gitbook.io/docs/), juntamente com o [API do servidor](../../server-api/overview.md). </li><li>**[!UICONTROL Apenas Autenticado]**: Quando essa opção é selecionada, a Rede de Borda aceita apenas solicitações autenticadas. Selecione essa opção quando planeja usar somente a API do servidor e deseja impedir que qualquer solicitação não autenticada seja processada pela variável [!DNL Edge Network]. </li></ul> |
| [Renderizar apresentações](../../edge/personalization/rendering-personalization-content.md#applypropositions) em aplicativos de página única sem aumentar métricas. | O recém-adicionado `applyPropositions` permite renderizar ou executar uma matriz de propostas a partir de [!DNL Target] em aplicativos de página única, sem aumentar o [!DNL Analytics] e [!DNL Target] métricas. Isso aumenta a precisão dos relatórios. |
| [Compartilhamento de IDs entre dispositivos móveis e domínios](../../edge/identity/id-sharing.md) | O SDK da Web da Adobe Experience Platform agora é compatível com recursos de compartilhamento de ID de visitante que permitem fornecer experiências personalizadas com mais precisão, entre aplicativos móveis e conteúdo da Web móvel e entre domínios. |
| [Extensão de tag da Camada de dados Google](../../tags/extensions/web/google-data-layer/overview.md) | A extensão Camada de dados da Google permite usar uma camada de dados da Google na implementação de tags. |
| [Extensão de encaminhamento de eventos de Conversões aprimoradas do Google Ads](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html) | A extensão Conversões aprimoradas do Google Ads permite aprimorar as conversões do Google Ads em tempo real. |
| [Extensão de encaminhamento de evento de mailchimp](../../tags/extensions/web/mailchimp/overview.md) | A extensão de encaminhamento de evento Mailchimp envia eventos para a API de Marketing Mailchimp que pode acionar emails para campanhas de marketing, jornadas ou transações de Mailchimp. |

Para obter mais informações, consulte o [visão geral da coleta de dados](../../rtcdp-connections/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Classe | [[!UICONTROL Medicação]](https://github.com/adobe/xdm/blob/master/components/classes/medication.schema.json) | Uma classe da indústria de saúde que capta detalhes sobre uma substância usada para tratamento médico, especialmente um medicamento ou medicamento. |
| Classe | [[!UICONTROL Plano]](https://github.com/adobe/xdm/blob/master/components/classes/plan.schema.json) | Uma classe de indústria de saúde que captura detalhes sobre um plano médico, como um plano de saúde ou plano de seguro. |
| Classe | [[!UICONTROL Provedor]](https://github.com/adobe/xdm/blob/master/components/classes/provider.schema.json) | Uma classe do setor de saúde que captura detalhes sobre um provedor de saúde. |
| Classe | [[!UICONTROL Pagador]](https://github.com/adobe/xdm/blob/master/components/classes/payer.schema.json) | Uma classe do setor de saúde que captura detalhes sobre uma seguradora. |
| Classe | [[!UICONTROL Programação de Evento ao Vivo]](https://github.com/adobe/xdm/blob/master/components/classes/live-event-schedule.json) | Uma classe do setor de esportes e entretenimento que captura detalhes sobre uma programação de eventos ao vivo, como uma programação de concertos itinerantes ou uma programação de uma equipe esportiva. |
| Classe | [[!UICONTROL Localização ]](https://github.com/adobe/xdm/blob/master/components/classes/location.json) | Uma classe da indústria de esportes e entretenimento que captura a localização de um evento ao vivo, como uma sala de concertos ou arena esportiva. |
| Grupo de campos | [[!UICONTROL Medicamentos para a saúde]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json) | Um grupo de campos para a variável [!UICONTROL Medicação] classe que captura detalhes sobre a medicação, como nome da marca, número do lote e quantidade. |
| Grupo de campos | [[!UICONTROL Detalhes do Plano de Saúde]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/plan/healthcare-plan-details.schema.json) | Um grupo de campos para a variável [!UICONTROL Plano] classe que captura detalhes como rede, tipo e status ativo. |
| Grupo de campos | [[!UICONTROL Provedor de saúde]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json) | Um grupo de campos para a variável [!UICONTROL Provedor] classe que capta dados de um profissional de saúde individual ou de uma organização de cuidados de saúde licenciada para prestar serviços de diagnóstico e tratamento de saúde. |
| Grupo de campos | [[!UICONTROL Detalhes do Membro da Saúde]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json) | Um grupo de campos para a variável [!UICONTROL Perfil individual XDM] classe que captura detalhes de uma pessoa que tem ou receberá um serviço ou assistência, como informações de contato, médico de assistência primária e informações de plano. |
| Grupo de campos | [[!UICONTROL Detalhes da Sitecool]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json) | Um grupo de campos para a variável [!UICONTROL ExperiênciaEvento XDM] classe que captura informações coletadas por ferramentas, como chatbot, pesquisa e assim por diante. |
| Grupo de campos | [[!UICONTROL Compra de Tíquete do Evento em Tempo Real]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-live-event-ticket-purchase.json) | Um grupo de campos para a variável [!UICONTROL ExperiênciaEvento XDM] classe que captura o histórico de compras de ingressos para um evento ao vivo, como um concerto ou um jogo esportivo. |
| Grupo de campos | [[!UICONTROL Programação de eventos desportivos e de entretenimento]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/live-event-schedule/sports-entertainment-event-schedule.schema.json) | Um grupo de campos para a variável [!UICONTROL Programação de Evento ao Vivo] classe que captura mais detalhes sobre a programação, como o nome da atração, os horários de abertura de portas e muito mais. |
| Grupo de campos | [[!UICONTROL Local de evento de entretenimento de esportes]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/location/sports-entertainment-event-venue.schema.json) | Um grupo de campos para a variável [!UICONTROL Localização] classe que captura mais detalhes sobre o local do evento, como capacidade de assentos e Áreas de Mercado Designadas (DMAs). |
| Schema global | (Vários) | Novos esquemas globais estão disponíveis para métricas de destinos para insights RTCDP. Veja o seguinte [solicitação pull](https://github.com/adobe/xdm/pull/1560) para obter mais detalhes. |

{style=&quot;table-layout:auto&quot;}

**Componentes XDM atualizados**

| Tipo de componente | Nome | Atualizar descrição |
| --- | --- | --- |
| Comportamento | [[!UICONTROL Esquema da série cronológica]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | Adição de um tipo de evento de atualização de estados de mídia. |
| Grupo de campos | [[!UICONTROL Reserva de Loja]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json) | Adição de uma propriedade de check-out de alojamento. |
| Tipo de dados | [[!UICONTROL Informações da mídia]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Adição de campos state-start e states-end . |
| Extensão | [[!UICONTROL Evento Workfront Change]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Adicionados dois campos usados para armazenar atributos para ajudar a identificar o usuário e a hora de um evento de criação. |
| Extensão | [[!UICONTROL Adobe CJM ExperienceEvent - Detalhes de interação da mensagem]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/message-interaction.schema.json) | Adição de assinatura, consentimento, email personalizado e informações de dados adicionais no objeto da landing page. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre o XDM na Platform, consulte o [Visão geral do sistema XDM](../../xdm/home.md).

## Serviço de query {#query-service}

O Serviço de Consulta permite que você use o SQL padrão para consultar dados no Adobe Experience Platform [!DNL Data Lake]. É possível unir qualquer conjunto de dados da [!DNL Data Lake] e capture os resultados do query como um novo conjunto de dados para usar nos relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Rotulação de esquema ad hoc | Gerencie o acesso a dados confidenciais aplicando rótulos a campos de dados de esquemas ad hoc que são automaticamente gerados por meio de consultas CTAS do Serviço de query. Você pode restringir o uso de determinados campos ou conjuntos de dados de esquemas ad hoc para controlar o acesso a dados pessoais confidenciais e a informações de identificação pessoal. Ao usar o recurso de controle de acesso baseado em atributos, você pode rotular campos de esquema ad hoc por meio da interface do usuário da plataforma. |
| `FLATTEN` definição | Ao se conectar a um banco de dados por meio de ferramentas de BI de terceiros, a variável `FLATTEN` a configuração nivela estruturas de dados aninhadas em colunas separadas, onde o nome do atributo se torna o nome da coluna que retém os valores da linha. Isso melhora a usabilidade de esquemas ad hoc e reduz a carga de trabalho necessária para recuperar, analisar, transformar e relatar dados em ferramentas de BI que não suportam estruturas de dados aninhadas. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre Serviços de query, consulte [Visão geral do Serviço de query](../../query-service/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| Versão beta de [!DNL Mixpanel] source | Agora você pode usar o [!DNL Mixpanel] fonte para assimilar dados de análise da sua [!DNL Mixpanel] para o Experience Platform. Consulte a [[!DNL Mixpanel] documentação de origem](../../sources/connectors/analytics/mixpanel.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
