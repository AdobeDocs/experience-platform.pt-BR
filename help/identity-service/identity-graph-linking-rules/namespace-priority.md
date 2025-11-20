---
title: Prioridade de namespace
description: Saiba mais sobre a prioridade de namespace no Serviço de identidade.
exl-id: bb04f02e-3826-45af-b935-752ea7e6ed7c
source-git-commit: 7df0d0c7eb97760190ac8b20d1b74472b87e8b6a
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 2%

---

# Prioridade de namespace {#namespace-priority}

>[!CONTEXTUALHELP]
>id="platform_identities_namespacepriority"
>title="Prioridade de namespace"
>abstract="A prioridade do namespace determina como os links são removidos do gráfico de identidade."

Cada implementação de cliente é exclusiva e personalizada para atender às metas de uma organização específica e, como tal, a importância de um determinado namespace varia de acordo com o cliente. Exemplos reais incluem:

* Sua empresa pode considerar cada endereço de email para representar uma entidade de uma única pessoa e, portanto, usar [configurações de identidade](./identity-settings-ui.md) para configurar o namespace de email como exclusivo. No entanto, outra empresa pode querer representar entidades de uma única pessoa com vários endereços de email e, portanto, configurar o namespace de email como não exclusivo. Essas empresas precisariam usar outro namespace de identidade como exclusivo, como um namespace CRMID, para que possa haver um identificador de uma única pessoa vinculado aos vários endereços de email.
* Você pode coletar o comportamento online usando um namespace de &quot;ID de logon&quot;. Esta ID de Logon pode ter uma relação 1:1 com o CRMID, que armazena atributos de um sistema CRM e pode ser considerada o namespace mais importante. Nesse caso, você está determinando que o namespace CRMID é uma representação mais precisa de uma pessoa, enquanto o namespace da ID de logon é o segundo mais importante.

Você deve fazer configurações no Serviço de identidade que reflitam a importância dos namespaces, pois isso influencia como os perfis e seus gráficos de identidade relacionados são formados e divididos.

## Determine suas prioridades

A determinação da prioridade do namespace é baseada nos seguintes fatores:

### Estrutura do gráfico de identidade

Se a estrutura de gráfico de sua organização estiver em camadas, a prioridade do namespace deverá refletir isso para que os links corretos sejam removidos no caso de recolhimento de gráficos.

>[!TIP]
>
>* &quot;Coleta de gráfico&quot; refere-se a cenários em que vários perfis diferentes são mesclados inadvertidamente em um único gráfico de identidade.
>
>* Um gráfico em camadas se refere aos gráficos de identidade que têm vários níveis de links. Veja a imagem abaixo para obter um exemplo de um gráfico com três camadas.

![Um diagrama de camadas de gráfico](../images/namespace-priority/graph-layers.png "Um diagrama de camadas de gráfico"){zoomable="yes"}

### Significado semântico do namespace

Uma identidade representa um objeto real. Há três objetos que são representados no gráfico de identidade. Em ordem de importância, eles são:

* Pessoas (entre dispositivos, email, número de telefone)
* Dispositivo de hardware
* Navegador da Web (Cookie)

Os namespaces de pessoa são relativamente imutáveis em comparação a dispositivos de hardware (como IDFA, GAID), que são relativamente imutáveis em comparação a navegadores da Web. Basicamente, você (pessoa) sempre será uma única entidade, que pode ter vários dispositivos de hardware (telefone, laptop, tablet etc.) e usar vários navegadores (Google Chrome, Safari, FireFox etc.)

Outra maneira de abordar este tópico é através da cardinalidade. Para uma determinada entidade de pessoa, quantas identidades serão criadas? Na maioria dos casos, uma pessoa terá uma CRMID, alguns identificadores de dispositivo de hardware (redefinições de IDFA/GAID não devem ocorrer com frequência) e ainda mais cookies (um indivíduo pode navegar em vários dispositivos, usar o modo incógnito ou redefinir cookies a qualquer momento). Geralmente, **a cardinalidade mais baixa indica um namespace com uma prioridade mais alta**.

## Validar as configurações de prioridade do namespace

Depois de ter uma ideia de como priorizar seus namespaces, você pode usar a ferramenta Simulação de gráfico na interface do para testar vários cenários de recolhimento de gráficos e garantir que suas configurações de prioridade retornem os resultados esperados do gráfico. Para obter mais informações, leia o manual sobre como usar a [Ferramenta de simulação de gráfico](./graph-simulation.md).

## Configurar prioridade de namespace

