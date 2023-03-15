---
title: Notas de versão da Adobe Experience Platform de outubro de 2022
description: As notas de versão de outubro de 2022 para Adobe Experience Platform.
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 3%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 26 de outubro de 2022**

- [Chaves gerenciadas pelo cliente](#cmk)

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Coleta de dados](#data-collection)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de query](#query-service)
- [Fontes](#sources)

## Chaves gerenciadas pelo cliente {#cmk}

Todos os dados armazenados no Adobe Experience Platform são criptografados em repouso usando chaves de nível de sistema. Se você estiver usando um aplicativo criado sobre a Platform, agora é possível optar por usar suas próprias chaves de criptografia, fornecendo maior controle sobre a segurança dos dados.

Consulte a visão geral em [chaves gerenciadas pelo cliente](../../landing/governance-privacy-security/customer-managed-keys.md) para obter detalhes sobre o recurso.

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente do lado do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Manuseio de dados confidenciais para fluxos de dados | As sequências de dados agora usam várias tecnologias da Platform para lidar adequadamente com dados confidenciais, conforme aplicado por regulamentações como a HIPAA (Health Insurance Portability and Accountability Act, Lei de Portabilidade e Responsabilidade do Seguro de Saúde). Consulte a seção sobre [tratamento de dados confidenciais em fluxos de dados](../../edge/datastreams/overview.md#sensitive) para obter mais informações. |
| [!DNL Splunk] extensão para encaminhamento de eventos | Agora você pode enviar dados para [!DNL Splunk] usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Splunk] visão geral da extensão](../../tags/extensions/server/splunk/overview.md) para obter mais informações. |
| [!DNL Zendesk] extensão para encaminhamento de eventos | Agora você pode enviar dados para [!DNL Zendesk] usando um [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) extensão. Consulte a [[!DNL Zendesk] visão geral da extensão](../../tags/extensions/server/zendesk/overview.md) para obter mais informações. |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, publicidade direcionada e muitos outros casos de uso.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| (Beta) Exportações de conjuntos de dados | A variável [Funcionalidade Beta de exportações de conjunto de dados](/help/destinations/ui/export-datasets.md) permite exportar os dados da primeira geração (conforme definido na [Descrição do produto Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)) do Adobe Experience Platform para seus próprios sistemas de clientes externos, por meio da interface do usuário de destinos. Isso permite que você obtenha dados do Experience Platform com um fluxo de trabalho sem código/low-code para seis destinos de armazenamento na nuvem (listados na tabela abaixo) para casos de uso analíticos e de conformidade. |
| (Beta) Recursos aprimorados de exportação de arquivos | Agora você pode se beneficiar da funcionalidade aprimorada de personalização ao exportar arquivos do Experience Platform: <br><ul><li>Adicional [opções de nomenclatura de arquivo](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).</li><li>Capacidade de definir cabeçalhos de arquivos personalizados em seus arquivos exportados por meio da [etapa de mapeamento aprimorada](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Capacidade de personalizar a formatação de arquivos de dados CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> Essa funcionalidade é compatível com os seis novos cartões de armazenamento beta na nuvem listados na tabela abaixo. |

{style="table-layout:auto"}

**Destinos novos ou atualizados**

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | O Line é uma plataforma de comunicação popular que conecta pessoas, serviços e informações e cresceu de um aplicativo de bate-papo para um centro de entretenimento, social e atividades diárias. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | O Microsoft Dynamics 365 é uma plataforma de aplicativos de negócios baseada em nuvem que combina ERP (Enterprise Resource Planning, planejamento de recursos corporativos) e CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente), além de aplicativos de produtividade e ferramentas de IA, para oferecer operações completas, mais perfeitas e controladas, melhor potencial de crescimento e custos reduzidos. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | A variável [!DNL (Beta) Adobe Commerce] o conector de destino permite selecionar um ou mais segmentos do Real-Time CDP para ativar no [!DNL Adobe Commerce] para fornecer uma experiência personalizada dinâmica aos seus compradores. Dentro de [!DNL Adobe Commerce], você pode selecionar esses segmentos do Real-Time CDP para personalizar ofertas exclusivas no carrinho, como &quot;comprar 2 e receber 1 grátis&quot;. Você também pode exibir banners ilustrativos e modificar os preços do produto por meio de ofertas promocionais, todas personalizadas para segmentos do Adobe Real-Time CDP. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Criar uma conexão de saída ativa com o [!DNL Azure Data Lake Storage Gen2] para exportar arquivos de dados do Adobe Experience Platform periodicamente para seu próprio local de armazenamento. Esse novo destino beta fornece funcionalidade aprimorada de exportação de arquivos e oferece suporte a exportações de conjuntos de dados. |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] é um [!DNL Azure Blob] interface de armazenamento de dados provisionada pela Adobe Experience Platform, que concede acesso a um recurso seguro de armazenamento de arquivos baseado em nuvem para exportar arquivos da plataforma. Esse novo destino beta fornece funcionalidade aprimorada de exportação de arquivos e oferece suporte a exportações de conjuntos de dados. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Criar uma conexão de saída ativa com o [!DNL Google Cloud Storage] para exportar arquivos de dados do Adobe Experience Platform periodicamente para seus próprios buckets. Esse novo destino beta fornece funcionalidade aprimorada de exportação de arquivos e oferece suporte a exportações de conjuntos de dados. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Os participantes beta estão vendo dois [!DNL Amazon S3] cartões de destino lado a lado no catálogo de destinos. O novo destino beta fornece funcionalidade aprimorada de exportação de arquivos e oferece suporte a exportações de conjuntos de dados. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Os participantes beta estão vendo dois [!DNL Azure Blob] cartões de destino lado a lado no catálogo de destinos. O novo destino beta fornece funcionalidade aprimorada de exportação de arquivos e oferece suporte a exportações de conjuntos de dados. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Os participantes beta estão vendo dois [!DNL SFTP] cartões de destino lado a lado no catálogo de destinos. O novo destino beta fornece funcionalidade aprimorada de exportação de arquivos e oferece suporte a exportações de conjuntos de dados. |

