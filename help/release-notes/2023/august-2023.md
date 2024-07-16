---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão de agosto de 2023 do Adobe Experience Platform.
exl-id: c67dca3a-eccb-427e-8ab3-b69c51b57938
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 35%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 23 de agosto de 2023**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [Real-Time Customer Data Platform](#rtcdp)
- [Controle de acesso baseado em atributos](#abac)
- [Painéis](#dashboards)
- [Coleção de dados](#data-collection)
- [Assimilação de dados](#data-ingestion)
- [Preparação de dados](#data-prep)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de identidade](#identity-service)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## Real-Time Customer Data Platform {#rtcdp}

Criada na Experience Platform, a Real-time Customer Data Platform ([!DNL Real-Time CDP]) ajuda empresas a reunir dados conhecidos e desconhecidos para ativar perfis de clientes com decisões inteligentes em toda a jornada do cliente.

A [!DNL Real-Time CDP] combina várias fontes de dados corporativos para criar perfis de clientes em tempo real. Os segmentos criados a partir desses perfis podem ser enviados para destinos downstream com o fim de oferecer experiências de cliente personalizadas em todos os canais e dispositivos.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Guia de caso de uso de reengajamento inteligente | O guia de caso de uso de [Reengajamento inteligente](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) fornece detalhes sobre como reengajar clientes que abandonaram uma conversão antes de concluí-la de forma inteligente e responsável. Este guia usa o seguinte exemplo de jornada para reengajar os clientes: <ul><li>Jornada de reengajamento - Direcionamento de clientes que abandonaram a navegação no produto.</li><li>Jornada de carrinho abandonada - Direcionamento de clientes que colocaram produtos no carrinho, mas ainda não concluíram a compra.</li><li>Jornada de confirmação de pedido - Foco nas compras de produtos</li></ul> Use o link de opções de feedback detalhado na parte inferior do [guia do caso de uso de Reengajamento inteligente](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) para fornecer feedback. |
| Suporte a dados de parceiros | Execute marketing de funil superior no Real-Time CDP, com perfis de prospecto e IDs de parceiros fornecidos pelos parceiros para alcançar novos clientes e enriquecer seus dados primários: <ul><li>Aquisição de clientes e capacidade de endereçamento: use identificadores sem cookies e PII com hash de parceiros de dados de sua escolha para alcançar novos clientes na rede e reduzir a dependência de cookies de terceiros.</li><li>Marketing de funil completo em um único sistema: segmentação de autoatendimento, curadoria de público-alvo e ativação nativa para clientes potenciais e conhecidos em um único sistema.</li><li>Base de confiança: controle dados e perfis de parceiros com uso de dados patenteado, rotulagem, controles de acesso e muito mais para comercializar de forma responsável. Leia os seguintes guias de casos de uso para obter mais informações: Os guias de casos de uso de prospecção estão agora disponíveis. Leia os guias de caso de uso de prospecção para saber como contratar e adquirir novos clientes por meio de casos de uso de prospecção:<ul><li>[Prospecção](../../rtcdp/partner-data/prospecting.md)</li><li>[Personalização no site](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[Suplemente perfis próprios](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[Ativar públicos-alvo potenciais](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral do Real-Time CDP](../../rtcdp/overview.md).

## Controle de acesso baseado em atributos {#abac}

O controle de acesso baseado em atributos é um recurso do Adobe Experience Platform que oferece às marcas preocupadas com a privacidade maior flexibilidade para gerenciar o acesso do usuário. Objetos individuais, como campos de esquema e segmentos, podem ser atribuídos a funções de usuário. Esse recurso permite conceder ou revogar o acesso a objetos individuais para usuários específicos da Platform em sua organização.

Por meio do controle de acesso baseado em atributos, os administradores da sua organização podem controlar o acesso dos usuários a dados pessoais confidenciais (SPD), informações de identificação pessoal (PII) e outros tipos personalizados de dados em todos os fluxos de trabalho e recursos da plataforma. Os administradores podem definir funções de usuário que tenham acesso somente a campos e dados específicos que correspondam a esses campos.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Configuração da sandbox da política de permissões | O novo recurso [configuração de sandbox de políticas de permissão](../../access-control/abac/ui/policies.md) permite impor uma política de controle de acesso baseada em atributo em todas as sandboxes ou em um número selecionado de sandboxes, dependendo das suas necessidades e requisitos. |

{style="table-layout:auto"}

Para obter mais informações sobre o controle de acesso baseado em atributos, consulte a [visão geral do controle de acesso baseado em atributos](../../access-control/abac/overview.md). Para obter um guia abrangente sobre o fluxo de trabalho do controle de acesso baseado em atributos, leia o [guia completo do controle de acesso baseado em atributos](../../access-control/abac/end-to-end-guide.md).

## Painéis {#dashboards}

A Adobe Experience Platform fornece vários painéis para você visualizar insights importantes sobre os dados de sua organização, que são capturados por instantâneos diários.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Caso de uso de análise de consentimento e rastreamento | Saiba como criar um painel de consentimento para vários casos de uso de marketing para dados do Real-Time CDP com o [documento de análise de consentimento e rastreamento](../../dashboards/insights-use-cases/consent-analysis.md). Ele detalha como criar um público-alvo com os atributos apropriados para suas necessidades comerciais e, em seguida, consumir os insights por meio do uso de widgets pré-configurados na interface do usuário do Adobe Experience Platform. Ele também fornece instruções sobre como criar seu próprio widget personalizado com o recurso de painéis definido pelo usuário. O documento abrange a tendência de consentimento e os casos de uso de sobreposição de consentimento. |

{style="table-layout:auto"}

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo a [visão geral dos painéis](../../dashboards/home.md).

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Recursos novos ou atualizados**

| Tipo | Recurso | Descrição |
| --- | --- | --- |
| Tags e encaminhamento de eventos | [Marcas de Experience Platform (China)](/help/tags/ui/publishing/premium-cdn.md) | O novo recurso Tags de Experience Platform (China) melhora a confiabilidade e a latência do site, resultando em tempos de resposta mais rápidos para clientes que implantam Tags em sites na China. Agora, os clientes podem utilizar o código JavaScript na biblioteca de tags ao implementar sites na China. Esse recurso também foi adicionado ao Unified Provisioning Protocol (UPP), permitindo que a implantação do produto seja automatizada após a compra. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral das coleções de dados](../../tags/home.md).

## Assimilação de dados {#data-ingestion}

A Adobe Experience Platform fornece um conjunto avançado de recursos para assimilar qualquer tipo e qualquer latência de dados. Você pode assimilar usando APIs de lote ou transmissão, origens construídas pela Adobe, parceiros de integração de dados ou a interface da Adobe Experience Platform.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Alterações nos fluxos de trabalho de assimilação de dados | Linhas de dados contendo valores maiores que o tipo de dados especificado (por exemplo, dados longos transmitidos como um tipo de dados inteiro) agora serão rejeitadas e mensagens de erro serão relatadas. Anteriormente, essas linhas eram rejeitadas sem aviso. |

Para obter mais informações, leia a [visão geral da assimilação de dados](../../ingestion/home.md).

## Preparação de dados {#data-prep}

A preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para filtrar identidades secundárias | Agora você pode usar o Preparo de dados para filtrar identidades provenientes do Adobe Analytics, como AAID e AACUSTOMID. Se filtradas, essas identidades não são assimiladas no Perfil do cliente em tempo real. Os dados não filtrados continuarão a ser assimilados no data lake. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral do Preparo de Dados](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

- Agora você pode [ativar públicos-alvo potenciais](../../destinations/ui/activate-prospect-audiences.md) para destinos de armazenamento na nuvem.
- A [proteção de ativação](../../destinations/guardrails.md#general-activation-guardrails) geral de no máximo 100 destinos por sandbox foi atualizada para ser um _limite rígido_.

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados inseridos na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Novos componentes de XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Classe | [[!UICONTROL Perfil de cliente potencial individual do XDM]](https://github.com/adobe/xdm/pull/1758/files) | Use esta classe para trazer perfis de prospecto obtidos de casos de uso de aquisição de clientes topo de funil de fornecedores de dados. Consulte a documentação do [[!UICONTROL Perfil de cliente potencial individual XDM]](../../xdm/classes/prospect.md) para ver exemplos e saber mais. |

{style="table-layout:auto"}

**Componentes de XDM atualizados**

| Tipo de componente | Nome | Atualizar descrição |
| --- | --- | --- |
| Extensão ([!UICONTROL Extensão completa do Adobe Analytics ExperienceEvent]) | [[!UICONTROL Dados de contexto]](https://github.com/adobe/xdm/pull/1761/files) | [!UICONTROL Objeto de mapa de Dados de Contexto] adicionado à [!UICONTROL Extensão Completa de ExperienceEvent do Adobe Analytics] para fornecer dados de contexto para o Adobe Analytics. |
| Grupo de campos | Múltiplo | Vários campos adicionados a [[!UICONTROL Detalhes de Segmento de Evento Enriquecido]](https://github.com/adobe/xdm/pull/1760/files). |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral do sistema XDM](../../xdm/home.md).

## Serviço de identidade {#identity-service}

O Serviço de identidade da Adobe Experience Platform fornece uma visão abrangente dos clientes e seu comportamento ao unir identidades entre dispositivos e sistemas, permitindo fornecer experiências digitais pessoais de impacto em tempo real.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Alterações nos limites do gráfico de identidade | Até o final de setembro, o gráfico de identidade será alterado para 50 identidades por gráfico, e a identidade mais recente será assimilada. Como consequência, a identidade mais antiga será excluída com base no carimbo de data e hora de assimilação e no tipo de identidade, com os tipos de identidade de cookie sendo excluídos primeiro. Hoje, os gráficos de identidade têm um limite de 150 identidades por gráfico e, uma vez atingido esse limite, os gráficos não são mais atualizados. Entre em contato com o representante de conta para solicitar uma alteração no tipo de identidade se a sandbox de produção contiver: <ul><li>um namespace personalizado em que os identificadores de pessoa (como IDs de CRM) são configurados como tipo de identidade de cookie/dispositivo.</li><li>um namespace personalizado em que os identificadores de cookie/dispositivo são configurados como tipo de identidade entre dispositivos.</li></ul> A engenharia de Adobe processará manualmente essas solicitações. Para obter mais informações, leia as [medidas de proteção para os dados do Serviço de Identidade](../../identity-service/guardrails.md). |

Para obter mais informações, leia a [visão geral do Serviço de Identidade](../../identity-service/home.md).

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] permite segmentar dados relacionados a indivíduos (como clientes, prospectos, usuários ou organizações) que estão armazenados na [!DNL Experience Platform] em públicos-alvo. Você pode criar públicos-alvo por meio de definições de segmento ou outras fontes a partir dos dados do [!DNL Real-Time Customer Profile]. Esses públicos-alvo são configurados e mantidos de forma centralizada na [!DNL Platform] e podem ser acessados a qualquer momento usando as soluções da Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Públicos-alvo semelhantes (disponibilidade limitada) | Públicos semelhantes fornecem insights inteligentes sobre cada um de seus públicos, aproveitando insights baseados em aprendizado de máquina para identificar e direcionar clientes de alto valor com suas campanhas de marketing. Com Públicos-alvo semelhantes, você pode criar públicos-alvo expandidos que direcionem clientes semelhantes aos seus públicos-alvo de alto desempenho ou clientes-alvo semelhantes aos públicos-alvo convertidos anteriormente. Para obter mais informações sobre públicos-alvo semelhantes, leia a [Visão geral sobre públicos-alvo semelhantes](../../segmentation/ui/lookalike-audiences.md). |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral da segmentação](../../segmentation/home.md).

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade geral de [!DNL SugarCRM] | [!DNL SugarCRM] fontes estão disponíveis agora. Use as origens [!DNL SugarCRM Accounts & Contacts] e [!DNL SugarCRM Events] para trazer dados da sua conta [!DNL SugarCRM] para a Experience Platform. Para obter mais informações, leia a [[!DNL SugarCRM] visão geral](../../sources/connectors/crm/sugarcrm.md). |
| Suporte para assimilação sob demanda para fluxos de dados de origens na interface do | Agora é possível criar execuções de fluxo sob demanda para um fluxo de dados de fontes existente na interface do usuário. Para obter mais informações, leia o manual sobre [criação de uma execução de fluxo sob demanda para fontes usando a interface](../../sources/tutorials/ui/on-demand-ingestion.md). |
| Suporte para o novo campo `correlationID` do Adobe Analytics | O campo `_experience.decisioning.propositions.scopeDetails.correlationID` agora está disponível no esquema do conector de origem do Adobe Analytics. Esse campo é usado em suporte às classificações do A4T e será preenchido a partir de setembro de 2023. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral das fontes](../../sources/home.md).
