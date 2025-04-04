---
title: Notas de versão da Adobe Experience Platform de outubro de 2022
description: As notas de versão de outubro de 2022 da Adobe Experience Platform.
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 29%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 26 de outubro de 2022**

- [Chaves gerenciadas pelo cliente](#cmk)
- [Coleção de dados](#data-collection)
- [Destinos](#destinations)
- [Experience Data Model](#xdm)
- [Query Service](#query-service)

## Chaves gerenciadas pelo cliente {#cmk}

Todos os dados armazenados no Adobe Experience Platform são criptografados em repouso usando chaves de nível de sistema. Se você estiver usando um aplicativo criado com base no Experience Platform, agora é possível optar por usar suas próprias chaves de criptografia, fornecendo maior controle sobre a segurança dos dados.

Consulte a visão geral em [chaves gerenciadas pelo cliente](../../landing/governance-privacy-security/customer-managed-keys/overview.md) para obter detalhes sobre o recurso.

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Manuseio de dados confidenciais para fluxos de dados | As sequências de dados agora usam várias tecnologias Experience Platform para lidar adequadamente com dados confidenciais, conforme aplicado por regulamentações como a HIPAA (Health Insurance Portability and Accountability Act, Lei de Portabilidade e Responsabilidade do Seguro de Saúde). Consulte a seção sobre [manipulação de dados sensíveis em sequências de dados](../../datastreams/overview.md#sensitive) para obter mais informações. |
| Extensão [!DNL Splunk] para encaminhamento de eventos | Agora você pode enviar dados para [!DNL Splunk] usando uma extensão de [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Consulte a [[!DNL Splunk] Visão geral de extensões](../../tags/extensions/server/splunk/overview.md) para obter mais informações. |
| Extensão [!DNL Zendesk] para encaminhamento de eventos | Agora você pode enviar dados para [!DNL Zendesk] usando uma extensão de [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Consulte a [[!DNL Zendesk] Visão geral de extensões](../../tags/extensions/server/zendesk/overview.md) para obter mais informações. |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Exportações de conjunto de dados do (Beta) | O [Conjunto de Dados exporta a funcionalidade do Beta](/help/destinations/ui/export-datasets.md) e permite exportar dados da primeira geração (conforme definido na [descrição do produto do Real-Time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)) do Adobe Experience Platform para seus próprios sistemas de clientes externos, por meio da interface do usuário de destinos. Isso permite obter dados do Experience Platform com um fluxo de trabalho sem código/low-code para seis destinos de armazenamento na nuvem (listados na tabela abaixo) para casos de uso analíticos e de conformidade. |
| (Beta) Recursos aprimorados de exportação de arquivos | Agora você pode se beneficiar da funcionalidade de personalização aprimorada ao exportar arquivos do Experience Platform: <br><ul><li>[Opções de nomenclatura de arquivo](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) adicionais.</li><li>Capacidade de definir cabeçalhos de arquivos personalizados em seus arquivos exportados por meio da [etapa de mapeamento aprimorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Capacidade de personalizar a formatação de arquivos de dados CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> Essa funcionalidade é suportada pelos seis novos cartões de armazenamento beta na nuvem listados na tabela abaixo. |

{style="table-layout:auto"}

**Destinos novos ou atualizados** {#new-or-updated-destinations}

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | O Line é uma plataforma de comunicação popular que conecta pessoas, serviços e informações e cresceu de um aplicativo de bate-papo para um centro de entretenimento, social e atividades diárias. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | O Microsoft Dynamics 365 é uma plataforma de aplicativos de negócios baseada em nuvem que combina ERP (Enterprise Resource Planning, planejamento de recursos corporativos) e CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente), além de aplicativos de produtividade e ferramentas de IA, para oferecer operações completas, mais perfeitas e controladas, melhor potencial de crescimento e custos reduzidos. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | O conector de destino [!DNL (Beta) Adobe Commerce] permite que você selecione um ou mais segmentos do Real-Time CDP para ativar em sua conta [!DNL Adobe Commerce] a fim de fornecer uma experiência personalizada dinâmica para seus compradores. Em [!DNL Adobe Commerce], você pode selecionar esses segmentos do Real-Time CDP para personalizar ofertas exclusivas no carrinho, como &quot;comprar 2 e receber 1 grátis&quot;. Você também pode exibir banners ilustrativos e modificar os preços do produto por meio de ofertas promocionais, todas personalizadas para segmentos do Adobe Real-Time CDP. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Criar uma conexão de saída ativa com o [!DNL Azure Data Lake Storage Gen2] para exportar periodicamente os arquivos de dados da Adobe Experience Platform para seu próprio local de armazenamento. Esse novo destino beta fornece funcionalidade aprimorada de exportação de arquivos e oferece suporte a exportações de conjuntos de dados. |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | O [!DNL Data Landing Zone] é uma interface de armazenamento do [!DNL Azure Blob] provisionada pela Adobe Experience Platform, que concede a você acesso a um recurso de armazenamento de arquivos seguro e baseado em nuvem para exportar arquivos do Experience Platform. Esse novo destino beta fornece funcionalidade aprimorada de exportação de arquivos e oferece suporte a exportações de conjuntos de dados. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Criar uma conexão de saída ativa com o [!DNL Google Cloud Storage] para exportar periodicamente os arquivos de dados da Adobe Experience Platform para seus próprios buckets. Esse novo destino beta fornece funcionalidade aprimorada de exportação de arquivos e oferece suporte a exportações de conjuntos de dados. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Os participantes do Beta agora veem dois cartões de destino [!DNL Amazon S3] lado a lado no catálogo de destinos. O novo destino beta fornece funcionalidade aprimorada de exportação de arquivos e oferece suporte a exportações de conjuntos de dados. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Os participantes do Beta agora veem dois cartões de destino [!DNL Azure Blob] lado a lado no catálogo de destinos. O novo destino beta fornece funcionalidade aprimorada de exportação de arquivos e oferece suporte a exportações de conjuntos de dados. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Os participantes do Beta agora veem dois cartões de destino [!DNL SFTP] lado a lado no catálogo de destinos. O novo destino beta fornece funcionalidade aprimorada de exportação de arquivos e oferece suporte a exportações de conjuntos de dados. |

{style="table-layout:auto"}

**Documentação nova ou atualizada**

| Documentação | Descrição |
| ----------- | ----------- |
| [Medidas de proteção de destinos](../../destinations/guardrails.md) | Esta página fornece limites de uso e taxa padrão em relação ao comportamento de ativação. |

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados inseridos na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Componentes de XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Tipo de dados | [[!UICONTROL Informações de detalhes da sessão]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Atualização do campo `authorized` de um tipo booleano para uma cadeia de caracteres. `season` e `episode` foram alterados de números inteiros para sequências de caracteres. |
| Tipo de dados | [[!UICONTROL Informações de detalhes de publicidade]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` foi renomeado para `friendlyName`, e `ID` foi renomeado para `name`. |
| Tipo de dados | [[!UICONTROL Informações de detalhes do erro]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` foi renomeado para `name`. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM no Experience Platform, consulte a [visão geral do sistema XDM](../../xdm/home.md).

## Query Service {#query-service}

O Query Service permite usar SQL padrão para consultar dados no [!DNL Data Lake] da Adobe Experience Platform. Você pode ingressar em qualquer conjunto de dados do [!DNL Data Lake] e capturar os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Monitorar consultas por meio da interface do usuário do Experience Platform | A guia Serviço de Consulta [!UICONTROL Consultas Agendadas] fornece visibilidade aprimorada para o status de todos os trabalhos de consulta por meio da interface. Agora você pode encontrar informações importantes sobre o status das execuções de consulta, incluindo mensagens de erro e códigos em caso de falha, na guia [!UICONTROL Consultas agendadas]. Também é possível assinar alertas por meio da interface do usuário para qualquer uma dessas consultas com base em seus status. Consulte o [documento Monitorar consultas](../../query-service/ui/monitor-queries.md) para saber mais sobre este recurso. |
| Consultar modelo de dados de insights de relatórios acelerado | Como parte do SKU do Data Distiller, o armazenamento acelerado de consultas permite reduzir o tempo e o poder de processamento necessários para obter insights críticos de seus dados. Com o armazenamento acelerado da query, é possível criar um modelo de dados personalizado e/ou estender modelos de dados existentes do Adobe Real-Time Customer Data Platform para melhorar os insights do relatório e suas visualizações. Consulte o [documento de insights de relatórios de armazenamento acelerado da consulta](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md) para saber mais sobre este recurso. |

{style="table-layout:auto"}

Para obter mais informações sobre os Serviços de Consulta, consulte a [visão geral do Serviço de Consulta](../../query-service/home.md).
Novos recursos na Adobe Experience Platform:

