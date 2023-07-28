---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão de julho de 2023 para o Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 7cc7d43f6424ff91bd237235b278bf13a0add45d
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 25%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 26 de julho de 2023**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [Coleção de dados](#data-collection)
- [Destinos](#data-prep)
- [Serviço de segmentação](#segmentation)
- [Fontes](#sources)

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Recursos novos ou atualizados**

| Tipo | Recurso | Descrição |
| --- | --- | --- |
| Tags e encaminhamento de eventos | Logs de auditoria da coleção de dados | Agora você pode ver quando uma ação foi executada e quem executou essa ação em Tags e no Encaminhamento de eventos. Isso facilita a solução de problemas do produto, o controle adequado e as atividades de auditoria interna. Esses dados de auditoria são exibidos por meio de menus deslizantes no contexto que também incluem ações rápidas e atualizações de status de recursos. Esses dados estão disponíveis na interface das Tags e do Encaminhamento de eventos nas seguintes telas:<br><ul><li>[Visão geral da propriedade](../../tags/ui/event-forwarding/overview.md#properties)</li><li>[Regras](../../tags/ui/event-forwarding/overview.md#rules)</li><li>[Elementos de dados](../../tags/ui/event-forwarding/overview.md#data-elements)</li><li>[Extensões](../../tags/ui/event-forwarding/overview.md#extensions)</li><li>[Revisão da biblioteca](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li><li>[Última build e publicação da biblioteca](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li></ul> |
| Datastreams | [Pesquisa geográfica](../../datastreams/configure.md#advanced-options) | Agora é possível configurar a geolocalização e a pesquisa de rede para que os fluxos de dados incluam informações como: <ul><li>País</li><li>Código postal</li><li>Estado/Província</li><li>DMA</li><li>Cidade</li><li>Latitude </li><li>Longitude</li><li>Operadora</li><li>Domain</li><li>ISP</li></ul> Você é responsável por garantir que obteve todas as permissões, consentimentos, autorizações e a autorização necessários, exigidos pelas leis e regulamentos aplicáveis, para coletar, processar e transmitir dados pessoais, incluindo informações precisas de geolocalização. <br> A seleção de ofuscação do endereço IP não afeta o nível de informações de geolocalização que serão derivadas do endereço IP e enviadas para as soluções de Adobe configuradas. As pesquisas de geolocalização devem ser limitadas ou desabilitadas separadamente. <br> Consulte a [documentação dos datastreams](../../datastreams/configure.md#advanced-options) para obter mais detalhes. |

{style="table-layout:auto"}

Para obter mais informações sobre a coleta de dados, leia o [visão geral das coleções de dados](../../tags/home.md).
<!-- 
## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions | You can now use the following functions when mapping objects in Data Prep: <ul><li>`map_get_values`</li><li>`map_has_keys`</li><li>`add_to_map`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md#hierarchies---objects). |

{style="table-layout:auto"}

For more information on Data Prep, please read the [Data Prep overview](../../data-prep/home.md). -->

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados** {#new-updated-destinations}

| Destino | Novo ou atualizado | Descrição |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Onboarding]](../../destinations/catalog/advertising/liveramp-onboarding.md) | Novo | Integrar identidades do Adobe Experience Platform no [!DNL LiveRamp Connect] para poder direcionar os usuários em dispositivos móveis, Web aberta, redes sociais e [!DNL CTV] plataformas, usando o [!DNL Ramp ID] identificador. |
| [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Novo | Criar uma conexão de saída ativa com o [!DNL Azure Data Lake Storage Gen2] para exportar arquivos de dados do Adobe Experience Platform periodicamente para seu próprio local de armazenamento. Esse novo destino oferece funcionalidade aprimorada de exportação de arquivos e suporte [!BADGE Beta]{type=Informative} |
| [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | Novo | [!DNL Data Landing Zone] é um [!DNL Azure Blob] interface de armazenamento de dados provisionada pela Adobe Experience Platform, que concede acesso a um recurso seguro de armazenamento de arquivos baseado em nuvem para exportar arquivos da plataforma. Esse novo destino oferece funcionalidade aprimorada de exportação de arquivos e suporte [!BADGE Beta]{type=Informative} |
| [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Novo | Criar uma conexão de saída ativa com o [!DNL Google Cloud Storage] para exportar arquivos de dados do Adobe Experience Platform periodicamente para seus próprios buckets. Esse novo destino oferece funcionalidade aprimorada de exportação de arquivos e suporte [!BADGE Beta]{type=Informative} |
| [[!DNL Amazon S3] update](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Atualização dos pacotes   | Com essa atualização, o destino oferece funcionalidade aprimorada de exportação de arquivos e suporte [!BADGE Beta]{type=Informative} |
| [[!DNL Azure Blob] update](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Atualização dos pacotes   | Com essa atualização, o destino oferece funcionalidade aprimorada de exportação de arquivos e suporte [!BADGE Beta]{type=Informative} |
| [[!DNL SFTP] update](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Atualização dos pacotes   | Com essa atualização, o destino oferece funcionalidade aprimorada de exportação de arquivos e suporte [!BADGE Beta]{type=Informative} |
| Conexão com o [[!DNL Adobe Campaign Managed Services] ](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Atualização dos pacotes   | A variável [!DNL Adobe Campaign Managed Services] a integração do com o Adobe Experience Platform agora oferece suporte a diferentes tipos de sincronização de público-alvo. Use o controle Selecionar tipo de sincronização para determinar se você deve exportar públicos para o Adobe Campaign ou se os públicos-alvo e seus atributos de perfil. <br> ![Novo Seletor do tipo de sincronização de seleção realçado.](/help/release-notes/2023/assets/acms-destination-export-type.png "Novo Seletor do tipo de sincronização de seleção realçado."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

A versão de atualização e disponibilidade geral dos seis destinos de armazenamento na nuvem acima fornece a seguinte funcionalidade:

- Adicional [opções de nomenclatura de arquivo](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
- Capacidade de definir cabeçalhos de arquivos personalizados em seus arquivos exportados por meio da [etapa de mapeamento aprimorada](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
- Capacidade de personalizar o [formatação de arquivos de dados CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).
- [!BADGE Beta]{type=Informative}[Suporte à exportação de conjuntos de dados](/help/destinations/ui/export-datasets.md).


**Correções e aprimoramentos** {#destinations-fixes-and-enhancements}

- Corrigimos um problema com o destino do Marketing Cloud (API) Salesforce no qual, na etapa de mapeamento, nem todos os atributos de destino disponíveis eram retornados do Salesforce. Existe agora uma [limite superior de atributos target 2000](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md#mapping-considerations-example) no Salesforce que pode ser exibido.
- Corrigimos um problema no destino do Microsoft Dynamics 365. O destino agora oferece suporte ao roteamento regional de dados por meio do [Seletor de região](/help/destinations/catalog/crm/microsoft-dynamics-365.md#authenticate), para que você possa rotear suas exportações de dados dependendo da região em que sua empresa está provisionada no ecossistema do Microsoft. ![Novo seletor de região realçado.](/help/release-notes/2023/assets/region-parameter-microsoft-dynamics-365.png "Novo seletor de região realçado."){width="100" zoomable="yes"}

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Serviço de segmentação {#segmentation}

[!DNL Segmentation Service] permite segmentar dados armazenados no [!DNL Experience Platform] que se relaciona a indivíduos (como clientes, clientes potenciais, usuários ou organizações) em públicos. Você pode criar públicos-alvo por meio de definições de segmento ou outras fontes da [!DNL Real-Time Customer Profile] dados. Esses públicos-alvo são configurados e mantidos de forma centralizada em [!DNL Platform]e são prontamente acessíveis por qualquer solução Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Portal de público | O Audience Portal oferece uma nova experiência de navegação para acessar, criar e gerenciar públicos no Adobe Experience Platform. No Audience Portal, você pode visualizar públicos gerados pela Platform e gerados externamente; melhorar a eficiência do trabalho por meio de filtragem, pastas e tags; criar públicos gerados pela Platform; e importar públicos gerados externamente por meio de arquivos CSV. Para obter mais informações sobre o Audience Portal, leia o [Guia da interface do usuário do serviço de segmentação](../../segmentation/ui/overview.md). |
| Composição de público-alvo | A Composição de público-alvo fornece um espaço de trabalho fácil de usar para criar e editar públicos-alvo, usando blocos usados para representar ações diferentes. Para obter mais informações sobre Composição de público, leia a [Guia da interface do usuário da Composição de público-alvo](../../segmentation/ui/audience-composition.md). |

Para obter mais informações sobre [!DNL Segmentation Service], leia o [Visão geral da segmentação](../../segmentation/home.md).

## Fontes {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL SAP Commerce] | Agora você pode usar o [[!DNL SAP Commerce] origem](../../sources/connectors/ecommerce/sap-commerce.md) para trazer os dados de cobrança da assinatura do seu [!DNL SAP Commerce] conta para Experience Platform. |
| Compatibilidade com o [!DNL Phoenix] | Agora você pode usar o [[!DNL Phoenix] origem](../../sources/connectors/databases/phoenix.md) para trazer dados de seu [!DNL Phoenix] banco de dados para Experience Platform. |
| Atualizações de autenticação do [!DNL Salesforce] e [!DNL Salesforce Service Cloud] | Agora você pode especificar a versão da API do [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) e [[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md) ao autenticar uma nova conta com a interface de usuário do Experience Platform ou o [!DNL Flow Service] API. |

{style="table-layout:auto"}

Para obter mais informações sobre fontes, leia o [visão geral das origens](../../sources/home.md).