A prioridade de namespace pode ser definida usando a [interface do usuário de configurações de identidade](./identity-settings-ui.md). Na interface das configurações de identidade, você pode arrastar e soltar um namespace para determinar sua importância relativa.

>[!IMPORTANT]
>
>Você não pode priorizar namespaces de dispositivo/cookie em relação a namespaces de pessoa. Essa restrição garante que não ocorram erros de configuração.

## Uso da prioridade de namespace

Atualmente, a prioridade do namespace influencia o comportamento do sistema do Perfil do cliente em tempo real. O diagrama abaixo ilustra esse conceito. Para obter mais informações, leia o guia em [diagramas de arquitetura de Adobe Experience Platform e aplicativos](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications).

![Um diagrama do escopo de aplicativo de prioridade de namespace.](../images/namespace-priority/application-scope.png "Um diagrama do escopo de aplicativo de prioridade de namespace."){zoomable="yes"}

## Serviço de identidade: algoritmo de otimização de identidade

Para estruturas de gráficos relativamente complexas, a prioridade de namespace desempenha um papel importante para garantir que os links corretos sejam removidos quando ocorrem cenários de recolhimento de gráficos. Para obter mais informações, leia a [visão geral do Algoritmo de otimização de identidade](../identity-graph-linking-rules/identity-optimization-algorithm.md).

## Perfil do cliente em tempo real: determinação de identidade principal para eventos de experiência

* Depois de definir as configurações de identidade para uma determinada sandbox, a identidade principal para eventos de experiência será determinada pela prioridade de namespace mais alta na configuração.
   * Isso ocorre porque os eventos de experiência são de natureza dinâmica. Um mapa de identidade pode conter três ou mais identidades, e a prioridade do namespace garante que o namespace mais importante esteja associado ao evento de experiência.
* Como resultado, as seguintes configurações **não serão mais usadas pelo Perfil de Cliente em Tempo Real**:
   * A configuração de identidade primária (`primary=true`) ao enviar identidades no `identityMap` usando o Web SDK, o Mobile SDK ou a API do Edge Network (o namespace de identidade e o valor de identidade continuarão a ser usados no Perfil). **Observação**: os serviços fora do Perfil do Cliente em Tempo Real, como o armazenamento em data lake ou a Adobe Target, continuarão a usar a configuração de identidade principal (`primary=true`).
   * Quaisquer campos marcados como identidade primária em um esquema de Classe de evento de experiência XDM.
   * Configurações de identidade primária padrão no conector de origem do Adobe Analytics (ECID ou AAID).
* Por outro lado, a **prioridade de namespace não determina a identidade principal dos registros de perfil**.
   * Para registros de perfil, você deve continuar a definir seus campos de identidade no esquema, incluindo a identidade principal. Leia o manual sobre [definição de campos de identidade na interface](../../xdm/ui/fields/identity.md) para obter mais informações.

>[!TIP]
>
>* A prioridade de namespace é **uma propriedade de um namespace**. É um valor numérico atribuído a um namespace para indicar sua importância relativa.
>
>* A identidade principal é a identidade na qual um fragmento de perfil é armazenado. Um fragmento de perfil é um registro de dados que armazena informações sobre um determinado usuário: atributos (por exemplo, registros CRM) ou eventos (por exemplo, navegação em sites).

### Exemplo de cenário

Esta seção fornece um exemplo de como a configuração de prioridade pode afetar seus dados.

Suponha que as seguintes configurações sejam estabelecidas para uma determinada sandbox:

| Namespace | Aplicação real do namespace | Prioridade |
| --- | --- | --- |
| CRMID | Usuário(a)  | 1 |
| IDFA | Dispositivo de hardware do Apple (iPhone, IPad etc.) | 2 |
| GAID | Dispositivo de hardware do Google (Google Pixel, Pixelbook, etc.) | 3 |
| ECID | Navegador da Web (Firefox, Safari, Google Chrome etc.) | 4 |
| AAID | Navegador da Web | 5 |

{style="table-layout:auto"}

Dadas as configurações descritas acima, as ações do usuário e a determinação da identidade principal serão resolvidas como:

| Ação do usuário (Evento de experiência) | Estado de autenticação | Fonte de dados | Namespaces no evento | Namespace da identidade primária |
| --- | --- | --- | --- | --- |
| Exibir página de oferta de cartão de crédito | Não autenticado (anônimo) | Web SDK | `{ECID}` | ECID |
| Exibir página de ajuda | Não autenticado | SDK móvel | `{ECID, IDFA}` | IDFA |
| Exibir saldo de conta corrente | Autenticado | Web SDK | `{CRMID, ECID}` | CRMID |
| Inscrever-se para obter empréstimo residencial | Autenticado | Conector de origem do Analytics | `{CRMID, ECID, AAID}` | CRMID |
| Transferência de US$ 1.000 da verificação para a economia | Autenticado | SDK móvel | `{CRMID, GAID, ECID}` | CRMID |

{style="table-layout:auto"}

## Serviço de segmentação: armazenamento de metadados de associação de segmento

![Um diagrama de armazenamento de associação de segmento.](../images/namespace-priority/segment-membership-storage.png "Um diagrama de armazenamento de associação de segmento."){zoomable="yes"}

Para um determinado perfil mesclado, as associações de segmento serão armazenadas em relação à identidade com a maior prioridade de namespace.

Por exemplo, suponha que haja dois perfis:

* O perfil 1 representa John.
   * O perfil de John é qualificado para S1 (segmento de afiliação 1). Por exemplo, S1 pode se referir a um segmento de clientes que se identifica como masculino.
   * O perfil de John também se qualifica para S2 (segmento de afiliação 2). Isso pode se referir a um segmento de clientes cujo status de fidelidade é ouro.
* O perfil 2 representa Jane.
   * O perfil de Jane se qualifica para S3 (segmento de afiliação 3). Pode se referir a um segmento de clientes que se identifica como do sexo feminino.
   * O perfil de Jane também se qualifica para S4 (segmento de afiliação 4). Isso pode se referir a um segmento de clientes cujo status de fidelidade é platina.

Se John e Jane compartilharem um dispositivo, a ECID (navegador da Web) será transferida de uma pessoa para outra. No entanto, isso não influencia as informações de associação do segmento armazenadas em relação a John e Jane.

Se os critérios de qualificação de segmento fossem baseados apenas em eventos anônimos armazenados na ECID, Jane se qualificaria para esse segmento.

## Implicações em outros serviços da Experience Platform {#implications}

Esta seção descreve como a prioridade de namespace pode afetar outros serviços da Experience Platform.

### Gerenciamento avançado do ciclo de vida de dados

A exclusão de registros da higiene de dados solicita funções da seguinte maneira, para uma determinada identidade:

* Perfil do cliente em tempo real: exclui qualquer fragmento de perfil com a identidade especificada como identidade principal. **A identidade principal no Perfil agora será determinada com base na prioridade do namespace.**
* Data lake: exclui qualquer registro com a identidade especificada como identidade principal. Ao contrário do Perfil do cliente em tempo real, a identidade principal no data lake é baseada na identidade principal especificada no WebSDK (`primary=true`) ou em um campo marcado como identidade principal

Para obter mais informações, leia a [visão geral avançada do gerenciamento do ciclo de vida](../../hygiene/home.md).

### Atributos computados

Se as configurações de identidade estiverem habilitadas, os atributos computados usarão a prioridade de namespace para armazenar o valor do atributo computado. Para um determinado evento, a identidade com a maior prioridade de namespace terá o valor do atributo calculado gravado nele. Para obter mais informações, leia o [guia da interface do usuário de atributos computados](../../profile/computed-attributes/ui.md).

### Data lake

