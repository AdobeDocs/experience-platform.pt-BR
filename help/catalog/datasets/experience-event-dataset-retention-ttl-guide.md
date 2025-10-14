---
title: Gerenciar a retenção do conjunto de dados do evento de experiência no Data Lake usando TTL
description: Saiba como avaliar, definir e gerenciar a Retenção de conjunto de dados de evento de experiência no data lake usando configurações de Tempo de vida (TTL) com APIs do Adobe Experience Platform. Este guia explica como a expiração em nível de linha de TTL suporta políticas de retenção de dados, otimiza a eficiência do armazenamento e garante um gerenciamento eficaz do ciclo de vida dos dados. Ela também fornece casos de uso e práticas recomendadas para ajudar você a aplicar o TTL de maneira eficaz.
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: a4662d1042122fa9c3260c0e53c50bd78935cf31
workflow-type: tm+mt
source-wordcount: '2472'
ht-degree: 0%

---

# Gerenciar a retenção do conjunto de dados do evento de experiência no data lake usando TTL

O gerenciamento eficiente de dados é essencial para o desempenho ideal, o controle de custos e a integridade dos dados. Use o TTL (Time-To-Live) de retenção de conjunto de dados de eventos de experiência para aplicar a expiração no nível de linha, removendo automaticamente registros desatualizados de conjuntos de dados no data lake e, ao mesmo tempo, garantindo a eficiência ideal do armazenamento e a relevância dos dados.

Este guia explica como avaliar, definir e gerenciar o TTL usando a API do Serviço de catálogo. Você aprenderá quando e por que aplicar o TTL, como configurar e atualizar valores TTL usando chamadas de API e práticas recomendadas para garantir uma implementação eficaz.

>[!IMPORTANT]
>
>O TTL foi projetado para otimizar o gerenciamento do ciclo de vida dos dados e a eficiência do armazenamento. Não é uma ferramenta de conformidade e não deve ser usada para requisitos normativos. A conformidade geralmente requer estratégias mais amplas de controle de dados.

## Por que usar TTL para gerenciamento de dados em nível de linha

À medida que os conjuntos de dados crescem, o gerenciamento eficiente de dados torna-se cada vez mais importante para preservar o desempenho, controlar os custos e manter os dados relevantes. A expiração de dados em nível de linha com base em TTL automatiza a limpeza de dados removendo registros desatualizados sem intervenção manual para ajudar a otimizar o armazenamento e melhorar a eficiência do sistema.

O TTL é útil ao gerenciar dados sensíveis ao tempo que perdem relevância ao longo do tempo. Considere implementar o TTL se precisar:

- Reduza os custos de armazenamento removendo automaticamente registros desatualizados.
- Melhore o desempenho da consulta minimizando dados irrelevantes.
- Mantenha a higiene de dados mantendo somente as informações relevantes.
- Otimize a retenção de dados para dar suporte aos objetivos de negócios.

>[!NOTE]
>
>A retenção do conjunto de dados do evento de experiência se aplica aos dados do evento armazenados no data lake. Se você estiver gerenciando a retenção no Real-Time Customer Data Platform, considere usar a [Expiração do evento de experiência](../../profile/event-expirations.md) e a [Expiração do perfil pseudônimo](../../profile/pseudonymous-profiles.md) junto com as configurações de retenção do data lake.

Use as configurações de TTL para otimizar o armazenamento com base nos direitos. Embora os dados do Armazenamento de perfil (usados no Real-Time CDP) possam ser considerados obsoletos e removidos após 30 dias, os mesmos dados de evento no data lake podem permanecer disponíveis por 12 a 13 meses (ou mais, com base no direito) para casos de uso do Analytics e do Data Distiller.

>[!TIP]
>
>Os direitos referem-se às licenças de armazenamento e retenção definidas pelos contratos de assinatura e licença da Adobe.

### Exemplo do setor {#industry-example}

Como exemplo, considere um serviço de streaming de vídeo que rastreia as interações do usuário, como exibições, pesquisas e recomendações de vídeo. Embora os dados recentes de engajamento sejam cruciais para a personalização, os logs de atividades mais antigos (por exemplo, interações de mais de um ano atrás) perdem relevância. Ao usar a expiração em nível de linha, o Experience Platform remove automaticamente os logs desatualizados, garantindo que somente os dados atuais e significativos sejam usados para análises e recomendações.

## Avaliar adequação do TTL {#evaluate-ttl-suitability}

Antes de aplicar uma política de retenção, avalie se o conjunto de dados é um bom candidato para a expiração em nível de linha. Considere o seguinte:

- Relevância dos dados ao longo do tempo: os dados mais antigos agregam valor ou se tornam obsoletos?
- Impacto nos processos downstream: a remoção de dados afetará os relatórios, as análises ou as integrações?
- Custo de armazenamento versus valor de retenção: o valor dos dados mais antigos justifica o custo de armazená-los?

Se os registros históricos forem essenciais para análises de longo prazo ou operações de negócios, o TTL pode não ser a abordagem correta. A análise desses fatores garante que o TTL se alinhe às suas necessidades de retenção de dados sem afetar negativamente a disponibilidade dos dados.

## Práticas recomendadas para definir o TTL {#best-practices}

Selecione o valor TTL correto para garantir que sua política de retenção do conjunto de dados do evento de experiência equilibre a retenção de dados, a eficiência do armazenamento e as necessidades analíticas. Um TTL muito curto pode causar perda de dados, enquanto um TTL muito longo pode aumentar os custos de armazenamento e o acúmulo desnecessário de dados. Verifique se o TTL está alinhado à finalidade do seu conjunto de dados, considerando a frequência com que os dados são acessados e por quanto tempo permanecem relevantes.

A tabela abaixo fornece recomendações comuns de TTL com base no tipo de conjunto de dados e nos padrões de uso:

| Tipo de conjunto de dados | TTL recomendado | Casos de uso típicos |
|-----------------------------|------------------------|-------------------|
| Conjuntos de dados acessados com frequência | 30 a 90 dias | Registros de engajamento do usuário, dados de sequência de cliques do site, dados de desempenho de campanha de curto prazo. |
| Conjuntos de dados de arquivamento | 1 ano ou mais | Registros de transações financeiras, dados de conformidade, análise de tendências a longo prazo, conjuntos de dados de treinamento de aprendizado de máquina. |
| Conjuntos de dados gerenciados por aplicativo | Até 13 meses | Os conjuntos de dados gerenciados pelo sistema têm restrições TTL predefinidas, que são automaticamente impostas para cumprir os limites impostos pelo sistema. |
| Conjuntos de dados gerenciados pelo cliente | 30 dias - TTL máximo | Conjuntos de dados criados por meio da interface, das APIs ou do Data Distiller. O TTL deve ser de pelo menos 30 dias e estar dentro do TTL máximo definido. |

Revise as configurações de TTL periodicamente para garantir que elas continuem alinhadas às suas políticas de armazenamento, necessidades analíticas e requisitos de negócios.

### Considerações principais ao definir o TTL {#key-considerations}

Siga estas práticas recomendadas para garantir que as configurações de TTL se alinhem à sua estratégia de retenção de dados:

- Auditoria de alterações de TTL regularmente. Cada atualização de TTL aciona um evento de auditoria. Use logs de auditoria para rastrear modificações do TTL para fins de conformidade, governança de dados e solução de problemas.
- Desative o TTL se os dados precisarem ser retidos indefinidamente. Para desabilitar o TTL, defina `ttlValue` como `null`. Isso impede a expiração automática e retém todos os registros permanentemente. Considere as implicações de armazenamento antes de fazer essa alteração.

## Limitações do TTL {#limitations}

Esteja ciente das seguintes limitações ao usar TTL:

