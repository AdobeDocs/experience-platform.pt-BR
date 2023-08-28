---
keywords: Experience Platform;ativação;solução de problemas;medidas de proteção;diretrizes;limite
title: Medidas de proteção padrão para dados de ativação
solution: Experience Platform
product: experience platform
type: Documentation
description: Saiba mais sobre o uso padrão da ativação de dados e os limites de taxa.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 0835021523a7eb1642a6dbcb24334eac535aaa6d
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 2%

---

# Medidas de proteção para dados de ativação

Esta página fornece limites de uso e taxa padrão em relação ao comportamento de ativação. Ao revisar as medidas de proteção a seguir, presume-se que você tenha [conectado aos destinos](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* A maioria dos clientes não excede esses limites padrão. Se quiser saber mais sobre limites personalizados, entre em contato com o representante do Atendimento ao cliente.
>* Os limites descritos neste documento estão sendo constantemente melhorados. Verifique regularmente se há atualizações.
>* Dependendo das limitações individuais de downstream, alguns destinos podem ter medidas de proteção mais rigorosas do que as documentadas nesta página. Verifique também o [catálogo](/help/destinations/catalog/overview.md) página do destino ao qual você está conectando e ativando dados.

## Tipos de limite {#limit-types}

Há dois tipos de limites padrão neste documento:

* **Limite flexível:** É possível ir além de um limite flexível, no entanto, os limites flexíveis fornecem uma diretriz recomendada para o desempenho do sistema.
* **Limite rígido:** Um limite rígido fornece um máximo absoluto. A interface do usuário ou a API do Experience Platform não permite ir além desse limite, ou um erro será retornado se você ir além desse limite.


## Limites de ativação {#activation-limits}

As medidas de proteção a seguir fornecem limites recomendados ao ativar dados do Perfil do cliente em tempo real para destinos.

### Medidas de proteção gerais de ativação {#general-activation-guardrails}

As medidas de proteção abaixo geralmente se aplicam à ativação por meio de [todos os tipos de destino](/help/destinations/destination-types.md#destination-types).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número máximo de públicos-alvo para um único destino | 250 | Suave | A recomendação é mapear um máximo de 250 públicos-alvo para um único destino em um fluxo de dados. <br><br> Se você precisar ativar mais de 250 públicos-alvo para um destino, é possível: <ul><li> Desmapeie os públicos-alvo que você não deseja mais ativar ou</li><li>Crie um novo fluxo de dados para o destino desejado e mapeie os públicos para esse novo fluxo de dados.</li></ul> <br> Observe que, no caso de alguns destinos, você pode estar limitado a menos de 250 públicos-alvo mapeados para o destino. Esses destinos são chamados mais abaixo na página, em suas respectivas seções. |
| Número máximo de atributos mapeados para um destino | 50 | Suave | No caso de vários destinos e tipos de destino, é possível selecionar atributos de perfil e identidades para mapear para exportação. Para um desempenho ideal, no máximo 50 atributos devem ser mapeados em um fluxo de dados para um destino. |
| Número máximo de destinos | 100 | Grave | É possível criar um máximo de 100 destinos para os quais você pode conectar e ativar dados, *por sandbox*. [Destinos de personalização da borda (Personalização personalizada)](#edge-destinations-activation) O pode representar, no máximo, 10 dos 100 destinos recomendados. |
| Tipo de dados ativados para destinos | Dados de perfil, incluindo identidades e mapa de identidade | Grave | Atualmente, só é possível exportar *atributos de registro de perfil* para destinos. No momento, não há suporte para atributos XDM que descrevem dados de evento para exportação. |
| Tipo de dados ativados para destinos — suporte a atributos de array e mapa | Não disponível | Grave | Neste momento, é **não** possível exportar *atributos de matriz ou mapa* para destinos. A exceção a esta regra é a [mapa de identidade](/help/xdm/field-groups/profile/identitymap.md), que é exportado em ativações de streaming e baseadas em arquivo. |

{style="table-layout:auto"}

### Ativação de transmissão {#streaming-activation}

As medidas de proteção abaixo se aplicam à ativação por meio de [destinos de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número de ativações (mensagens HTTP com exportações de perfil) por segundo | N/D | - | No momento, não há limite para o número de mensagens por segundo enviadas do Experience Platform para os endpoints da API dos destinos do parceiro. <br> Quaisquer limites ou latências são determinados pelo endpoint para o qual o Experience Platform está enviando dados. Verifique também o [catálogo](/help/destinations/catalog/overview.md) página do destino ao qual você está conectando e ativando dados. |

{style="table-layout:auto"}

### Ativação em lote (baseada em arquivo) {#batch-file-based-activation}

As medidas de proteção abaixo se aplicam à ativação por meio de [destinos em lote (baseados em arquivo)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Frequência de ativação | Uma exportação completa diária ou exportações incrementais mais frequentes a cada 3, 6, 8 ou 12 horas. | Grave | Leia o [exportar arquivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [exportar arquivos incrementais](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) seções de documentação para obter mais informações sobre os incrementos de frequência para exportações em lote. |
| Número máximo de públicos que podem ser exportados em uma determinada hora | 100 | Suave | A recomendação é adicionar no máximo 100 públicos-alvo aos fluxos de dados de destino em lote. |
| Número máximo de linhas (registros) por arquivo a serem ativados | 5 milhões | Grave | O Adobe Experience Platform divide automaticamente os arquivos exportados em 5 milhões de registros (linhas) por arquivo. Cada linha representa um perfil. Nomes de arquivos divididos são anexados com um número que indica que o arquivo é parte de uma exportação maior, como: `filename.csv`, `filename_2.csv`, `filename_3.csv`. Para obter mais informações, leia a [seção de agendamento](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) do tutorial ativar destinos em lote. |

{style="table-layout:auto"}

### Ativação ad hoc {#ad-hoc-activation}

As medidas de proteção a seguir [ativação ad-hoc](/help/destinations/api/ad-hoc-activation-api.md) método.

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Públicos ativados por trabalho de ativação ad-hoc | 80 | Grave | Atualmente, cada trabalho de ativação ad-hoc pode ativar até 80 públicos-alvo. Tentar ativar mais de 80 públicos-alvo por trabalho causará falha no trabalho. Esse comportamento está sujeito a alterações em versões futuras. |
| Trabalhos de ativação ad-hoc simultâneos por público-alvo | 1 | Grave | Não execute mais de um trabalho de ativação ad-hoc simultâneo por público-alvo. |

{style="table-layout:auto"}

### Ativação de destinos de personalização de borda {#edge-destinations-activation}

As medidas de proteção abaixo se aplicam à ativação por meio de [destinos de personalização de borda](/help/destinations/destination-types.md#streaming-profile-export).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número máximo de [Personalização personalizada](/help/destinations/catalog/personalization/custom-personalization.md) destinos | 10 | Suave | Você pode configurar fluxos de dados para 10 destinos de personalização personalizados por sandbox. |
| Número máximo de atributos mapeados para um destino de personalização por sandbox | 30 | Grave | No máximo 30 atributos podem ser mapeados em um fluxo de dados para um destino de personalização, por sandbox. |
| Número máximo de públicos mapeados para um único [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) destino | 50 | Suave | É possível ativar no máximo 50 públicos-alvo em um fluxo de ativação para um único destino do Adobe Target. |

{style="table-layout:auto"}

### [!BADGE Beta]Exportações de conjunto de dados {type=Informative} {#dataset-exports}

Atualmente, as exportações de conjuntos de dados são compatíveis com um **[!UICONTROL Primeiro Completa e, em seguida, Incremental]** [padrão](/help/destinations/ui/export-datasets.md#scheduling). As medidas de proteção descritas nesta seção se aplicam à primeira exportação completa que ocorre após a configuração de um fluxo de trabalho de exportação do conjunto de dados.

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Tamanho dos conjuntos de dados exportados | 5 bilhões de registros | Suave | O limite descrito aqui para exportações de conjunto de dados é um *grade de proteção flexível*. Por exemplo, embora a interface do usuário não impeça a exportação de conjuntos de dados maiores que 5 bilhões de registros, o comportamento é imprevisível e as exportações podem falhar ou ter uma latência de exportação muito longa. |

{style="table-layout:auto"}

<!--

### Dataset Types {#dataset-types}

Datasets exported from Experience Platform can be of two types, as described below:

**Timeseries**
Timeseries datasets are also known as *XDM Experience Events* datasets in Experience Platform terminology.
The dataset schema includes a top level *timestamp* column. Data is ingested in an append-only fashion.

**Record** 
Record datasets are also known as *XDM Individual Profile* datasets in Experience Platform terminology.
The dataset schema does not include a top level *timestamp* column. Data is ingested in upsert fashion.

The guardrails below are grouped by the format of the exported file, and then further by dataset type.

**Parquet output**

|Dataset type | Compression | Guardrail | Description |
|---------|----------|---------|-----------|
| Timeseries | N/A | Last seven days per file | The data from the last seven days only is exported. |
| Record | N/A | Five billion records per file | Only the data from the last seven days is exported. |

{style="table-layout:auto"}

**JSON output**

|Dataset type | Compression | Guardrail | Description |
|---------|----------|---------|-----------|
| Timeseries | N/A | Last seven days per file | The data from the last seven days only is exported. |
| <p>Record</p> | <p><ul><li>Yes</li><li>No</li></ul></p> | <p><ul><li>Five billion records per compressed file</li><li>One million records per uncompressed file</li></ul></p> | <p>The record count of the dataset must be less than five billion for compressed files and one million for uncompressed files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</p> |

{style="table-layout:auto"}

-->

<!--

<table>
<thead>
  <tr>
    <th>Output format</th>
    <th>Dataset type</th>
    <th>Compression</th>
    <th>Guardrail</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Parquet</td>
    <td>Timeseries</td>
    <td>-</td>
    <td>Last seven days per file</td>
    <td>Only the data from the last seven days is exported.</td>
  </tr>
  <tr>
    <td>Record</td>
    <td>-</td>
    <td>Five billion records per file</td>
    <td>The record count of the dataset must be less than five billion, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
  <tr>
    <td rowspan="3">JSON</td>
    <td>Timeseries</td>
    <td>-</td>
    <td>Last seven days per file</td>
    <td>Only the data from the last seven days is exported.</td>
  </tr>
  <tr>
    <td rowspan="2">Record</td>
    <td>Yes</td>
    <td>Five billion records per file</td>
    <td>The record count of the dataset must be less than five billion, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
  <tr>
    <td>No</td>
    <td>One million records per file</td>
    <td>The record count of the dataset must be less than one million, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
</tbody>
</table>

-->

### Grades de proteção de Destination SDK {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) O é um conjunto de APIs de configuração que permitem configurar padrões de integração de destino para que o Experience Platform forneça dados de público-alvo e perfil para o seu endpoint, com base nos formatos de dados e autenticação de sua escolha. As medidas de proteção abaixo se aplicam aos destinos configurados por meio do Destination SDK.

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número máximo de [destinos personalizados privados](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Suave | Você pode criar no máximo 5 destinos personalizados de streaming ou lote privados usando o Destination SDK. Entre em contato com um representante de atendimento personalizado se precisar criar mais de 5 desses destinos. |
| Política de exportação de perfil para Destination SDK | <ul><li>`maxBatchAgeInSecs` (mínimo 1.800 e máximo 3.600)</li><li>`maxNumEventsInBatch` (mínimo 1.000, máximo 10.000)</li></ul> | Grave | Ao usar o [agregação configurável](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) para o seu destino, lembre-se dos valores mínimo e máximo que determinam a frequência com que as mensagens HTTP são enviadas para o seu destino baseado em API e quantos perfis as mensagens devem incluir. |

{style="table-layout:auto"}

### Política de limitação de destino e de repetição {#destination-throttling-and-retry-policy}

Detalhes sobre limites ou limitações de limitação para determinados destinos. Esta seção também fornece informações sobre a política de novas tentativas para destinos.

| Tipo de destino | Descrição |
| --- | --- |
| Destinos empresariais (API HTTP, Amazon Kinesis, EventHubs do Azure) | Em 95% das vezes, o Experience Platform tenta oferecer uma latência de throughput de menos de 10 minutos para mensagens enviadas com êxito, com uma taxa de menos de 10 mil solicitações por segundo para cada fluxo de dados a um destino corporativo. <br> Em caso de falha nas solicitações para o destino da empresa, o Experience Platform armazena as solicitações com falha e tenta enviar as solicitações duas vezes para o endpoint. |

{style="table-layout:auto"}

## Medidas de proteção para outros serviços de Experience Platform {#guardrails-other-services}

Exibir informações de medidas de proteção para outros serviços de Experience Platform:

* Medidas de proteção para [assimilação de dados](/help/ingestion/guardrails.md)
* Medidas de proteção para [[!DNL Identity Service] dados](/help/identity-service/guardrails.md)
* Medidas de proteção para [[!DNL Real-Time Customer Profile] dados](/help/profile/guardrails.md)
* Medidas de proteção para [[!DNL Query Service] dados](/help/query-service/guardrails.md)
