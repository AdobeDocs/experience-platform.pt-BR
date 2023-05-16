---
keywords: Experience Platform, ativação, solução de problemas, grades, diretrizes, limite
title: Medidas de proteção padrão para dados de ativação
solution: Experience Platform
product: experience platform
type: Documentation
description: Saiba mais sobre o uso padrão da ativação de dados e limites de taxa.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 7c1d956e3b6a1314baa13fef823d73d42404516a
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 3%

---

# Medidas de proteção para dados de ativação

Esta página fornece limites de uso e taxa padrão em relação ao comportamento de ativação. Ao analisar as seguintes medidas de proteção, parte-se do princípio de que tem a [ligado a destinos](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* A maioria dos clientes não excede esses limites padrão. Se quiser saber mais sobre limites personalizados, entre em contato com seu representante de atendimento ao cliente.
>* Os limites indicados neste documento são constantemente melhorados. Verifique regularmente se há atualizações.
>* Dependendo das limitações individuais de downstream, alguns destinos podem ter medidas de proteção mais restritivas do que as documentadas nesta página. Verifique também a variável [catálogo](/help/destinations/catalog/overview.md) página do destino para a qual você está conectando e ativando os dados.


## Tipos de limite {#limit-types}

Existem dois tipos de limites padrão neste documento:

* **Limite suave:** É possível ir além de um limite suave, no entanto, os limites suaves fornecem uma diretriz recomendada para o desempenho do sistema.
* **Limite rígido:** Um limite rígido fornece um máximo absoluto. A interface do usuário ou a API do Experience Platform não permite ir além desse limite, ou um erro é retornado se você ultrapassar esse limite.


## Limites de ativação {#activation-limits}

As seguintes medidas de proteção fornecem limites recomendados ao ativar dados de Perfil do cliente em tempo real para destinos.

### Medidas de proteção gerais de ativação {#general-activation-guardrails}

As medidas de proteção abaixo geralmente se aplicam à ativação através de [todos os tipos de destino](/help/destinations/destination-types.md#destination-types).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número máximo de segmentos para um único destino | 250 | Suave | A recomendação é mapear no máximo 250 segmentos para um único destino em um fluxo de dados. <br><br> Se você precisar ativar mais de 250 segmentos para um destino, poderá: <ul><li> Desmapeie os segmentos que você não deseja mais ativar ou</li><li>Crie um novo fluxo de dados para o destino desejado e mapeie os segmentos para esse novo fluxo de dados.</li></ul> <br> Observe que, no caso de alguns destinos, você pode estar limitado a menos de 250 segmentos mapeados para o destino. Esses destinos são chamados mais adiante na página, em suas respectivas seções. |
| Número máximo de destinos | 100 | Suave | A recomendação é criar um máximo de 100 destinos para os quais você pode conectar e ativar os dados *por sandbox*. [Destinos de personalização de borda (personalização personalizada)](#edge-destinations-activation) podem ser, no máximo, 10 dos 100 destinos recomendados. |
| Número máximo de atributos mapeados para um destino | 50 | Suave | No caso de vários destinos e tipos de destino, é possível selecionar atributos e identidades de perfil para mapear para exportação. Para um desempenho ideal, no máximo 50 atributos devem ser mapeados em um fluxo de dados para um destino. |
| Tipo de dados ativado para destinos | Dados do perfil, incluindo identidades e mapa de identidade | Grave | Atualmente, só é possível exportar *atributos de registro de perfil* para destinos. Atributos XDM que descrevem dados de evento não são suportados para exportação no momento. |
| Tipo de dados ativado para destinos - suporte a atributos de matriz e mapa | Não disponível | Grave | Neste momento, é **not** possível exportar *atributos de matriz ou mapa* para destinos. A exceção para essa regra é o [mapa de identidade](/help/xdm/field-groups/profile/identitymap.md), que é exportado em streaming e ativações baseadas em arquivo. |

{style="table-layout:auto"}

### Ativação de streaming {#streaming-activation}

As medidas de proteção abaixo aplicam-se à ativação através de [destinos de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número de ativações (mensagens HTTP com exportações de perfil) por segundo | N/D | - | No momento, não há limite para o número de mensagens por segundo enviadas do Experience Platform para os pontos de extremidade da API dos destinos de parceiros. <br> Quaisquer limites ou latências são ditados pelo endpoint em que o Experience Platform está enviando dados. Verifique também a variável [catálogo](/help/destinations/catalog/overview.md) página do destino para a qual você está conectando e ativando os dados. |

{style="table-layout:auto"}

### Ativação em lote (com base em arquivo) {#batch-file-based-activation}

As medidas de proteção abaixo aplicam-se à ativação através de [destinos em lote (com base em arquivo)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Frequência de ativação | Uma exportação completa diária ou exportações incrementais mais frequentes a cada 3, 6, 8 ou 12 horas. | Grave | Leia o [exportar arquivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [exportar arquivos incrementais](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) seções de documentação para obter mais informações sobre os incrementos de frequência para exportações em lote. |
| Número máximo de segmentos que podem ser exportados em uma determinada hora | 100 | Suave | A recomendação é adicionar um máximo de 100 segmentos aos fluxos de dados de destino em lote. |
| Número máximo de linhas (registros) por arquivo para ativar | 5 milhões | Grave | O Adobe Experience Platform divide automaticamente os arquivos exportados em 5 milhões de registros (linhas) por arquivo. Cada linha representa um perfil. Nomes de arquivos divididos são anexados com um número que indica que o arquivo faz parte de uma exportação maior, desta forma: `filename.csv`, `filename_2.csv`, `filename_3.csv`. Para obter mais informações, leia a [seção de programação](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) do tutorial ativar destinos em lote. |

{style="table-layout:auto"}

### Ativação ad-hoc {#ad-hoc-activation}

As medidas de proteção a seguir indicadas aplicam-se [ativação ad-hoc](/help/destinations/api/ad-hoc-activation-api.md) método .

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Segmentos ativados por trabalho de ativação ad-hoc | 80 | Grave | Atualmente, cada trabalho de ativação ad-hoc pode ativar até 80 segmentos. Tentar ativar mais de 80 segmentos por trabalho causará falha na tarefa. Esse comportamento está sujeito a alterações em versões futuras. |
| Trabalhos de ativação ad-hoc simultâneos por segmento | 1 | Grave | Não execute mais de um trabalho de ativação ad hoc simultâneo por segmento. |

{style="table-layout:auto"}

### Ativação de destinos de personalização de borda {#edge-destinations-activation}

As medidas de proteção abaixo aplicam-se à ativação através de [destinos de personalização de borda](/help/destinations/destination-types.md#streaming-profile-export).

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número máximo de [Personalização personalizada](/help/destinations/catalog/personalization/custom-personalization.md) destinos | 10 | Suave | Você pode configurar fluxos de dados para 10 destinos de personalização personalizados por sandbox. |
| Número máximo de atributos mapeados para um destino de personalização por sandbox | 30 | Grave | É possível mapear no máximo 30 atributos em um fluxo de dados para um destino de personalização, por sandbox. |
| Número máximo de segmentos mapeados para um único [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) destino | 50 | Suave | Você pode ativar no máximo 50 segmentos em um fluxo de ativação para um único destino do Adobe Target. |

{style="table-layout:auto"}

### Medidas de proteção de Destination SDK {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) é um conjunto de APIs de configuração que permitem configurar padrões de integração de destino para o Experience Platform para fornecer dados de público-alvo e perfil ao endpoint, com base em dados e formatos de autenticação de sua escolha. As grades de proteção abaixo se aplicam aos destinos configurados com o Destination SDK.

| Grade de Proteção | Limite | Tipo de limite | Descrição |
| --- | --- | --- | --- |
| Número máximo de [destinos personalizados privados](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Suave | Você pode criar um máximo de 5 destinos de streaming personalizados privados ou de lote usando o Destination SDK. Entre em contato com um representante de atendimento personalizado se precisar criar mais de 5 desses destinos. |
| Política de exportação de perfil para o Destination SDK | <ul><li>`maxBatchAgeInSecs` (mínimo 1,800 e máximo 3,600)</li><li>`maxNumEventsInBatch` (mínimo 1.000, máximo 10.000)</li></ul> | Grave | Ao usar a variável [agregação configurável](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) para seu destino, tenha em mente os valores mínimo e máximo que determinam a frequência com que as mensagens HTTP são enviadas para seu destino baseado em API e quantos perfis as mensagens devem incluir. |

{style="table-layout:auto"}

### Política de limitação e tentativa de destino {#destination-throttling-and-retry-policy}

Detalhes sobre limites ou limitações de limitação para determinados destinos. Esta seção também fornece informações sobre a política de tentativas para destinos.

| Tipo de destino | Descrição |
| --- | --- |
| Destinos corporativos (API HTTP, Amazon Kinesis, Azure EventHubs) | Em 95% das vezes, o Experience Platform tenta oferecer uma latência de taxa de transferência inferior a 10 minutos para mensagens enviadas com êxito com uma taxa inferior a 10 mil solicitações por segundo para cada fluxo de dados para um destino empresarial. <br> No caso de solicitações com falha para o destino da empresa, o Experience Platform armazena as solicitações com falha e tenta novamente duas vezes para enviar as solicitações para o terminal. |

{style="table-layout:auto"}

## Medidas de proteção para outros serviços de Experience Platform {#guardrails-other-services}

Exibir informações de medidas de proteção para outros serviços de Experience Platform:

* Medidas de proteção [ingestão de dados](/help/ingestion/guardrails.md)
* Medidas de proteção [[!DNL Identity Service] dados](/help/identity-service/guardrails.md)
* Medidas de proteção [[!DNL Real-Time Customer Profile] dados](/help/profile/guardrails.md)
* Medidas de proteção [[!DNL Query Service] dados](/help/query-service/guardrails.md)