- **A Retenção do Conjunto de Dados de Evento de Experiência usando TTL se aplica à expiração em nível de linha**, não à exclusão do conjunto de dados. O TTL remove registros com base em um período de retenção definido, mas não exclui conjuntos de dados inteiros. Para remover um conjunto de dados, use o [ponto de extremidade de expiração do conjunto de dados](../../hygiene/api/dataset-expiration.md) ou a exclusão manual.
- **A configuração de TTL permanece ativa até ser explicitamente desabilitada**. A configuração permanece em vigor até que você a desative. Desabilitar o TTL interrompe a expiração e garante que todos os registros no conjunto de dados sejam retidos.
- **TTL não é uma ferramenta de conformidade**. Embora o TTL otimize o gerenciamento do armazenamento e do ciclo de vida, você deve implementar estratégias de controle mais amplas para garantir a conformidade normativa.

## Analisar o tamanho e a relevância do conjunto de dados antes de aplicar o TTL {#analyze-dataset-size}

Antes de aplicar o TTL, use consultas para analisar o tamanho e a relevância do conjunto de dados. Execute consultas direcionadas (como contar registros em intervalos de datas específicos) para visualizar o impacto de vários valores TTL. Em seguida, use essas informações para escolher um período de retenção ideal que equilibre a utilidade dos dados e a economia.

![Um fluxo de trabalho visual para implementar o TTL em conjuntos de dados de eventos de experiência. As etapas incluem: avaliar o tempo de vida dos dados e o impacto da remoção, validar configurações TTL com consultas, configurar o TTL por meio da API do Serviço de Catálogo, monitorar continuamente o impacto do TTL e fazer ajustes.](../images/datasets/dataset-retention-ttl-guide/manage-experience-event-dataset-retention-in-the-data-lake.png)

A execução de consultas direcionadas ajuda a determinar quantos dados seriam retidos ou removidos em diferentes configurações de TTL. Por exemplo, a consulta SQL a seguir conta o número de registros criados nos últimos 30 dias:

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

A execução de consultas semelhantes em intervalos de tempo diferentes ajuda a validar as configurações de TTL e a garantir que elas equilibrem a eficiência do armazenamento e a acessibilidade dos dados.

## Introdução ao gerenciamento TTL

Antes de avaliar, definir e gerenciar a Retenção do conjunto de dados do evento de experiência usando a API do serviço de catálogo, você deve entender como formatar suas solicitações corretamente. Isso inclui conhecer os caminhos da API, fornecer cabeçalhos necessários e formatar cargas de solicitação. Consulte o [Guia de introdução à API do Serviço de Catálogo](../api/getting-started.md) para obter essas informações essenciais.

>[!NOTE]
>
>Este documento abrange a expiração em nível de linha, que exclui linhas expiradas individuais em um conjunto de dados, mantendo o próprio conjunto de dados intacto. Isso não se aplica à expiração do conjunto de dados, que remove conjuntos de dados inteiros e é gerenciada por um recurso separado. Para expiração no nível do conjunto de dados, consulte a [documentação da API de expiração do conjunto de dados](../../hygiene/api/dataset-expiration.md).

### Verifique suas restrições de TTL {#check-ttl-constraints}

Use o ponto de extremidade `/ttl/{DATASET_ID}` da API de Higiene de Dados para ajudar a planejar as configurações de TTL. Esse ponto de extremidade retorna os valores TTL mínimo e máximo com suporte para sua organização, juntamente com um valor recomendado (`defaultValue`) para o tipo de conjunto de dados.

Consulte a documentação da [API de higiene de dados](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/#operation/getTtl) do Adobe Developer para obter mais informações.

Para [verificar o TTL aplicado atualmente a um conjunto de dados](#check-applied-ttl-values), faça uma solicitação GET para o ponto de extremidade [&#x200B; da &#x200B;](https://developer.adobe.com/experience-platform-apis/references/catalog/)API do Serviço de Catálogo`/dataSets/{DATASET_ID}`.

>[!TIP]
>
>A URL do Gateway Experience Platform e o caminho base para a API do Serviço de Catálogo são: `https://platform.adobe.io/data/foundation/catalog`. O caminho base para a API de higiene de dados é: `https://platform.adobe.io/data/core/hygiene`

**Formato da API**

```http
GET /ttl/{DATASET_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | Uma string gerada pelo sistema que identifica exclusivamente um conjunto de dados. Para localizar uma ID de conjunto de dados, use o ponto de extremidade `/datasets`. Consulte o [guia da API de objetos de catálogo de lista](../api/list-objects.md) para obter instruções sobre como filtrar respostas para conjuntos de dados relevantes. |

**Solicitação**

A solicitação a seguir recupera as restrições de TTL da organização para um conjunto de dados específico.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna os valores de TTL recomendados, máximos e mínimos com base nos direitos da organização, juntamente com um TTL sugerido (`defaultValue`) para o conjunto de dados. Esta `defaultValue` é uma duração de TTL recomendada, fornecida somente para orientação. Ela não é aplicada a menos que seja configurada explicitamente por você. A resposta não inclui valores TTL personalizados que já possam ter sido definidos. Para exibir o TTL atual de um conjunto de dados, use o ponto de extremidade `/catalog/dataSets/{DATASET_ID}` do GET.

+++Selecionar para exibir a resposta

```json
{
  "extensions": {
    "adobe_lakeHouse": {
      "rowExpiration": {
        "defaultValue": "P12M",
        "maxValue": "P12M",
        "minValue": "P7D"
      }
    }
  }
}
```

+++

| Propriedade | Descrição |
|--------------|-------------|
| `defaultValue` | Um valor TTL recomendado para seu conjunto de dados. Este valor **não** é aplicado automaticamente. Você deve definir explicitamente um TTL para que ele entre em vigor. |
| `maxValue` | A duração máxima de TTL permitida pelos direitos da organização. Normalmente, essa duração é de 10 anos (`P10Y`). |
| `minValue` | A duração TTL mínima permitida pelos direitos da organização. Normalmente, essa duração é de 30 dias (`P30D`). |

### Como verificar valores TTL aplicados {#check-applied-ttl-values}

Para verificar o valor TTL atual que foi aplicado a um conjunto de dados, use a seguinte chamada de API:

```http
GET /dataSets/{DATASET_ID}
```

Esta chamada retorna o `ttlValue` atual (se definido) na seção `extensions.adobe_lakeHouse.rowExpiration`.

**Solicitação**

A solicitação a seguir recupera o valor TTL da organização para um conjunto de dados específico.

```shell
curl -X GET \
https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida inclui o objeto `extensions`, que contém a configuração TTL atual aplicada ao conjunto de dados. O exemplo de resposta abaixo está truncado por questões de brevidade.

```json
{
    "{DATASET_ID}": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M",
            }
            }
        }
        ...
    }
}
```

### Definir ou atualizar o TTL para um conjunto de dados {#set-update-ttl}

>[!IMPORTANT]
>
>A expiração em nível de linha com base em TTL só pode ser aplicada a conjuntos de dados de evento que usam um esquema de série temporal. Isso inclui conjuntos de dados com base na classe XDM ExperienceEvent padrão, bem como esquemas personalizados que estendem o esquema de Série de Tempo (`https://ns.adobe.com/xdm/data/time-series`).
>
>Antes de aplicar o TTL, use a API do Registro de Esquema para verificar se o esquema do conjunto de dados inclui a extensão correta, verificando a propriedade `meta:extends`. Consulte a [documentação do endpoint de esquema](../../xdm/api/schemas.md#lookup) para obter orientação sobre como fazer isso.

Você pode configurar a Retenção do conjunto de dados de evento de experiência definindo um novo TTL ou atualizando um TTL existente usando o mesmo método de API. Use uma solicitação PATCH para o ponto de extremidade `/v2/datasets/{DATASET_ID}` para aplicar ou ajustar o TTL.

**Formato da API**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | A ID do conjunto de dados para o qual você deseja atualizar o valor TTL. |

**Solicitação**

No exemplo abaixo, o `ttlValue` está definido como `P3M`. Isso significa que os registros com mais de três meses são excluídos automaticamente. Ajuste o período de retenção para atender às suas necessidades comerciais (por exemplo, `P6M` para seis meses ou `P12M` para um ano).

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M"  // A 3 month retention period
            }
        }
    }
}
```

| Propriedade | Descrição |
|----------------------------------|-------------|
| `rowExpiration.ttlValue` | Define a duração antes da remoção automática dos registros no conjunto de dados. Usa o formato de período ISO-8601 (por exemplo, `P3M` para 3 meses ou `P30D` para 30 dias). |

**Resposta**

Uma resposta bem-sucedida retorna uma referência ao conjunto de dados atualizado, mas não inclui explicitamente as configurações de TTL. Para confirmar a configuração TTL, faça uma solicitação de acompanhamento `GET /dataSets/{DATASET_ID}`.

```JSON
[
  "@/dataSets/{DATASET_ID}"
]
```

#### Exemplo de cenário {#example-scenario}

Considere uma plataforma de transmissão de vídeo que define inicialmente o TTL como três meses para garantir novos dados de envolvimento para personalização. No entanto, se a análise subsequente revelar que interações mais antigas ainda fornecem insights valiosos, o TTL pode ser estendido para seis meses com a seguinte solicitação:

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P6M"  // Extend to 6 months
            }
        }
    }
}
```

