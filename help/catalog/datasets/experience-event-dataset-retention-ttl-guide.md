---
title: Gerenciar a retenção do conjunto de dados do evento de experiência no Data Lake usando TTL
description: Saiba como avaliar, definir e gerenciar a Retenção de conjunto de dados de evento de experiência no data lake usando configurações de Tempo de vida (TTL) com APIs do Adobe Experience Platform. Este guia explica como a expiração em nível de linha de TTL suporta políticas de retenção de dados, otimiza a eficiência do armazenamento e garante um gerenciamento eficaz do ciclo de vida dos dados. Ela também fornece casos de uso e práticas recomendadas para ajudar você a aplicar o TTL de maneira eficaz.
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2341'
ht-degree: 0%

---

# Gerenciar a retenção do conjunto de dados do evento de experiência no data lake usando TTL

O gerenciamento eficiente de dados é essencial para o desempenho ideal, o controle de custos e a integridade dos dados. Use o TTL (Time-To-Live) de retenção de conjunto de dados de eventos de experiência para aplicar a expiração no nível de linha, removendo automaticamente registros desatualizados de conjuntos de dados no data lake e, ao mesmo tempo, garantindo a eficiência ideal do armazenamento e a relevância dos dados.

Este guia explica como avaliar, definir e gerenciar o TTL usando a API do Serviço de catálogo. Você aprenderá quando e por que aplicar o TTL, como configurar e atualizar valores TTL usando chamadas de API e práticas recomendadas para garantir uma implementação eficaz.

>[!IMPORTANT]
>
> O TTL foi projetado para otimizar o gerenciamento do ciclo de vida dos dados e a eficiência do armazenamento. Não é uma ferramenta de conformidade e não deve ser usada para requisitos normativos. A conformidade geralmente requer estratégias mais amplas de controle de dados.

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
>
>As configurações de TTL ajudam a otimizar o armazenamento com base nos direitos. Embora os dados do Armazenamento de perfil (usados no Real-Time CDP) possam ser considerados obsoletos e removidos após 30 dias, os mesmos dados de evento no data lake podem permanecer disponíveis por 12 a 13 meses (ou mais, com base no direito) para casos de uso do Analytics e do Data Distiller.

### Exemplo do setor {#industry-example}

Como exemplo, considere um serviço de streaming de vídeo que rastreia as interações do usuário, como exibições, pesquisas e recomendações de vídeo. Embora os dados recentes de engajamento sejam cruciais para a personalização, os logs de atividades mais antigos (por exemplo, interações de mais de um ano atrás) perdem relevância. Ao usar a expiração em nível de linha, o Experience Platform remove automaticamente os logs desatualizados, garantindo que somente os dados atuais e significativos sejam usados para análises e recomendações.

## Avaliar adequação do TTL

Antes de aplicar uma política de retenção, avalie se o conjunto de dados é um bom candidato para a expiração em nível de linha. Considere o seguinte:

- Relevância dos dados ao longo do tempo: os dados mais antigos agregam valor ou se tornam obsoletos?
- Impacto nos processos downstream: a remoção de dados afetará os relatórios, as análises ou as integrações?
- Custo de armazenamento versus valor de retenção: o valor dos dados mais antigos justifica o custo de armazená-los?

Se os registros históricos forem essenciais para análises de longo prazo ou operações de negócios, o TTL pode não ser a abordagem correta. A análise desses fatores garante que o TTL se alinhe às suas necessidades de retenção de dados sem afetar negativamente a disponibilidade dos dados.

## Planejar suas consultas

Antes de aplicar o TTL, use consultas para analisar o tamanho e a relevância do conjunto de dados. A execução de consultas direcionadas ajuda a determinar quantos dados seriam retidos ou removidos em diferentes configurações de TTL.

Por exemplo, a consulta SQL a seguir conta o número de registros criados nos últimos 30 dias:

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

A execução de consultas semelhantes em intervalos de tempo diferentes ajuda a validar as configurações de TTL e a garantir que elas equilibrem a eficiência do armazenamento e a acessibilidade dos dados.

