---
keywords: Experience Platform;api de destino;ativação ad-hoc;ativar segmentos ad-hoc
solution: Experience Platform
title: Ativar segmentos de público para destinos em lote por meio da API de ativação ad-hoc
description: Este artigo ilustra o fluxo de trabalho completo para ativar segmentos de público-alvo por meio da API de ativação ad-hoc, incluindo os trabalhos de segmentação que ocorrem antes da ativação.
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 1%

---

# Ativar segmentos de público-alvo sob demanda para destinos em lote por meio da API de ativação ad-hoc

>[!IMPORTANT]
>
>Após a conclusão da fase Beta, a variável [!DNL ad-hoc activation API] O agora está disponível para todos os clientes do Experience Platform. Na versão do GA, a API foi atualizada para a versão 2. Etapa 4 ([Obter a ID de trabalho de exportação de segmento mais recente](#segment-export-id)) não é mais necessário, pois a API não exige mais a ID de exportação.
>
>Consulte [Executar o trabalho de ativação ad-hoc](#activation-job) mais abaixo neste tutorial para obter mais informações.

## Visão geral {#overview}

A API de ativação ad-hoc permite que os profissionais de marketing ativem programaticamente segmentos de público-alvo para destinos, de forma rápida e eficiente, para situações em que a ativação imediata é necessária.

Use a API de ativação ad-hoc para exportar arquivos completos para o sistema de recepção de arquivos desejado. A ativação de público-alvo ad-hoc é suportada somente pelo [destinos baseados em arquivo em lote](../destination-types.md#file-based).

O diagrama abaixo ilustra o fluxo de trabalho completo para ativar segmentos por meio da API de ativação ad-hoc, incluindo os trabalhos de segmentação que ocorrem na Platform a cada 24 horas.

![ad-hoc-activation](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)



## Casos de uso {#use-cases}

### Vendas ou promoções de Flashes

Um varejista online está preparando uma venda rápida limitada e deseja notificar os clientes em um curto prazo. Por meio da API de ativação ad-hoc do Experience Platform, a equipe de marketing pode exportar segmentos sob demanda e enviar rapidamente emails promocionais para a base de clientes.

### Eventos atuais ou últimas notícias

Um hotel espera intempéries nos dias seguintes, e a equipe quer informar os hóspedes que chegam rapidamente, para que possam planejar de acordo. A equipe de marketing pode usar a API de ativação ad-hoc do Experience Platform para exportar segmentos sob demanda e notificar os convidados.

### Teste de integração

Os gerentes de TI podem usar a API de ativação ad-hoc do Experience Platform para exportar segmentos sob demanda, para que possam testar a integração personalizada com o Adobe Experience Platform e garantir que tudo esteja funcionando corretamente.

## Medidas de proteção {#guardrails}

Lembre-se das seguintes medidas de proteção ao usar a API de ativação ad-hoc.

* Atualmente, cada trabalho de ativação ad-hoc pode ativar até 80 segmentos. Tentar ativar mais de 80 segmentos por trabalho causará falha no trabalho. Esse comportamento está sujeito a alterações em versões futuras.
* Os trabalhos de ativação ad-hoc não podem ser executados em paralelo ao agendado [trabalhos de exportação de segmento](../../segmentation/api/export-jobs.md). Antes de executar um trabalho de ativação ad-hoc, verifique se o trabalho de exportação de segmento agendado foi concluído. Consulte [monitoramento do fluxo de dados de destino](../../dataflows/ui/monitor-destinations.md) para obter informações sobre como monitorar o status dos fluxos de ativação. Por exemplo, se o fluxo de dados de ativação mostrar uma variável **[!UICONTROL Processando]** aguarde a conclusão antes de executar o trabalho de ativação ad-hoc.
* Não execute mais de um trabalho de ativação ad-hoc simultâneo por segmento.

## Considerações de segmentação {#segmentation-considerations}

O Adobe Experience Platform executa tarefas de segmentação programadas uma vez a cada 24 horas. A API de ativação ad-hoc é executada com base nos resultados de segmentação mais recentes.

## Etapa 1: Pré-requisitos {#prerequisites}

Antes de fazer chamadas para as APIs do Adobe Experience Platform, verifique se os seguintes pré-requisitos são atendidos:

* Você tem uma conta da Organização IMS com acesso ao Adobe Experience Platform.
* Sua conta Experience Platform tem o `developer` e `user` funções habilitadas para o perfil de produto API do Adobe Experience Platform. Entre em contato com [Admin Console](../../access-control/home.md) administrador para habilitar essas funções para sua conta.
* Você tem uma Adobe ID. Se você não tiver uma Adobe ID, acesse o [Console do Adobe Developer](https://developer.adobe.com/console) e criar uma nova conta.

## Etapa 2: Coletar credenciais {#credentials}

Para fazer chamadas para APIs da Platform, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Os recursos no Experience Platform podem ser isolados em sandboxes virtuais específicas. Em solicitações para APIs da Platform, é possível especificar o nome e a ID da sandbox em que a operação ocorrerá. Esses parâmetros são opcionais.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no Experience Platform, consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Etapa 3: Criar fluxo de ativação na interface do usuário da Platform {#activation-flow}

Antes de ativar segmentos por meio da API de ativação ad-hoc, primeiro é necessário ter um fluxo de ativação configurado na interface do usuário da Platform para o destino escolhido.

Isso inclui acessar o fluxo de trabalho de ativação, selecionar os segmentos, configurar um agendamento e ativá-los. Você pode usar a interface ou a API para criar um fluxo de ativação:

* [Use a interface do Platform para criar um fluxo de ativação para destinos de exportação de perfil em lote](../ui/activate-batch-profile-destinations.md)
* [Use a API do Serviço de fluxo para se conectar aos destinos de exportação do perfil de lote e ativar dados](../api/connect-activate-batch-destinations.md)

## Etapa 4: obter a ID de trabalho de exportação de segmento mais recente (Não obrigatório na v2) {#segment-export-id}

>[!IMPORTANT]
>
>Na v2 da API de ativação ad-hoc, não é necessário obter a ID do trabalho de exportação de segmento mais recente. Você pode pular esta etapa e prosseguir para a próxima.

Após configurar um fluxo de ativação para o destino em lote, os trabalhos de segmentação programados começam a ser executados automaticamente a cada 24 horas.

Antes de executar o trabalho de ativação ad-hoc, obtenha a ID do trabalho de exportação de segmento mais recente. Você deve passar essa ID na solicitação de trabalho de ativação ad-hoc.

Siga as instruções descritas [aqui](../../segmentation/api/export-jobs.md#retrieve-list) para recuperar uma lista de todos os trabalhos de exportação de segmento.

Na resposta, procure o primeiro registro que inclui a propriedade de schema abaixo.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

A ID do trabalho de exportação de segmento está na `id` como mostrado abaixo.

![ID do trabalho de exportação de segmento](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Etapa 5: Executar o trabalho de ativação ad-hoc {#activation-job}

O Adobe Experience Platform executa tarefas de segmentação programadas uma vez a cada 24 horas. A API de ativação ad-hoc é executada com base nos resultados de segmentação mais recentes.

>[!IMPORTANT]
>
>Observe a seguinte restrição única: Antes de executar um job de ativação ad-hoc, verifique se passaram pelo menos 20 minutos desde o momento em que o segmento foi ativado pela primeira vez, de acordo com o agendamento definido em [Etapa 3 - Criar fluxo de ativação na interface do usuário da Platform](#activation-flow).

Antes de executar um trabalho de ativação ad-hoc, verifique se o trabalho de exportação de segmento agendado para os seus segmentos foi concluído. Consulte [monitoramento do fluxo de dados de destino](../../dataflows/ui/monitor-destinations.md) para obter informações sobre como monitorar o status dos fluxos de ativação. Por exemplo, se o fluxo de dados de ativação mostrar uma variável **[!UICONTROL Processando]** aguarde a conclusão antes de executar o trabalho de ativação ad-hoc para exportar um arquivo completo.

Depois que o trabalho de exportação de segmento for concluído, você poderá acionar a ativação.

>[!NOTE]
>
>Atualmente, cada trabalho de ativação ad-hoc pode ativar até 80 segmentos. Tentar ativar mais de 80 segmentos por trabalho causará falha no trabalho. Esse comportamento está sujeito a alterações em versões futuras.

### Solicitação {#request}

>[!IMPORTANT]
>
>É obrigatório incluir a `Accept: application/vnd.adobe.adhoc.activation+json; version=2` em sua solicitação para usar a v2 da API de ativação ad-hoc.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun' \
--header 'x-gw-ims-org-id: 5555467B5D8013E50A494220@AdobeOrg' \
--header 'Authorization: Bearer {{token}}' \
--header 'x-sandbox-id: 6ef74723-3ee7-46a4-b747-233ee7a6a41a' \
--header 'x-sandbox-name: {sandbox-id}' \
--header 'Accept: application/vnd.adobe.adhoc.activation+json; version=2' \
--header 'Content-Type: application/json' \
--data-raw '{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   }
}'
```

| Propriedade | Descrição |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | As IDs das instâncias de destino para as quais você deseja ativar segmentos. Você pode obter essas IDs na interface do usuário da Platform navegando até **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** e clicando na linha de destino desejada para exibir a ID de destino no painel direito. Para obter mais informações, leia a [documentação do espaço de trabalho de destinos](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | As IDs dos segmentos que você deseja ativar para o destino selecionado. |

{style="table-layout:auto"}

### Solicitação com IDs de exportação (a ser descontinuada) {#request-deprecated}

>[!IMPORTANT]
>
>**Tipo de solicitação obsoleta**. Esse tipo de exemplo descreve o tipo de solicitação para a API versão 1. Na v2 da API de ativação ad-hoc, não é necessário incluir a ID do trabalho de exportação de segmento mais recente.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -d '
{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   },
   "exportIds":[
      "exportId1"
   ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | As IDs das instâncias de destino para as quais você deseja ativar segmentos. Você pode obter essas IDs na interface do usuário da Platform navegando até **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** e clicando na linha de destino desejada para exibir a ID de destino no painel direito. Para obter mais informações, leia a [documentação do espaço de trabalho de destinos](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | As IDs dos segmentos que você deseja ativar para o destino selecionado. |
| <ul><li>`exportId1`</li></ul> | A ID retornada na resposta do [exportação de segmentos](../../segmentation/api/export-jobs.md#retrieve-list) tarefa. Consulte [Etapa 4: obter a ID de trabalho de exportação de segmento mais recente](#segment-export-id) para obter instruções sobre como encontrar essa ID. |

{style="table-layout:auto"}

### Resposta {#response}

Uma resposta bem-sucedida retorna o status HTTP 200.

```shell
{
   "order":[
      {
         "segment":"db8961e9-d52f-45bc-b3fb-76d0382a6851",
         "order":"ef2dcbd6-36fc-49a3-afed-d7b8e8f724eb",
         "statusURL":"https://platform.adobe.io/data/foundation/flowservice/runs/88d6da63-dc97-460e-b781-fc795a7386d9"
      }
   ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `segment` | A ID do segmento ativado. |
| `order` | A ID do destino no qual o segmento foi ativado. |
| `statusURL` | A URL de status do fluxo de ativação. É possível rastrear o progresso do fluxo usando a variável [API do serviço de fluxo](../../sources/tutorials/api/monitor.md). |

{style="table-layout:auto"}

## Manipulação de erros de API {#api-error-handling}

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

### Códigos de erro de API e mensagens específicas para a API de ativação ad-hoc {#specific-error-messages}

Ao usar a API de ativação ad-hoc, você pode encontrar mensagens de erro específicas para esse endpoint da API. Revise a tabela para entender como abordá-los quando eles forem exibidos.

| Mensagem de erro | Resolução |
|---------|----------|
| Execução já em andamento para o segmento `segment ID` para pedido `dataflow ID` com id de execução `flow run ID` | Essa mensagem de erro indica que um fluxo de ativação ad-hoc está em andamento para um segmento. Aguarde a conclusão do trabalho antes de acionar o trabalho de ativação novamente. |
| Segmentos `<segment name>` não fazem parte desse fluxo de dados ou estão fora do intervalo programado! | Essa mensagem de erro indica que os segmentos selecionados para ativação não estão mapeados para o fluxo de dados ou que o agendamento de ativação configurado para os segmentos expirou ou ainda não foi iniciado. Verifique se o segmento é de fato mapeado para o fluxo de dados e se a programação de ativação do segmento se sobrepõe à data atual. |

## Informações relacionadas {#related-information}

* [Conectar-se a destinos em lote e ativar dados usando a API do Serviço de fluxo](/help/destinations/api/connect-activate-batch-destinations.md)
* [(Beta) Exportar arquivos sob demanda para destinos em lote usando a interface do Experience Platform](/help/destinations/ui/export-file-now.md)