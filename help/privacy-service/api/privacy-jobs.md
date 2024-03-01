---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Ponto de extremidade da API de trabalhos de privacidade
description: Saiba como gerenciar processos de privacidade para aplicativos Experience Cloud usando a API de Privacy Service.
role: Developer
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: 0ffc9648fbc6e6aa3c43a7125f25a98452e8af9a
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 1%

---

# Ponto de extremidade de trabalhos de privacidade

Este documento aborda como trabalhar com processos de privacidade usando chamadas de API. Mais especificamente, abrange a utilização dos `/job` endpoint na variável [!DNL Privacy Service] API. Antes de ler este guia, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo cabeçalhos necessários e como ler chamadas de API de exemplo.

>[!NOTE]
>
>Se estiver tentando gerenciar solicitações de consentimento ou recusa dos clientes, consulte o [manual de endpoint de consentimento](./consent.md).

## Listar todos os trabalhos {#list}

Você pode exibir uma lista de todos os processos de privacidade disponíveis em sua organização fazendo uma solicitação de GET para a `/jobs` terminal.

**Formato da API**

Este formato de solicitação usa um `regulation` parâmetro de consulta no `/jobs` ponto de extremidade, portanto, começa com um ponto de interrogação (`?`) conforme mostrado abaixo. Ao listar recursos, a API de Privacy Service retorna até 1000 tarefas e pagina a resposta. Usar outros parâmetros de consulta (`page`, `size`e filtros de data) para filtrar a resposta. É possível separar vários parâmetros usando &quot;E&quot; comercial (`&`).

