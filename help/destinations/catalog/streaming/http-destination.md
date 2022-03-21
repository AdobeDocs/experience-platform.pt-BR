---
keywords: transmissão contínua;
title: Conexão da API HTTP
description: O destino da API HTTP no Adobe Experience Platform permite enviar dados do perfil para pontos de extremidade HTTP de terceiros.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: c2e726a7e66267bf8f301014ae30dedd7472c693
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 1%

---

# Conexão da API HTTP (Beta)

>[!IMPORTANT]
>
>O destino da API HTTP no Platform está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

## Visão geral {#overview}

O destino da API HTTP é um [!DNL Adobe Experience Platform] destino de fluxo que ajuda a enviar dados de perfil para pontos de extremidade HTTP de terceiros.

Para enviar dados de perfil para pontos de extremidade HTTP, primeiro é necessário [conectar-se ao destino](#connect-destination) em [!DNL Adobe Experience Platform].

## Casos de uso {#use-cases}

O destino HTTP é direcionado para clientes que precisam exportar dados de perfil XDM e segmentos de público-alvo para pontos de extremidade HTTP genéricos.

Os endpoints HTTP podem ser sistemas próprios do cliente ou soluções de terceiros.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Pré-requisitos {#prerequisites}

>[!IMPORTANT]
>
>Entre em contato com os representantes do Adobe ou com o Atendimento ao cliente do Adobe se desejar ativar a funcionalidade beta de destino da API HTTP para sua empresa.

Para usar o destino da API HTTP para exportar dados do Experience Platform, você deve atender aos seguintes pré-requisitos:

* Você deve ter um terminal HTTP compatível com REST API.
* Seu terminal HTTP deve oferecer suporte ao esquema de perfil Experience Platform. Nenhuma transformação em um esquema de carga de terceiros é compatível com o destino da API HTTP. Consulte a [dados exportados](#exported-data) para obter um exemplo do schema de saída Experience Platform.
* Seu terminal HTTP deve suportar cabeçalhos.
* Seu ponto de extremidade HTTP deve ser compatível com [Credenciais do cliente OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) autenticação. Esse requisito é válido enquanto o destino da API HTTP está na fase beta.
* A credencial do cliente precisa ser incluída no corpo das solicitações do POST para o terminal, conforme mostrado no exemplo abaixo.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```


Você também pode usar [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) para configurar uma integração e enviar dados de perfil do Experience Platform para um endpoint HTTP.

## Conecte-se ao destino {#connect-destination}

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL httpEndpoint]**: o [!DNL URL] do endpoint HTTP para o qual você deseja enviar os dados do perfil.
   * Opcionalmente, é possível adicionar parâmetros de consulta à variável [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: o [!DNL URL] do endpoint HTTP usado para [!DNL OAuth2] autenticação.
* **[!UICONTROL ID do cliente]**: o [!DNL clientID] utilizado na variável [!DNL OAuth2] credenciais do cliente.
* **[!UICONTROL Segredo do cliente]**: o [!DNL clientSecret] utilizado na variável [!DNL OAuth2] credenciais do cliente.

   >[!NOTE]
   >
   >Somente [!DNL OAuth2] no momento, as credenciais do cliente são compatíveis.

* **[!UICONTROL Nome]**: insira um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: insira uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Cabeçalhos personalizados]**: insira quaisquer cabeçalhos personalizados que você deseja incluir nas chamadas de destino, seguindo este formato: `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >A implementação atual requer pelo menos um cabeçalho personalizado. Essa limitação será resolvida em uma atualização futura.

## Ativar segmentos para este destino {#activate}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil de fluxo](../../ui/activate-streaming-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Atributos de destino {#attributes}

No [[!UICONTROL Selecionar atributos]](../../ui/activate-streaming-profile-destinations.md#select-attributes) , o Adobe recomenda selecionar um identificador exclusivo de [schema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que deseja exportar para o destino.

## Considerações sobre o produto {#product-considerations}

O Experience Platform não faz o stream de dados para pontos de extremidade HTTP por meio de um conjunto fixo de IPs estáticos. Portanto, o Adobe não pode fornecer uma lista de IPs estáticos que você pode lista de permissões para o destino da API HTTP.

## Comportamento de exportação de perfil {#profile-export-behavior}

O Experience Platform otimiza o comportamento de exportação do perfil para o destino da API HTTP, a fim de exportar apenas dados para o ponto de extremidade da API quando ocorrerem atualizações relevantes para um perfil após a qualificação de segmento ou outros eventos significativos. Os perfis são exportados para o seu destino nas seguintes situações:

* A atualização de perfil foi determinada por uma alteração na associação de segmento para pelo menos um dos segmentos mapeados para o destino. Por exemplo, o perfil se qualificou para um dos segmentos mapeados para o destino ou saiu de um dos segmentos mapeados para o destino.
* A atualização do perfil foi determinada por uma alteração no [mapa de identidade](/help/xdm/field-groups/profile/identitymap.md). Por exemplo, um perfil que já se qualificou para um dos segmentos mapeados para o destino foi adicionado a uma nova identidade no atributo do mapa de identidade.
* A atualização do perfil foi determinada por uma alteração nos atributos para pelo menos um dos atributos mapeados para o destino. Por exemplo, um dos atributos mapeados para o destino na etapa de mapeamento é adicionado a um perfil.

Em todos os casos descritos acima, somente os perfis onde as atualizações relevantes ocorreram são exportados para o seu destino. Por exemplo, se um segmento mapeado para o fluxo de destino tiver cem membros e cinco novos perfis se qualificarem para o segmento, a exportação para o seu destino será incremental e incluirá apenas os cinco novos perfis.

Observe que todos os atributos mapeados são exportados para um perfil, independentemente de onde as alterações se encontrem. Portanto, no exemplo acima, todos os atributos mapeados para esses cinco novos perfis serão exportados mesmo se os atributos em si não tiverem sido alterados.

### O que determina uma exportação de dados e o que está incluído na exportação {#what-determines-export-what-is-included}

Com relação aos dados exportados para um determinado perfil, é importante entender os dois conceitos diferentes de *o que determina uma exportação de dados para o destino da API HTTP* e *que dados estão incluídos na exportação*.

| O que determina uma exportação de destino | O que está incluído na exportação de destino |
|---------|----------|
| <ul><li>Atributos e segmentos mapeados servem como a dica para uma exportação de destino. Isso significa que, se qualquer segmento mapeado alterar estados (de nulo para realizado ou de realizado/existente para existente) ou se qualquer atributo mapeado for atualizado, uma exportação de destino será iniciada.</li><li>Como as identidades não podem ser mapeadas no momento para destinos da API HTTP, as alterações em qualquer identidade em um determinado perfil também determinam as exportações de destino.</li><li>Uma alteração para um atributo é definida como qualquer atualização no atributo, independentemente de ser ou não o mesmo valor. Isso significa que uma substituição em um atributo é considerada uma alteração mesmo que o valor em si não tenha sido alterado.</li></ul> | <ul><li>Todos os segmentos (com o status de associação mais recente), independentemente de estarem ou não mapeados no fluxo de dados, são incluídos na variável `segmentMembership` objeto.</li><li>Todas as identidades na `identityMap` também são incluídos (no momento, o Experience Platform não suporta mapeamento de identidade no destino da API HTTP).</li><li>Somente os atributos mapeados são incluídos na exportação de destino.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Por exemplo, considere esse fluxo de dados como um destino HTTP, onde três segmentos são selecionados no fluxo de dados e quatro atributos são mapeados para o destino.

![Fluxo de dados de destino da API HTTP](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Uma exportação de perfil para o destino pode ser determinada por um perfil que se qualifica para ou sai de um dos *três segmentos mapeados*. No entanto, na exportação de dados, no `segmentMembership` objeto (consulte [Dados exportados](#exported-data) seção abaixo), outros segmentos não mapeados podem aparecer, se esse perfil específico for membro deles. Se um perfil se qualificar para o segmento Cliente com Carros coreanos, mas também for membro do filme &quot;Voltar ao futuro&quot; assistido e dos segmentos de fãs de ficção científica, esses dois outros segmentos também estarão presentes `segmentMembership` objeto da exportação de dados, mesmo que não estejam mapeados no fluxo de dados.

Do ponto de vista dos atributos do perfil, qualquer alteração nos quatro atributos mapeados acima determinará uma exportação de destino e qualquer um dos quatro atributos mapeados presentes no perfil estará presente na exportação de dados.

## Dados exportados {#exported-data}

Seu exportado [!DNL Experience Platform] os dados chegam ao seu [!DNL HTTP] destino no formato JSON. Por exemplo, a exportação abaixo contém um perfil que se qualificou para um determinado segmento, é um membro de outros dois segmentos e saiu de outro segmento. A exportação também inclui o atributo de perfil nome, sobrenome, data de nascimento e endereço de email pessoal. As identidades desse perfil são ECID e email.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
      }
   }
},
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