## Introdução ao gerenciamento TTL

Antes de avaliar, definir e gerenciar a Retenção do conjunto de dados do evento de experiência usando a API do serviço de catálogo, você deve entender como formatar suas solicitações corretamente. Isso inclui conhecer os caminhos da API, fornecer cabeçalhos necessários e formatar cargas de solicitação. Consulte o [Guia de introdução à API do Serviço de Catálogo](../api/getting-started.md) para obter essas informações essenciais.

>[!NOTE]
>
>Este documento abrange a expiração em nível de linha, que exclui linhas expiradas individuais em um conjunto de dados, mantendo o próprio conjunto de dados intacto. Isso não se aplica à expiração do conjunto de dados, que remove conjuntos de dados inteiros e é gerenciada por um recurso separado. Para expiração no nível do conjunto de dados, consulte a [documentação da API de expiração do conjunto de dados](../../hygiene/api/dataset-expiration.md).

### Como verificar as configurações atuais de TTL

Para iniciar o gerenciamento de TTL, verifique primeiro as configurações atuais de TTL. Faça uma solicitação GET ao ponto de extremidade `/ttl/{datasetId}` para recuperar as configurações de TTL padrão, máximo e mínimo de um conjunto de dados. Essa etapa é necessária porque as regras TTL podem variar de acordo com o tipo de conjunto de dados.

>[!TIP]
>
>A URL do Gateway Experience Platform e o caminho base para a API do Serviço de Catálogo são: `https://platform.adobe.io/data/foundation/catalog`.

**Formato da API**

```http
GET /ttl/{DATASET_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | Uma string gerada pelo sistema que identifica exclusivamente um conjunto de dados. Para localizar uma ID de conjunto de dados, use o ponto de extremidade `/datasets`. Consulte o [guia da API de objetos de catálogo de lista](../api/list-objects.md) para obter instruções sobre como filtrar respostas para conjuntos de dados relevantes. |

**Solicitação**

A solicitação a seguir recupera as configurações TTL da organização para um conjunto de dados específico.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/5ba9452f7de80408007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna a configuração TTL para o conjunto de dados, incluindo os valores TTL padrão, máximo e mínimo para o armazenamento `adobe_lakeHouse` e `adobe_unifiedProfile`.

+++Selecione para exibir a resposta

```json
{
    "67976f0b4878252ab887ccd9": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "tags": {
            "adobe/pqs/table": [
                "acme_sales_20250127_113331_106"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ]
        },
        "extensions": {
            "adobe_lakeHouse": {  
                "rowExpiration": {
                    "defaultValue": "P12M",
                    "maxValue": "P12M",
                    "minValue": "P30D"
                }
            },
            "adobe_unifiedProfile": {  
                "rowExpiration": {
                    "defaultValue": "P12M",
                    "maxValue": "P12M",
                    "minValue": "P7D"
                }
            }
        },
        "version": "1.0.0",
        "created": 1737977611118,
        "updated": 1737977611118,
        "createdClient": "acme_data_pipeline",
        "createdUser": "john.snow@acmecorp.com",
        "updatedUser": "arya.stark@acmecorp.com",
        "classification": {
            "managedBy": "CUSTOMER"
        }
    }
}
```

+++

| Propriedade | Descrição |
|--------------|-------------|
| `defaultValue` | O período TTL padrão aplicado se nenhum TTL personalizado estiver definido. |
| `maxValue` | O TTL mais longo permitido para o conjunto de dados. Se for nulo, não há limite máximo. |
| `minValue` | O TTL mais curto permitido para garantir a conformidade com as políticas do sistema. |

<!-- Q) what is the default Max and Min values and are they system-imposed? -->

### Como definir o TTL para um conjunto de dados {#set-ttl}

>[!IMPORTANT]
>
>A expiração de linha só pode ser aplicada a conjuntos de dados de evento que usam um esquema de série temporal. Antes de definir o TTL, verifique se o esquema do conjunto de dados estende `https://ns.adobe.com/xdm/data/time-series` para garantir que a solicitação de API tenha êxito. Use a API do Registro de Esquema para recuperar os detalhes do esquema e verificar a propriedade `meta:extends`. Consulte a [documentação do endpoint do esquema](../../xdm/api/schemas.md#lookup) para obter orientação sobre como fazer isso.

