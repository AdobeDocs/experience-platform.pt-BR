---
keywords: Experience Platform, home, tópicos populares, gerenciamento de dados, direito de licença, licenciamento, práticas recomendadas
title: Práticas recomendadas de direito à licença de gerenciamento de dados
description: Saiba mais sobre as práticas recomendadas e as ferramentas que você pode usar para gerenciar melhor seus direitos de licença na Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: fd594e19e13ca6e7f9f92674107d8ac6dabac9d6
workflow-type: tm+mt
source-wordcount: '2169'
ht-degree: 2%

---

# Práticas recomendadas de direito à licença de gestão de dados

O Adobe Experience Platform é um sistema aberto que transforma seus dados em perfis robustos do cliente, que são atualizados em tempo real e usa insights orientados por IA para ajudar você a fornecer as experiências certas em cada canal. Você pode inserir dados de tipos, volumes e históricos variados no Experience Platform usando fontes e, em seguida, atender esses dados para usar casos que vão da segmentação e personalização ao analytics e ao aprendizado de máquina.

A Platform oferece licenças que estabelecem o número de perfis que você pode criar e a quantidade de dados que você pode trazer. Dada a capacidade de trazer qualquer fonte, volume ou histórico de dados, é possível exceder seus direitos de licenciamento à medida que seus volumes de dados crescem.

Este documento descreve as práticas recomendadas e as ferramentas que você pode usar para gerenciar melhor seus direitos de licença na Adobe Experience Platform.

## Como entender o armazenamento de dados do Adobe Experience Platform

O Experience Platform é composto principalmente por dois repositórios de dados: o [!DNL data lake] e na Loja de perfis.

O **[!DNL data lake]** Serve principalmente os seguintes objetivos:

* Atua como área de armazenamento temporário para a integração de dados no Experience Platform;
* Atua como armazenamento de dados a longo prazo para todos os dados de Experience Platform;
* Habilita casos de uso como análise de dados e ciência de dados.

O **Loja de perfis** é onde os perfis do cliente são criados e servem principalmente os seguintes objetivos:

* Atua como um armazenamento de dados para perfis usados para oferecer suporte a experiências em tempo real;
* Permite casos de uso como segmentação, ativação e personalização.

>[!NOTE]
>
>Seu acesso ao [!DNL data lake] pode depender do SKU do produto que você comprou. Para obter mais informações sobre SKUs de produtos, fale com o representante do Adobe.

## Uso da licença {#license-usage}

Ao licenciar o Experience Platform, você recebe direitos de uso de licença que variam de acordo com o SKU:

**[!DNL Addressable Audience]** - o número total de perfis de clientes contratualmente permitidos no Experience Platform, incluindo perfis conhecidos e pseudônimos.

**[!DNL Profile Richness]** - o tamanho médio dos dados do seu perfil no Experience Platform. Você pode aumentar sua [!DNL Profile Richness] ao comprar um pacote de riqueza.

O [!DNL Profile Richness] varia dependendo do licenciamento adquirido. Há dois cálculos para [!DNL Profile Richness] disponível:

* A soma de todos os dados de produção armazenados no Adobe Real-time Customer Data Platform (ou seja, Perfil do cliente em tempo real e Serviço de identidade) em qualquer momento, dividida pela variável [!DNL Addressable Audience];
* A soma de todos os dados armazenados no Platform (incluindo, mas não se limitando a, [!DNL data lake], Perfil do cliente em tempo real e Serviço de identidade) em qualquer momento e quaisquer dados transmitidos (em vez de armazenar na) na plataforma nos últimos 12 meses, divididos pela variável [!DNL Addressable Audience].

A disponibilidade dessas métricas e a definição específica de cada uma delas variam de acordo com o licenciamento adquirido pela sua organização.

## Painel de uso da licença

A interface do usuário do Adobe Experience Platform fornece um painel pelo qual você pode visualizar um instantâneo dos dados relacionados à licença da sua organização para a Platform. Os dados no painel são exibidos exatamente como aparecem no momento específico em que o instantâneo foi tirado. O instantâneo não é uma aproximação nem uma amostra de dados, e o painel não está sendo atualizado em tempo real.

