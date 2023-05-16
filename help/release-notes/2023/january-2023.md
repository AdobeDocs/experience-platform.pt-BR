---
title: Notas de versão da Adobe Experience Platform em janeiro de 2023
description: As notas de versão de janeiro de 2023 para o Adobe Experience Platform.
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: a0400ab255b3b6a7edb4dcfd5c33a0f9e18b5157
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 25 de janeiro de 2023**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [Assurance](#assurance)
- [Coleta de dados](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Perfil do cliente em tempo real](#profile)
- [Serviço de segmentação](#segmentation)
- [Fontes](#sources)

## Serviços de aprendizado artificial/de máquina {#ai-ml}

Os serviços de inteligência artificial e aprendizado de máquina capacitam analistas e profissionais de marketing a aproveitar o potencial da IA/ML nos casos de uso da experiência do cliente. Isso permite que os analistas de marketing configurem previsões, sem a necessidade de conhecimento em ciência de dados, específicas para as necessidades de uma empresa, usando configurações de nível empresarial.

### IA de atribuição

O Attribution AI é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Ele pode ser usado pelos comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em várias jornadas de clientes.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Preparo para a HIPAA | Os clientes do Healthcare Shield agora podem receber, usar, manter ou transmitir informações de saúde protegidas no Attribution AI e em determinados outros aplicativos baseados em Experience Platform. O Healthcare Shield destina-se aos clientes de saúde que são uma entidade coberta ou associados de negócios sob a HIPAA. Para obter mais informações, leia a documentação em [HIPAA e produtos e serviços de Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |
| Editar colunas adicionais de conjunto de dados de pontuação | Agora é possível adicionar ou remover colunas adicionais de conjunto de dados de pontuação (colunas de relatório) ao editar modelos existentes. Isso estende a flexibilidade das pontuações de atribuição para fornecer insights para dimensões adicionais depois que um modelo já tiver sido criado. Consulte a [Guia da interface do usuário de atribuição](../../intelligent-services/attribution-ai/user-guide.md) para saber mais. |

{style="table-layout:auto"}

Consulte a [Serviços de IA/ML](../../intelligent-services/attribution-ai/overview.md) visão geral para obter mais informações.

### Customer AI

O Customer AI para Real-time Customer Data Platform é usado para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala. Isso é feito sem precisar transformar as necessidades de negócios em um problema de aprendizado de máquina, escolher um algoritmo, treinar ou implantar.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Preparo para a HIPAA | Os clientes do Healthcare Shield agora podem receber, usar, manter ou transmitir informações de saúde protegidas no Customer AI para Real-time Customer Data Platform e em determinados outros aplicativos baseados em Experience Platform. O Healthcare Shield destina-se aos clientes de saúde que são uma entidade coberta ou associados de negócios sob a HIPAA. Para obter mais informações, consulte a documentação em [HIPAA e produtos e serviços de Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |

{style="table-layout:auto"}

Consulte a [Serviços de IA/ML](../../intelligent-services/customer-ai/overview.md) visão geral para obter mais informações.

## Assurance {#assurance}

O Adobe Assurance permite inspecionar, provar, simular e validar a forma como você coleta dados ou veicula experiências em seu aplicativo móvel.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Editor de validação | Foram adicionados novos aprimoramentos ao editor de validação. Esses aprimoramentos incluem colunas de validação, novas ferramentas de criação de código e exibições aprimoradas. |

{style="table-layout:auto"}

Para obter mais informações sobre o Assurance, leia o [Documentação de garantia](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente e enviá-los para a Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não-Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Nova tela inicial | A página inicial da interface do usuário da coleta de dados foi atualizada para incluir informações úteis sobre integração e links para simplificar a produtividade. Isso inclui:<ol><li>Documentação e fluxos de trabalho recomendados para começar</li><li>Propriedades, regras e elementos de dados recentes</li><li>Extensões populares</li><li>Novas atualizações de extensão com um recurso de instalação rápida</li></ol> |
| Enviar dados para [!DNL Google Ads] uso do encaminhamento de eventos | Agora você pode usar o [[!DNL Google Ads Enhanced Conversions] Extensão da API](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para encaminhamento de eventos, combinado com [Segredo do Google Oauth 2](../../tags/ui/event-forwarding/secrets.md#google-oauth2), para enviar dados do lado do servidor para o [!DNL Google Ads] em tempo real. |

{style="table-layout:auto"}

## Destinos (atualizado em 2 de fevereiro) {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [(Beta) Conexão do Adobe Experience Cloud Audiences](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Use o [!UICONTROL (Beta) Públicos-alvo da Adobe Experience Cloud] conexão para compartilhar segmentos do Experience Platform para várias soluções Experience Platform, como Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target ou Marketo. |
| [Conexão de perfil Pega](../../destinations/catalog/personalization/pega-profile.md) | Use o [!DNL Pega Profile Connector] no Adobe Experience Platform para criar uma conexão de saída ao vivo com seu [!DNL Amazon] Armazenamento S3 para exportar periodicamente dados de perfil para arquivos CSV do Adobe Experience Platform em seus próprios buckets do S3. Em [!DNL Pega Customer Decision Hub], você pode agendar trabalhos de dados para importar esses dados de perfil do armazenamento S3 para atualizar o [!DNL Pega Customer Decision Hub] perfil. |
| [(Beta) A conexão EU do CRM do Trade Desk](../../destinations/catalog/advertising/tradedesk-emails.md) | Com o lançamento da EUID (European Unified ID), você verá duas [!DNL The Trade Desk - CRM] os destinos [catálogo de destinos](/help/destinations/catalog/overview.md). <ul><li> Se você criar dados na UE, use a variável **[!DNL The Trade Desk - CRM (EU)]** destino.</li><li> Se você gerar dados nas regiões APAC ou NAMER, use a variável **[!DNL The Trade Desk - CRM (NAMER & APAC)]** destino. </li></ul> |

**Funcionalidade nova ou atualizada** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Aprimoramento da política de consentimento de mídia paga para integrações com destinos de transmissão | Um [reforço da aplicação da política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) on [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations) para casos de uso de ativação de mídia paga. Quando os perfis não estão mais qualificados para uma política de consentimento, o Experience Platform agora comunica proativamente sua saída da política para destinos de streaming. <br> <b>Observação</b>: Essa funcionalidade está disponível somente para clientes do **[!UICONTROL Privacy e Security Shield]**, bem como os **[!UICONTROL Escudo da Saúde]**. |
| Novas opções de delimitador para conectores de destino de armazenamento na nuvem beta | Três novas opções de delimitador (dois pontos) `:`, Pipe, Ponto e Vírgula `;`) agora estão disponíveis para os novos destinos de armazenamento na nuvem beta - [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Armazenamento Azure Data Lake Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Zona de aterrissagem de dados (Beta)](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Armazenamento em nuvem Google](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP (Beta)](/help/destinations/catalog/cloud-storage/sftp.md). <br> Leia sobre os [opções de formatação de arquivo](/help/destinations/ui/batch-destinations-file-formatting-options.md) para destinos com base em arquivo. |
| Novo parâmetro opcional disponível em [campos de dados do cliente](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md) configurações em [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: Use esse parâmetro quando precisar criar um campo de dados do cliente cujo valor deve ser exclusivo em todos os fluxos de dados de destino configurados pela organização do usuário. <br> Por exemplo, a variável **[!UICONTROL Alias de integração]** no campo [[!UICONTROL Personalização personalizada]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) o destino deve ser exclusivo, o que significa que dois fluxos de dados separados para esse destino não podem ter o mesmo valor para esse campo. |

**Correções e aprimoramentos** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Correção ou aprimoramento</b></td>
        <td><b>Descrição</b></td>
    </tr>
    <tr>
        <td>Comportamento de exportação atualizado para destinos com base em arquivo (PLAT-123316)</td>
        <td>Corrigimos um problema no comportamento do <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">atributos obrigatórios</a> ao exportar arquivos de dados para destinos em lote. <br> Anteriormente, cada registro nos arquivos de saída era verificado para conter ambos: <ol><li>Um valor não nulo da variável <code>mandatoryField</code> coluna e</li><li>Um valor não nulo em pelo menos um dos outros campos não obrigatórios.</li></ol> A segunda condição foi removida. Como resultado, você pode estar vendo mais linhas de saída em seus arquivos de dados exportados, conforme mostrado no exemplo abaixo:<br> <b> Exemplo de comportamento antes da versão de janeiro de 2023 </b> <br> Campo obrigatório: <code>emailAddress</code> <br> <b>Inserir dados para ativar</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>nulo</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>nulo</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Saída de Ativation</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Exemplo de comportamento após a versão de janeiro de 2023 </b> <br> <b>Saída de Ativation</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>nulo</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>nulo</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>Validação de interface do usuário e API para mapeamentos e mapeamentos duplicados necessários (PLAT-123316)</td>
        <td>A validação agora é aplicada da seguinte maneira na interface do usuário e na API quando <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mapping">campos de mapeamento</a> no workflow ativar destinos :<ul><li><b>Mapeamentos necessários</b>: Se o destino tiver sido configurado pelo desenvolvedor de destino com os mapeamentos necessários (por exemplo, a variável <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html?lang=en">Google Ad Manager 360</a> destino), esses mapeamentos necessários precisam ser adicionados pelo usuário ao ativar os dados no destino. </li><li><b>Mapeamentos duplicados</b>: Na etapa de mapeamento do fluxo de trabalho de ativação, é possível adicionar valores duplicados nos campos de origem, mas não nos campos de destino. Consulte a tabela abaixo para obter um exemplo de combinações de mapeamento permitidas e proibidas. <br><table><thead><tr><th>Permitido/proibido</th><th>Campo de origem</th><th>Campo de destino</th></tr></thead><tbody><tr><td>Permitido</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>alias de email2</li></ul></td></tr><tr><td>Proibido</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

Para obter informações mais gerais sobre destinos, consulte [visão geral dos destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Melhorias no nome de exibição da árvore de esquema | Anteriormente, os nomes de campo eram exibidos na interface do usuário, mas agora, os nomes de exibição dos campos de esquema na tela de esquema eram mais amigáveis para leitura. |

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Classe | [[!UICONTROL Conversão]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Uma classe para rastrear dados de conversão como conversões de moeda. |
| Grupo de campos | [[!UICONTROL Detalhes da Taxa de Conversão de Moeda]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Um grupo de campos para a variável [!UICONTROL Conversão] , capturando detalhes adicionais relacionados à conversão de moeda. |
| Grupo de campos | [[!UICONTROL Mapa de resultados de avaliação de políticas de consentimento com metadados]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | Captura detalhes para o resultado da avaliação de várias políticas de consentimento, incluindo informações de metadados sobre entradas e saídas da política de consentimento. |

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Tipo de dados | [[!UICONTROL Informações de detalhes de publicidade]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | O `ID` foi renomeado para `name`e as `name` campo agora `friendlyName`. |
| Tipo de dados | [[!UICONTROL Detalhes da proposta de decisão]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Adicionado um `selectionStrategy` campo que captura os detalhes de uma estratégia de seleção. |
| Grupo de campos | [[!UICONTROL Evento de experiência - Interações de proposta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | O grupo de campos agora é compatível com o [!UICONTROL Evento de etapa de Jornada] classe . |
| Tipo de dados | [[!UICONTROL Informações de detalhes do erro]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | O `ID` foi renomeado para `name`. |
| Tipo de dados | [[!UICONTROL Informações da mídia]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Reversão de uma alteração no padrão para a propriedade de segmento de vídeo. |
| Tipo de dados | [[!UICONTROL Informações de detalhes de dados de Qoe]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Remoção do `droppedFrameCount` campo. |
| Tipo de dados | [[!UICONTROL Informações de detalhes da sessão]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Renomeada a função `isAuthorized` campo para `authorized`e atualizou seu `type` para uma string quando era anteriormente uma booleana. |
| Tipo de dados | [[!UICONTROL Envio]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Adição de vários novos campos: `shipDate`, `trackingNumber`e `trackingURL`. |
| Grupo de campos | [[!UICONTROL Campos de entidade AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Adição de vários novos campos: `journeyNodeID`, `journeyNodeName`e `journeyModeType`. |
| Grupo de campos | [[!UICONTROL Evento de experiência do consumidor]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | O grupo de campos agora também é compatível com o [!UICONTROL Métricas de resumo] classe . |
| Grupo de campos | [[!UICONTROL Acionadores do produto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | O `productTriggers` agora está aninhado em um `weather` objeto. |
| Grupo de campos | [[!UICONTROL Acionadores relativos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | O `relativeTriggers` agora está aninhado em um `weather` objeto. |
| Grupo de campos | [[!UICONTROL Acionadores graves]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | O `severeTriggers` agora está aninhado em um `weather` objeto. |
| Grupo de campos | [[!UICONTROL Acionadores do tempo]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | O `weatherTriggers` agora está aninhado em um `weather` objeto. |
| Grupo de campos | [[!UICONTROL Contas Comerciais Relacionadas ao XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | O grupo de campos agora está estável. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM na Platform, consulte o [Visão geral do sistema XDM](../../xdm/home.md).

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagirem com sua marca. Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Descontinuação futura** {#deprecation}

Para remover a redundância no ciclo de vida de associação do segmento, a variável `Existing` será descontinuado do [mapa de associação de segmento](../../xdm/field-groups/profile/segmentation.md) no final de março de 2023. Um anúncio de acompanhamento incluirá a data exata da desativação.

Pós-descontinuação, os perfis qualificados em um segmento serão representados como `Realized` e os perfis desqualificados continuarão sendo representados como `Exited`. Isso trará paridade com destinos baseados em arquivo com `Active` e `Expired` status do segmento.

Essa alteração pode afetar você se estiver usando o [destinos corporativos](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Hubs de eventos do Azure, API HTTP) e tem processos downstream automatizados em vigor, com base no `Existing` status. Revise suas integrações downstream, se for o caso. Se estiver interessado em identificar perfis recém-qualificados além de um determinado tempo, considere usar uma combinação do `Realized` e o `lastQualificationTime` no mapa de associação de segmentos. Para obter mais informações, entre em contato com o representante do Adobe.

Para saber mais sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com dados de perfil, comece lendo o [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

## Serviço de segmentação {#segmentation}

[!DNL Segmentation Service] O define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da base do cliente. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Importação de valor em massa no Construtor de segmentos | O Construtor de segmentos agora é compatível com a importação de vários valores, seja fazendo upload de um arquivo CSV ou TSV ou inserindo valores separados por vírgula manualmente. Mais informações podem ser encontradas no [Guia do Construtor de segmentos](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| Expiração de associação de público-alvo externo | Por padrão, as associações de público-alvo externo são mantidas por 30 dias. Para mantê-los por mais tempo, use a variável `validUntil` durante a assimilação dos dados de público-alvo. |
| Expiração de associação de segmento gerado pela plataforma | Qualquer associação de segmento que esteja no `Exited` por mais de 30 dias, com base no `lastQualificationTime` estará sujeito a exclusão. |

{style="table-layout:auto"}

Para obter mais informações sobre [!DNL Segmentation Service]consulte o [Visão geral da segmentação](../../segmentation/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| Permitir acesso do usuário às subpastas de fontes de armazenamento na nuvem | Agora é possível definir o acesso a uma subpasta específica da fonte de armazenamento na nuvem ao criar uma nova conta. Depois de criados, os usuários só poderão acessar dados da subpasta permitida. Esse recurso está disponível nas seguintes fontes de armazenamento em nuvem: [Armazenamento Azure Blob](../../sources/connectors/cloud-storage/blob.md), [Armazenamento em nuvem Google](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)e [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilidade beta de [!DNL SugarCRM] | [!DNL SugarCRM] Agora, as fontes estão disponíveis em beta. Use o [!DNL SugarCRM Accounts & Contacts] e [!DNL SugarCRM Events] fontes para trazer dados de [!DNL SugarCRM] para o Experience Platform. Para obter mais informações, leia a [[!DNL SugarCRM] visão geral](../../sources/connectors/crm/sugarcrm.md). |
