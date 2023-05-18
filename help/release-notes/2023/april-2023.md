---
title: Notas de versão da Adobe Experience Platform, abril de 2023
description: As notas de versão de abril de 2023 para o Adobe Experience Platform.
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: 963fc5e31e1728a8a1a7e94bc0cc47d010347325
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 4%

---

# Notas de versão da Adobe Experience Platform

>[!IMPORTANT]
>
>A partir de 15 de maio de 2023, a `Existing` será descontinuado do mapa de associação de segmentos para remover a redundância no ciclo de vida de associação de segmentos. Após essa alteração, os perfis qualificados em um segmento serão representados como `Realized` e os perfis desqualificados continuarão sendo representados como `Exited`. Para obter mais detalhes sobre esta alteração, leia o [Seção Serviço de segmentação](#segmentation).

**Data de lançamento: 26 de abril de 2023**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Painéis](#dashboards)
- [Preparação de dados](#data-prep)
- [Coleção de dados](#data-collection)
- [Destinos](#destinations)
- [Experience Data Model](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [Perfil do cliente em tempo real](#profile)
- [Serviço de segmentação](#segmentation)
- [Fontes](#sources)

## Painéis {#dashboards}

O Adobe Experience Platform fornece vários painéis através dos quais você pode visualizar informações importantes sobre os dados de sua organização, como capturados durante os instantâneos diários.

**Recursos novos ou atualizados** {#dashboards-new-updated-features}

| Recurso | Descrição |
| --- | --- |
| Painéis definidos pelo usuário | Agora você pode **filtrar dados históricos** dos seus insights de widget e use dados recentes ou um período de análise personalizado. Consulte a [guia de painéis definidos pelo usuário](../../dashboards/user-defined-dashboards.md#filter-historical-data) para obter mais informações.<br>Você também pode **duplicar os widgets existentes**. Ao personalizar uma duplicata e editar seus atributos, você pode evitar a reinicialização a partir do início ao criar um novo widget exclusivo. Leia o [guia de duplicação de widgets](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) para saber mais. |

{style="table-layout:auto"}

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo o [visão geral dos painéis](../../dashboards/home.md).

## Preparação de dados {#data-prep}

A Preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Atualizações do período de preenchimento retroativo para Adobe Analytics em sandboxes de não produção | O período de preenchimento retroativo para Adobe Analytics em sandboxes de não produção foi reduzido para três meses. O preenchimento retroativo de sandboxes de produção permanece o mesmo em 13 meses. Essa alteração se aplica somente a novos fluxos e não afetará os fluxos existentes. Para obter mais informações, leia a [Visão geral do Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nova função mapeadora para converter strings FPID em ECID | Use o `fpid_to_ecid` para converter strings FPID em ECID para uso em aplicativos Experience Platform e Experience Cloud. Para obter mais informações, leia a [Guia de funções de Preparação de dados](../../data-prep/functions.md). |

{style="table-layout:auto"}

Para obter mais informações sobre Preparação de dados, leia a [Visão geral da preparação de dados](../../data-prep/home.md).

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente e enviá-los para a Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não-Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Ofuscação de endereço IP para datastreams | Agora é possível definir opções de ofuscação de IP no nível do conjunto de dados parcial ou completo na variável [interface do usuário de configuração do datastream](../../edge/datastreams/configure.md). <br><br>A configuração de ofuscação de IP no nível do conjunto de dados tem prioridade sobre qualquer ofuscação de IP configurada no Adobe Target e no Audience Manager. <br><br>Os dados enviados para a Adobe Analytics não são afetados pelo nível do conjunto de dados [!UICONTROL Ofuscação de IP] configuração. No momento, a Adobe Analytics recebe endereços IP não ofuscados. Para que o Analytics receba endereços IP ofuscados, é necessário configurar a ofuscação de IP separadamente, no Adobe Analytics. Esse comportamento será atualizado em versões futuras.<br><br> Para obter mais detalhes sobre ofuscação de IP e instruções sobre como configurá-lo, consulte o [documentação de configuração do datastream](../../edge/datastreams/configure.md#advanced-options). |
| [Substituições de configuração do fluxo de dados](../../edge/datastreams/overrides.md) | Agora é possível definir opções de configuração adicionais para conjuntos de dados, que podem ser usadas para substituir configurações específicas, como conjuntos de dados de eventos, tokens de propriedade do Target, contêineres de sincronização de ID e conjuntos de relatórios do Analytics. <br><br>A substituição das configurações do conjunto de dados é um processo de duas etapas: <ol><li>Primeiro, você deve definir as substituições de configuração do conjunto de dados na variável [página de configuração do datastream](../../edge/datastreams/configure.md).</li><li>Em seguida, você deve enviar as substituições para a Edge Network por meio de um comando do SDK da Web ou usando o SDK da Web [extensão de tag](../../edge/extension/web-sdk-extension-configuration.md).</li></ol> |
| Segredo JWT OAuth | O [Segredo JWT OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) permite que os clientes usem tokens do Adobe e do Google Service para suportar interações servidor a servidor no encaminhamento de eventos. |
| [!DNL Pinterest Conversions API] extensão | O [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) a extensão de encaminhamento de eventos permite aproveitar os dados capturados na Rede de borda do Adobe Experience Platform e enviá-los para [!DNL Pinterest] na forma de eventos do lado do servidor usando o [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Novos destinos** {#new-destinations}

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] conexão](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Use o destino Envolvimento da conta do Marketing Cloud do Salesforce (antigo Pardot) para capturar, rastrear, pontuar e classificar leads. Use esse destino para casos de uso B2B envolvendo vários departamentos e tomadores de decisão que exigem ciclos de vendas e decisões mais longos. |

{style="table-layout:auto"}

**Funcionalidade nova ou atualizada** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Monitoramento de fluxo de dados para [!DNL Custom Personalization] e [!DNL Adobe Commerce] destinos | <p> Agora você pode ver as métricas de ativação do [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [Personalização personalizada](../../destinations/catalog/personalization/custom-personalization.md) e [Personalização Personalizada Com Atributos](../../destinations/catalog/personalization/custom-personalization.md) conexões. </p> <p>![Imagem Adobe Commerce](/help/destinations/assets/common/adobe-commerce-metrics.png "Métricas do Adobe Commerce"){width="100" zoomable="yes"}</p>  Consulte [Monitorar fluxos de dados no espaço de trabalho Destinos](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) para obter mais detalhes. |
| Novo **[!UICONTROL Anexar ID de segmento ao nome do segmento]** para o campo [!DNL Google Ad Manager] e [!DNL Google Ad Manager 360] destinos | <p>Agora você pode ter o nome do segmento em [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) e [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) inclua a ID de segmento do Experience Platform, desta forma: `Segment Name (Segment ID)`.</p><p>![Anexar imagem da ID de segmento](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Novo Anexar ID de segmento ao campo de nome de segmento "){width="100" zoomable="yes"}</p> |
| Preenchimentos retroativos do público-alvo agendados | <p>Para o [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) no destino, a ativação dos preenchimentos retroativos do público-alvo no destino está programada para ocorrer de 24 a 48 horas após um segmento ser mapeado pela primeira vez para uma conexão de destino. Essa atualização é uma resposta à política da Google de esperar 24 horas até assimilar dados e melhorará as taxas de correspondência entre a CDP em tempo real e a [!DNL Google Display & Video 360].</p> <p>Observe que essa é uma configuração de backend aplicável somente a esse destino e que não está relacionada a nenhuma opção de agendamento configurável pelo cliente na interface do usuário.</p> |

{style="table-layout:auto"}

**Correções e aprimoramentos** {#destinations-fixes-and-enhancements}

- Corrigimos um problema no **Identidades excluídas** métricas de relatório para exportações de destino baseadas em arquivo. Os clientes recebiam todas as IDs exportadas da exportação ativada, conforme esperado. No entanto, a variável **Identidades excluídas** a métrica de relatórios na interface do usuário exibia incorretamente números altos de identidades excluídas devido a identidades de contagem incorretas que nunca deveriam ser exportadas. (PLAT-149774)
- Corrigimos um problema no **Agendamento** etapa do fluxo de trabalho de ativação. Para destinos que exigem uma ID de mapeamento, os clientes não conseguiram adicionar uma ID de mapeamento para segmentos adicionados às conexões de destino existentes. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Para obter informações mais gerais sobre destinos, consulte [visão geral dos destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Alternar nomes para exibição | O Editor de esquema agora oferece um botão para alterar os nomes dos campos originais e os nomes de exibição legíveis em humanos.<br>![O Editor de esquema com o botão de opção de nome de exibição é realçado.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "Alternar nome de exibição do Editor de esquemas"){width="100" zoomable="yes"}<br>Essa flexibilidade permite uma melhor descoberta de campo e edição de seus esquemas. Os nomes de exibição para grupos de campos padrão são gerados pelo sistema, mas também podem ser personalizados por meio da interface do usuário, se necessário. Leia o [exibir a documentação de alternância de nome](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) para saber mais. |

{style="table-layout:auto"}

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Esquema | [[!UICONTROL Campos de classificação Adobe Target]](https://github.com/adobe/xdm/pull/1719/files) | Um novo esquema XDM para conjuntos de dados de Classificação do Target contendo um conjunto de campos de metadados para classificar atividades e experiências do Target. |

{style="table-layout:auto"}

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Extensão de União de Conta do Serviço de Perfil Unificado do Adobe]](https://github.com/adobe/xdm/pull/1696/files) | Adição de um grupo de campos de extensão de conta para Perfil do cliente em tempo real que permite que os usuários adicionem associação de segmento à união de contas. |
| Esquema | [[!UICONTROL Esquema do Sistema de Atributos Calculados]](https://github.com/adobe/xdm/pull/1696/files) | O grupo de campos Atributos calculados usado pelo Perfil do cliente em tempo real foi atualizado para um esquema global somente leitura do sistema. |
| Grupo de campos | Vários | Adição de vários eventos como campos para [[!UICONTROL Esquema da série cronológica]](https://github.com/adobe/xdm/pull/1718/files). |
| Grupo de campos | Detalhes de fidelidade do perfil | [Correção do título](https://github.com/adobe/xdm/pull/1717/files) para `xdm:upgradeDate` de &quot;Nome do programa&quot; para &quot;Data de atualização&quot;. |
| Grupo de campos | Vários | Vários campos de [[!UICONTROL Item de decisão]](https://github.com/adobe/xdm/pull/1714/files) foram atualizadas para remover a hierarquia aninhada dupla. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM na Platform, leia o [Visão geral do sistema XDM](../../xdm/home.md).

## Real-Time Customer Data Platform

Criado no Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) ajuda as empresas a unirem dados conhecidos e desconhecidos para ativar perfis do cliente com decisões inteligentes na jornada do cliente. [!DNL Real-Time CDP] O combina várias fontes de dados corporativas para criar perfis de clientes em tempo real. Os segmentos criados a partir desses perfis podem ser enviados para destinos downstream para fornecer experiências personalizadas individuais do cliente em todos os canais e dispositivos.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Página inicial do Real-Time CDP aprimorada | O [Página inicial do Real-Time CDP](https://experience.adobe.com) O foi aprimorado com uma aparência atualizada e desempenho aprimorado. A página inicial agora tem reconhecimento de permissões e apresentará widgets relevantes aos recursos aos quais você tem acesso. Para obter mais informações, leia a [Visão geral do painel da página inicial do Real-Time CDP](../../rtcdp/home-page-dashboards.md). |
| Pesquisa de autoidentificação | A pesquisa de autoidentificação é um breve questionário apresentado na página inicial da interface do usuário do Adobe Experience Platform. Use a pesquisa de autoidentificação para criar seu perfil pessoal do Experience Platform e receber diretrizes personalizadas com base em suas seleções. Para obter mais informações, leia a [visão geral da pesquisa de autoidentificação](../../landing/self-identification.md). |

Para obter mais informações sobre [!DNL Real-Time CDP], consulte o [[!DNL Real-Time CDP] visão geral](../../rtcdp/overview.md).

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagirem com sua marca. Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Expiração de dados de perfil pseudônimo | O prazo de validade dos dados de perfil pseudônimo está agora disponível! Esta versão removerá continuamente perfis pseudônimos obsoletos da sua instância do Experience Platform depois de ativados. Para saber mais sobre esse recurso e Perfis pseudônimos, leia o [Guia de expiração de dados de perfil pseudônimo](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## Serviço de segmentação {#segmentation}

[!DNL Segmentation Service] O define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da base do cliente. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Mapa de associação de segmento | Como seguimento ao anúncio anterior em fevereiro, em 15 de maio de 2023, o `Existing` será descontinuado do mapa de associação de segmentos para remover a redundância no ciclo de vida de associação de segmentos. Após essa alteração, os perfis qualificados em um segmento serão representados como `Realized` e os perfis desqualificados continuarão sendo representados como `Exited`.<br/><br/> Essa alteração pode afetar você se, você estiver usando [destinos corporativos](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Hubs de eventos do Azure, API HTTP) e pode ter processos downstream automatizados em vigor com base no `Existing` status. Se esse for o caso, reveja suas integrações downstream. Se estiver interessado em identificar perfis recém-qualificados além de um determinado tempo, considere usar uma combinação do `Realized` e o `lastQualificationTime` no mapa de associação de segmentos. Para obter mais informações, entre em contato com o representante do Adobe. |

{style="table-layout:auto"}

Para obter mais informações sobre [!DNL Segmentation Service]consulte o [Visão geral da segmentação](../../segmentation/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte a API para filtrar dados no nível da linha para a fonte do Salesforce CRM. | Use operadores lógicos e de comparação para filtrar dados no nível da linha para a origem do CRM do Salesforce. Leia o guia em [filtragem de dados de uma fonte usando a API](../../sources/tutorials/api/filter.md) para obter mais informações. |
| Disponibilidade beta do Shopify Streaming | O [Comprar fonte de transmissão](../../sources/connectors/ecommerce/shopify-streaming.md) O agora está disponível em beta. Use a fonte de transmissão Shopify para transmitir dados da sua conta de parceiros Shopify para o Experience Platform. |
| Disponibilidade geral da integração do OneTrust | O [Origem de Integração do OneTrust](../../sources/connectors/consent-and-preferences/onetrust.md) agora está pronta. Use a fonte de integração do OneTrust para trazer os dados de consentimento e preferências da sua conta de Integração do OneTrust para o Experience Platform. |
| Disponibilidade geral da Oracle Service Cloud | O [Origem da nuvem do Oracle Service](../../sources/connectors/customer-success/oracle-service-cloud.md) agora está pronta. Use a fonte da nuvem do Oracle Service para trazer seus dados da nuvem do Oracle Service para o Experience Platform. |

{style="table-layout:auto"}

Para saber mais sobre fontes, leia a [visão geral das fontes](../../sources/home.md).