Para obter mais informações, consulte o guia sobre [uso do painel de uso da licença na interface do usuário da plataforma](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## Práticas recomendadas de gestão de dados

As seções a seguir descrevem as práticas recomendadas a serem seguidas para gerenciar melhor seus dados.

### Como entender seus dados

Nem todos os dados são iguais no Adobe Experience Platform. Alguns dados podem ser densos, mas de baixo valor, enquanto outros podem ser esparsos, mas de alto valor. Alguns dados podem perder valor assim que gerados, enquanto outros podem ser valiosos por meses, se não anos.

Há três dimensões a serem consideradas na compreensão do valor de seus dados:

| Dimensão | Descrição | Exemplo |
| --- | --- | --- |
| Volume | Representa a quantidade e a totalidade dos dados assimilados. | Cliques na Web - alto volume e moderado em fidelidade. O valor pode diminuir rapidamente. |
| Tempo | Representa o tempo em que os dados assimilados continuam a ser valiosos. | Compras offline - moderem o volume e a fidelidade, mas podem ser valiosas por longos períodos. |
| Fidelidade | Representa a riqueza de dados com as informações. | Contas do cliente - baixo volume, mas alta fidelidade. Pode ser valioso além da vida útil de um cliente. |

### Ferramentas de gerenciamento de dados {#data-management-tools}

Há dois cenários centrais a serem considerados ao garantir que o uso de dados permaneça dentro dos limites do direito de licença:

### Quais dados trazer para o Platform?

Os dados podem ser assimilados em um ou vários sistemas na Platform, ou seja, o [!DNL data lake] e/ou na Loja de perfis. Isso significa que podem existir dados diferentes em ambos os sistemas para uma variedade de casos de uso diferentes. Por exemplo, talvez você queira manter os dados históricos no [!DNL data lake], mas não na Loja de perfis. Você pode selecionar quais dados enviar para o armazenamento de Perfil ativando um conjunto de dados para assimilação de Perfil.

>[!NOTE]
>
>Seu acesso ao [!DNL data lake] pode depender do SKU do produto que você comprou. Para obter mais informações sobre SKUs de produtos, fale com o representante do Adobe.

### Quais dados manter?

Você pode aplicar filtros de assimilação de dados e regras de expiração para remover dados que se tornaram obsoletos em seus casos de uso. Normalmente, os dados comportamentais (como os dados do Analytics) consomem significativamente mais armazenamento do que os dados de registro (como dados de CRM). Por exemplo, muitos usuários da plataforma têm até 90% dos perfis preenchidos apenas por dados comportamentais, em comparação aos dados de registro. Portanto, o gerenciamento de seus dados comportamentais é essencial para garantir a conformidade com os direitos de licença.

Há várias ferramentas que você pode aproveitar para se manter dentro dos direitos de uso de licença:

* [Filtros de assimilação](#ingestion-filters)
* [Loja de perfis](#profile-service)

### Filtros de assimilação {#ingestion-filters}

Os filtros de assimilação permitem trazer somente os dados necessários para seus casos de uso e filtram todos os eventos que não são necessários.

| Filtro de assimilação | Descrição |
| --- | --- |
| Filtragem de origem do Adobe Audience Manager | Ao criar uma conexão de origem Adobe Audience Manager, você pode escolher quais segmentos e características serão trazidas para a [!DNL data lake] e Perfil do cliente em tempo real, em vez de assimilar os dados do Audience Manager em sua totalidade. Consulte o guia sobre [criação de uma conexão Audience Manager source](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) para obter mais informações. |
| Preparação de dados do Adobe Analytics | Você pode usar [!DNL Data Prep] funcionalidades ao criar uma conexão de origem do Analytics para filtrar dados que não são necessários para seus casos de uso. Através de [!DNL Data Prep], você pode definir quais atributos/colunas precisam ser publicadas no Perfil. Você também pode fornecer declarações condicionais para informar à Platform se os dados devem ser publicados no Perfil ou apenas no [!DNL data lake]. Consulte o guia sobre [criação de uma conexão de origem do Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) para obter mais informações. |
| Suporte para ativar/desativar conjuntos de dados para Perfil | Para assimilar dados no Perfil do cliente em tempo real, é necessário ativar um conjunto de dados para uso no armazenamento de perfil. Ao fazer isso, o adiciona [!DNL Addressable Audience] e [!DNL Profile Richness] direitos. Quando um conjunto de dados não for mais necessário para casos de uso de perfil do cliente, você poderá desativar a integração desse conjunto de dados no Perfil para garantir que seus dados permaneçam compatíveis com a licença. Consulte o guia sobre [ativar e desativar conjuntos de dados para o Perfil](../../catalog/datasets/enable-for-profile.md) para obter mais informações. |
| Exclusão de dados do SDK da Web e do SDK móvel | Há dois tipos de dados coletados pelo SDK da Web e do Mobile: dados coletados automaticamente e dados que são coletados explicitamente pelo seu desenvolvedor. Para gerenciar melhor a conformidade da licença, você pode desativar a coleta automática de dados na configuração do SDK por meio da configuração de contexto. Os dados personalizados também podem ser removidos ou não ser definidos pelo seu desenvolvedor. Consulte o guia sobre [configuração dos fundamentos do SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) para obter mais informações. |
| Exclusão de dados do encaminhamento pelo lado do servidor | Se você estiver enviando dados para a Platform usando o encaminhamento pelo lado do servidor, poderá excluir quais dados serão enviados, removendo o mapeamento em uma ação de regra para excluí-lo em todos os eventos ou adicionando condições à regra para que os dados sejam disparados apenas para determinados eventos. Consulte a documentação em [eventos e condições](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if)) para obter mais informações. |

{style="table-layout:auto"}

### Loja de perfis {#profile-service}

A Loja de perfis é composta pelos seguintes componentes:

| Componente de loja de perfis | Descrição |
| --- | --- |
| Fragmentos de perfil | Cada perfil de cliente é composto de vários **fragmentos de perfil** que foram mescladas para formar uma única visualização desse cliente. Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização terá vários **fragmentos de perfil** relacionado a esse único cliente que aparece em vários conjuntos de dados. Quando esses fragmentos são assimilados no Platform, eles são agrupados usando o gráfico de identidade para criar um único perfil para esse cliente. **Fragmentos de perfil** consiste em um namespace de identidade como identificador, com dados de registro associados e/ou dados de séries de tempo. |
| Registrar dados (Atributos) | Um perfil é uma representação de um assunto, uma organização ou um indivíduo, composto por vários **Atributos** (também conhecido como **registrar dados**). Por exemplo, o perfil de um produto pode incluir um SKU e uma descrição, enquanto o perfil de uma pessoa contém informações como nome, sobrenome e endereço de email. **Registrar dados** geralmente é baixo/moderado em volume, mas valioso por longos períodos. |
| Dados da série de tempo (Comportamento) | **Dados da série cronológica** O fornece informações sobre o comportamento do usuário. Representado pela classe de esquema padrão Experience Data Model (XDM) [!DNL ExperienceEvent], os dados da série de tempo podem descrever eventos como itens adicionados a um carrinho, links clicados e vídeos visualizados. O valor do comportamento pode diminuir com o tempo. |
| Namespace de identidade (identidades) | À medida que os dados do cliente se unem, eles são unidos em um único perfil por meio do uso de **namespaces de identidade** e a capacidade de unir essas identidades à medida que mais informações são conhecidas sobre o usuário. Consulte a [visão geral dos namespaces de identidade](../../identity-service/namespaces.md) para obter mais informações. |

{style="table-layout:auto"}

#### Relatórios de composição do armazenamento de perfis

Há vários relatórios disponíveis para ajudá-lo a entender a composição da loja de perfis. Esses relatórios ajudam você a tomar decisões informadas sobre como e onde definir as expirações do evento de experiência para otimizar melhor o uso da licença:

* **API de relatório de sobreposição de conjunto de dados**: Expõe os conjuntos de dados que mais contribuem para o seu público-alvo endereçável. Você pode usar esse relatório para identificar qual [!DNL ExperienceEvent] conjuntos de dados para definir uma expiração de. Veja o tutorial em [geração do relatório de sobreposição de conjunto de dados](../../profile/tutorials/dataset-overlap-report.md) para obter mais informações.
* **API de relatório de sobreposição de identidade**: Expõe os namespaces de identidade que mais contribuem para o seu público-alvo endereçável. Veja o tutorial em [geração do relatório de sobreposição de identidade](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) para obter mais informações.
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### Expirações de dados de perfil pseudônimo {#pseudonymous-profile-expirations}

Esse recurso permite remover automaticamente perfis pseudônimos obsoletos da Loja de perfis. Para obter mais informações sobre este recurso, leia o [Visão geral da expiração de dados de perfil pseudônimo](../../profile/pseudonymous-profiles.md).

#### Expirações de evento de experiência {#event-expirations}

Esse recurso permite remover automaticamente dados comportamentais de um conjunto de dados habilitado para perfil que não é mais valioso para seus casos de uso. Consulte a visão geral em [Expirações de evento de experiência](../../profile/event-expirations.md) para obter detalhes sobre como esse processo funciona depois que ele é ativado para um conjunto de dados.

## Resumo das práticas recomendadas para conformidade do uso de licença {#best-practices}

Esta é uma lista de algumas práticas recomendadas que você pode seguir para garantir uma melhor adesão ao seu direito de uso de licença:

* Use o [painel de uso de licença](../../dashboards/guides/license-usage.md) para rastrear e monitorar as tendências de uso do cliente. Isso permite que você se antecipe a possíveis excedentes que possam ocorrer.
* Configurar [filtros de ingestão](#ingestion-filters) ao identificar os eventos necessários para os casos de uso de segmentação e personalização. Isso permite enviar somente eventos importantes necessários para seus casos de uso.
* Certifique-se de que você tenha somente [conjuntos de dados habilitados para perfil](#ingestion-filters) necessárias para os casos de uso de segmentação e personalização.
* Configurar [Expirações de evento de experiência](#event-expirations) e [Expirações de dados de perfil pseudônimo](#pseudonymous-profile-expirations) para dados de alta frequência, como dados da Web.
* Verifique periodicamente a [Relatórios de composição de perfil](#profile-store-composition-reports) para entender a composição da loja de perfis. Isso permite compreender as fontes de dados que mais contribuem para seu consumo de licença.

## Resumo e disponibilidade dos recursos {#feature-summary}

As práticas recomendadas e as ferramentas descritas neste documento ajudarão você a gerenciar melhor o uso do direito de licença no Adobe Experience Platform. Este documento será atualizado à medida que recursos adicionais forem lançados para ajudar a fornecer visibilidade e controle a todos os clientes do Experience Platform.

A tabela a seguir descreve a lista de recursos disponíveis no momento à sua disposição, para gerenciar melhor seu direito de uso de licenças.

| Recurso | Descrição |
| --- | --- |
| [Ativar/desativar conjuntos de dados para o perfil](../../catalog/datasets/user-guide.md) | Ative ou desative a assimilação do conjunto de dados no Perfil do cliente em tempo real. |
| [Expirações de evento de experiência](../../profile/event-expirations.md) | Aplique um tempo de expiração para todos os eventos assimilados em um conjunto de dados habilitado para perfil. Entre em contato com a equipe de conta do Adobe ou com o Atendimento ao cliente para ativar esse recurso. |
| [Filtros de preparação de dados do Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Aplicar [!DNL Kafka] filtros para excluir dados desnecessários da assimilação |
| [Filtros do conector de origem do Adobe Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Aplique filtros de conexão de origem de Audience Manager para excluir dados desnecessários da assimilação |
| [Ativar filtros de dados do SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) | Aplicar filtros de Alloy para excluir dados desnecessários da assimilação |
| [Filtros de dados do encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) | Aplicar servidor [!DNL Kafka] filtros para excluir dados desnecessários da assimilação.  Consulte a documentação em [regras de tags](../../tags/ui/managing-resources/rules.md) para obter mais informações. |
| [Interface do usuário do painel de uso de licença](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Visualizar um instantâneo dos dados relacionados à licença de sua organização para o Experience Platform |
| [API de relatório de sobreposição de conjunto de dados](../../profile/tutorials/dataset-overlap-report.md) | Gera os conjuntos de dados que mais contribuem para o seu público-alvo endereçável |
| [API de relatório de sobreposição de identidade](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Gera os namespaces de identidade que mais contribuem para o seu Público-alvo endereçável |

{style="table-layout:auto"}
