---
title: Conexão da API HTTP
keywords: transmissão contínua;
description: Use o destino da API HTTP no Adobe Experience Platform para enviar dados de perfil ao endpoint HTTP de terceiros para executar sua própria análise ou executar quaisquer outras operações necessárias nos dados de perfil exportados do Experience Platform.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: d4a4baf330925d6696f515bf650d86740c18e97c
workflow-type: tm+mt
source-wordcount: '2296'
ht-degree: 0%

---

# Conexão da API HTTP

## Visão geral {#overview}

>[!IMPORTANT]
>
> Este destino só está disponível para [Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clientes.

O destino da API HTTP é um [!DNL Adobe Experience Platform] destino de fluxo que ajuda a enviar dados de perfil para pontos de extremidade HTTP de terceiros.

Para enviar dados de perfil para pontos de extremidade HTTP, primeiro é necessário [conectar-se ao destino](#connect-destination) em [!DNL Adobe Experience Platform].

## Casos de uso {#use-cases}

O destino da API HTTP permite exportar dados de perfil XDM e segmentos de público-alvo para pontos de extremidade HTTP genéricos. Lá, você pode executar suas próprias análises ou executar qualquer outra operação necessária nos dados de perfil exportados do Experience Platform.

Os endpoints HTTP podem ser sistemas próprios do cliente ou soluções de terceiros.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela de mapeamento do [fluxo de trabalho de ativação de destino](../../ui/activate-segment-streaming-destinations.md#mapping). |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Pré-requisitos {#prerequisites}

Para usar o destino da API HTTP para exportar dados do Experience Platform, você deve atender aos seguintes pré-requisitos:

* Você deve ter um terminal HTTP compatível com REST API.
* Seu terminal HTTP deve oferecer suporte ao esquema de perfil Experience Platform. Nenhuma transformação em um esquema de carga de terceiros é compatível com o destino da API HTTP. Consulte a [dados exportados](#exported-data) para obter um exemplo do schema de saída Experience Platform.
* Seu terminal HTTP deve suportar cabeçalhos.

>[!TIP]
>
> Você também pode usar [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) para configurar uma integração e enviar dados de perfil do Experience Platform para um endpoint HTTP.

## Endereço IP lista de permissões {#ip-address-allowlist}

Para atender aos requisitos de segurança e conformidade dos clientes, o Experience Platform fornece uma lista de IPs estáticos que você pode lista de permissões para o destino da API HTTP. Consulte [LISTA DE PERMISSÕES de endereço IP para destinos de transmissão](/help/destinations/catalog/streaming/ip-address-allow-list.md) para obter a lista completa de IPs a serem lista de permissões.

## Tipos de autenticação compatíveis {#supported-authentication-types}

O destino da API HTTP suporta vários tipos de autenticação para o seu ponto de extremidade HTTP:

* Ponto de extremidade HTTP sem autenticação;
* Autenticação do token portador;
* [Credenciais do cliente OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) autenticação com o formulário body, com [!DNL client ID], [!DNL client secret] e [!DNL grant type] no corpo da solicitação HTTP, como mostrado no exemplo abaixo.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [Credenciais do cliente OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) com autorização básica, com um cabeçalho de autorização que contém codificação de URL [!DNL client ID] e [!DNL client secret].

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [Concessão de senha do OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## Conecte-se ao destino {#connect-destination}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). Ao se conectar a esse destino, você deve fornecer as seguintes informações:

### Informações de autenticação {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="Tipo de credenciais do cliente"
>abstract="Selecionar **Formulário de corpo codificado** para incluir a ID do cliente e o segredo do cliente no corpo da solicitação ou **Autorização básica** para incluir a ID do cliente e o segredo do cliente em um cabeçalho de autorização. Veja exemplos na documentação."

#### Autenticação de token portador {#bearer-token-authentication}

Se você selecionar a variável **[!UICONTROL Token de portador]** tipo de autenticação para se conectar ao terminal HTTP, insira os campos abaixo e selecione **[!UICONTROL Ligar ao destino]**:

![Imagem da tela da interface do usuário, onde você pode se conectar ao destino da API HTTP, usando autenticação de token portador](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Token de portador]**: insira o token portador para autenticar no seu local HTTP.

#### Sem autenticação {#no-authentication}

Se você selecionar a variável **[!UICONTROL Nenhum]** tipo de autenticação para se conectar ao terminal HTTP:

![Imagem da tela da interface do usuário na qual você pode se conectar ao destino da API HTTP, sem autenticação](../../assets/catalog/http/http-api-authentication-none.png)

Ao selecionar essa autenticação aberta, você só precisa selecionar **[!UICONTROL Ligar ao destino]** e a conexão com seu terminal é estabelecida.

#### Autenticação de senha OAuth 2 {#oauth-2-password-authentication}

Se você selecionar a variável **[!UICONTROL Senha do OAuth 2]** tipo de autenticação para se conectar ao terminal HTTP, insira os campos abaixo e selecione **[!UICONTROL Ligar ao destino]**:

![Imagem da tela da interface do usuário na qual você pode se conectar ao destino da API HTTP, usando OAuth 2 com autenticação por senha](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL URL do token de acesso]**: O URL do seu lado que emite tokens de acesso e, opcionalmente, de atualização.
* **[!UICONTROL ID do cliente]**: O [!DNL client ID] que seu sistema atribui à Adobe Experience Platform.
* **[!UICONTROL Segredo do cliente]**: O [!DNL client secret] que seu sistema atribui à Adobe Experience Platform.
* **[!UICONTROL Nome do usuário]**: O nome de usuário para acessar o terminal HTTP.
* **[!UICONTROL Senha]**: A senha para acessar o terminal HTTP.

#### Autenticação de credenciais de cliente OAuth 2 {#oauth-2-client-credentials-authentication}

Se você selecionar a variável **[!UICONTROL Credenciais do Cliente OAuth 2]** tipo de autenticação para se conectar ao terminal HTTP, insira os campos abaixo e selecione **[!UICONTROL Ligar ao destino]**:

![Imagem da tela da interface do usuário na qual você pode se conectar ao destino da API HTTP, usando OAuth 2 com autenticação de credenciais do cliente](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

* **[!UICONTROL URL do token de acesso]**: O URL do seu lado que emite tokens de acesso e, opcionalmente, de atualização.
* **[!UICONTROL ID do cliente]**: O [!DNL client ID] que seu sistema atribui à Adobe Experience Platform.
* **[!UICONTROL Segredo do cliente]**: O [!DNL client secret] que seu sistema atribui à Adobe Experience Platform.
* **[!UICONTROL Tipo de credenciais do cliente]**: Selecione o tipo de concessão de Credenciais do Cliente OAuth2 com suporte do seu ponto de extremidade:
   * **[!UICONTROL Formulário de corpo codificado]**: Nesse caso, a variável [!DNL client ID] e [!DNL client secret] estão incluídos *no corpo do pedido* enviado para o seu destino. Para ver um exemplo, consulte a [Tipos de autenticação compatíveis](#supported-authentication-types) seção.
   * **[!UICONTROL Autorização básica]**: Nesse caso, a variável [!DNL client ID] e [!DNL client secret] estão incluídos *em um `Authorization` header* depois de ser codificado em base64 e enviado para seu destino. Para ver um exemplo, consulte a [Tipos de autenticação compatíveis](#supported-authentication-types) seção.

### Detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="Cabeçalhos"
>abstract="Insira quaisquer cabeçalhos personalizados que você deseja incluir nas chamadas de destino, seguindo este formato: `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="Endpoint HTTP"
>abstract="O URL do endpoint HTTP para o qual você deseja enviar os dados do perfil."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="Incluir nomes de segmentos"
>abstract="Alterne se deseja que a exportação de dados inclua os nomes dos segmentos que você está exportando. Visualize a documentação de um exemplo de exportação de dados com esta opção selecionada."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="Incluir carimbos de data e hora do segmento"
>abstract="Alterne se deseja que a exportação de dados inclua o carimbo de data e hora UNIX quando os segmentos foram criados e atualizados, bem como o carimbo de data e hora UNIX quando os segmentos foram mapeados para o destino para ativação. Visualize a documentação de um exemplo de exportação de dados com esta opção selecionada."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="Parâmetros de consulta"
>abstract="Opcionalmente, é possível adicionar parâmetros de consulta ao URL do ponto de extremidade HTTP. Formate os parâmetros de consulta usados desta forma: `parameter1=value&parameter2=value`."

Depois de estabelecer a conexão de autenticação com o endpoint HTTP, forneça as seguintes informações para o destino:

![Imagem da tela da interface do usuário mostrando campos preenchidos para os detalhes do destino HTTP](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Nome]**: Insira um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Insira uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Cabeçalhos]**: Insira quaisquer cabeçalhos personalizados que você deseja incluir nas chamadas de destino, seguindo este formato: `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL Endpoint HTTP]**: O URL do endpoint HTTP para o qual você deseja enviar os dados do perfil.
* **[!UICONTROL Parâmetros de consulta]**: Opcionalmente, é possível adicionar parâmetros de consulta ao URL do ponto de extremidade HTTP. Formate os parâmetros de consulta usados desta forma: `parameter1=value&parameter2=value`.
* **[!UICONTROL Incluir nomes de segmentos]**: Alterne se deseja que a exportação de dados inclua os nomes dos segmentos que você está exportando. Para obter um exemplo de exportação de dados com essa opção selecionada, consulte [Dados exportados](#exported-data) mais abaixo.
* **[!UICONTROL Incluir carimbos de data e hora do segmento]**: Alterne se deseja que a exportação de dados inclua o carimbo de data e hora UNIX quando os segmentos foram criados e atualizados, bem como o carimbo de data e hora UNIX quando os segmentos foram mapeados para o destino para ativação. Para obter um exemplo de exportação de dados com essa opção selecionada, consulte [Dados exportados](#exported-data) mais abaixo.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil de fluxo](../../ui/activate-streaming-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Atributos de destino {#attributes}

No [[!UICONTROL Selecionar atributos]](../../ui/activate-streaming-profile-destinations.md#select-attributes) , o Adobe recomenda selecionar um identificador exclusivo de [schema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que deseja exportar para o destino.

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

## Preenchimento retroativo de dados históricos {#historical-data-backfill}

Ao adicionar um novo segmento a um destino existente ou ao criar um novo destino e mapear segmentos a ele, o Experience Platform exporta os dados de qualificação de segmento históricos para o destino. Perfis que se qualificaram para o segmento *before* o segmento adicionado ao destino é exportado para o destino dentro de aproximadamente uma hora.

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

Abaixo estão outros exemplos de dados exportados, dependendo das configurações da interface do usuário selecionadas no fluxo de destino de conexão para a variável **[!UICONTROL Incluir nomes de segmentos]** e **[!UICONTROL Incluir carimbos de data e hora do segmento]** opções:

+++ A amostra de exportação de dados abaixo inclui nomes de segmentos na `segmentMembership` seção

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ A amostra de exportação de dados abaixo inclui carimbos de data e hora do segmento na `segmentMembership` seção

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Limites e política de repetição {#limits-retry-policy}

Em 95% das vezes, o Experience Platform tenta oferecer uma latência de taxa de transferência inferior a 10 minutos para mensagens enviadas com êxito com uma taxa inferior a 10.000 solicitações por segundo para cada fluxo de dados para um destino HTTP.

No caso de solicitações com falha no destino da API HTTP, o Experience Platform armazena as solicitações com falha e tenta novamente duas vezes para enviar as solicitações para o terminal.