## Perguntas frequentes sobre a política de retenção do conjunto de dados {#faqs}

Estas perguntas frequentes abordam questões práticas sobre tarefas de retenção de conjuntos de dados, efeitos imediatos de alterações de TTL, opções de recuperação e como os períodos de retenção diferem entre os serviços da plataforma.

### A quais tipos de conjuntos de dados posso aplicar regras de política de retenção?

+++Resposta
Você pode aplicar políticas de retenção baseadas em TTL a qualquer conjunto de dados que use comportamento de série temporal. Isso inclui conjuntos de dados com base na classe XDM ExperienceEvent padrão, bem como esquemas personalizados projetados para capturar dados de séries de tempo.

A expiração em nível de linha requer as seguintes condições técnicas:

- O esquema deve ser projetado para capturar dados de série temporal.
- O esquema deve incluir um campo de carimbo de data e hora usado para avaliar a expiração.
- O conjunto de dados deve armazenar dados no nível do evento, normalmente usando ou estendendo a classe XDM ExperienceEvent.
- O conjunto de dados deve ser registrado no Serviço de Catálogo, já que as configurações de TTL são aplicadas via `extensions.adobe_lakeHouse.rowExpiration`.
- Os valores TTL devem usar o formato duration ISO-8601 (por exemplo, `P30D`, `P6M`, `P1Y`).
+++

### Quando o trabalho de Retenção de conjunto de dados excluirá os dados dos serviços do data lake?

+++Resposta
Os TTLs do conjunto de dados são avaliados e processados a cada 30 dias, excluindo todos os registros expirados. Um evento será considerado expirado se tiver sido assimilado na Experience Platform há mais de 30 dias (data de assimilação > 30 dias) e sua data de evento exceder o período de retenção definido (TTL).
+++

<!-- ### How soon will the Dataset Retention job delete data from Profile services?

+++Answer
Once a retention policy is set, existing events that already exceed the newly defined TTL are immediately deleted. Newer events remain until their timestamps surpass the retention period.

For example, if you apply a 30-day expiration policy on May 15th, the following occurs:

- New events receive a 30-day expiration as they are ingested.
- Existing events with a timestamp older than April 15th are immediately deleted.
- Existing events with a timestamp after April 15th are set to expire 30 days after their timestamp (for example, an event from April 18th would be deleted on May 18th).
+++ -->

### Posso definir políticas de retenção diferentes para data lake e serviços de perfil?

+++Resposta

