---
keywords: Experience Platform;ativação;solução de problemas;medidas de proteção;diretrizes;limite
title: Medidas de proteção padrão para ativação de dados
solution: Experience Platform
product: experience platform
type: Documentation
description: Saiba mais sobre o uso padrão da ativação de dados e os limites de taxa.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 0b607decfa687f89c74fb81055ac2bf4cc54d59b
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 1%

---

# Medidas de proteção para ativação de dados

>[!IMPORTANT]
>
>Verifique os direitos de licença em seu Pedido de Venda e a [Descrição do Produto](https://helpx.adobe.com/legal/product-descriptions.html?lang=pt-BR) correspondente sobre os limites de uso reais, além desta página de medidas de proteção.

Esta página fornece limites de uso e taxa padrão em relação ao comportamento de ativação. Ao revisar as medidas de proteção a seguir, presume-se que você [esteja conectado corretamente aos destinos](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* A maioria dos clientes não excede esses limites padrão. Se quiser saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.
>* Os limites descritos neste documento estão sendo constantemente melhorados. Verifique regularmente se há atualizações.
>* Dependendo das limitações individuais de downstream, alguns destinos podem ter medidas de proteção mais rigorosas do que as documentadas nesta página. Verifique também a página do [catálogo](/help/destinations/catalog/overview.md) do destino ao qual você está conectando e ativando dados.

## Tipos de grade de proteção {#limit-types}

Há dois tipos de limites padrão neste documento:

| Tipo de grade de proteção | Descrição |
|----------|---------|
| **Proteção de desempenho (limite flexível)** | As medidas de proteção de desempenho são limites de uso relacionados ao escopo dos seus casos de uso. Ao exceder as medidas de proteção de desempenho, você pode enfrentar degradação e latência do desempenho. A Adobe não é responsável por essa degradação de desempenho. Os clientes que excederem consistentemente uma garantia de desempenho podem optar por licenciar capacidade adicional para evitar a degradação do desempenho. |
| **Medidas de proteção aplicadas pelo sistema (Limite rígido)** | As medidas de proteção aplicadas pelo sistema são aplicadas pela interface do usuário ou API do Real-Time CDP. Esses são limites que você não pode exceder, pois a interface do usuário e a API o bloquearão de fazer isso ou retornarão um erro. |

{style="table-layout:auto"}


## Limites de ativação {#activation-limits}

As medidas de proteção a seguir fornecem limites recomendados ao ativar dados do Perfil do cliente em tempo real para destinos.

### Medidas de proteção gerais de ativação {#general-activation-guardrails}

As medidas de proteção abaixo geralmente se aplicam à ativação por meio de [todos os tipos de destino](/help/destinations/destination-types.md#destination-types).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número máximo de públicos-alvo para um único destino | 250 | Proteção de desempenho | A recomendação é mapear um máximo de 250 públicos-alvo para um único destino em um fluxo de dados. <br><br> Se precisar ativar mais de 250 públicos-alvo para um destino, você pode: <ul><li> Desmapeie os públicos-alvo que você não deseja mais ativar ou</li><li>Crie um novo fluxo de dados para o destino desejado e mapeie os públicos para esse novo fluxo de dados.</li></ul> <br> Observe que, no caso de alguns destinos, você pode estar limitado a menos de 250 públicos-alvo mapeados para o destino. Esses destinos são chamados mais abaixo na página, em suas respectivas seções. |
| Número máximo de atributos mapeados para um destino | 50  | Proteção de desempenho | No caso de vários destinos e tipos de destino, é possível selecionar atributos de perfil e identidades para mapear para exportação. Para um desempenho ideal, no máximo 50 atributos devem ser mapeados em um fluxo de dados para um destino. |
| Número máximo de destinos | 100 | Proteção imposta pelo sistema | É possível criar um máximo de 100 destinos aos quais você pode conectar e ativar dados, *por sandbox*. [Os destinos de personalização do Edge (Personalização personalizada)](#edge-destinations-activation) podem representar, no máximo, 10 dos 100 destinos recomendados. |
| Tipo de dados ativados para destinos | Dados de perfil, incluindo identidades e mapa de identidade | Proteção imposta pelo sistema | Atualmente, só é possível exportar *atributos de registro de perfil* para destinos. No momento, não há suporte para atributos XDM que descrevem dados de evento para exportação. |
| Tipo de dados ativados para destinos — suporte a atributos de array e mapa | Parcialmente disponível | Proteção imposta pelo sistema | Você pode exportar atributos de matriz para [destinos baseados em arquivo](/help/destinations/destination-types.md#file-based). [Leia mais](/help/destinations/ui/export-arrays-maps-objects.md) sobre a funcionalidade. |

{style="table-layout:auto"}

### Ativação de transmissão {#streaming-activation}

As medidas de proteção abaixo se aplicam à ativação por meio de [destinos de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número de ativações (mensagens HTTP com exportações de perfil) por segundo | N/D | - | No momento, não há limite para o número de mensagens por segundo enviadas do Experience Platform para os endpoints da API de destinos do parceiro. <br> Quaisquer limites ou latências são ditados pelo ponto de extremidade onde a Experience Platform está enviando dados. Verifique também a página do [catálogo](/help/destinations/catalog/overview.md) do destino ao qual você está conectando e ativando dados. |

{style="table-layout:auto"}

### Ativação em lote (baseada em arquivo) {#batch-file-based-activation}

As medidas de proteção abaixo se aplicam à ativação por meio de [destinos em lote (baseados em arquivo)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Frequência de ativação | Uma exportação completa diária ou exportações incrementais mais frequentes a cada 3, 6, 8 ou 12 horas. | Proteção imposta pelo sistema | Leia as seções de documentação de [exportar arquivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [exportar arquivos incrementais](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) para obter mais informações sobre os incrementos de frequência para exportações em lote. |
| Número máximo de públicos que podem ser exportados em uma determinada hora | 100 | Proteção de desempenho | A recomendação é adicionar no máximo 100 públicos-alvo aos fluxos de dados de destino em lote. |
| Número máximo de linhas (registros) por arquivo a serem ativados | 5 milhões | Proteção imposta pelo sistema | O Adobe Experience Platform divide automaticamente os arquivos exportados em 5 milhões de registros (linhas) por arquivo. Cada linha representa um perfil. Nomes de arquivos divididos são anexados com um número que indica que o arquivo é parte de uma exportação maior, como: `filename.csv`, `filename_2.csv`, `filename_3.csv`. Para obter mais informações, leia a [seção de agendamento](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) do tutorial ativar destinos em lote. |
| Número máximo de públicos-alvo de upload personalizados para ativar em um fluxo de dados | 10 | Proteção imposta pelo sistema | Ao ativar [públicos-alvo personalizados](/help/segmentation/ui/audience-portal.md#import-audience) para destinos baseados em arquivo em lote, há um limite de 10 desses públicos-alvo que você pode ativar em um fluxo de dados. Leia mais sobre o fluxo de trabalho para [ativar públicos-alvo de carregamento personalizado para destinos baseados em arquivo em lote](/help/destinations/ui/activate-batch-profile-destinations.md#select-audiences). |

{style="table-layout:auto"}

### Ativação ad hoc {#ad-hoc-activation}

As medidas de proteção abaixo se aplicam ao método [ativação ad hoc](/help/destinations/api/ad-hoc-activation-api.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Públicos ativados por trabalho de ativação ad-hoc | 80 | Proteção imposta pelo sistema | Atualmente, cada trabalho de ativação ad-hoc pode ativar até 80 públicos-alvo. Tentar ativar mais de 80 públicos-alvo por trabalho causará falha no trabalho. Esse comportamento está sujeito a alterações em versões futuras. |
| Trabalhos de ativação ad-hoc simultâneos por público-alvo | 1 | Proteção imposta pelo sistema | Não execute mais de um trabalho de ativação ad-hoc simultâneo por público-alvo. |

{style="table-layout:auto"}

### Ativação de destinos de personalização do Edge {#edge-destinations-activation}

As medidas de proteção abaixo se aplicam à ativação por meio de [destinos de personalização de borda](/help/destinations/destination-types.md#advanced-enterprise-destinations).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número máximo de [Destinos de personalização personalizada](/help/destinations/catalog/personalization/custom-personalization.md) | 10 | Proteção de desempenho | Você pode configurar fluxos de dados para 10 destinos de personalização personalizados por sandbox. |
| Número máximo de atributos mapeados para um destino de personalização por sandbox | 30 | Proteção de desempenho | No máximo 30 atributos podem ser mapeados em um fluxo de dados para um destino de personalização, por sandbox. |
| Número máximo de públicos mapeados para um único destino do [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) | 50  | Proteção de desempenho | É possível ativar no máximo 50 públicos-alvo em um fluxo de ativação para um único destino do Adobe Target. |

{style="table-layout:auto"}

### Exportações de conjunto de dados {#dataset-exports}

Atualmente, há suporte para exportações de conjunto de dados em um **[!UICONTROL First Full and then Incremental]** [padrão](/help/destinations/ui/export-datasets.md#scheduling). As medidas de proteção descritas nesta seção *se aplicam à primeira exportação completa* que ocorre após a configuração de um fluxo de trabalho de exportação do conjunto de dados.

<!--

| Guardrail | Limit | Limit Type | Description |
| --- | --- | --- | --- |
| Size of exported datasets | 5 billion records | Soft | The limit described here for dataset exports is a *soft guardrail*. For example, while the user interface will not block you from exporting datasets larger than 5 billion records, the behavior is unpredictable and exports might either fail or have very long export latency. |

{style="table-layout:auto"}

-->

#### Tipos de conjunto de dados {#dataset-types}

As medidas de proteção de exportação do conjunto de dados se aplicam a dois tipos de conjuntos de dados exportados do Experience Platform, conforme descrito abaixo:

**Conjuntos de dados com base no esquema XDM Experience Events e conjuntos de dados com base em qualquer outro esquema**

No caso de conjuntos de dados baseados no esquema XDM Experience Events, o esquema do conjunto de dados inclui uma coluna de carimbo de data e hora de nível superior. Os dados são assimilados somente de forma anexada. No caso de conjuntos de dados baseados em qualquer outro esquema, o esquema do conjunto de dados pode incluir uma coluna de carimbo de data e hora e os dados são assimilados de forma ascendente.

A proteção simples abaixo se aplica a todos os conjuntos de dados exportados do Experience Platform. Revise também as medidas de proteção rígidas mais abaixo, específicas para diferentes conjuntos de dados e tipos de compactação.

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Tamanho dos conjuntos de dados exportados | 5 bilhões de registros | Proteção de desempenho | O limite descrito aqui para exportações de conjunto de dados é uma *proteção flexível*. Por exemplo, embora a interface do usuário não impeça a exportação de conjuntos de dados maiores que 5 bilhões de registros, o comportamento é imprevisível e as exportações podem falhar ou ter uma latência de exportação muito longa. |

{style="table-layout:auto"}

#### Proteções para exportações programadas de conjunto de dados

Para exportações agendadas ou recorrentes de conjunto de dados, as medidas de proteção abaixo são idênticas para os dois formatos do arquivo exportado (JSON ou parquet) e são agrupadas por tipo de conjunto de dados.

>[!WARNING]
>
>As exportações para arquivos JSON são suportadas somente em um modo compactado.

| Tipo de conjunto de dados | Grade de Proteção | Tipo de grade de proteção | Descrição |
|---------|----------|---------|-------|
| Conjuntos de dados com base no **esquema de Eventos de experiência XDM** | Últimos 365 dias de dados | Proteção imposta pelo sistema | Os dados do último ano civil são exportados. |
| Conjuntos de dados baseados em **qualquer esquema, exceto o esquema XDM Experience Events** | Dez bilhões de registros em todos os arquivos exportados em um fluxo de dados | Proteção imposta pelo sistema | A contagem de registros do conjunto de dados deve ser inferior a dez bilhões para arquivos JSON ou parquet compactados e um milhão para arquivos parquet não compactados, caso contrário, a exportação falhará. Reduza o tamanho do conjunto de dados que você está tentando exportar se ele for maior que o limite permitido. |

{style="table-layout:auto"}

<!--

#### Ad-hoc dataset exports

Exporting datasets in an-hoc manner is currently supported via API only. For ad-hoc dataset exports, you must use the backfill parameter in the API to limit the timeframe of exported data. 

The guardrails below are the same whether you are exporting parquet of JSON files ad-hoc. 

**Parquet and JSON output**

|Dataset type | Backfill parameter provided | Guardrail | Guardrail type | Description |
|---------|---------|-----------|-----------|------------|
| Datasets based on the **XDM Experience Events schema** |  <p><ul><li>Both start and end date provided in `backfill` parameter in API call</li><li>Incomplete `backfill` parameter provided in API call</li></ul></p> | <p><ul><li>Last 30 days</li><li>Last 365 days</li></ul></p> | Hard | <p><ul><li>The export fails if the `startDate - endDate` interval is over 30 days</li><li>Either the `startDate` or `endDate` are missing or  incorrectly formatted in the API call. Expected format: `yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`</li></ul></p> |
| Datasets based on the **XDM Individual Profile schema** |  - | Ten billion records across all files exported in a dataflow | Hard | The record count of the dataset must be less than ten billion for compressed JSON or parquet files and one million for uncompressed parquet files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold. |

{style="table-layout:auto"}

-->

Leia mais sobre [exportação de conjuntos de dados](/help/destinations/ui/export-datasets.md).


### Medidas de proteção do Destination SDK {#destination-sdk-guardrails}

O [Destination SDK](/help/destinations/destination-sdk/overview.md) é um conjunto de APIs de configuração que permitem configurar padrões de integração de destino para que o Experience Platform forneça dados de público-alvo e perfil para o seu ponto de extremidade, com base nos formatos de dados e autenticação de sua escolha. As medidas de proteção abaixo se aplicam aos destinos configurados por você com o Destination SDK.

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número máximo de [destinos personalizados privados](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Proteção de desempenho | Você pode criar no máximo 5 destinos personalizados de streaming ou lote privados usando o Destination SDK. Entre em contato com um representante de atendimento personalizado se precisar criar mais de 5 desses destinos. |
| Política de exportação de perfil para o Destination SDK | <ul><li>`maxBatchAgeInSecs` (mínimo 301 e máximo 3.600)</li><li>`maxNumEventsInBatch` (mínimo 1.000 e máximo 10.000)</li></ul> | Proteção imposta pelo sistema | Ao usar a opção [agregação configurável](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) para seu destino, lembre-se dos valores mínimo e máximo que determinam a frequência com que as mensagens HTTP são enviadas para seu destino baseado em API e quantos perfis as mensagens devem incluir. |
| Tempo de vida do token OAuth 2 para Destination SDK | Mínimo de 24 horas recomendado | Proteção de desempenho | Para destinos que usam a [autorização OAuth 2](/help/destinations/destination-sdk/functionality/destination-configuration/oauth2-authorization.md), a Adobe recomenda definir os valores de vida útil do token de acesso para um mínimo de 24 horas. As conexões com tokens com duração inferior a 1 hora resultarão no descarte de perfis durante a ativação. |

{style="table-layout:auto"}

### Política de limitação de destino e de repetição {#destination-throttling-and-retry-policy}

Detalhes sobre limites ou limitações de limitação para determinados destinos. Esta seção também fornece informações sobre a política de novas tentativas para destinos.

| Tipo de destino | Descrição |
| --- | --- |
| Destinos empresariais (API HTTP, Amazon Kinesis, Azure EventHubs) | Em 95% das vezes, o Experience Platform tenta oferecer uma latência de taxa de transferência de menos de 10 minutos para mensagens enviadas com êxito, com uma taxa de menos de 10 mil solicitações por segundo para cada fluxo de dados a um destino corporativo. <br> Em caso de falha nas solicitações para o destino da sua empresa, o Experience Platform armazena as solicitações com falha e tenta enviar novamente as solicitações para o seu ponto de extremidade. |

{style="table-layout:auto"}

## Próximas etapas

Consulte a documentação a seguir para obter mais informações sobre outras medidas de proteção dos serviços da Experience Platform, informações de latência de ponta a ponta e informações de licenciamento dos documentos Descrição do produto da Real-Time CDP:

* [Medidas de proteção do Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagramas de latência de ponta a ponta](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) para vários serviços da Experience Platform.
* [Real-Time Customer Data Platform (B2C Edition - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
