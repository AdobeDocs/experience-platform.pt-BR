---
title: Notas da versão de fevereiro de 2024 da Adobe Experience Platform
description: Notas da versão de fevereiro de 2024 da Adobe Experience Platform.
source-git-commit: 3c0b7c4eee7c790a8ffae95c05a8db6ba7c3b285
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 22%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 21 de fevereiro de 2024**

Atualizações dos recursos existentes no Experience Platform:

- [Alertas](#alerts)
- [Coleção de dados](#data-collection)
- [Destinos](#destinations)
- [Sandboxes](#sandboxes)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades da Platform. É possível assinar diferentes regras de alerta por meio da [!UICONTROL Alertas] na interface do usuário da Platform e podem optar por receber mensagens de alerta na própria interface ou por notificações por email.
**Recursos novos ou atualizados**
| Recurso | Descrição | | — | — | | Guia Histórico de alertas | Como administrador de Experience Platform, você pode usar o recurso gerenciar assinantes de alertas para atribuir um alerta a uma ID de usuário Adobe, endereço de email externo ou uma lista de grupo de email. Para obter mais informações, consulte [documentação da interface de alertas](../../observability/alerts/ui.md) para obter mais informações sobre a guia histórico. |

{style="table-layout:auto"}

Para saber mais sobre alertas, leia a [[!DNL Observability Insights] visão geral](../../observability/home.md).

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| [Suporte a mensagens no aplicativo da Web no SDK da Web](../../edge/personalization/web-in-app-messaging.md) | O Adobe Experience Platform Web SDK agora é compatível com a configuração de mensagens no aplicativo da Web para campanhas do Adobe Journey Optimizer. |

{style="table-layout:auto"}

Para saber mais sobre coleções de dados, leia a [visão geral das coleções de dados](../../tags/home.md).

<!-- ## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions for Adobe Analytics | You can now use the following functions to extract event data from Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md) |

{style="table-layout:auto"}

For more information on Data Prep, read the [Data Prep overview](../../data-prep/home.md). -->

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos** {#new-destinations}

| Destino | Descrição |
| ----------- | ----------- |
| [Conexão Gainsight PX](../../destinations/catalog/analytics/gainsight-px.md) | O Gainsight PX é uma plataforma de experiência de produto que permite que as equipes de produtos entendam como os usuários usam seus produtos, coletam feedback e criam envolvimentos no aplicativo, como apresentações de produtos para impulsionar a integração de usuários e a adoção de produtos. |
| [Conexão de Tags do Mailchimp](../../destinations/catalog/email-marketing/mailchimp-tags.md) | O Mailchimp é uma plataforma de automação de marketing popular e um serviço de marketing por email. Você pode usar o conector de tags do Mailchimp para estruturar, rotular ou categorizar seus contatos. |
| [Conexão com o SAP Commerce](../../destinations/catalog/ecommerce/sap-commerce.md) | O SAP Commerce é uma solução de plataforma de comércio eletrônico baseada em nuvem para empresas B2B e B2C e está disponível como parte do portfólio SAP Customer Experience. Você pode usar esse destino para atualizar os detalhes do cliente no SAP Commerce a partir de um público Experience Platform existente. |

{style="table-layout:auto"}

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Ativar públicos-alvo de conta disponíveis no geral | A funcionalidade para ativar públicos-alvo da conta para determinados destinos agora está geralmente disponível para empresas que compram o [B2B](/help/rtcdp/overview.md#rtcdp-b2b) e [Negócio para pessoa](/help/rtcdp/overview.md#rtcdp-b2p) Real-time Customer Data Platform. Leia o tutorial sobre [ativação de públicos da conta](/help/destinations/ui/activate-account-audiences.md) para obter informações completas, incluindo destinos compatíveis. |
| Ferramentas de aplicação de consentimento da Lei de Mercados Digitais para destinos Google | A Google está lançando alterações no [API do Google Ads](https://developers.google.com/google-ads/api/docs/start), [Correspondência de Cliente](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html), e o [API de vídeo e exibição 360](https://developers.google.com/display-video/api/guides/getting-started/overview) a fim de apoiar os requisitos de conformidade e consentimento definidos no [Lei dos Mercados Digitais](https://digital-markets-act.ec.europa.eu/index_en) (DMA) na União Europeia ([Política de consentimento do usuário da UE](https://www.google.com/about/company/user-consent-policy/)). A aplicação dessas alterações aos requisitos de consentimento deve entrar em vigor a partir de 6 de março de 2024. <br/><br/> Para aderir à política de consentimento do usuário da UE e continuar criando listas de públicos-alvo para usuários no Espaço Econômico Europeu (EEE), anunciantes e parceiros devem garantir que eles transmitem o consentimento do usuário final ao fazer upload dos dados de público-alvo. Como Parceiro da Google, o Adobe fornece as ferramentas necessárias para cumprir esses requisitos de consentimento de acordo com a DMA na União Europeia.<br/><br/>Clientes que compraram o Adobe Privacy &amp; Security Shield e configuraram um [política de consentimento](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar perfis não consentidos, não é necessário tomar nenhuma ação.<br/><br/>Os clientes que não compraram o Adobe Privacy &amp; Security Shield devem usar o [definição de segmento](../../segmentation/home.md#segment-definitions) recursos no [Construtor de segmentos](../../segmentation/ui/segment-builder.md) para filtrar perfis não consentidos, a fim de continuar usando os destinos existentes do Real-Time CDP Google sem interrupção. |
| [!BADGE Beta]{type=Informative} Reordenar campos de mapeamento para destinos em lote | Agora é possível alterar a ordem das colunas nas exportações de CSV arrastando e soltando os campos de mapeamento na [mapeamento](../../destinations/ui/activate-batch-profile-destinations.md#mapping) etapa. A ordem dos campos mapeados na interface reflete a ordem das colunas no arquivo CSV exportado, de cima para baixo, com a linha superior sendo a coluna mais à esquerda do arquivo CSV. <br/><br/> Esse recurso está na versão beta e só está disponível para clientes selecionados. Para solicitar acesso a esse recurso, entre em contato com o representante da Adobe. |
| [!BADGE Beta]{type=Informative} Agendamentos de exportação padrão pré-selecionados para destinos em lote | O Experience Platform agora define automaticamente um agendamento padrão para cada exportação de arquivo. Consulte a documentação em [agendamento de exportações de público](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) para saber como modificar o cronograma padrão. <br/><br/> Esse recurso está na versão beta e só está disponível para clientes selecionados. Para solicitar acesso a esse recurso, entre em contato com o representante da Adobe. |
| [!BADGE Beta]{type=Informative} Agendamentos de ativação de públicos-alvo de edição em massa para destinos em lote | Agora você pode editar o agendamento de ativação para vários públicos-alvo em massa, no [Dados de ativação](../../destinations/ui/destination-details-page.md#bulk-edit-schedule) página. <br/><br/> Esse recurso está na versão beta e só está disponível para clientes selecionados. Para solicitar acesso a esse recurso, entre em contato com o representante da Adobe. |
| [!BADGE Beta]{type=Informative} Arquivos de exportação em massa sob demanda para destinos em lote | Agora você pode exportar públicos-alvo em massa para destinos em lote por meio do [exportar arquivos por demanda](../../destinations/ui/export-file-now.md) funcionalidade. <br/><br/> Esse recurso está na versão beta e só está disponível para clientes selecionados. Para solicitar acesso a esse recurso, entre em contato com o representante da Adobe. |

{style="table-layout:auto"}

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Sandboxes {#sandboxes}

O Adobe Experience Platform foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional. Para atender a essa necessidade, o Experience Platform fornece sandboxes que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Ferramentas de sandbox | Além de agora suportar tipos de objeto para regras de consentimento e governança, use as ferramentas da sandbox para importar esquemas sem perfis unificados ativados, verifique se há atributos ausentes na sandbox de destino ao importar um segmento e use a política de mesclagem existente como padrão. Para obter mais informações sobre esses recursos, consulte [guia da interface do usuário de ferramentas da sandbox](../../sandboxes/ui/sandbox-tooling.md). |

{style="table-layout:auto"}

Para obter mais informações sobre sandboxes, leia a [visão geral das sandboxes](../../sandboxes/home.md).

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] permite segmentar dados relacionados a indivíduos (como clientes, prospectos, usuários ou organizações) que estão armazenados na [!DNL Experience Platform] em públicos-alvo. Você pode criar públicos-alvo por meio de definições de segmento ou outras fontes a partir dos dados do [!DNL Real-Time Customer Profile]. Esses públicos-alvo são configurados e mantidos de forma centralizada na [!DNL Platform] e podem ser acessados a qualquer momento usando as soluções da Adobe.

**Novo recurso**

| Recurso | Descrição |
| ------- | ----------- |
| Públicos da conta | Os públicos-alvo da conta agora estão disponíveis! Agora você pode usar a segmentação de conta para trazer a total facilidade e sofisticação da experiência de segmentação de marketing de públicos com base em pessoas para públicos com base em conta nas edições B2B e B2P da Real-Time Customer Platform. Essa versão permite usar públicos-alvo com base em pessoas como um predicado para públicos-alvo com base em conta, adiciona recursos de pesquisa, suporta o uso de entidades personalizadas e é compatível com a Governança de dados. Para obter mais informações sobre esse recurso, leia a [visão geral dos públicos-alvo da conta](../../segmentation/ui/account-audiences.md). |

{style="table-layout:auto"}

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| [!BADGE Beta]{type=Informativo} [!DNL Acxiom] origem | Use o [[!DNL Acxiom Prospecting Data Import] origem](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md) para recuperar e mapear dados do [!DNL Acxiom] serviço de prospecto para o Experience Platform. |

{style="table-layout:auto"}

Para obter mais informações sobre fontes, leia a [visão geral das origens](../../sources/home.md).
