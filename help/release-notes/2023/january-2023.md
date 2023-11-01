---
title: Notas da versão de janeiro de 2023 da Adobe Experience Platform
description: As notas da versão de janeiro de 2023 da Adobe Experience Platform.
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2408'
ht-degree: 98%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 25 de janeiro de 2023**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [Assurance](#assurance)
- [Coleção de dados](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Perfil do cliente em tempo real](#profile)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## Serviços de inteligência artificial/aprendizado de máquina {#ai-ml}

Os serviços de inteligência artificial e aprendizado de máquina capacitam analistas e profissionais de marketing para que aproveitem o potencial da inteligência artificial/aprendizado de máquina em casos de uso de experiência do cliente. Isso permite que os analistas de marketing definam previsões específicas para as necessidades de uma empresa sem a necessidade de conhecimento especializado em ciência de dados, usando configurações de nível empresarial.

### IA de atribuição

A IA de atribuição é usada para atribuir créditos a pontos de contato que levam a eventos de conversão. Ela pode ser usada por comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em várias jornadas de clientes.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Preparo para a HIPAA | Os clientes do Healthcare Shield agora podem receber, usar, manter ou transmitir informações protegidas de saúde na IA de atribuição e em determinados aplicativos baseados na Experience Platform. O Healthcare Shield é orientado para clientes da área da saúde que sejam ou entidades cobertas ou empresas associadas nos termos da lei americana HIPAA. Para obter mais informações, leia a documentação em [HIPAA e produtos e serviços da Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |
| Editar colunas adicionais do conjunto de dados de pontuação | Agora é possível adicionar ou remover mais colunas de conjunto de dados de pontuação (colunas de relatórios) ao editar modelos já existentes. Isso estende a flexibilidade das pontuações de atribuição para fornecer insights de dimensões adicionais com um modelo já criado. Consulte o [Guia da interface de atribuição](../../intelligent-services/attribution-ai/user-guide.md) para saber mais. |

{style="table-layout:auto"}

Consulte a visão geral dos [Serviços de inteligência artificial/aprendizado de máquina](../../intelligent-services/attribution-ai/overview.md) para obter mais informações.

### IA do cliente

A IA do cliente para a Real-time Customer Data Platform é usada para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em grande escala. Isso é feito sem precisar transformar as necessidades de negócios em um problema de aprendizado de máquina, escolher um algoritmo, treinar ou implantar.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Preparo para a HIPAA | Os clientes do Healthcare Shield agora podem receber, usar, manter ou transmitir informações protegidas de saúde na IA do cliente do Real-time Customer Data Platform e outros aplicativos baseados na Experience Platform. O Healthcare Shield é orientado para clientes da área da saúde que sejam ou entidades cobertas ou empresas associadas nos termos da lei americana HIPAA. Para obter mais informações, consulte a documentação em [HIPAA e produtos e serviços da Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |

{style="table-layout:auto"}

Consulte a visão geral dos [Serviços de inteligência artificial/aprendizado de máquina](../../intelligent-services/customer-ai/overview.md) para obter mais informações.

## Assurance {#assurance}

O Adobe Assurance permite inspecionar, provar, simular e validar a forma como você coleta dados ou fornece experiências em seus aplicativos móveis.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Editor de validação | Foram adicionados novas melhorias ao editor de validação. Essas melhorias incluem colunas de validação, novas ferramentas de criação de código e visualizações aprimoradas. |

{style="table-layout:auto"}

Para obter mais informações sobre o Assurance, leia a [Documentação do Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Nova página inicial | A página inicial da interface da Coleção de dados foi atualizada para incluir informações de integração úteis e links para simplificar a produtividade. Isso inclui:<ol><li>Documentação e fluxos de trabalho recomendados para começar</li><li>Propriedades, regras e elementos de dados recentes</li><li>Extensões populares</li><li>Novas atualizações de extensão com recurso de instalação rápida</li></ol> |
| Enviar dados para o [!DNL Google Ads] usando o encaminhamento de eventos | Agora é possível usar o extensão da API](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) do [[!DNL Google Ads Enhanced Conversions]  para encaminhamento de eventos, combinado com [segredos do Google Oauth 2](../../tags/ui/event-forwarding/secrets.md#google-oauth2), para enviar com segurança os dados do lado do servidor para o [!DNL Google Ads] em tempo real. |

{style="table-layout:auto"}

## Destinos (atualizado em 2 de fevereiro) {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [(Beta) Conexão do Adobe Experience Cloud Audiences](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Use a conexão do [!UICONTROL (Beta) Adobe Experience Cloud Audiences] para compartilhar segmentos da Experience Platform com várias de suas soluções, como Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target e Marketo. |
| [Conexão do Pega Profile](../../destinations/catalog/personalization/pega-profile.md) | Use o [!DNL Pega Profile Connector] na Adobe Experience Platform para criar uma conexão de saída ativa para o seu armazenamento [!DNL Amazon] S3 e exportar dados de perfil periodicamente para arquivos CSV da Adobe Experience Platform em seus próprios buckets S3. No [!DNL Pega Customer Decision Hub], você pode agendar processos para importar esses dados de perfil do armazenamento S3 para atualizar o perfil do [!DNL Pega Customer Decision Hub]. |
| [(Beta) Conexão CRM EU da Trade Desk](../../destinations/catalog/advertising/tradedesk-emails.md) | Com o lançamento da EUID (European Unified ID), você verá agora dois destinos do [!DNL The Trade Desk - CRM] no [catálogo de destinos](/help/destinations/catalog/overview.md). <ul><li> Se seus dados se originarem da UE, use o destino **[!DNL The Trade Desk - CRM (EU)]**.</li><li> Se seus dados se originarem das regiões da Ásia-Pacífico ou América do Norte, use o destino **[!DNL The Trade Desk - CRM (NAMER & APAC)]**. </li></ul> |

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Aprimoramento da política de consentimento de mídia paga para integrações com destinos de transmissão | Um [aprimoramento da aplicação de políticas de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) em [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations) para casos de uso de ativação de mídia paga. Quando os perfis não estão mais qualificados para uma política de consentimento, a Experience Platform agora comunica proativamente sua política de saída para destinos de transmissão. <br> <b>Observação</b>: essa funcionalidade está disponível somente para clientes do **[!UICONTROL Privacy and Security Shield]** e do **[!UICONTROL Healthcare Shield]**. |
| Novas opções de delimitador para conectores de destinos beta de armazenamento na nuvem | Três novas opções de delimitador (dois pontos `:`, barra vertical, ponto e vírgula `;`) agora estão disponíveis para os novos destinos beta de armazenamento na nuvem: [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Zona de destino de dados](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Armazenamento na nuvem do Google](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> Leia sobre as [opções de formatação de arquivo](/help/destinations/ui/batch-destinations-file-formatting-options.md) compatíveis para destinos baseados em arquivo. |
| Novo parâmetro opcional disponível nas configurações de [campos de dados do cliente](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md) no [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: use esse parâmetro quando precisar criar um campo de dados do cliente cujo valor deve ser exclusivo em todos os fluxos de dados de destino configurados pela organização de um usuário. <br> Por exemplo, o campo **[!UICONTROL Alias de integração]** no destino [[!UICONTROL Personalização individual]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) deve ser exclusivo, o que significa que dois fluxos de dados separados para esse destino não podem ter o mesmo valor nesse campo. |

**Correções e aprimoramentos** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Correção ou aprimoramento</b></td>
        <td><b>Descrição</b></td>
    </tr>
    <tr>
        <td>Atualização do comportamento de exportação para destinos baseados em arquivo (PLAT-123316)</td>
        <td>Corrigimos um problema no comportamento dos <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mandatory-attributes">atributos obrigatórios</a> ao exportar arquivos de dados para destinos em lote. <br> Anteriormente, cada registro dos arquivos de saída era verificado para garantir que continham: <ol><li>Um valor não nulo na coluna <code>mandatoryField</code> e</li><li>Um valor não nulo em pelo menos um dos outros campos não obrigatórios.</li></ol> A segunda condição foi removida. Como resultado, você pode estar vendo mais linhas de saída em seus arquivos de dados exportados, como mostrado no exemplo abaixo:<br> <b> Exemplo de comportamento antes da versão de janeiro de 2023 </b> <br> Campo obrigatório: <code>emailAddress</code> <br> <b>Dados de entrada a serem ativados</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>nulo</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>nulo</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Saída de ativação</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Exemplo de comportamento após a versão de janeiro de 2023 </b> <br> <b>Saída de ativação</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>nulo</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>nulo</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>Validação da interface e da API para mapeamentos obrigatórios e mapeamentos duplicados (PLAT-123316)</td>
        <td>A validação agora é aplicada da seguinte maneira na interface e na API ao <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mapping">mapear campos</a> no fluxo de trabalho de ativação de destinos:<ul><li><b>Mapeamentos obrigatórios</b>: se o destino tiver sido configurado pelo desenvolvedor do destino com os mapeamentos obrigatórios (por exemplo, o destino <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html">Google Ad Manager 360</a>), esses mapeamentos precisarão ser adicionados pelo usuário ao ativar dados no destino. </li><li><b>Mapeamentos duplicados</b>: na etapa de mapeamento do fluxo de trabalho de ativação, é possível adicionar valores duplicados nos campos de origem, mas não nos campos de destino. Consulte a tabela abaixo para obter um exemplo de combinações de mapeamento permitidas e proibidas. <br><table><thead><tr><th>Permitido/proibido</th><th>Campo de origem</th><th>Campo de destino</th></tr></thead><tbody><tr><td>Permitido</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>alias2 de email</li></ul></td></tr><tr><td>Proibido</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados inseridos na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Melhorias no nome de exibição da árvore de esquema | Anteriormente, os nomes de campo eram exibidos na interface, mas agora, os nomes de exibição dos campos de esquema na tela do esquema são mais fáceis de ler. |

**Novos componentes de XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Classe | [[!UICONTROL Conversão]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Uma classe para rastrear dados de conversão como conversões de moeda. |
| Grupo de campos | [[!UICONTROL Detalhes da taxa de conversão de moeda]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Um grupo de campos para a classe [!UICONTROL Conversão] captura detalhes adicionais relacionados à conversão de moeda. |
| Grupo de campos | [[!UICONTROL Mapa de resultados da avaliação de políticas de consentimento com metadados]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | Captura detalhes para o resultado da avaliação de várias políticas de consentimento, incluindo informações de metadados sobre as entradas e saídas da política de consentimento. |

**Componentes de XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Tipo de dados | [[!UICONTROL Informações de detalhes de publicidade]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | O campo `ID` foi renomeado para `name`, e o antigo campo `name` agora é `friendlyName`. |
| Tipo de dados | [[!UICONTROL Detalhes da proposta de decisão]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Um campo `selectionStrategy` que captura os detalhes de uma estratégia de seleção foi adicionado. |
| Grupo de campos | [[!UICONTROL Evento de experiência - Interações de proposição]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | O grupo de campos agora é compatível com a classe [!UICONTROL Evento de etapa de jornada]. |
| Tipo de dados | [[!UICONTROL Informações de detalhes do erro]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | O campo `ID` foi renomeado para `name`. |
| Tipo de dados | [[!UICONTROL Informações de mídia]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Uma alteração no padrão da propriedade de segmento do vídeo foi revertida. |
| Tipo de dados | [[!UICONTROL Informações detalhadas de dados de QoE]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Remoção do campo `droppedFrameCount`. |
| Tipo de dados | [[!UICONTROL Informações de detalhes da sessão]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | O campo `isAuthorized` foi renomeado para `authorized` e teve seu `type`, que era um booleano, atualizado para uma string. |
| Tipo de dados | [[!UICONTROL Envio]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Vários novos campos foram adicionados: `shipDate`, `trackingNumber`, e `trackingURL`. |
| Grupo de campos | [[!UICONTROL Campos de entidade do AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Vários novos campos foram adicionados: `journeyNodeID`, `journeyNodeName`, e `journeyModeType`. |
| Grupo de campos | [[!UICONTROL Evento de experiência do consumidor]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | O grupo de campos agora também é compatível com a classe [!UICONTROL Métricas de resumo]. |
| Grupo de campos | [[!UICONTROL Acionadores do produto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | O campo `productTriggers` agora está aninhado em um objeto `weather`. |
| Grupo de campos | [[!UICONTROL Acionadores relativos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | O campo `relativeTriggers` agora está aninhado em um objeto `weather`. |
| Grupo de campos | [[!UICONTROL Acionadores graves]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | O campo `severeTriggers` agora está aninhado em um objeto `weather`. |
| Grupo de campos | [[!UICONTROL Acionadores meteorológicos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | O campo `weatherTriggers` agora está aninhado em um objeto `weather`. |
| Grupo de campos | [[!UICONTROL Contas de negócios relacionadas ao XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | O grupo de campos agora está estável. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM na Platform, consulte a [Visão geral do sistema de XDM](../../xdm/home.md).

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, é possível ter uma visão integral de cada cliente ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Próxima descontinuação** {#deprecation}

Para remover a redundância no ciclo de vida de associação do segmento, o status `Existing` será descontinuado do [mapa de associação de segmento](../../xdm/field-groups/profile/segmentation.md) no final de março de 2023. Um anúncio posterior incluirá a data exata da descontinuação.

Após a descontinuação, os perfis qualificados em um segmento serão representados como `Realized` e os perfis desqualificados continuarão a ser representados como `Exited`. Isso trará paridade dos destinos baseados em arquivo com os status de segmento `Active` e `Expired`.

Essa alteração pode afetar você se estiver usando [destinos corporativos](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Hubs de Eventos do Azure, API HTTP) e possuir processos downstream automatizados em vigor, com base no status `Existing`. Revise suas integrações downstream se esse for o seu caso. Caso se interesse em identificar perfis recém-qualificados além de um determinado período, considere usar uma combinação dos status `Realized` e `lastQualificationTime` no mapa de associação do segmento. Para obter mais informações, entre em contato com o representante da Adobe.

Para saber mais sobre o Perfil de cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com dados de perfil, comece lendo a [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Importação de valor em massa no Construtor de segmentos | O Construtor de segmentos agora é compatível com à importação de vários valores, seja fazendo upload de um arquivo CSV ou TSV, ou inserindo manualmente valores separados por vírgula. Mais informações podem ser encontradas no [Guia do Construtor de segmentos](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| Expiração de associação de público-alvo externo | Por padrão, as associações de público-alvo externo são mantidas por 30 dias. Para mantê-las por mais tempo, use o campo `validUntil` durante a assimilação de dados do público-alvo. |
| Expiração da associação de segmento gerada pela Platform | Qualquer associação de segmento que esteja no estado `Exited` por mais de 30 dias, com base no campo `lastQualificationTime`, estará sujeita a exclusão. |

{style="table-layout:auto"}

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## Origens {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da Platform. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| Permitir acesso do usuário a subpastas de origens de armazenamento na nuvem | Agora é possível definir o acesso a uma subpasta específica da origem de armazenamento na nuvem ao criar uma nova conta. Depois de criada, os usuários ou usuárias só poderão acessar os dados da subpasta permitida. Esse recurso está disponível para as seguintes origens de armazenamento na nuvem: [Azure Blob Storage](../../sources/connectors/cloud-storage/blob.md), [Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md), e [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilidade beta do [!DNL SugarCRM] | As origens do [!DNL SugarCRM] agora estão disponíveis na versão beta. Use as origens [!DNL SugarCRM Accounts & Contacts] e [!DNL SugarCRM Events] para trazer dados da sua conta [!DNL SugarCRM] para a Experience Platform. Para obter mais informações, leia a [[!DNL SugarCRM] visão geral](../../sources/connectors/crm/sugarcrm.md). |