>[!NOTE]
>
>O período de retenção do Serviço de perfil só pode ser atualizado uma vez a cada 30 dias.

Sim, você pode definir políticas de retenção diferentes para os serviços de perfil e data lake. O período de retenção do armazenamento de perfis pode ser menor ou mais longo que o período de retenção do data lake, dependendo das necessidades da sua organização.

+++

### Como posso verificar o uso do meu conjunto de dados atual?

+++Resposta
Você pode verificar o tamanho de armazenamento do conjunto de dados mais recente para armazenamentos de data lake e Perfil como métricas separadas no espaço de trabalho de inventário [!UICONTROL Conjunto de dados]. Classifique as colunas para identificar os maiores conjuntos de dados e verificar se as políticas de retenção foram aplicadas.

Para uso em nível de sandbox, consulte o Painel de uso da licença. Consulte a [documentação de Uso da Licença](../../dashboards/guides/license-usage.md) para obter detalhes.
+++

### Como posso verificar se o trabalho de retenção de dados foi bem-sucedido?

+++Resposta
Você pode verificar o último trabalho de retenção de dados verificando o carimbo de data/hora na [Interface de Usuário de Configuração de Retenção de Conjunto de Dados](./user-guide.md#data-retention-policy) ou na página Inventário de Dados.

Como alternativa, você pode fazer uma solicitação do GET para o seguinte endpoint:

`GET https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID}`

A resposta inclui a propriedade `extensions.adobe_lakeHouse.rowExpiration.lastCompleted`, que indica o carimbo de data/hora Unix (em milissegundos) de quando o trabalho TTL mais recente foi concluído.

Os relatórios de uso do conjunto de dados histórico não estão disponíveis no momento.
+++

### Posso recuperar dados excluídos?

+++Resposta
Não, depois que uma política de retenção é aplicada, os dados anteriores ao período de retenção são permanentemente excluídos e não podem ser recuperados.
+++

### Qual é o TTL mínimo que posso configurar em um conjunto de dados de Evento de experiência do data lake?

+++Resposta 
O TTL mínimo para um conjunto de dados de Evento de experiência do data lake é de 30 dias. O data lake funciona como um sistema de processamento de backup e recuperação durante a assimilação e o processamento iniciais. Como resultado, os dados devem permanecer no data lake por pelo menos 30 dias após a ingestão antes de expirarem.
+++

### E se for necessário reter alguns campos do data lake por mais tempo do que minha política de TTL permite?

+++Resposta 
Use o Data Distiller para reter campos específicos além do TTL do conjunto de dados, mantendo-o dentro dos limites de utilização. Crie um trabalho que grava regularmente apenas os campos necessários em um conjunto de dados derivado. Esse fluxo de trabalho garante a conformidade com um TTL mais curto, preservando os dados críticos para uso estendido.

Para obter mais detalhes, consulte o [Criar conjuntos de dados derivados com o guia SQL](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md).
+++

## Próximas etapas {#next-steps}

Agora que você aprendeu a gerenciar configurações de TTL para expiração em nível de linha, revise a seguinte documentação para aprimorar sua compreensão do gerenciamento de TTL:

- Trabalhos de retenção: saiba como agendar e automatizar as expirações de conjuntos de dados na interface do usuário do Experience Platform com o [guia da interface do usuário do ciclo de vida dos dados](../../hygiene/ui/dataset-expiration.md), ou verifique as configurações de Retenção do conjunto de dados e se os registros expirados foram excluídos.
- [Guia de ponto de extremidade da API de expiração do conjunto de dados](../../hygiene/api/dataset-expiration.md): descubra como excluir conjuntos de dados inteiros em vez de apenas linhas. Saiba como agendar, gerenciar e automatizar a expiração do conjunto de dados usando a API para garantir uma retenção de dados eficiente.
- [Visão geral das políticas de uso de dados](../../data-governance/policies/overview.md): saiba como alinhar sua estratégia de retenção de dados a requisitos de conformidade mais amplos e restrições de uso de marketing.