{style="table-layout:auto"}

**Documentação nova ou atualizada**

| Documentação | Descrição |
| ----------- | ----------- |
| [Medidas de proteção de destinos](../../destinations/guardrails.md) | Esta página fornece limites de uso e taxa padrão em relação ao comportamento de ativação. |

Para obter informações mais gerais sobre destinos, consulte o [visão geral dos destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos das ações do cliente, definir públicos do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Tipo de dados | [[!UICONTROL Informações de detalhes da sessão]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Atualização do `authorized` de um tipo booleano para uma string. `season` e `episode` foram alterados de números inteiros para sequências de caracteres. |
| Tipo de dados | [[!UICONTROL Informações de detalhes de publicidade]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` foi renomeado para `friendlyName`, e `ID` foi renomeado para `name`. |
| Tipo de dados | [[!UICONTROL Informações de detalhes do erro]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | A `ID` foi renomeada como `name`.  |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM na Platform, consulte a [Visão geral do sistema XDM](../../xdm/home.md).

## Serviço de query {#query-service}

O Serviço de consulta permite usar o SQL padrão para consultar dados no Adobe Experience Platform [!DNL Data Lake]. Você pode associar qualquer conjunto de dados da [!DNL Data Lake] e capture os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Monitorar consultas por meio da interface do usuário da Platform | O Serviço de consulta [!UICONTROL Consultas programadas] A guia fornece visibilidade aprimorada para o status de todos os trabalhos de consulta por meio da interface. Agora você pode encontrar informações importantes sobre o status das execuções de consulta, incluindo mensagens de erro e códigos em caso de falha, no [!UICONTROL Consultas programadas] guia. Também é possível assinar alertas por meio da interface do usuário para qualquer uma dessas consultas com base em seus status. Consulte a [Monitorar documento de consultas](../../query-service/ui/monitor-queries.md) para saber mais sobre este recurso. |
| Consultar modelo de dados de insights de relatórios acelerado | Como parte do SKU do Data Distiller, o armazenamento acelerado de consultas permite reduzir o tempo e o poder de processamento necessários para obter insights críticos de seus dados. Com o armazenamento acelerado da query, é possível criar um modelo de dados personalizado e/ou estender modelos de dados existentes do Adobe Real-time Customer Data Platform para melhorar os insights do relatório e suas visualizações. Consulte a [consultar documento de insights de relatórios de loja acelerada](../../query-service/data-distiller/query-accelerated-store/reporting-insights-data-model.md) para saber mais sobre este recurso. |

{style="table-layout:auto"}

Para obter mais informações sobre os Serviços de consulta, consulte [Visão geral do Serviço de consulta](../../query-service/home.md).
Novos recursos na Adobe Experience Platform:

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- | 
| Disponibilidade beta da fonte do Adobe Workfront | Use o [Origem do Adobe Workfront](../../sources/connectors/adobe-applications/workfront.md) para trazer seus dados do Workfront para o Experience Platform e executar casos de uso, como combinar seus registros de trabalho com dados de terceiros, aplicar análises de séries históricas e de tempo em registros de trabalho e consultar dados de trabalho usando SQL padrão. Para obter mais informações, leia o guia em [criação de uma conexão de origem do Workfront na interface](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |

Para saber mais sobre fontes, leia o [visão geral das origens](../../sources/home.md).
