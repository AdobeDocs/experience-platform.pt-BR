---
keywords: transmissão contínua;
title: Conexão da API HTTP
description: O destino da API HTTP no Adobe Experience Platform permite enviar dados do perfil para pontos de extremidade HTTP de terceiros.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: f098df9df2baa971db44a6746949f021e212ae3e
workflow-type: tm+mt
source-wordcount: '833'
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

## Comportamento de exportação de perfil {#profile-export-behavior}

O Experience Platform otimiza o comportamento de exportação do perfil para o destino da API HTTP, a fim de exportar apenas dados para o ponto de extremidade da API quando ocorrerem atualizações relevantes para um perfil após a qualificação de segmento ou outros eventos significativos. Os perfis são exportados para o seu destino nas seguintes situações:

* A atualização de perfil foi acionada por uma alteração na associação de segmento para pelo menos um dos segmentos mapeados para o destino. Por exemplo, o perfil se qualificou para um dos segmentos mapeados para o destino ou saiu de um dos segmentos mapeados para o destino.
* A atualização do perfil foi acionada por uma alteração no [mapa de identidade](/help/xdm/field-groups/profile/identitymap.md). Por exemplo, um perfil que já se qualificou para um dos segmentos mapeados para o destino foi adicionado a uma nova identidade no atributo do mapa de identidade.
* A atualização do perfil foi acionada por uma alteração em atributos para pelo menos um dos atributos mapeados para o destino. Por exemplo, um dos atributos mapeados para o destino na etapa de mapeamento é adicionado a um perfil.

Em todos os casos descritos acima, somente os perfis onde as atualizações relevantes ocorreram são exportados para o seu destino. Por exemplo, se um segmento mapeado para o fluxo de destino tiver cem membros e cinco novos perfis se qualificarem para o segmento, a exportação para o seu destino será incremental e incluirá apenas os cinco novos perfis.

Observe que todos os atributos mapeados são exportados para um perfil, independentemente de onde as alterações se encontrem. Portanto, no exemplo acima, todos os atributos mapeados para esses cinco novos perfis serão exportados mesmo se os atributos em si não tiverem sido alterados.

## Dados exportados {#exported-data}

Seu exportado [!DNL Experience Platform] os dados chegam ao seu [!DNL HTTP] destino no formato JSON. Por exemplo, a exportação abaixo contém um perfil que se qualificou para um determinado segmento e saiu de outro segmento, e inclui o nome do atributo de perfil, o sobrenome, a data de nascimento e o endereço de email pessoal. As identidades desse perfil são ECID e email.

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
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
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
