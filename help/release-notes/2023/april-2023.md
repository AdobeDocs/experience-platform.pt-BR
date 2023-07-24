---
title: Notas de versão da Adobe Experience Platform de abril de 2023
description: As notas de versão de abril de 2023 do Adobe Experience Platform.
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 13%

---

# Notas de versão da Adobe Experience Platform

>[!IMPORTANT]
>
>A partir de 15 de maio de 2023, a `Existing` o status será descontinuado do mapa de associação de segmento para remover a redundância no ciclo de vida da associação de segmento. Após essa alteração, os perfis qualificados em um segmento serão representados como `Realized` e os perfis desqualificados continuarão a ser representados como `Exited`. Para obter mais detalhes sobre esta alteração, leia a [Seção Serviço de segmentação](#segmentation).

**Data de lançamento: 26 de abril de 2023**

Atualizações dos recursos já existentes na Adobe Experience Platform:

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

O Adobe Experience Platform fornece vários painéis por meio dos quais você pode visualizar insights importantes sobre os dados de sua organização, conforme capturados durante instantâneos diários.

**Recursos novos ou atualizados** {#dashboards-new-updated-features}

| Recurso | Descrição |
| --- | --- |
| Painéis definidos pelo usuário | Agora você pode **filtrar dados históricos** dos insights do widget e use dados recentes ou um período de análise personalizado. Consulte a [guia de painéis definido pelo usuário](../../dashboards/user-defined-dashboards.md#filter-historical-data) para obter mais informações.<br>Você também pode agora **duplicar widgets existentes**. Personalizando uma duplicata e editando seus atributos, você pode evitar reiniciar do início ao criar um widget novo e exclusivo. Leia o [guia de duplicação do widget](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) para saber mais. |

{style="table-layout:auto"}

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo o [visão geral dos painéis](../../dashboards/home.md).

## Preparação de dados {#data-prep}

O Preparo de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Atualizações no período de preenchimento retroativo para Adobe Analytics em sandboxes de não produção | O período de preenchimento retroativo para o Adobe Analytics em sandboxes de não produção foi reduzido para três meses. O preenchimento retroativo para sandboxes de produção permanece o mesmo em 13 meses. Essa alteração se aplica somente a novos fluxos e não afetará os existentes. Para obter mais informações, leia a [Visão geral do Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nova função de mapeador para converter cadeias de caracteres FPID para ECID | Use o `fpid_to_ecid` Função para converter strings FPID em ECID para uso em aplicativos Experience Platform e Experience Cloud. Para obter mais informações, leia a [Guia de funções do Preparo de dados](../../data-prep/functions.md). |

{style="table-layout:auto"}

Para obter mais informações sobre o Preparo de dados, leia o [Visão geral do Preparo de dados](../../data-prep/home.md).

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Ofuscação de endereço IP para sequências de dados | Agora é possível definir opções de ofuscação de IP no nível de fluxo de dados parcial ou completo na [interface de configuração de sequência de dados](../../datastreams/configure.md). <br><br>A configuração de ofuscação de IP no nível de fluxo de dados tem precedência sobre qualquer ofuscação de IP configurada no Adobe Target e no Audience Manager. <br><br>Os dados enviados para a Adobe Analytics não são afetados pelo nível de fluxo de dados [!UICONTROL Ofuscação de IP] configuração. Atualmente, o Adobe Analytics recebe endereços IP não ofuscados. Para que o Analytics receba endereços IP ofuscados, você deve configurar a ofuscação de IP separadamente no Adobe Analytics. Esse comportamento será atualizado em versões futuras.<br><br> Para obter mais detalhes sobre a ofuscação de IP e instruções sobre como configurá-la, consulte o [documentação de configuração da sequência de dados](../../datastreams/configure.md#advanced-options). |
| [Substituições de configuração da sequência de dados](../../datastreams/overrides.md) | Agora é possível definir opções de configuração adicionais para fluxos de dados, que você pode usar para substituir configurações específicas, como conjuntos de dados de eventos, tokens de propriedade do Target, contêineres de sincronização de ID e conjuntos de relatórios do Analytics. <br><br>Substituir as configurações de sequência de dados é um processo de duas etapas: <ol><li>Primeiro, você deve definir as substituições de configuração da sequência de dados no [página de configuração do fluxo de dados](../../datastreams/configure.md).</li><li>Em seguida, você deve enviar as substituições para a Rede de borda por meio de um comando do SDK da Web ou usando o SDK da Web [extensão de tag](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).</li></ol> |
| Segredo JWT do OAuth  | A variável [Segredo JWT do OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) O permite que os clientes usem os tokens de serviço do Adobe e do Google para oferecer suporte às interações servidor a servidor no encaminhamento de eventos. |
| [!DNL Pinterest Conversions API] extensão | A variável [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) a extensão de encaminhamento de eventos permite aproveitar os dados capturados na rede de borda da Adobe Experience Platform e enviá-los para o [!DNL Pinterest] na forma de eventos do lado do servidor usando o [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos** {#new-destinations}

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] conexão](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Use o destino Salesforce Marketing Cloud Account Engagement (anteriormente conhecido como Pardot) para capturar, rastrear, pontuar e pontuar leads. Use esse destino para casos de uso de B2B que envolvam vários departamentos e tomadores de decisão que exigem ciclos de vendas e decisões mais longos. |

{style="table-layout:auto"}

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Monitoramento de fluxo de dados para [!DNL Custom Personalization] e [!DNL Adobe Commerce] destinos | <p> Agora você pode ver as métricas de ativação para o [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [Personalização personalizada](../../destinations/catalog/personalization/custom-personalization.md) e a variável [Personalização personalizada com atributos](../../destinations/catalog/personalization/custom-personalization.md) conexões. </p> <p>![Imagem do Adobe Commerce](/help/destinations/assets/common/adobe-commerce-metrics.png "Métricas do Adobe Commerce"){width="100" zoomable="yes"}</p>  Consulte [Monitorar fluxos de dados no espaço de trabalho de Destinos](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) para obter mais detalhes. |
| Novo **[!UICONTROL Anexar ID do segmento ao nome do segmento]** campo para o [!DNL Google Ad Manager] e [!DNL Google Ad Manager 360] destinos | <p>Agora você pode ter o nome do segmento no [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) e [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) inclua a ID de segmento do Experience Platform, desta forma: `Segment Name (Segment ID)`.</p><p>![Anexar imagem da ID do segmento](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Novo Anexar ID de segmento ao campo de nome do segmento "){width="100" zoomable="yes"}</p> |
| Preenchimentos retroativos de público programados | <p>Para o [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) destino, a ativação de preenchimentos retroativos de público para o destino é agendada para ocorrer de 24 a 48 horas depois que um segmento é mapeado pela primeira vez para uma conexão de destino. Essa atualização é uma resposta à política da Google de aguardar 24 horas até a assimilação de dados e melhorará as taxas de correspondência entre a Real-time CDP e [!DNL Google Display & Video 360].</p> <p>Observe que essa é uma configuração de backend aplicável somente a esse destino e não está relacionada a nenhuma opção de agendamento configurável pelo cliente na interface do usuário do.</p> |

{style="table-layout:auto"}

**Correções e aprimoramentos** {#destinations-fixes-and-enhancements}

- Corrigimos um problema no **Identidades excluídas** métricas de relatório para exportações de destino baseadas em arquivo. Os clientes recebiam todas as IDs exportadas da exportação ativada, conforme esperado. No entanto, a **Identidades excluídas** a métrica de relatórios na interface exibia incorretamente números altos de identidades excluídas devido à contagem incorreta de identidades que nunca deveriam ser exportadas. (PLAT-149774)
- Corrigimos um problema no **Agendamento** etapa do workflow de ativação. Para destinos que exigem uma ID de mapeamento, os clientes não conseguiram adicionar uma ID de mapeamento para segmentos adicionados a conexões de destino existentes. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos das ações do cliente, definir públicos do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Alternância de nomes de exibição | O Editor de esquemas agora fornece uma alternância entre os nomes de campo originais e os nomes de exibição mais legíveis.<br>![O Editor de esquemas com a opção de nome de exibição realçada.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "Alternância do nome de exibição do Editor de esquemas"){width="100" zoomable="yes"}<br>Essa flexibilidade permite uma melhor descoberta de campo e edição de seus esquemas. Os nomes de exibição para grupos de campos padrão são gerados pelo sistema, mas também podem ser personalizados por meio da interface do usuário, se necessário. Leia as [documentação de alternância do nome de exibição](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) para saber mais. |

{style="table-layout:auto"}

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Esquema | [[!UICONTROL Campos de classificação do Adobe Target]](https://github.com/adobe/xdm/pull/1719/files) | Um novo esquema XDM para conjuntos de dados de Classificação do Target contendo um conjunto de campos de metadados para classificar atividades e experiências do Target. |

{style="table-layout:auto"}

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Extensão de União da Conta de Serviço de Perfil Unificado do Adobe]](https://github.com/adobe/xdm/pull/1696/files) | Adição de um grupo de campos de extensão de conta para o Perfil de cliente em tempo real que permite aos usuários adicionar associação de segmento na união de contas. |
| Esquema | [[!UICONTROL Esquema de Sistema de Atributos Calculados]](https://github.com/adobe/xdm/pull/1696/files) | O grupo de campos Atributos computados usado pelo Perfil do cliente em tempo real foi atualizado para um esquema global somente leitura do sistema. |
| Grupo de campos | Múltiplo | Adição de vários eventos como campos para [[!UICONTROL Esquema de série temporal]](https://github.com/adobe/xdm/pull/1718/files). |
| Grupo de campos | Detalhes de fidelidade do perfil | [Corrigido o título](https://github.com/adobe/xdm/pull/1717/files) para `xdm:upgradeDate` de &quot;Nome do programa&quot; para &quot;Data de atualização&quot;. |
| Grupo de campos | Múltiplo | Vários campos de [[!UICONTROL Item de decisão]](https://github.com/adobe/xdm/pull/1714/files) foram atualizadas para remover a hierarquia aninhada dupla. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM na Platform, leia o [Visão geral do sistema XDM](../../xdm/home.md).

## Real-Time Customer Data Platform

Integrado no Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) ajuda as empresas a unirem dados conhecidos e desconhecidos para ativar perfis de clientes com decisões inteligentes em toda a jornada do cliente. [!DNL Real-Time CDP] O combina várias fontes de dados corporativos para criar perfis de clientes em tempo real. Os segmentos criados a partir desses perfis podem ser enviados para destinos downstream para fornecer experiências personalizadas de um para um do cliente em todos os canais e dispositivos.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Página inicial do Real-Time CDP aprimorada | A variável [Página inicial do Real-Time CDP](https://experience.adobe.com) O foi aprimorado com uma aparência atualizada e melhor desempenho. A página inicial agora tem reconhecimento de permissões e apresentará widgets relevantes para os recursos aos quais você tem acesso. Para obter mais informações, leia a [Visão geral do painel da página inicial do Real-Time CDP](../../rtcdp/home-page-dashboards.md). |
| Pesquisa de autoidentificação | A pesquisa de autoidentificação é um pequeno questionário apresentado na página inicial da interface do usuário do Adobe Experience Platform. Use a pesquisa de autoidentificação para criar seu perfil pessoal do Experience Platform e receber diretrizes personalizadas com base em suas seleções. Para obter mais informações, leia a [visão geral da pesquisa de autoidentificação](../../landing/self-identification.md). |

Para obter mais informações sobre [!DNL Real-Time CDP], consulte o [[!DNL Real-Time CDP] visão geral](../../rtcdp/overview.md).

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde e quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, você pode ter uma visualização integral de cada cliente individual, combinando dados de vários canais, inclusive dados online, offline, de CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Expiração de dados de perfil pseudônimo | A expiração de dados de perfis pseudônimos agora está geralmente disponível! Essa versão removerá continuamente perfis pseudônimos obsoletos da instância do Experience Platform, uma vez ativados. Para saber mais sobre este recurso e Perfis de pseudônimo, leia o [Guia de expiração de dados do perfil de pseudônimo](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## Serviço de segmentação {#segmentation}

[!DNL Segmentation Service] O define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo comercializável de pessoas na sua base de clientes. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Mapa de associação de segmento | Como consequência do anúncio anterior em fevereiro, em 15 de maio de 2023, a `Existing` o status será descontinuado do mapa de associação de segmento para remover a redundância no ciclo de vida da associação de segmento. Após essa alteração, os perfis qualificados em um segmento serão representados como `Realized` e os perfis desqualificados continuarão a ser representados como `Exited`.<br/><br/> Essa alteração pode impactar você se estiver usando [destinos corporativos](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Hubs de Eventos do Azure, API HTTP) e podem ter processos de downstream automatizados em vigor com base no `Existing` status. Se esse for o seu caso, revise suas integrações downstream. Se você estiver interessado em identificar perfis recém-qualificados além de um determinado período, considere usar uma combinação das opções `Realized` status e o `lastQualificationTime` no mapa de associação do segmento. Para obter mais informações, entre em contato com o representante da Adobe. |

{style="table-layout:auto"}

Para obter mais informações sobre [!DNL Segmentation Service], consulte o [Visão geral da segmentação](../../segmentation/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da Platform. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte à API para filtrar dados em nível de linha para a origem do Salesforce CRM. | Use operadores lógicos e de comparação para filtrar dados de nível de linha para a origem do Salesforce CRM. Leia o guia em [filtragem de dados de uma origem usando a API](../../sources/tutorials/api/filter.md) para obter mais informações. |
| Disponibilidade beta da transmissão do Shopify | A variável [Shopify Fonte de transmissão](../../sources/connectors/ecommerce/shopify-streaming.md) O agora está disponível na versão beta. Use a fonte de transmissão do Shopify para transmitir os dados da sua conta de parceiros do Shopify para o Experience Platform. |
| Disponibilidade geral da Integração do OneTrust | A variável [Fonte de integração do OneTrust](../../sources/connectors/consent-and-preferences/onetrust.md) agora é GA. Use a fonte de Integração do OneTrust para trazer dados de consentimento e preferências da sua conta de Integração do OneTrust para o Experience Platform. |
| Disponibilidade geral da Oracle Service Cloud | A variável [Origem da nuvem do serviço do Oracle](../../sources/connectors/customer-success/oracle-service-cloud.md) agora é GA. Use a fonte da nuvem do serviço do Oracle para trazer seus dados da nuvem do serviço do Oracle para o Experience Platform. |

{style="table-layout:auto"}

Para saber mais sobre origens, leia a [visão geral de origens](../../sources/home.md).