---
title: Criar e ativar um público-alvo externo
type: Tutorial
description: Saiba como criar um público-alvo externo no Adobe Experience Platform usando as APIs do Experience Platform.
source-git-commit: 0a37ef2f5fc08eb515c7c5056936fd904ea6d360
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 3%

---


# Criar e ativar um público externo usando a API

Este tutorial aborda as etapas necessárias para criar um público-alvo externo usando as APIs do Adobe Experience Platform.

## Introdução

Este tutorial requer um entendimento prático dos vários serviços da Experience Platform envolvidos na criação de um público-alvo externo. Antes de começar este tutorial, leia a documentação dos seguintes serviços:

- [Fontes](../../sources/home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): permite que você compile públicos a partir de dados externos.
- [Destinos](../../destinations/home.md): os destinos são integrações pré-criadas com aplicativos comumente usados que permitem a ativação contínua de dados do Experience Platform para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muito mais.

### Cabeçalhos obrigatórios

Este tutorial também requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para as APIs [!DNL Experience Platform]. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. As solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações POST, PUT e PATCH exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Preparar o público externo {#prepare}

Antes de criar um público-alvo externo no Experience Platform, será necessário preparar um arquivo que contenha os dados do público-alvo.

Neste exemplo, você deve usar um arquivo CSV. Verifique se o arquivo CSV contém **pelo menos** uma coluna com um valor de identidade, como ECID, ID de email ou CRM. Além disso, verifique se contém todos os atributos de enriquecimento de que você precisará para segmentação e ativação.

Você também precisará verificar se o arquivo está em conformidade com os requisitos do esquema do Experience Platform. Para obter mais informações sobre como criar um esquema, leia o [tutorial sobre como criar um esquema usando a API](/help/xdm/tutorials/create-schema-api.md) ou o [tutorial sobre como criar um esquema usando a interface](/help/xdm/tutorials/create-schema-ui.md).

Depois de confirmar que o arquivo CSV contém todas as informações necessárias e está em conformidade com o esquema, será necessário carregar o arquivo CSV para o provedor de armazenamento na nuvem para que você possa usar fontes para assimilar os dados na Experience Platform. Para obter mais informações sobre como usar uma fonte de armazenamento na nuvem, leia o [tutorial sobre como explorar opções de armazenamento na nuvem usando a API](/help/sources/tutorials/api/explore/cloud-storage.md) ou a [visão geral das fontes](/help/sources/home.md#cloud-storage).

## Criar um público-alvo externo {#create}

Depois de preparar seu arquivo CSV, você pode iniciar o processo de criação do público-alvo externo.

Você pode criar uma audiência externa fazendo uma solicitação POST para o ponto de extremidade `/external-audience/`.

Ao fazer essa solicitação, você precisará especificar as seguintes informações:

- O nome do público
- Uma descrição para o público
- Os campos correspondentes entre o CSV e o esquema
- As informações de especificação de origem
   - Isso inclui o caminho do arquivo CSV para assimilação
      - O caminho de arquivo **não pode** conter espaços. Por exemplo, se o caminho for `activation/sample-source/Example CSV File.csv`, defina o caminho como `activation/sample-source/ExampleCSVFile.csv`.

Para obter informações mais detalhadas sobre como usar este ponto de extremidade, leia o [manual de ponto de extremidade de públicos externos](/help/segmentation/api/external-audiences.md#create-audience).

+++Solicitação

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

+++

Depois de fazer essa solicitação, anote o `operationId` que você recebe da resposta para que possa recuperar a ID do público-alvo.

## Recuperar ID de público-alvo {#retrieve-audience-id}

Agora que você criou o público-alvo externo, será necessário obter a ID de público-alvo para assimilar o público-alvo no Experience Platform.

Você pode recuperar a ID de público-alvo fazendo uma solicitação GET para o ponto de extremidade `/external-audiences/operations` e fornecendo a ID da operação recebida anteriormente da resposta de criação de público-alvo externo.

Para obter informações mais detalhadas sobre como usar este ponto de extremidade, leia o [manual do ponto de extremidade do público-alvo externo](/help/segmentation/api/external-audiences.md#retrieve-status).

+++ Solicitação

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/{OPERATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

Depois de fazer essa solicitação, anote o `audienceId` que você recebe da resposta para que possa acionar o trabalho de assimilação para o público-alvo.

## Iniciar assimilação de público {#start-ingestion}

Como você tem o `audienceId`, agora é possível acionar a assimilação do público externo na Experience Platform.

Você pode iniciar uma assimilação de público-alvo fazendo uma solicitação POST para o endpoint a seguir ao fornecer a ID do público-alvo. Além disso, será necessário especificar a hora de início para determinar quais arquivos serão processados.

Para obter informações mais detalhadas sobre como usar este ponto de extremidade, leia o [manual do ponto de extremidade de públicos externos](/help/segmentation/api/external-audiences.md#start-audience-ingestion)

+++ Solicitação

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

+++

Depois de fazer essa solicitação, anote o `runId` que você recebe da resposta para que possa monitorar o status de assimilação.

## Monitorar status de assimilação {#monitor-ingestion}

Depois de acionar a assimilação de público-alvo, agora é possível monitorar o progresso da assimilação para confirmar o sucesso da assimilação e validar a disponibilidade do público-alvo para ativação downstream.

Você pode recuperar o status de uma assimilação de público-alvo fazendo uma solicitação GET para o endpoint a seguir enquanto fornece o público-alvo e as IDs de execução.

Para obter informações mais detalhadas sobre como usar este ponto de extremidade, leia o [manual do ponto de extremidade do público-alvo externo](/help/segmentation/api/external-audiences.md#retrieve-ingestion-status).

+++ Solicitação

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs/{RUN_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

## Próximas etapas {#next-steps}

>[!IMPORTANT]
>
>Para usar o público gerado externamente, você **deve** aguardar até que o trabalho diário de segmentação seja concluído.

Depois de confirmar que o público-alvo externo foi assimilado com êxito, você pode vê-lo no Portal de público-alvo e usá-lo em serviços downstream, como destinos.

Para obter mais informações sobre o Audience Portal, leia o [Guia da Interface do Usuário do Audience Portal](/help/segmentation/ui/audience-portal.md). Para obter mais informações sobre destinos, leia a [visão geral sobre destinos](/help/destinations/home.md).

