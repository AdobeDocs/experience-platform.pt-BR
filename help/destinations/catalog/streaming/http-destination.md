---
keywords: transmissão; destino HTTP
title: Conexão da API HTTP
description: Use o destino da API HTTP no Adobe Experience Platform para enviar dados de perfil para um endpoint HTTP de terceiros para executar sua própria análise ou executar outras operações necessárias nos dados de perfil exportados do Experience Platform.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 72225ac673ed921b5857a14070660134949e7e3e
workflow-type: tm+mt
source-wordcount: '2466'
ht-degree: 8%

---

# Conexão da API HTTP

## Visão geral {#overview}

>[!IMPORTANT]
>
> Este destino está disponível somente para [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=pt-BR) clientes.

O destino da API HTTP é um [!DNL Adobe Experience Platform] destino de transmissão que ajuda a enviar dados do perfil para endpoints HTTP de terceiros.

Para enviar dados de perfil para endpoints HTTP, primeiro você deve [conectar ao destino](#connect-destination) in [!DNL Adobe Experience Platform].

## Casos de uso {#use-cases}

O destino da API HTTP permite exportar dados de perfil XDM e públicos para endpoints HTTP genéricos. Lá, você pode executar suas próprias análises ou executar outras operações que possam ser necessárias nos dados de perfil exportados do Experience Platform.

Os endpoints HTTP podem ser sistemas próprios dos clientes ou soluções de terceiros.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | ✓ | Públicos-alvo [importado](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela de mapeamento do [workflow de ativação de destino](../../ui/activate-segment-streaming-destinations.md#mapping). |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

Para usar o destino da API HTTP para exportar dados do Experience Platform, você deve atender aos seguintes pré-requisitos:

* Você deve ter um endpoint HTTP compatível com REST API.
* Seu ponto de extremidade HTTP deve ser compatível com o esquema do perfil de Experience Platform. Nenhuma transformação em um esquema de carga de terceiros é compatível com o destino da API HTTP. Consulte a [dados exportados](#exported-data) para obter um exemplo do schema de saída Experience Platform.
* Seu ponto de extremidade HTTP deve oferecer suporte a cabeçalhos.

>[!TIP]
>
> Também é possível usar [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) para configurar uma integração e enviar dados de perfil do Experience Platform para um endpoint HTTP.

## INCLUIR NA LISTA DE PERMISSÕES endereço IP {#ip-address-allowlist}

Para atender aos requisitos de segurança e conformidade dos clientes, o Experience Platform fornece uma lista de IPs estáticos que você pode incluir na lista de permissões pelo destino da API HTTP. Consulte [LISTA DE PERMISSÕES de endereço IP para destinos de transmissão](/help/destinations/catalog/streaming/ip-address-allow-list.md) para obter a lista completa de IPs a serem incluídos na lista de permissões.

## Tipos de autenticação compatíveis {#supported-authentication-types}

O destino da API HTTP oferece suporte a vários tipos de autenticação para o terminal HTTP:

* Endpoint HTTP sem autenticação;
* Autenticação do token portador;
* [Credenciais de cliente do OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) autenticação com o formulário do corpo, com [!DNL client ID], [!DNL client secret] e [!DNL grant type] no corpo da solicitação HTTP, como mostrado no exemplo abaixo.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [Credenciais de cliente do OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) com autorização básica, com um cabeçalho de autorização que contém URL codificado [!DNL client ID] e [!DNL client secret].

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [Concessão de senha do OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## Conectar ao destino {#connect-destination}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). Ao se conectar a esse destino, você deve fornecer as seguintes informações:

### Informações de autenticação {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="Tipo de credenciais do cliente"
>abstract="Selecione **Corpo codificado em formato** para incluir a ID do cliente e o segredo do cliente no corpo da solicitação ou **Autorização básica** para incluir a ID do cliente e o segredo do cliente em um cabeçalho de autorização. Veja exemplos na documentação."

#### Autenticação de token do portador {#bearer-token-authentication}

Se você selecionar a variável **[!UICONTROL Token de portador]** tipo de autenticação para se conectar ao terminal HTTP, insira os campos abaixo e selecione **[!UICONTROL Conectar ao destino]**:

![Imagem da tela da interface do usuário na qual é possível se conectar ao destino da API HTTP usando a autenticação de token de portador](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Token de portador]**: insira o token do portador para autenticar no local HTTP.

#### Sem autenticação {#no-authentication}

Se você selecionar a variável **[!UICONTROL Nenhum]** tipo de autenticação para se conectar ao seu ponto de extremidade HTTP:

![Imagem da tela da interface do usuário onde é possível se conectar ao destino da API HTTP sem usar autenticação](../../assets/catalog/http/http-api-authentication-none.png)

Ao selecionar essa autenticação para abrir, você só precisa selecionar **[!UICONTROL Conectar ao destino]** e a conexão com o terminal for estabelecida.

#### Autenticação de senha do OAuth 2 {#oauth-2-password-authentication}

Se você selecionar a variável **[!UICONTROL Senha do OAuth 2]** tipo de autenticação para se conectar ao terminal HTTP, insira os campos abaixo e selecione **[!UICONTROL Conectar ao destino]**:

![Imagem da tela da interface do usuário na qual é possível se conectar ao destino da API HTTP, usando o OAuth 2 com autenticação de senha](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL URL do token de acesso]**: o URL no seu lado que emite tokens de acesso e, opcionalmente, atualiza tokens.
* **[!UICONTROL ID do cliente]**: A variável [!DNL client ID] que seu sistema atribui à Adobe Experience Platform.
* **[!UICONTROL Segredo do cliente]**: A variável [!DNL client secret] que seu sistema atribui à Adobe Experience Platform.
* **[!UICONTROL Nome de usuário]**: o nome de usuário para acessar seu endpoint HTTP.
* **[!UICONTROL Senha]**: a senha para acessar seu ponto de extremidade HTTP.

#### Autenticação de Credenciais de Cliente OAuth 2 {#oauth-2-client-credentials-authentication}

Se você selecionar a variável **[!UICONTROL Credenciais de cliente OAuth 2]** tipo de autenticação para se conectar ao terminal HTTP, insira os campos abaixo e selecione **[!UICONTROL Conectar ao destino]**:

![Imagem da tela da interface do usuário na qual é possível se conectar ao destino da API HTTP, usando o OAuth 2 com autenticação de Credenciais de Cliente](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

* **[!UICONTROL URL do token de acesso]**: o URL no seu lado que emite tokens de acesso e, opcionalmente, atualiza tokens.
* **[!UICONTROL ID do cliente]**: A variável [!DNL client ID] que seu sistema atribui à Adobe Experience Platform.
* **[!UICONTROL Segredo do cliente]**: A variável [!DNL client secret] que seu sistema atribui à Adobe Experience Platform.
* **[!UICONTROL Tipo de credenciais do cliente]**: selecione o tipo de concessão de Credenciais de cliente OAuth2 suportada pelo seu ponto de extremidade:
   * **[!UICONTROL Formulário de corpo codificado]**: Nesse caso, a variável [!DNL client ID] e [!DNL client secret] estão incluídos *no corpo da solicitação* enviado ao seu destino. Para obter um exemplo, consulte a [Tipos de autenticação compatíveis](#supported-authentication-types) seção.
   * **[!UICONTROL Autorização básica]**: Nesse caso, a variável [!DNL client ID] e [!DNL client secret] estão incluídos *em um `Authorization` cabeçalho* depois de ser codificado em base64 e enviado para o seu destino. Para obter um exemplo, consulte a [Tipos de autenticação compatíveis](#supported-authentication-types) seção.

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="Cabeçalhos"
>abstract="Insira os cabeçalhos personalizados que você deseja incluir nas chamadas de destino, seguindo este formato: `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="Ponto de acesso HTTP"
>abstract="O URL do ponto de acesso HTTP para o qual você deseja enviar os dados do perfil."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="Incluir nomes de segmentos"
>abstract="Ative se quiser que a exportação de dados inclua os nomes dos públicos-alvo que você está exportando. Veja a documentação para ter um exemplo de exportação de dados com esta opção selecionada."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="Incluir carimbos de data e hora do segmento"
>abstract="Ative se quiser que a exportação de dados inclua o carimbo de data e hora UNIX de quando os públicos-alvo foram criados e atualizados, bem como o carimbo de data e hora UNIX de quando os públicos-alvo foram mapeados para o destino para ativação. Consulte a documentação para ver um exemplo de exportação de dados com esta opção selecionada."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="Parâmetros de consulta"
>abstract="Opcionalmente, é possível adicionar parâmetros de consulta ao URL do ponto de acesso HTTP. Formate os parâmetros de consulta usados desta forma: `parameter1=value&parameter2=value`."

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Imagem da tela da interface do usuário mostrando campos concluídos para detalhes de destino HTTP](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Nome]**: digite um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: insira uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Cabeçalhos]**: insira todos os cabeçalhos personalizados que deseja incluir nas chamadas de destino, seguindo este formato: `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL Endpoint HTTP]**: o URL do endpoint HTTP para o qual você deseja enviar os dados do perfil.
* **[!UICONTROL Parâmetros de consulta]**: Opcionalmente, é possível adicionar parâmetros de consulta ao URL do endpoint HTTP. Formate os parâmetros de consulta usados desta forma: `parameter1=value&parameter2=value`.
* **[!UICONTROL Incluir nomes de segmentos]**: alterne se quiser que a exportação de dados inclua os nomes dos públicos-alvo que você está exportando. Para obter um exemplo de exportação de dados com essa opção selecionada, consulte [Dados exportados](#exported-data) seção mais abaixo.
* **[!UICONTROL Incluir carimbos de data e hora do segmento]**: ative se desejar que a exportação de dados inclua o carimbo de data e hora UNIX quando os públicos-alvo foram criados e atualizados, bem como o carimbo de data e hora UNIX quando os públicos-alvo foram mapeados para o destino para ativação. Para obter um exemplo de exportação de dados com essa opção selecionada, consulte [Dados exportados](#exported-data) seção mais abaixo.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil de transmissão](../../ui/activate-streaming-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Atributos de destino {#attributes}

No [[!UICONTROL Selecionar atributos]](../../ui/activate-streaming-profile-destinations.md#select-attributes) etapa, o Adobe recomenda que você selecione um identificador exclusivo de sua [esquema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino.

## Comportamento de exportação de perfil {#profile-export-behavior}

O Experience Platform otimiza o comportamento de exportação de perfil para seu destino de API HTTP, a fim de exportar dados somente para seu endpoint de API quando atualizações relevantes para um perfil tiverem ocorrido após a qualificação de público-alvo ou outros eventos significativos. Os perfis são exportados para seu destino nas seguintes situações:

* A atualização do perfil foi determinada por uma alteração na associação de público-alvo para pelo menos um dos públicos-alvo mapeados para o destino. Por exemplo, o perfil se qualificou para um dos públicos mapeados para o destino ou saiu de um dos públicos mapeados para o destino.
* A atualização do perfil foi determinada por uma alteração no [mapa de identidade](/help/xdm/field-groups/profile/identitymap.md). Por exemplo, um perfil que já se qualificou para um dos públicos-alvo mapeados para o destino recebeu uma nova identidade no atributo de mapa de identidade.
* A atualização do perfil foi determinada por uma alteração nos atributos de pelo menos um dos atributos mapeados para o destino. Por exemplo, um dos atributos mapeados para o destino na etapa de mapeamento é adicionado a um perfil.

Em todos os casos descritos acima, somente os perfis em que ocorreram atualizações relevantes são exportados para o seu destino. Por exemplo, se um público-alvo mapeado para o fluxo de destino tiver cem membros e cinco novos perfis se qualificarem para o segmento, a exportação para o destino será incremental e incluirá apenas os cinco novos perfis.

Observe que todos os atributos mapeados são exportados para um perfil, independentemente de onde estejam as alterações. Portanto, no exemplo acima, todos os atributos mapeados para esses cinco novos perfis serão exportados mesmo se os atributos em si não tiverem sido alterados.

### O que determina uma exportação de dados e o que está incluído na exportação {#what-determines-export-what-is-included}

Em relação aos dados exportados para um determinado perfil, é importante entender os dois conceitos diferentes de *o que determina uma exportação de dados para o seu destino da API HTTP* e *quais dados estão incluídos na exportação*.

| O que determina uma exportação de destino | O que está incluído na exportação de destino |
|---------|----------|
| <ul><li>Atributos e públicos mapeados servem como indicação para uma exportação de destino. Isso significa que, se qualquer público mapeado alterar os estados (de `null` para `realized` ou de `realized` para `exiting`) ou qualquer atributo mapeado for atualizado, uma exportação de destino será iniciada.</li><li>Como as identidades não podem ser mapeadas para destinos da API HTTP no momento, as alterações em qualquer identidade em um determinado perfil também determinam as exportações de destino.</li><li>Uma alteração em um atributo é definida como qualquer atualização no atributo, seja ou não o mesmo valor. Isso significa que uma substituição em um atributo é considerada uma alteração, mesmo que o valor em si não tenha sido alterado.</li></ul> | <ul><li>A variável `segmentMembership` o objeto inclui o público-alvo mapeado no fluxo de dados de ativação, para o qual o status do perfil foi alterado após um evento de qualificação ou de saída de público-alvo. Observe que outros públicos não mapeados para os quais o perfil se qualificou podem fazer parte da exportação de destino, se esses públicos pertencerem à mesma [política de mesclagem](/help/profile/merge-policies/overview.md) como o público mapeado no fluxo de dados de ativação. </li><li>Todas as identidades na `identityMap` Os objetos do também estão incluídos (no momento, o Experience Platform não oferece suporte ao mapeamento de identidade no destino da API HTTP).</li><li>Somente os atributos mapeados são incluídos na exportação de destino.</li></ul> |

{style="table-layout:fixed"}

Por exemplo, considere esse fluxo de dados para um destino HTTP, onde três públicos-alvo são selecionados no fluxo de dados e quatro atributos são mapeados para o destino.

![Fluxo de dados de destino da API HTTP](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Uma exportação de perfil para o destino pode ser determinada por um perfil qualificado para ou que sai de um dos *três segmentos mapeados*. No entanto, na exportação de dados, no campo `segmentMembership` objeto (consulte [Dados exportados](#exported-data) abaixo), outros públicos-alvo não mapeados poderão ser exibidos se esse perfil específico for membro deles e se eles compartilharem a mesma política de mesclagem que o público-alvo que acionou a exportação. Se um perfil se qualificar para a variável **Cliente com DeLorean Cars** segmento, mas também é membro do **Assistido &quot;De volta ao futuro&quot;** filme e **Fãs de ficção científica** segmentos, esses outros dois públicos-alvo também estarão presentes na `segmentMembership` objeto da exportação de dados, mesmo que não estejam mapeados no fluxo de dados, se compartilharem a mesma política de mesclagem com o **Cliente com DeLorean Cars** segmento.

Do ponto de vista dos atributos de perfil, qualquer alteração nos quatro atributos mapeados acima determinará uma exportação de destino e qualquer um dos quatro atributos mapeados presentes no perfil estará presente na exportação de dados.

## Preenchimento retroativo de dados históricos {#historical-data-backfill}

Quando você adiciona um novo público a um destino existente ou cria um novo destino e mapeia públicos a ele, o Experience Platform exporta dados históricos de qualificação de público para o destino. Perfis qualificados para o público *antes* o público-alvo foi adicionado ao destino e é exportado para o destino em aproximadamente uma hora.

## Dados exportados {#exported-data}

Seu exportado [!DNL Experience Platform] os dados chegam em seu [!DNL HTTP] destino no formato JSON. Por exemplo, a exportação abaixo contém um perfil que se qualificou para um determinado segmento, é um membro de outros dois segmentos e saiu de outro segmento. A exportação também inclui o nome, sobrenome, data de nascimento e endereço de email pessoal do atributo de perfil. As identidades para esse perfil são ECID e email.

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
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
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

Abaixo estão mais exemplos de dados exportados, dependendo das configurações da interface do usuário que você selecionar no fluxo de destino de conexão para o **[!UICONTROL Incluir nomes de segmentos]** e **[!UICONTROL Incluir carimbos de data e hora do segmento]** opções:

+++ A amostra de exportação de dados abaixo inclui nomes de público-alvo na variável `segmentMembership` seção

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
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

+++ A amostra de exportação de dados abaixo inclui carimbos de data e hora de público-alvo na variável `segmentMembership` seção

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Política de limites e novas tentativas {#limits-retry-policy}

Em 95% das vezes, o Experience Platform tenta oferecer uma latência de taxa de transferência de menos de 10 minutos para mensagens enviadas com êxito, com uma taxa de menos de 10 mil solicitações por segundo para cada fluxo de dados para um destino HTTP.

No caso de solicitações com falha para o destino da API HTTP, o Experience Platform armazena as solicitações com falha e tenta enviar as solicitações duas vezes para o endpoint.