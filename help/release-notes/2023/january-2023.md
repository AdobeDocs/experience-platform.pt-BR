---
title: Notas de versão da Adobe Experience Platform de janeiro de 2023
description: As notas de versão de janeiro de 2023 para o Adobe Experience Platform.
source-git-commit: 6388c72aa0be8f5f91efaaa6a0edd22f3eb99de8
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

## Serviços de inteligência artificial/aprendizado de máquina {#ai-ml}

Os serviços de inteligência artificial e aprendizado de máquina capacitam os analistas e profissionais de marketing a aproveitar o potencial da IA/ML em casos de uso de experiência do cliente. Isso permite que os analistas de marketing definam previsões, sem a necessidade de conhecimento especializado em ciência de dados, específico para as necessidades de uma empresa usando configurações de nível empresarial.

### IA de atribuição

O Attribution AI é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Ele pode ser usado pelos comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em várias jornadas de clientes.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Preparo para a HIPAA | Os clientes do Healthcare Shield agora podem receber, usar, manter ou transmitir informações de saúde protegidas no Attribution AI e em determinados outros aplicativos baseados em Experience Platform. O Healthcare Shield destina-se a clientes de assistência médica que são uma entidade coberta ou um associado comercial de acordo com a HIPAA. Para obter mais informações, leia a documentação em [Produtos e serviços HIPAA e Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |
| Editar colunas adicionais do conjunto de dados de pontuação | Agora é possível adicionar ou remover mais colunas de conjunto de dados de pontuação (colunas de relatórios) ao editar modelos existentes. Isso estende a flexibilidade das pontuações de atribuição para fornecer insights para dimensões adicionais depois que um modelo já foi criado. Consulte a [Guia da interface de atribuição](../../intelligent-services/attribution-ai/user-guide.md) para saber mais. |

{style="table-layout:auto"}

Consulte a [Serviços de IA/ML](../../intelligent-services/attribution-ai/overview.md) visão geral para obter mais informações.

### IA do cliente

A IA do cliente para o Real-time Customer Data Platform é usada para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala. Isso é feito sem precisar transformar as necessidades de negócios em um problema de aprendizado de máquina, escolher um algoritmo, treinar ou implantar.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Preparo para a HIPAA | Os clientes do Healthcare Shield agora podem receber, usar, manter ou transmitir informações de saúde protegidas na IA do cliente para o Real-time Customer Data Platform e outros aplicativos baseados em Experience Platform. O Healthcare Shield destina-se a clientes de assistência médica que são uma entidade coberta ou um associado comercial de acordo com a HIPAA. Para obter mais informações, consulte a documentação em [Produtos e serviços HIPAA e Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |

{style="table-layout:auto"}

Consulte a [Serviços de IA/ML](../../intelligent-services/customer-ai/overview.md) visão geral para obter mais informações.

## Assurance {#assurance}

O Adobe Assurance permite inspecionar, testar, simular e validar como você coleta dados ou veicula experiências em seu aplicativo móvel.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Editor de validação | Foram adicionados novos aprimoramentos ao editor de validação. Esses aprimoramentos incluem colunas de validação, novas ferramentas de criação de código e exibições aprimoradas. |

{style="table-layout:auto"}

Para obter mais informações sobre o Assurance, leia o [Documentação de garantia](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente do lado do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Nova tela inicial | A página inicial da interface da Coleção de dados foi atualizada para incluir informações de integração úteis e links para simplificar a produtividade. Isso inclui:<ol><li>Documentação e fluxos de trabalho recomendados para começar</li><li>Propriedades, regras e elementos de dados recentes</li><li>Extensões populares</li><li>Novas atualizações de extensão com um recurso de instalação rápida</li></ol> |
| Enviar dados para [!DNL Google Ads] usar o encaminhamento de eventos | Agora você pode usar o [[!DNL Google Ads Enhanced Conversions] Extensão da API](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) para encaminhamento de eventos, combinado com [Segredos do Google Oauth 2](../../tags/ui/event-forwarding/secrets.md#google-oauth2), para enviar com segurança os dados do lado do servidor para o [!DNL Google Ads] em tempo real. |

{style="table-layout:auto"}

## Destinos (atualizado em 2 de fevereiro) {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, publicidade direcionada e muitos outros casos de uso.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [(Beta) Conexão do Adobe Experience Cloud Audiences](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Use o [!UICONTROL (Beta) Públicos-alvo da Adobe Experience Cloud] conexão para compartilhar segmentos do Experience Platform para várias soluções de Experience Platform, como Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target ou Marketo. |
| [Conexão do Perfil Pega](../../destinations/catalog/personalization/pega-profile.md) | Use o [!DNL Pega Profile Connector] no Adobe Experience Platform para criar uma conexão de saída ativa com o seu [!DNL Amazon] Armazenamento S3 para exportar periodicamente dados de perfil para arquivos CSV da Adobe Experience Platform em seus próprios buckets S3. Entrada [!DNL Pega Customer Decision Hub], você pode agendar trabalhos de dados para importar esses dados de perfil do armazenamento S3 para atualizar o [!DNL Pega Customer Decision Hub] perfil. |
| [(Beta) A conexão CRM EU da Trade Desk](../../destinations/catalog/advertising/tradedesk-emails.md) | Com o lançamento da EUID (European Unified ID), você verá agora duas [!DNL The Trade Desk - CRM] destinos na [catálogo de destinos](/help/destinations/catalog/overview.md). <ul><li> Se você obtiver dados na UE, use o **[!DNL The Trade Desk - CRM (EU)]** destino.</li><li> Se você originar dados nas regiões APAC ou NAMER, use o **[!DNL The Trade Desk - CRM (NAMER & APAC)]** destino. </li></ul> |

**Funcionalidade nova ou atualizada** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| Aprimoramento da Política de consentimento de mídia paga para integrações com destinos de transmissão | Um [aprimoramento da aplicação de políticas de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) em [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations) para casos de uso de ativação de mídia paga. Quando os perfis não estão mais qualificados para uma política de consentimento, o Experience Platform agora comunica proativamente sua saída de política para destinos de streaming. <br> <b>Nota</b>: essa funcionalidade está disponível somente para clientes do **[!UICONTROL Escudo de Proteção e Privacidade]** e as de **[!UICONTROL Healthcare Shield]**. |
| Novas opções de delimitador para conectores beta de destino de armazenamento na nuvem | Três novas opções de delimitador (dois pontos `:`, Tubulação, Ponto e vírgula `;`) agora estão disponíveis para os novos destinos de armazenamento na nuvem beta - [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Armazenamento do Azure Data Lake Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Zona de aterrissagem de dados](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Armazenamento em nuvem do Google](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> Leia sobre o compatível [opções de formatação de arquivo](/help/destinations/ui/batch-destinations-file-formatting-options.md) para destinos baseados em arquivo. |
| Novo parâmetro opcional disponível em [campos de dados do cliente](/help/destinations/destination-sdk/destination-configuration.md#customer-data-fields) configurações em [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: use esse parâmetro quando precisar criar um campo de dados do cliente cujo valor deve ser exclusivo em todos os fluxos de dados de destino configurados pela organização de um usuário. <br> Por exemplo, a variável **[!UICONTROL Alias de integração]** no campo [[!UICONTROL Personalização personalizada]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) o destino deve ser exclusivo, o que significa que dois fluxos de dados separados para esse destino não podem ter o mesmo valor para esse campo. |

**Correções e aprimoramentos** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Correção ou aprimoramento</b></td>
        <td><b>Descrição</b></td>
    </tr>
    <tr>
        <td>Atualização do comportamento de exportação para destinos baseados em arquivo (PLAT-123316)</td>
        <td>Corrigimos um problema no comportamento do <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">atributos obrigatórios</a> ao exportar arquivos de dados para destinos em lote. <br> Anteriormente, cada registro nos arquivos de saída era verificado para conter ambos: <ol><li>Um valor não nulo de <code>mandatoryField</code> coluna e</li><li>Um valor não nulo em pelo menos um dos outros campos não obrigatórios.</li></ol> A segunda condição foi removida. Como resultado, você pode estar vendo mais linhas de saída em seus arquivos de dados exportados, como mostrado no exemplo abaixo:<br> <b> Exemplo de comportamento antes da versão de janeiro de 2023 </b> <br> Campo obrigatório: <code>emailAddress</code> <br> <b>Dados de entrada a serem ativados</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>nulo</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>nulo</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Saída de ativação</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Exemplo de comportamento após a versão de janeiro de 2023 </b> <br> <b>Saída de ativação</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>nulo</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>nulo</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>Validação da interface do usuário e da API para mapeamentos necessários e mapeamentos duplicados (PLAT-123316)</td>
        <td>A validação agora é imposta da seguinte maneira na interface e na API quando <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mapping">mapeamento de campos</a> no workflow ativar destinos:<ul><li><b>Mapeamentos necessários</b>: se o destino tiver sido configurado pelo desenvolvedor de destino com os mapeamentos necessários (por exemplo, o <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html?lang=en">Google Ad Manager 360</a> destino), esses mapeamentos necessários precisarão ser adicionados pelo usuário ao ativar dados no destino. </li><li><b>Duplicar mapeamentos</b>: na etapa de mapeamento do fluxo de trabalho de ativação, é possível adicionar valores duplicados nos campos de origem, mas não nos campos de destino. Consulte a tabela abaixo para obter um exemplo de combinações de mapeamento permitidas e proibidas. <br><table><thead><tr><th>Permitido/proibido</th><th>Campo de origem</th><th>Campo de destino</th></tr></thead><tbody><tr><td>Permitido</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>alias2 de email</li></ul></td></tr><tr><td>Proibido</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

Para obter informações mais gerais sobre destinos, consulte o [visão geral dos destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos das ações do cliente, definir públicos do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Melhorias no nome de exibição da árvore de esquema | Anteriormente, os nomes de campo eram exibidos na interface do usuário, mas agora, os nomes de exibição dos campos de esquema na tela do esquema são mais fáceis de ler. |

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Classe | [[!UICONTROL Conversão]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Uma classe para rastrear dados de conversão como conversões de moeda. |
| Grupo de campos | [[!UICONTROL Detalhes do Índice de Conversão Monetária]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Um grupo de campos para o [!UICONTROL Conversão] classe, captura de detalhes adicionais relacionados à conversão de moeda. |
| Grupo de campos | [[!UICONTROL Mapa de resultados da avaliação de políticas de consentimento com metadados]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | Captura detalhes para o resultado da avaliação de várias políticas de consentimento, incluindo informações de metadados sobre as entradas da política de consentimento e existe. |

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Tipo de dados | [[!UICONTROL Informações de detalhes de publicidade]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | A variável `ID` O campo foi renomeado para `name`, e a anterior `name` o campo agora é `friendlyName`. |
| Tipo de dados | [[!UICONTROL Detalhes da apresentação de decisão]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Adição de um `selectionStrategy` campo que captura os detalhes de uma estratégia de seleção. |
| Grupo de campos | [[!UICONTROL Evento de experiência - Interações de apresentação]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | O grupo de campos agora é compatível com o [!UICONTROL Jornada evento de etapa] classe. |
| Tipo de dados | [[!UICONTROL Informações de detalhes do erro]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | A variável `ID` O campo foi renomeado para `name`. |
| Tipo de dados | [[!UICONTROL Informações da mídia]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Reversão de uma alteração no padrão para a propriedade do segmento do vídeo. |
| Tipo de dados | [[!UICONTROL Informações detalhadas de Dados de Qoe]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Remoção da `droppedFrameCount` campo. |
| Tipo de dados | [[!UICONTROL Informações de detalhes da sessão]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | A variável foi renomeada `isAuthorized` campo para `authorized`e atualizou seu `type` a uma string quando ela era anteriormente booleana. |
| Tipo de dados | [[!UICONTROL Envio]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Adição de vários novos campos: `shipDate`, `trackingNumber`, e `trackingURL`. |
| Grupo de campos | [[!UICONTROL Campos de entidade do AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Adição de vários novos campos: `journeyNodeID`, `journeyNodeName`, e `journeyModeType`. |
| Grupo de campos | [[!UICONTROL Evento de experiência do consumidor]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | O grupo de campos agora também é compatível com o [!UICONTROL Métricas de resumo] classe. |
| Grupo de campos | [[!UICONTROL Acionadores do produto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | A variável `productTriggers` O campo agora está aninhado em um `weather` objeto. |
| Grupo de campos | [[!UICONTROL Acionadores relativos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | A variável `relativeTriggers` O campo agora está aninhado em um `weather` objeto. |
| Grupo de campos | [[!UICONTROL Acionadores graves]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | A variável `severeTriggers` O campo agora está aninhado em um `weather` objeto. |
| Grupo de campos | [[!UICONTROL Disparadores meteorológicos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | A variável `weatherTriggers` O campo agora está aninhado em um `weather` objeto. |
| Grupo de campos | [[!UICONTROL Contas de negócios relacionadas ao XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | O grupo de campos agora está estável. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM na Platform, consulte a [Visão geral do sistema XDM](../../xdm/home.md).

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde e quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, você pode ter uma visualização integral de cada cliente individual, combinando dados de vários canais, inclusive dados online, offline, de CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Próxima descontinuação** {#deprecation}

Para remover a redundância no ciclo de vida de associação do segmento, a variável `Existing` O status será descontinuado do [mapa de associação de segmento](../../xdm/field-groups/profile/segmentation.md) no final de março de 2023. Um anúncio de acompanhamento incluirá a data exata de desativação.

Após a descontinuação, os perfis qualificados em um segmento serão representados como `Realized` e os perfis desqualificados continuarão a ser representados como `Exited`. Isso trará paridade com destinos baseados em arquivos com `Active` e `Expired` status do segmento.

Essa alteração pode afetar você se estiver usando [destinos corporativos](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Hubs de Eventos do Azure, API HTTP) e têm processos downstream automatizados em vigor, com base na `Existing` status. Revise suas integrações downstream se esse for o seu caso. Se você estiver interessado em identificar perfis recém-qualificados além de um determinado período, considere usar uma combinação das opções `Realized` status e o `lastQualificationTime` no mapa de associação do segmento. Para obter mais informações, entre em contato com o representante da Adobe.

Para saber mais sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com dados de perfil, comece lendo o [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## Serviço de segmentação {#segmentation}

[!DNL Segmentation Service] O define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo comercializável de pessoas na sua base de clientes. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Importação de valor em massa no Construtor de segmentos | O Construtor de segmentos agora oferece suporte à importação de vários valores, fazendo upload de um arquivo CSV ou TSV ou inserindo manualmente valores separados por vírgula. Mais informações podem ser encontradas na [Guia do Construtor de segmentos](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| Expiração de associação de público externo | Por padrão, as associações de público-alvo externo são retidas por 30 dias. Para mantê-los por mais tempo, use o `validUntil` durante a assimilação de dados de público-alvo. |
| Expiração de associação de segmento gerado pela plataforma | Qualquer associação de segmento que esteja no `Exited` por mais de 30 dias, com base na `lastQualificationTime` campo estará sujeito a exclusão. |

{style="table-layout:auto"}

Para obter mais informações sobre [!DNL Segmentation Service], consulte o [Visão geral da segmentação](../../segmentation/home.md).

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| Permitir acesso do usuário a subpastas de fontes de armazenamento na nuvem | Agora é possível definir o acesso a uma subpasta específica da sua fonte de armazenamento em nuvem ao criar uma nova conta. Depois de criado, os usuários só poderão acessar os dados da subpasta permitida. Esse recurso está disponível para as seguintes fontes de armazenamento na nuvem: [Armazenamento Azure Blob](../../sources/connectors/cloud-storage/blob.md), [Armazenamento em nuvem Google](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md), e [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilidade beta de [!DNL SugarCRM] | [!DNL SugarCRM] as fontes agora estão disponíveis na versão beta. Use o [!DNL SugarCRM Accounts & Contacts] e a variável [!DNL SugarCRM Events] fontes para trazer dados de seu [!DNL SugarCRM] conta para Experience Platform. Para obter mais informações, leia a [[!DNL SugarCRM] visão geral](../../sources/connectors/crm/sugarcrm.md). |