Para configurar a Retenção do conjunto de dados de evento de experiência para o seu conjunto de dados, defina um novo valor de TTL fazendo uma solicitação PATCH para o ponto de extremidade `/v2/datasets/{ID}`.

**Formato da API**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | A ID do conjunto de dados para o qual você deseja atualizar o valor TTL. |

**Solicitação**

No exemplo de solicitação abaixo, o `ttlValue` está definido como `P3M`. Isso garante que os registros com mais de três meses sejam excluídos automaticamente. Você pode ajustar o período de retenção para atender às suas necessidades comerciais usando valores como `P6M` para seis meses ou `P12M` para um ano.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -h 'Authorization: Bearer {ACCESS_TOKEN}' \
  -h 'Content-Type: application/json' \
  -h 'x-api-key: {API_KEY}' \
  -h 'x-gw-ims-org-id: {ORG_ID}' \
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

**Resposta**

Uma resposta bem-sucedida mostra a configuração de TTL do conjunto de dados. Inclui detalhes sobre as configurações de expiração em nível de linha para o armazenamento `adobe_lakeHouse` e `adobe_unifiedProfile`.

+++Selecione para exibir a resposta

```JSON
{
    "67976f0b4878252ab887ccd9": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "tags": {
            "adobe/pqs/table": [
                "acme_sales_20250127_113331_106"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ]
        },
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                "ttlValue": "P3M",
                    "valueStatus": "custom",
                    "setBy": "user",
                    "updated": 1737977766499
                }
            },
            "adobe_unifiedProfile": {  
                "rowExpiration": {
                    "ttlValue": "P3M",
                    "valueStatus": "custom",
                    "setBy": "user",
                    "updated": 1737977766499
                }
            }
        },
        "version": "1.0.0",
        "created": 1737977611118,
        "updated": 1737977611118,
        "createdClient": "acme_data_pipeline",
        "createdUser": "john.snow@acmecorp.com",
        "updatedUser": "arya.stark@acmecorp.com",
        "classification": {
            "managedBy": "CUSTOMER"
        }
    }
}
```

+++

| Propriedade | Descrição |
|----------------------------------|-------------|
| `extensions` | Um container para metadados adicionais relacionados ao conjunto de dados. |
| `extensions.adobe_lakeHouse` | Especifica configurações relacionadas à arquitetura de armazenamento, incluindo configurações de expiração em nível de linha |
| `rowExpiration` | O objeto contém configurações TTL que definem o período de retenção do conjunto de dados. |
| `rowExpiration.ttlValue` | Define a duração antes da remoção automática dos registros no conjunto de dados. Usa o formato de período ISO-8601 (por exemplo, `P3M` para 3 meses ou `P30D` para uma semana). |
| `rowExpiration.valueStatus` | A string indica se a configuração TTL é um valor padrão do sistema ou um valor personalizado definido por um usuário. Valores possíveis: `default`, `custom`. |
| `rowExpiration.setBy` | Especifica quem modificou a configuração TTL pela última vez. Os valores possíveis incluem: `user` (definido manualmente) ou `service` (atribuído automaticamente). |
| `rowExpiration.updated` | O carimbo de data e hora da última atualização TTL. Esse valor indica quando a configuração TTL foi modificada pela última vez. |

### Como atualizar o TTL {#update-ttl}

Estenda ou reduza o período de retenção para atender às suas necessidades comerciais ajustando o TTL. Por exemplo, ao considerar a plataforma de streaming de vídeo mencionada anteriormente, a plataforma pode definir inicialmente o TTL como três meses para garantir novos dados de engajamento para personalização. No entanto, se a análise mostrar que os padrões de interação com mais de três meses ainda fornecem insights valiosos, eles poderão estender o período de TTL para seis meses para manter registros mais antigos para melhores modelos de recomendação.