>[!TIP]
>
>Use parâmetros de consulta adicionais para filtrar ainda mais os resultados de consultas específicas. Por exemplo, você pode descobrir quantos trabalhos de privacidade foram enviados em um determinado período e qual status está usando o `status`, `fromDate`, e `toDate` parâmetros de consulta.

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
GET /jobs?regulation={REGULATION}&fromDate={FROMDATE}&toDate={TODATE}&status={STATUS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{REGULATION}` | O tipo de regulamento a ser consultado. Os valores aceitos incluem: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpa`</li><li>`cpra_usa`</li><li>`ctdpa`</li><li>`ctdpa_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`mhmda`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`ucpa_usa`</li><li>`vcdpa_usa`</li></ul><br>Consulte a visão geral em [regulamentos suportados](../regulations/overview.md) para obter mais informações sobre as regras de privacidade que os valores acima representam. |
| `{PAGE}` | A página de dados a ser exibida, usando a numeração com base em 0. O padrão é `0`. |
| `{SIZE}` | O número de resultados a serem exibidos em cada página. O padrão é `100` e o máximo é `1000`. Exceder o máximo faz com que a API retorne um erro de código 400. |
| `{status}` | O comportamento padrão é incluir todos os status. Se você especificar um tipo de status, a solicitação retornará somente os processos de privacidade que correspondam a esse tipo de status. Os valores aceitos incluem: <ul><li>`processing`</li><li>`complete`</li><li>`error`</li></ul> |
| `{toDate}` | Esse parâmetro limita os resultados aos processados antes de uma data especificada. A partir da data da solicitação, o sistema pode consultar 45 dias. No entanto, o intervalo não pode ser superior a 30 dias.<br>Ele aceita o formato AAAA-MM-DD. A data fornecida é interpretada como a data de encerramento expressa no Horário de Greenwich (GMT).<br>Se você não fornecer esse parâmetro (e uma variável `fromDate`), o comportamento padrão retorna tarefas cujos dados foram retornados nos últimos sete dias. Se você usar `toDate`, você também deve usar o `fromDate` parâmetro de consulta. Se você não usar ambos, a chamada retornará um erro 400. |
| `{fromDate}` | Esse parâmetro limita os resultados aos processados após uma data especificada. A partir da data da solicitação, o sistema pode consultar 45 dias. No entanto, o intervalo não pode ser superior a 30 dias.<br>Ele aceita o formato AAAA-MM-DD. A data fornecida é interpretada como a data de origem da solicitação expressa na Hora Média de Greenwich (GMT).<br>Se você não fornecer esse parâmetro (e uma variável `toDate`), o comportamento padrão retorna tarefas cujos dados foram retornados nos últimos sete dias. Se você usar `fromDate`, você também deve usar o `toDate` parâmetro de consulta. Se você não usar ambos, a chamada retornará um erro 400. |
| `{filterDate}` | Esse parâmetro limita os resultados aos processados em uma data especificada. Ele aceita o formato AAAA-MM-DD. O sistema pode analisar os últimos 45 dias. |

{style="table-layout:auto"}

<!-- Not released yet:
<li>`pdpd_vnm`</li> 
 -->

**Solicitação**

A solicitação a seguir recupera uma lista paginada de todos os cargos em uma organização, começando pela terceira página com um tamanho de página de 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de tarefas, com cada tarefa contendo detalhes como `jobId`. Neste exemplo, a resposta conteria uma lista de 50 tarefas, começando na terceira página de resultados.

### Acesso às páginas subsequentes

Para buscar o próximo conjunto de resultados em uma resposta paginada, você deve fazer outra chamada de API para o mesmo endpoint enquanto aumenta o `page` parâmetro de consulta por 1.

## Criar um trabalho de privacidade {#create-job}

>[!IMPORTANT]
>
>O Privacy Service se destina apenas a solicitações de titulares de dados e de direitos do consumidor. Qualquer outro uso do Privacy Service para limpeza ou manutenção de dados não é suportado ou permitido. A Adobe tem a obrigação legal de os cumprir em tempo útil. Dessa forma, o teste de carga no Privacy Service não é permitido, pois é um ambiente somente de produção e cria um backlog desnecessário de solicitações de privacidade válidas.
>
>Um limite rígido de upload diário está em vigor para ajudar a evitar o abuso do serviço. Os usuários que abusam do sistema terão o acesso ao serviço desativado. Uma reunião subsequente será realizada com eles para abordar suas ações e discutir o uso aceitável do Privacy Service.

Antes de criar uma nova solicitação de emprego, primeiro você deve coletar informações de identificação sobre os titulares de dados cujos dados deseja acessar, excluir ou recusar a venda. Depois de obter os dados necessários, eles devem ser fornecidos na carga de uma solicitação POST para o `/jobs` terminal.

>[!NOTE]
>
>Aplicativos compatíveis com o Adobe Experience Cloud usam valores diferentes para identificar titulares de dados. Consulte o guia sobre [aplicativos Privacy Service e Experience Cloud](../experience-cloud-apps.md) para obter mais informações sobre os identificadores necessários para seu(s) aplicativo(s). Para obter uma orientação mais geral sobre como determinar quais IDs enviar para o [!DNL Privacy Service], consulte o documento sobre [dados de identidade em solicitações de privacidade](../identity-data.md).

A variável [!DNL Privacy Service] A API oferece suporte a dois tipos de solicitações de trabalho para dados pessoais:

* [Acessar e/ou excluir](#access-delete): Acesse (leia) ou exclua dados pessoais.
* [Recusar venda](#opt-out): marque os dados pessoais como não serão vendidos.

>[!IMPORTANT]
>
>Embora as solicitações de acesso e exclusão possam ser combinadas como uma única chamada de API, as solicitações de recusa devem ser feitas separadamente.

### Criar um trabalho de acesso/exclusão {#access-delete}

Esta seção demonstra como fazer uma solicitação de trabalho de acesso/exclusão usando a API.

**Formato da API**

```http
POST /jobs
```

**Solicitação**

A solicitação a seguir cria uma nova solicitação de trabalho, configurada pelos atributos fornecidos na carga, conforme descrito abaixo.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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
    "include": ["Analytics", "AudienceManager","profileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| Propriedade | Descrição |
| --- | --- |
| `companyContexts` **(Obrigatório)** | Uma matriz que contém informações de autenticação para sua organização. Cada identificador listado inclui os seguintes atributos: <ul><li>`namespace`: O namespace de um identificador.</li><li>`value`: O valor do identificador.</li></ul>É necessário **obrigatório** que um dos identificadores usa `imsOrgId` como seu `namespace`, com as suas `value` contendo o identificador exclusivo da organização. <br/><br/>Identificadores adicionais podem ser qualificadores de empresa específicos do produto (por exemplo, `Campaign`), que identificam uma integração com um aplicativo Adobe pertencente à sua organização. Os valores potenciais incluem nomes de conta, códigos de cliente, IDs de locatário ou outros identificadores de aplicativo. |
| `users` **(Obrigatório)** | Uma matriz que contém uma coleção de pelo menos um usuário cujas informações você deseja acessar ou excluir. Um máximo de 1000 usuários pode ser fornecido em uma única solicitação. Cada objeto de usuário contém as seguintes informações: <ul><li>`key`: um identificador para um usuário que é usado para qualificar as IDs de trabalho separadas nos dados de resposta. É uma prática recomendada escolher uma string exclusiva e de fácil identificação para esse valor, para que ele possa ser facilmente referenciado ou pesquisado posteriormente.</li><li>`action`: uma matriz que lista as ações desejadas para tomar os dados do usuário. Dependendo das ações que você deseja realizar, esse array deve incluir `access`, `delete`, ou ambos.</li><li>`userIDs`: uma coleção de identidades para o usuário. O número de identidades que um único usuário pode ter é limitado a nove. Cada identidade consiste em um `namespace`, um `value`, e um qualificador de namespace (`type`). Consulte a [apêndice](appendix.md) para obter mais detalhes sobre essas propriedades obrigatórias.</li></ul> Para obter uma explicação mais detalhada sobre `users` e `userIDs`, consulte o [guia de solução de problemas](../troubleshooting-guide.md#user-ids). |
| `include` **(Obrigatório)** | Uma matriz de produtos Adobe a serem incluídos no processamento. Se esse valor estiver ausente ou vazio, a solicitação será rejeitada. Inclua somente produtos com os quais sua organização tenha uma integração. Consulte a seção sobre [valores de produto aceitos](appendix.md) no apêndice para obter mais informações. |
| `expandIDs` | Uma propriedade opcional que, quando definida como `true`, representa uma otimização para o processamento de IDs nos aplicativos (atualmente compatível apenas com o [!DNL Analytics]). Se omitido, esse valor assumirá como padrão `false`. |
| `priority` | Uma propriedade opcional usada pelo Adobe Analytics que define a prioridade para processar solicitações. Os valores aceitos são `normal` e `low`. Se `priority` for omitido, o comportamento padrão será `normal`. |
| `analyticsDeleteMethod` | Uma propriedade opcional que especifica como o Adobe Analytics deve lidar com os dados pessoais. Dois valores possíveis são aceitos para este atributo: <ul><li>`anonymize`: todos os dados referenciados pela coleção de IDs de usuário fornecida se tornam anônimos. Se `analyticsDeleteMethod` for omitido, esse será o comportamento padrão.</li><li>`purge`: Todos os dados são removidos completamente.</li></ul> |
| `mergePolicyId` | Ao fazer solicitações de privacidade para o Perfil do cliente em tempo real (`profileService`), você pode fornecer opcionalmente a ID do [política de mesclagem](../../profile/merge-policies/overview.md) que você deseja usar para a compilação de ID. Ao especificar uma política de mesclagem, as solicitações de privacidade podem incluir informações de público-alvo ao retornar dados sobre um cliente. Somente uma política de mesclagem pode ser especificada por solicitação. Se nenhuma política de mesclagem for fornecida, as informações de segmentação não serão incluídas na resposta. |
| `regulation` **(Obrigatório)** | O regulamento para o trabalho de privacidade. Os seguintes valores são aceitos: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>Consulte a visão geral em [regulamentos suportados](../regulations/overview.md) para obter mais informações sobre as regras de privacidade que os valores acima representam. |

{style="table-layout:auto"}

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
| `jobId` | Uma ID exclusiva, somente leitura, gerada pelo sistema para uma tarefa. Esse valor é usado na próxima etapa da pesquisa de uma tarefa específica. |

{style="table-layout:auto"}

Depois de submeter a solicitação de job com sucesso, você pode prosseguir para a próxima etapa do [verificação do status da tarefa](#check-status).

## Verificar o status de um trabalho {#check-status}

É possível recuperar informações sobre um job específico, como seu status de processamento atual, incluindo o `jobId` no caminho de uma solicitação GET para o `/jobs` terminal.

>[!IMPORTANT]
>
>Os dados de jobs criados anteriormente só estarão disponíveis para recuperação dentro de 30 dias da data de conclusão do job.

**Formato da API**

```http
GET /jobs/{JOB_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{JOB_ID}` | A ID do trabalho que você deseja pesquisar. Essa ID é retornada em `jobId` em respostas bem-sucedidas da API para [criação de uma tarefa](#create-job) e [listando todos os trabalhos](#list). |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera os detalhes do job cujo `jobId` é fornecido no caminho da solicitação.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do trabalho especificado.

```json
{
    "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "complete",
    "submittedBy": "{ACCOUNT_ID}",
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
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Finished successfully."
            }
        },
        {
            "product": "Profile",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Success dataSetIds = [5dbb87aad37beb18a96feb61], Failed dataSetIds = []"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6054-200",
                "responseMsgDetail": "PARTIALLY COMPLETED- Data not found for some requests, check results for more info.",
                "results": {
                  "processed": ["1123A4D5690B32A"],
                  "ignored": ["dsmith@acme.com"]
                }
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| Propriedade | Descrição |
| --- | --- |
| `productStatusResponse` | Cada objeto dentro do `productResponses` contém informações sobre o status atual da tarefa em relação a um [!DNL Experience Cloud] aplicação. |
| `productStatusResponse.status` | A categoria de status atual do trabalho. Consulte a tabela abaixo para obter uma lista de [categorias de status disponíveis](#status-categories) e seus significados correspondentes. |
| `productStatusResponse.message` | O status específico do trabalho, correspondente à categoria de status. |
| `productStatusResponse.responseMsgCode` | Um código padrão para mensagens de resposta do produto recebidas por [!DNL Privacy Service]. Os detalhes da mensagem são fornecidos em `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Uma explicação mais detalhada do status da tarefa. As mensagens para status semelhantes podem variar entre os produtos. |
| `productStatusResponse.results` | Para certos status, alguns produtos podem retornar uma `results` objeto que fornece informações adicionais não abrangidas pelo `responseMsgDetail`. |
| `downloadURL` | Se o status do job for `complete`, este atributo fornece um URL para baixar os resultados do processo como um arquivo ZIP. Esse arquivo está disponível para download por 60 dias após a conclusão do trabalho. |

{style="table-layout:auto"}

### Categorias de status de trabalho {#status-categories}

A tabela a seguir lista as diferentes categorias possíveis de status do cargo e o respectivo significado:

| Categoria de status | Significado |
| -------------- | -------- |
| `complete` | O trabalho está concluído e (se necessário) os arquivos são carregados de cada aplicativo. |
| `processing` | Os aplicativos reconheceram a tarefa e estão sendo processados no momento. |
| `submitted` | O processo é enviado a todos os aplicativos aplicáveis. |
| `error` | Ocorreu uma falha no processamento do trabalho - informações mais específicas podem ser obtidas recuperando detalhes do trabalho individuais. |

{style="table-layout:auto"}

>[!NOTE]
>
>Uma tarefa enviada pode permanecer em um `processing` se tiver um trabalho filho dependente que ainda esteja em processamento.

## Próximas etapas

Agora você sabe como criar e monitorar processos de privacidade usando o [!DNL Privacy Service] API. Para obter informações sobre como executar as mesmas tarefas usando a interface, consulte [Visão geral da interface do Privacy Service](../ui/overview.md).
