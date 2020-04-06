---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tarefas
topic: developer guide
translation-type: tm+mt
source-git-commit: cde7acc2fd112b9a5d0b86b40b3bc712c6505064

---


# Tarefas de privacidade

As seções a seguir percorrem as chamadas que você pode fazer usando o terminal raiz (`/`) na API do Privacy Service. Cada chamada inclui o formato de API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

## Criar um trabalho de privacidade

Antes de criar uma nova solicitação de cargo, é necessário coletar primeiro informações de identificação sobre as pessoas cujos dados você deseja acessar, excluir ou opt out de venda. Depois que você tiver os dados necessários, eles deverão ser fornecidos na carga de uma solicitação POST para o terminal raiz.

>[!NOTE] Os aplicativos compatíveis da Adobe Experience Cloud usam valores diferentes para identificar os indivíduos de dados. Consulte o guia sobre o [Privacy Service e os aplicativos](../experience-cloud-apps.md) da Experience Cloud para obter mais informações sobre os identificadores necessários para seus aplicativos.

A API Privacy Service suporta dois tipos de solicitações de trabalho para dados pessoais:

* [Acesso e/ou eliminação](#access-delete): Acesse (leia) ou exclua dados pessoais.
* [Opt out de venda](#opt-out): Marcar dados pessoais como não vendidos.

>[!IMPORTANT] Embora as solicitações de acesso e exclusão possam ser combinadas como uma única chamada de API, as solicitações de cancelamento devem ser feitas separadamente.

### Criar um trabalho de acesso/exclusão {#access-delete}

Esta seção demonstra como fazer uma solicitação de trabalho de acesso/exclusão usando a API.

**Formato da API**

```http
POST /
```

**Solicitação**

A solicitação a seguir cria uma nova solicitação de cargo, configurada pelos atributos fornecidos na carga, conforme descrito abaixo.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| Propriedade | Descrição |
| --- | --- |
| `companyContexts` **(Obrigatório)** | Uma matriz que contém informações de autenticação para sua organização. Cada identificador listado inclui os seguintes atributos: <ul><li>`namespace`: A namespace de um identificador.</li><li>`value`: O valor do identificador.</li></ul>É **necessário** que um dos identificadores use `imsOrgId` como seu `namespace`, com `value` a ID exclusiva para sua Organização IMS. <br/><br/>Identificadores adicionais podem ser qualificadores de empresa específicos do produto (por exemplo, `Campaign`), que identificam uma integração com um aplicativo da Adobe pertencente à sua organização. Os valores potenciais incluem nomes de conta, códigos de cliente, IDs de locatário ou outros identificadores de aplicativo. |
| `users` **(Obrigatório)** | Uma matriz que contém uma coleção de pelo menos um usuário cujas informações você gostaria de acessar ou excluir. É possível fornecer no máximo 1000 IDs de usuário em uma única solicitação. Cada objeto de usuário contém as seguintes informações: <ul><li>`key`: Um identificador usado para qualificar as IDs de trabalho separadas nos dados de resposta. É prática recomendada escolher uma string exclusiva e facilmente identificável para esse valor, para que possa ser facilmente referenciada ou pesquisada posteriormente.</li><li>`action`: Um storage que lista as ações desejadas para executar os dados. Dependendo das ações que você deseja realizar, essa matriz deve incluir `access`, `delete`ou ambos.</li><li>`userIDs`: Uma coleção de identidades para um usuário específico. O número de identidades que um único usuário pode ter está limitado a nove. Cada identidade consiste em um qualificador `namespace`, um `value`e um qualificador de namespace (`type`). Consulte o [apêndice](appendix.md) para obter mais detalhes sobre essas propriedades necessárias.</li></ul> |
| `include` **(Obrigatório)** | Uma matriz de produtos da Adobe a serem incluídos no seu processamento. Se esse valor estiver ausente ou vazio, a solicitação será rejeitada. Inclua somente os produtos com os quais sua organização tem uma integração. Para mais informações, consulte a seção sobre valores [de produtos](appendix.md) aceites no apêndice. |
| `expandIDs` | Uma propriedade opcional que, quando definida como `true`, representa uma otimização para o processamento das IDs nos aplicativos (atualmente apenas compatível com o Analytics). If omitted, this value defaults to `false`. |
| `priority` | Uma propriedade opcional usada pelo Adobe Analytics que define a prioridade para o processamento de solicitações. Os valores aceitos são `normal` e `low`. Se `priority` for omitido, o comportamento padrão será `normal`. |
| `analyticsDeleteMethod` | Uma propriedade opcional que especifica como o Adobe Analytics deve lidar com os dados pessoais. Dois valores possíveis são aceitos para este atributo: <ul><li>`anonymize`: Todos os dados referenciados pela coleção específica de IDs de usuário são tornados anônimos. Se `analyticsDeleteMethod` for omitido, esse é o comportamento padrão.</li><li>`purge`: Todos os dados são completamente removidos.</li></ul> |
| `regulation` **(Obrigatório)** | O regulamento do pedido. Deve ser um dos três valores a seguir: <ul><li>gdpr</li><li>ccpa</li><li>pdpa_tha</li></ul> |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes dos trabalhos recém-criados.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076be029f3",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd023j1",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "delete"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 3
}
```

| Propriedade | Descrição |
| --- | --- |
| `jobId` | Uma ID gerada pelo sistema exclusiva e somente leitura para um trabalho. Esse valor é usado na próxima etapa da pesquisa de um trabalho específico. |

Depois de submeter a solicitação de emprego com êxito, você pode prosseguir para a próxima etapa de [verificação do status](#check-the-status-of-a-job)da tarefa.

### Criar um trabalho de não participação na venda {#opt-out}

Esta seção demonstra como fazer uma solicitação de trabalho de não participação usando a API.

**Formato da API**

```http
POST /
```

**Solicitação**

A solicitação a seguir cria uma nova solicitação de cargo, configurada pelos atributos fornecidos na carga, conforme descrito abaixo.

```shell
curl -X POST \
  https://platform.adobe.io/data/privacy/gdpr/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["opt-out-of-sale"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["opt-out-of-sale"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| Propriedade | Descrição |
| --- | --- |
| `companyContexts` **(Obrigatório)** | Uma matriz que contém informações de autenticação para sua organização. Cada identificador listado inclui os seguintes atributos: <ul><li>`namespace`: A namespace de um identificador.</li><li>`value`: O valor do identificador.</li></ul>É **necessário** que um dos identificadores use `imsOrgId` como seu `namespace`, com `value` a ID exclusiva para sua Organização IMS. <br/><br/>Identificadores adicionais podem ser qualificadores de empresa específicos do produto (por exemplo, `Campaign`), que identificam uma integração com um aplicativo da Adobe pertencente à sua organização. Os valores potenciais incluem nomes de conta, códigos de cliente, IDs de locatário ou outros identificadores de aplicativo. |
| `users` **(Obrigatório)** | Uma matriz que contém uma coleção de pelo menos um usuário cujas informações você gostaria de acessar ou excluir. É possível fornecer no máximo 1000 IDs de usuário em uma única solicitação. Cada objeto de usuário contém as seguintes informações: <ul><li>`key`: Um identificador usado para qualificar as IDs de trabalho separadas nos dados de resposta. É prática recomendada escolher uma string exclusiva e facilmente identificável para esse valor, para que possa ser facilmente referenciada ou pesquisada posteriormente.</li><li>`action`: Um storage que lista as ações desejadas para executar os dados. Para solicitações de não participação na venda, a matriz deve conter apenas o valor `opt-out-of-sale`.</li><li>`userIDs`: Uma coleção de identidades para um usuário específico. O número de identidades que um único usuário pode ter está limitado a nove. Cada identidade consiste em um qualificador `namespace`, um `value`e um qualificador de namespace (`type`). Consulte o [apêndice](appendix.md) para obter mais detalhes sobre essas propriedades necessárias.</li></ul> |
| `include` **(Obrigatório)** | Uma matriz de produtos da Adobe a serem incluídos no seu processamento. Se esse valor estiver ausente ou vazio, a solicitação será rejeitada. Inclua somente os produtos com os quais sua organização tem uma integração. Para mais informações, consulte a seção sobre valores [de produtos](appendix.md) aceites no apêndice. |
| `expandIDs` | Uma propriedade opcional que, quando definida como `true`, representa uma otimização para o processamento das IDs nos aplicativos (atualmente apenas compatível com o Analytics). If omitted, this value defaults to `false`. |
| `priority` | Uma propriedade opcional usada pelo Adobe Analytics que define a prioridade para o processamento de solicitações. Os valores aceitos são `normal` e `low`. Se `priority` for omitido, o comportamento padrão será `normal`. |
| `analyticsDeleteMethod` | Uma propriedade opcional que especifica como o Adobe Analytics deve lidar com os dados pessoais. Dois valores possíveis são aceitos para este atributo: <ul><li>`anonymize`: Todos os dados referenciados pela coleção específica de IDs de usuário são tornados anônimos. Se `analyticsDeleteMethod` for omitido, esse é o comportamento padrão.</li><li>`purge`: Todos os dados são completamente removidos.</li></ul> |
| `regulation` **(Obrigatório)** | O regulamento do pedido. Deve ser um dos três valores a seguir: <ul><li>gdpr</li><li>ccpa</li><li>pdpa_tha</li></ul> |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes dos trabalhos recém-criados.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd9vjs0",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bes0ewj2",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 2
}
```

| Propriedade | Descrição |
| --- | --- |
| `jobId` | Uma ID gerada pelo sistema exclusiva e somente leitura para um trabalho. Esse valor é usado para procurar um trabalho específico na próxima etapa. |

Depois de submeter a solicitação de emprego com êxito, você pode prosseguir para a próxima etapa de verificação do status da tarefa.

## Verificar o status de uma tarefa

Usando um dos `jobId` valores retornados na etapa anterior, você pode recuperar informações sobre essa tarefa, como seu status de processamento atual.

>[!IMPORTANT] Os dados para trabalhos criados anteriormente só estão disponíveis para recuperação dentro de 30 dias da data de conclusão do trabalho.

**Formato da API**

```http
GET /{JOB_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{JOB_ID}` | A ID do trabalho que você deseja pesquisar, retornada `jobId` na resposta da etapa [](#create-a-job-request)anterior. |

**Solicitação**

A solicitação a seguir recupera os detalhes da tarefa `jobId` fornecida no caminho da solicitação.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da tarefa especificada.

```json
{
    "jobId": "527ef92d-6cd9-45cc-9bf1-477cfa1e2ca2",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "error",
    "submittedBy": "02b38adf-6573-401e-b4cc-6b08dbc0e61c@techacct.adobe.com",
    "createdDate": "10/02/2019 08:25 PM GMT",
    "lastModifiedDate": "10/02/2019 08:25 PM GMT",
    "userIds": [
        {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard",
            "namespaceId": 6,
            "isDeletedClientSide": false
        },
        {
            "namespace": "ECID",
            "value": "1123A4D5690B32A",
            "type": "standard",
            "namespaceId": 4,
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Analytics",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "submitted",
                "message": "processing"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "submitted",
                "message": "processing"
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| Propriedade | Descrição |
| --- | --- |
| `productStatusResponse` | O status atual da tarefa. Os detalhes sobre cada status possível são fornecidos na tabela abaixo. |
| `downloadURL` | Se o status do trabalho for `complete`, este atributo fornecerá um URL para baixar os resultados do trabalho como um arquivo ZIP. Este arquivo está disponível para download por 60 dias após a conclusão do trabalho. |

### Respostas de status do trabalho

A tabela a seguir lista os diferentes status possíveis da ordem de produção e seu significado correspondente:

| Código de status | Mensagem de status | Significado |
| ----------- | -------------- | -------- |
| 1 | Concluído | O trabalho está concluído e (se necessário) os arquivos são carregados de cada aplicativo. |
| 2 | Processamento | Os aplicativos reconheceram o trabalho e estão sendo processados no momento. |
| 3 | Enviada | O trabalho é submetido a cada solicitação aplicável. |
| 4 | Erro | Ocorreu uma falha no processamento da tarefa - informações mais específicas podem ser obtidas através da recuperação de detalhes da tarefa individual. |

>[!NOTE] Um trabalho enviado pode permanecer em um estado de processamento se ele tiver um trabalho filho dependente que ainda esteja em processamento.

## Lista de todos os trabalhos

Você pode visualização uma lista de todas as solicitações de trabalho disponíveis em sua organização, fazendo uma solicitação GET ao terminal raiz (`/`).

**Formato da API**

Esse formato de solicitação usa um parâmetro de `regulation` query no terminal raiz (`/`), portanto, começa com um ponto de interrogação (`?`), como mostrado abaixo. A resposta é paginada, permitindo que você use outros parâmetros de query (`page` e `size`) para filtrar a resposta. É possível separar vários parâmetros usando os E-mails (`&`).

```http
GET ?regulation={REGULATION}
GET ?regulation={REGULATION}&page={PAGE}
GET ?regulation={REGULATION}&size={SIZE}
GET ?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{REGULATION}` | O tipo de regulamento a ser query. Os valores aceitos são `gdpr`, `ccpa`e `pdpa_tha`. |
| `{PAGE}` | A página de dados a ser exibida, usando a numeração com base em 0. O padrão é `0`. |
| `{SIZE}` | O número de resultados a serem exibidos em cada página. O padrão é `1` e o máximo é `100`. Exceder o máximo faz com que a API retorne um erro de código 400. |

**Solicitação**

A solicitação a seguir recupera uma lista paginada de todos os trabalhos em uma Organização IMS, começando na terceira página com um tamanho de página de 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de jobs, com cada job contendo detalhes como seus `jobId`. Neste exemplo, a resposta conteria uma lista de 50 trabalhos, começando na terceira página de resultados.

### Acessar páginas subsequentes

Para obter o próximo conjunto de resultados em uma resposta paginada, você deve fazer outra chamada de API para o mesmo terminal enquanto aumenta o parâmetro do `page` query em 1.

## Próximas etapas

Agora você sabe como criar e monitorar trabalhos de privacidade usando a API do Privacy Service. Para obter informações sobre como executar as mesmas tarefas usando a interface do usuário, consulte a visão geral [da interface do usuário do](../ui/overview.md)Privacy Service.