Para modificar um valor TTL existente, use o método `PATCH` no ponto de extremidade `/v2/datasets/{DATASET_ID}`.

#### Formato da API

```http
PATCH /v2/datasets/{DATASET_ID}
```

**Solicitação**

Na solicitação a seguir, o TTL é atualizado para seis meses (`P6M`), estendendo o período de retenção de registros antes da exclusão automática.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -h 'Authorization: Bearer {ACCESS_TOKEN}' \
  -h 'Content-Type: application/json' \
  -h 'x-api-key: {API_KEY}' \
  -h 'x-gw-ims-org-id: {ORG_ID}' \
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

<!-- Q) For Clarity, should this example show both data stores being updated by expanding the example payload above? -->

**Resposta**

```JSON
{  "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
              "ttlValue": "P6M",
              "valueStatus": "custom",
              "setBy": "user",
              "updated": "1737977766499"
            }
        },
        "adobe_unifiedProfile": {
            "rowExpiration": {
                "ttlValue": "P3M",
                "valueStatus": "custom",
                "setBy": "user",
                "updated": "17379754766355"
            }
        }
    }
}
```

## Práticas recomendadas para definir o TTL {#best-practices}

Escolher o valor TTL correto é fundamental para garantir que sua política de retenção do conjunto de dados do evento de experiência equilibre a retenção de dados, a eficiência do armazenamento e as necessidades analíticas. Um TTL muito curto pode causar perda de dados, enquanto um TTL muito longo pode aumentar os custos de armazenamento e o acúmulo desnecessário de dados. Verifique se o TTL está alinhado à finalidade do seu conjunto de dados, considerando a frequência com que os dados são acessados e por quanto tempo permanecem relevantes.

A tabela abaixo fornece recomendações comuns de TTL com base no tipo de conjunto de dados e nos padrões de uso:

| Tipo de conjunto de dados | TTL recomendado | Casos de uso típicos |
|-----------------------------|------------------------|-------------------|
| Conjuntos de dados acessados com frequência | 30 a 90 dias | Registros de engajamento do usuário, dados de sequência de cliques do site, dados de desempenho de campanha de curto prazo. |
| Conjuntos de dados de arquivamento | 1 ano ou mais | Registros de transações financeiras, dados de conformidade, análise de tendências a longo prazo, conjuntos de dados de treinamento de aprendizado de máquina. |
| Conjuntos de dados gerenciados por aplicativo | Até 13 meses | Os conjuntos de dados gerenciados pelo sistema têm restrições TTL predefinidas, que são automaticamente impostas para cumprir os limites impostos pelo sistema. |
| Conjuntos de dados gerenciados pelo cliente | 30 dias - TTL máximo | Conjuntos de dados criados por meio da interface, das APIs ou do Data Distiller. O TTL deve ser de pelo menos 30 dias e estar dentro do TTL máximo definido. |

Revise as configurações de TTL periodicamente para garantir que elas continuem alinhadas às suas políticas de armazenamento, necessidades analíticas e requisitos de negócios.

### Considerações principais ao definir o TTL

<!-- What are the default TTL limits for system-generated Profile Store and data lake datasets? -->

<!-- Q) Are the limits: 90 days for data in the Profile store and 13 months for data in the data lake? This is true for Journey Optimizer. -->

Siga estas práticas recomendadas para garantir que as configurações de TTL se alinhem à sua estratégia de retenção de dados:

- Auditoria de alterações de TTL regularmente. Cada atualização de TTL aciona um evento de auditoria. Use logs de auditoria para rastrear modificações do TTL para fins de conformidade, governança de dados e solução de problemas.
- Remova o TTL se os dados precisarem ser retidos indefinidamente. Para desabilitar o TTL, defina `ttlValue` como `null`. Isso impede a expiração automática e retém todos os registros permanentemente. Considere as implicações de armazenamento antes de fazer essa alteração.

<!-- Q) Are there any specific system constraints or impacts of setting TTL to null? -->

## Limitações do TTL {#limitations}

Esteja ciente das seguintes limitações ao usar TTL:

- **A Retenção do Conjunto de Dados de Evento de Experiência usando TTL se aplica à expiração em nível de linha**, não à exclusão do conjunto de dados. O TTL remove registros com base em um período de retenção definido, mas não exclui conjuntos de dados inteiros. Para remover um conjunto de dados, use o [ponto de extremidade de expiração do conjunto de dados](../../hygiene/api/dataset-expiration.md) ou a exclusão manual.
- **O TTL não pode ser removido**, apenas atualizado. Depois de aplicado, o TTL não pode ser excluído, mas você pode [modificar o período de retenção](#update-ttl) para estendê-lo ou reduzi-lo. Para reter dados indefinidamente, defina um TTL longo o suficiente em vez de tentar removê-lo.
- **TTL não é uma ferramenta de conformidade**. O TTL otimiza o gerenciamento do armazenamento e do ciclo de vida dos dados, mas não atende aos requisitos normativos de retenção de dados. Para conformidade, implemente estratégias mais amplas de controle de dados.

## Perguntas frequentes sobre a política de retenção do conjunto de dados {#faqs}

Esta seção fornece respostas para perguntas frequentes sobre as políticas de retenção de conjuntos de dados na Adobe Experience Platform.

### A quais tipos de conjuntos de dados posso aplicar regras de política de retenção?

+++Resposta
Você pode aplicar políticas de retenção a conjuntos de dados criados usando a classe XDM ExperienceEvent. Para serviços de Perfil, as políticas de retenção são aplicáveis somente a conjuntos de dados de Evento de experiência que foram habilitados para perfil.
+++

### Quando o trabalho de Retenção de conjunto de dados excluirá os dados dos serviços do data lake?

+++Resposta
Os TTLs do conjunto de dados são avaliados e processados semanalmente, excluindo todos os registros expirados. Um evento será considerado expirado se tiver sido assimilado na Experience Platform há mais de 30 dias (data de assimilação > 30 dias) e sua data de evento exceder o período de retenção definido (TTL).
+++

### Quando o trabalho de Retenção de conjunto de dados excluirá os dados dos serviços de perfil?

+++Resposta
Depois que uma política de retenção é definida, os eventos existentes no Experience Platform são imediatamente excluídos se o carimbo de data e hora do evento exceder o período de retenção (TTL). Novos eventos são excluídos assim que o carimbo de data e hora ultrapassar o período de retenção.

Por exemplo, se você aplicar uma política de expiração de 30 dias em 15 de maio, ocorre o seguinte:

- Os novos eventos recebem uma expiração de 30 dias à medida que são assimilados.
- Os eventos existentes com um carimbo de data e hora anterior a 15 de abril são excluídos imediatamente.
- Os eventos existentes com um carimbo de data e hora após 15 de abril são definidos para expirar 30 dias após seu carimbo de data e hora (por exemplo, um evento de 18 de abril seria excluído em 18 de maio).
+++

### Posso definir políticas de retenção diferentes para data lake e serviços de perfil?

+++Resposta
Sim, você pode definir políticas de retenção diferentes para os serviços de perfil e data lake. No entanto, o período de retenção do Perfil não deve ser menor que o definido para o data lake.
+++

### Como posso verificar o uso do meu conjunto de dados atual?

+++Resposta
Você pode verificar o tamanho de armazenamento do conjunto de dados mais recente para armazenamentos de data lake e Perfil como métricas separadas no espaço de trabalho de inventário [!UICONTROL Conjunto de dados]. Classifique as colunas para identificar os maiores conjuntos de dados e verificar se as políticas de retenção foram aplicadas.

Para uso em nível de sandbox, consulte o Painel de uso da licença. Consulte a [documentação de Uso da Licença](../../dashboards/guides/license-usage.md) para obter detalhes.
+++

### Como posso verificar se o trabalho de retenção de dados foi bem-sucedido?

+++Resposta
Você pode verificar o último trabalho de retenção de dados verificando o carimbo de data/hora na [Interface de Usuário de Configuração de Retenção de Conjunto de Dados](./user-guide.md#data-retention-policy) ou na página Inventário de Dados.

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