A assimilação de dados no data lake continuará respeitando as configurações de identidade primárias definidas no [Web SDK](../../tags/extensions/client/web-sdk/data-element-types.md#identity-map) e nos esquemas.

O data lake não determinará a identidade principal com base na prioridade do namespace. Por exemplo, o Adobe Customer Journey Analytics continuará a usar valores no mapa de identidade mesmo após a prioridade do namespace ser ativada (como adicionar um conjunto de dados a uma nova conexão), porque o Customer Journey Analytics consome seus dados do data lake.

### Esquemas do Experience Data Model (XDM)

Qualquer esquema que não seja um Evento de experiência XDM, como Perfis individuais XDM, continuará respeitando qualquer [campo que você marcar como uma identidade](../../xdm/ui/fields/identity.md).

Para obter mais informações sobre esquemas XDM, leia a [visão geral dos esquemas](../../xdm/home.md).

### Serviços inteligentes

Ao selecionar seus dados, você precisará especificar um namespace, que será usado para determinar os eventos que calculam pontuações e os eventos que armazenam as pontuações calculadas. É recomendável selecionar o namespace que representa uma pessoa.

* Se você estiver coletando dados de comportamento da Web usando o WebSDk, é recomendável escolher o namespace CRMID no mapa de identidade.
* Se você estiver coletando dados de comportamento da Web usando o conector de origem do Analytics, selecione o descritor de identidade (CRMID).

Esta configuração resulta no cálculo de pontuações somente usando eventos autenticados.

Para obter mais informações, leia os documentos sobre a [IA de atribuição](../../intelligent-services/attribution-ai/overview.md) e a [IA do cliente](../../intelligent-services/customer-ai/overview.md).

### Destinos criados por parceiros

Os resultados atualizados de desqualificação de público-alvo para perfis associados a um dispositivo compartilhado não podem ser enviados para destinos downstream. Isso pode acontecer em determinadas ocorrências raras em que:

* A qualificação de público-alvo é baseada apenas em atividades anônimas.
* Os logons em vários perfis ocorrem em um curto período de tempo.

Para obter mais informações sobre destinos criados por parceiros, leia a [visão geral sobre destinos](../../destinations/home.md#adobe-built-and-partner-built-destinations).

### Privacy Service

[As solicitações de exclusão do Privacy Service](../privacy.md) funcionam da seguinte maneira para uma determinada identidade:

* Perfil do cliente em tempo real: exclui qualquer fragmento de perfil com valor de identidade especificado como identidade principal. **A identidade principal no Perfil agora será determinada com base na prioridade do namespace.**
* Data lake: exclui qualquer registro com a identidade especificada como identidade primária ou secundária.

Para obter mais informações, leia a [Visão geral do Privacy Service](../../privacy-service/home.md).

### Aplicativos de segmentação do Edge e Edge Network

No contexto de [!DNL Identity Graph Linking Rules], há duas alterações comportamentais principais que devem ser observadas em relação à segmentação do Edge e aos aplicativos do Edge Network:

1. `identityMap` deve conter um namespace de pessoa que foi marcado como exclusivo. Os campos marcados como uma identidade (descritores de identidade) não são compatíveis.
2. O namespace de pessoa deve ter a configuração `primary = true` quando um usuário final estiver navegando enquanto estiver autenticado.

#### Segmentação de borda

Em um determinado evento, verifique se todos os namespaces que representam uma entidade de pessoa estão incluídos em `identityMap` porque [identidades enviadas como campos XDM](../../xdm/ui/fields/identity.md) são ignoradas e não são usadas para o armazenamento de metadados de associação de segmento.

* **Aplicabilidade de evento**: esse comportamento se aplica somente a eventos enviados diretamente para a Edge Network (como WebSDK e Mobile SDK). Os eventos assimilados do [hub do Experience Platform](../../landing/edge-and-hub-comparison.md), como aqueles assimilados com a fonte da API HTTP, outras fontes de transmissão e fontes em lote, não estão sujeitos a essa limitação.
* **Especificidade da segmentação do Edge**: esse comportamento é específico da segmentação de borda. A segmentação em lote e por transmissão são serviços separados avaliados no hub e não seguem o mesmo processo. Leia o [guia de segmentação de borda](../../segmentation/methods/edge-segmentation.md) para obter mais informações.
* Leia as [páginas de diagramas de arquitetura de Adobe Experience Platform e aplicativos](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications#detailed-architecture-diagram) e [comparação de Edge Network e hub](../../landing/edge-and-hub-comparison.md) para obter mais informações.

#### aplicativos Edge Network

Para garantir que os aplicativos na Edge Network tenham acesso ao Perfil do Edge sem demora, verifique se os eventos incluem `primary=true` no CRMID. Isso garante disponibilidade imediata sem esperar por atualizações do gráfico de identidade do hub.

* Aplicativos no Edge Network, como Adobe Target, Offer Decisioning e Destinos personalizados do Personalization continuarão a depender da identidade principal nos eventos para acessar perfis do Perfil do Edge.
* Leia o [diagrama de arquitetura do Experience Platform Web SDK &amp; Edge Network](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/deployment/websdk#experience-platform-webmobile-sdk-or-edge-network-server-api-deployment) para obter mais informações sobre o comportamento do Edge Network.
* Leia a documentação sobre [Tipos de elementos de dados](../../tags/extensions/client/web-sdk/data-element-types.md) e [Dados de identidade no Web SDK](../../web-sdk/identity/overview.md) para obter mais informações sobre como configurar a identidade principal no Web SDK.
* Verifique se a ECID está incluída no evento de experiência. Se a ECID estiver ausente, ela será adicionada à carga do evento com `primary=true`, o que pode levar a resultados inesperados.