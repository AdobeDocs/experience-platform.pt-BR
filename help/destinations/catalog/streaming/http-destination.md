---
keywords: transmissão; destino HTTP
title: Conexão da API HTTP
description: Use o destino da API HTTP no Adobe Experience Platform para enviar dados de perfil para um endpoint HTTP de terceiros para executar sua própria análise ou executar outras operações necessárias nos dados de perfil exportados do Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 6d1b73c1557124f283558e1daeb3ddeaaec8e8a4
workflow-type: tm+mt
source-wordcount: '3079'
ht-degree: 6%

---

# Conexão da API HTTP

## Visão geral {#overview}

>[!IMPORTANT]
>
> Este destino está disponível somente para clientes do [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=pt-BR).

O destino da API HTTP é um destino de streaming [!DNL Adobe Experience Platform] que ajuda a enviar dados de perfil para pontos de extremidade HTTP de terceiros.

Para enviar dados de perfil para pontos de extremidade HTTP, primeiro você deve [se conectar ao destino](#connect-destination) em [!DNL Adobe Experience Platform].

## Casos de uso {#use-cases}

O destino da API HTTP permite exportar dados de perfil XDM e públicos para endpoints HTTP genéricos. Lá, você pode executar suas próprias análises ou executar outras operações que possam ser necessárias nos dados de perfil exportados do Experience Platform.

Os endpoints HTTP podem ser sistemas próprios dos clientes ou soluções de terceiros.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
| ---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Profile-based]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela de mapeamento do [fluxo de trabalho de ativação de destino](../../ui/activate-segment-streaming-destinations.md#mapping). |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

Para usar o destino da API HTTP para exportar dados do Experience Platform, você deve atender aos seguintes pré-requisitos:

* Você deve ter um endpoint HTTP compatível com REST API.
* Seu endpoint HTTP deve ser compatível com o esquema de perfil do Experience Platform. Nenhuma transformação em um esquema de carga de terceiros é compatível com o destino da API HTTP. Consulte a seção [dados exportados](#exported-data) para obter um exemplo do esquema de saída do Experience Platform.
* Seu ponto de extremidade HTTP deve oferecer suporte a cabeçalhos.
* Seu endpoint HTTP deve responder em 2 segundos para garantir o processamento de dados adequado e evitar erros de tempo limite.
* Se você planeja usar mTLS: o endpoint de recebimento de dados deve ter o TLS desativado e somente o mTLS ativado. Se também usar a autenticação OAuth 2, você deverá manter um endpoint HTTPS padrão separado para a recuperação do token. Consulte a seção [Considerações sobre mTLS](#mtls-considerations) para obter detalhes.

>[!TIP]
>
> Você também pode usar o [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) para configurar uma integração e enviar dados de perfil do Experience Platform para um ponto de extremidade HTTP.

## Suporte e certificado do protocolo mTLS {#mtls-protocol-support}

Você pode usar [!DNL Mutual Transport Layer Security] ([!DNL mTLS]) para garantir segurança aprimorada em conexões de saída com suas conexões de destino de API HTTP.

[!DNL mTLS] é um protocolo de autenticação mútua que garante que ambas as partes que compartilham informações sejam quem afirmam ser antes que os dados sejam compartilhados. [!DNL mTLS] inclui uma etapa adicional em comparação ao padrão [!DNL TLS], em que o servidor também solicita e verifica o certificado do cliente, enquanto o cliente verifica o certificado do servidor.

### Considerações sobre mTLS {#mtls-considerations}

O suporte mTLS para destinos da API HTTP se aplica **somente ao ponto de extremidade de recebimento de dados** para o qual são enviadas exportações de perfil (o campo **[!UICONTROL HTTP Endpoint]** em [detalhes do destino](#destination-details)).

Não há suporte para **mTLS para os pontos de extremidade de autenticação do OAuth 2:**

* O **[!UICONTROL Access Token URL]** usado nas Credenciais de Cliente OAuth 2 ou na autenticação de Senha OAuth 2 não dá suporte a mTLS
* As solicitações de recuperação e atualização de token são enviadas por HTTPS padrão sem autenticação de certificado de cliente

**Arquitetura Necessária:** Se você precisar de mTLS para o ponto de extremidade de recebimento de dados e usar a autenticação OAuth 2, será necessário manter dois pontos de extremidade separados:

* **Ponto de extremidade de autenticação:** HTTPS padrão (sem mTLS) para gerenciamento de token
* **Ponto de extremidade de recebimento de dados:** HTTPS com mTLS somente habilitado para exportações de perfil

Essa arquitetura é uma limitação atual da plataforma. O suporte para mTLS em endpoints de autenticação está sendo avaliado para versões futuras.

### Configuração de mTLS para exportação de dados {#configuring-mtls}

Para usar o [!DNL mTLS] com [!DNL HTTP API] destinos, o **[!UICONTROL HTTP Endpoint]** (ponto de extremidade de recebimento de dados) configurado na página [detalhes do destino](#destination-details) deve ter [!DNL TLS] protocolos desabilitados e apenas [!DNL mTLS] habilitados. Se o protocolo [!DNL TLS] 1.2 ainda estiver habilitado no ponto de extremidade, nenhum certificado será enviado para a autenticação de cliente. Isso significa que para usar [!DNL mTLS] com seu destino [!DNL HTTP API], seu ponto de extremidade do servidor de recebimento de dados deve ser um ponto de extremidade de conexão habilitado somente para [!DNL mTLS].

### Recuperar e inspecionar detalhes do certificado {#certificate}

Se você quiser inspecionar detalhes de certificados como o [!DNL Common Name] (CN) e o [!DNL Subject Alternative Names] (SAN) para validação adicional de terceiros, use a API para recuperar o certificado e extrair esses campos da resposta.

Consulte a [documentação do ponto de extremidade do certificado público](../../../data-governance/mtls-api/public-certificate-endpoint.md) para obter mais informações.

## INCLUO NA LISTA DE PERMISSÕES de endereços IP {#ip-address-allowlist}

Para atender aos requisitos de segurança e conformidade dos clientes, o Experience Platform fornece uma lista de IPs estáticos que você pode incluir na lista de permissões para o destino da API HTTP. Consulte [incluo na lista de permissões de endereços IP para destinos de streaming](/help/destinations/catalog/streaming/ip-address-allow-list.md) para obter a lista completa de IPs a serem incluídos na lista de permissões.

## Tipos de autenticação compatíveis {#supported-authentication-types}

O destino da API HTTP oferece suporte a vários tipos de autenticação para o terminal HTTP:

* Endpoint HTTP sem autenticação;
* Autenticação do token portador;
* Autenticação de [credenciais de cliente OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) com o formulário de corpo, com [!DNL client ID], [!DNL client secret] e [!DNL grant type] no corpo da solicitação HTTP, como mostrado no exemplo abaixo.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [Credenciais de cliente OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) com autorização básica, com um cabeçalho de autorização que contém [!DNL client ID] e [!DNL client secret] codificados em URL.

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
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). Ao se conectar a esse destino, você deve fornecer as seguintes informações:

### Informações de autenticação {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="Tipo de credenciais do cliente"
>abstract="Selecione **Corpo codificado em formato** para incluir a ID do cliente e o segredo do cliente no corpo da solicitação ou **Autorização básica** para incluir a ID do cliente e o segredo do cliente em um cabeçalho de autorização. Veja exemplos na documentação."

#### Autenticação de token do portador {#bearer-token-authentication}

Se você selecionar o tipo de autenticação **[!UICONTROL Bearer token]** para se conectar ao seu ponto de extremidade HTTP, insira os campos abaixo e selecione **[!UICONTROL Connect to destination]**:

![Imagem da tela da interface do usuário onde você pode se conectar ao destino da API HTTP, usando a autenticação de token de portador.](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Bearer token]**: inserir o token portador para autenticar em seu local HTTP.

#### Sem autenticação {#no-authentication}

Se você selecionar o tipo de autenticação **[!UICONTROL None]** para se conectar ao seu ponto de extremidade HTTP:

![Imagem da tela da interface do usuário onde você pode se conectar ao destino da API HTTP sem autenticação.](../../assets/catalog/http/http-api-authentication-none.png)

Ao selecionar esta autenticação aberta, você só precisa selecionar **[!UICONTROL Connect to destination]** e a conexão com o seu ponto de extremidade é estabelecida.

#### Autenticação de senha do OAuth 2 {#oauth-2-password-authentication}

Se você selecionar o tipo de autenticação **[!UICONTROL OAuth 2 Password]** para se conectar ao seu ponto de extremidade HTTP, insira os campos abaixo e selecione **[!UICONTROL Connect to destination]**:

![Imagem da tela da interface do usuário onde você pode se conectar ao destino da API HTTP, usando OAuth 2 com autenticação de Senha.](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

>[!NOTE]
>
>**Limitação de mTLS:** [!UICONTROL Access Token URL] não dá suporte a mTLS. Se você planeja usar mTLS para seu endpoint de recebimento de dados, seu endpoint de autenticação deve usar HTTPS padrão. Consulte a seção [Considerações sobre mTLS](#mtls-considerations) para obter mais detalhes sobre a arquitetura necessária.

* **[!UICONTROL Access Token URL]**: A URL no seu lado que emite tokens de acesso e, opcionalmente, atualiza tokens. Esse endpoint deve usar HTTPS padrão e não oferece suporte a mTLS.
* **[!UICONTROL Client ID]**: o [!DNL client ID] que seu sistema atribui à Adobe Experience Platform.
* **[!UICONTROL Client Secret]**: o [!DNL client secret] que seu sistema atribui à Adobe Experience Platform.
* **[!UICONTROL Username]**: O nome de usuário para acessar seu ponto de extremidade HTTP.
* **[!UICONTROL Password]**: A senha para acessar seu ponto de extremidade HTTP.

#### Autenticação de Credenciais de Cliente OAuth 2 {#oauth-2-client-credentials-authentication}

Se você selecionar o tipo de autenticação **[!UICONTROL OAuth 2 Client Credentials]** para se conectar ao seu ponto de extremidade HTTP, insira os campos abaixo e selecione **[!UICONTROL Connect to destination]**:

![Imagem da tela da interface do usuário na qual você pode se conectar ao destino da API HTTP, usando o OAuth 2 com autenticação de Credenciais de Cliente.](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

>[!WARNING]
> 
>Ao usar a autenticação [!UICONTROL OAuth 2 Client Credentials], o [!UICONTROL Access Token URL] pode ter no máximo um parâmetro de consulta. Adicionar um [!UICONTROL Access Token URL] com mais parâmetros de consulta pode levar a problemas ao conectar ao seu ponto de extremidade.

>[!NOTE]
>
>**Limitação de mTLS:** [!UICONTROL Access Token URL] não dá suporte a mTLS. Se você planeja usar mTLS para seu endpoint de recebimento de dados, seu endpoint de autenticação deve usar HTTPS padrão. Consulte a seção [Considerações sobre mTLS](#mtls-considerations) para obter mais detalhes sobre a arquitetura necessária.

* **[!UICONTROL Access Token URL]**: A URL no seu lado que emite tokens de acesso e, opcionalmente, atualiza tokens. Esse endpoint deve usar HTTPS padrão e não oferece suporte a mTLS.
* **[!UICONTROL Client ID]**: o [!DNL client ID] que seu sistema atribui à Adobe Experience Platform.
* **[!UICONTROL Client Secret]**: o [!DNL client secret] que seu sistema atribui à Adobe Experience Platform.
* **[!UICONTROL Client Credentials Type]**: Selecione o tipo de concessão de Credenciais de Cliente OAuth2 suportada pelo seu ponto de extremidade:
   * **[!UICONTROL Body Form Encoded]**: Nesse caso, o [!DNL client ID] e o [!DNL client secret] estão incluídos *no corpo da solicitação* enviada para o seu destino. Para ver um exemplo, consulte a seção [Tipos de autenticação suportados](#supported-authentication-types).
   * **[!UICONTROL Basic Authorization]**: Nesse caso, o [!DNL client ID] e [!DNL client secret] estão incluídos *em um cabeçalho `Authorization`* depois de serem codificados em base64 e enviados para o seu destino. Para ver um exemplo, consulte a seção [Tipos de autenticação suportados](#supported-authentication-types).

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="Cabeçalhos"
>abstract="Insira os cabeçalhos personalizados que você deseja incluir nas chamadas de destino, seguindo este formato: `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="Ponto de acesso HTTP"
>abstract="A URL do endpoint HTTP para o qual você deseja enviar os dados do perfil. Este é o terminal de recebimento de dados e oferece suporte a mTLS, se configurado. Isso é separado do URL do token de acesso OAuth 2, que não oferece suporte a mTLS."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="Incluir nomes de segmentos"
>abstract="Ative se quiser que a exportação de dados inclua os nomes dos públicos-alvo que você está exportando. Consulte a documentação para ver um exemplo de exportação de dados com esta opção selecionada."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="Incluir carimbos de data e hora do segmento"
>abstract="Ative se quiser que a exportação de dados inclua o carimbo de data e hora UNIX de quando os públicos-alvo foram criados e atualizados, bem como o carimbo de data e hora UNIX de quando os públicos-alvo foram mapeados para o destino para ativação. Consulte a documentação para ver um exemplo de exportação de dados com esta opção selecionada."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="Parâmetros de consulta"
>abstract="Opcionalmente, é possível adicionar parâmetros de consulta ao URL do ponto de acesso HTTP. Formate os parâmetros de consulta usados desta forma: `parameter1=value&parameter2=value`."

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Imagem da tela da interface do usuário mostrando campos concluídos para os detalhes de destino HTTP.](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Name]**: Digite um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: insira uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Headers]**: Insira todos os cabeçalhos personalizados que você deseja incluir nas chamadas de destino, seguindo este formato: `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL HTTP Endpoint]**: A URL do ponto de extremidade HTTP para o qual você deseja enviar os dados do perfil. Este é o terminal de recebimento de dados. Se estiver usando mTLS, esse endpoint deve ter o TLS desativado e somente o mTLS ativado. Observe que isso é diferente do URL do token de acesso OAuth 2 configurado durante a autenticação.
* **[!UICONTROL Query parameters]**: Opcionalmente, você pode adicionar parâmetros de consulta à URL do ponto de extremidade HTTP. Formate os parâmetros de consulta usados desta forma: `parameter1=value&parameter2=value`.
* **[!UICONTROL Include Segment Names]**: alterne se quiser que a exportação de dados inclua os nomes dos públicos que você está exportando. **Observação**: os nomes de segmentos são incluídos apenas em segmentos mapeados para o destino. Os segmentos não mapeados que aparecem na exportação não incluirão o campo `name`. Para obter um exemplo de exportação de dados com essa opção selecionada, consulte a seção [Dados exportados](#exported-data), mais abaixo.
* **[!UICONTROL Include Segment Timestamps]**: alterne se desejar que a exportação de dados inclua o carimbo de data e hora UNIX quando os públicos-alvo foram criados e atualizados, bem como o carimbo de data e hora UNIX quando os públicos-alvo foram mapeados para o destino para ativação. Para obter um exemplo de exportação de dados com essa opção selecionada, consulte a seção [Dados exportados](#exported-data), mais abaixo.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* [A avaliação de política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) não tem suporte atualmente em exportações para o destino da API HTTP. [Leia mais](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Consulte [Ativar dados de público-alvo para destinos de exportação de perfil de streaming](../../ui/activate-streaming-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

### Atributos de destino {#attributes}

Na etapa [[!UICONTROL Select attributes]](../../ui/activate-streaming-profile-destinations.md#select-attributes), a Adobe recomenda selecionar um identificador exclusivo do seu [esquema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino.

## Comportamento de exportação de perfil {#profile-export-behavior}

O Experience Platform otimiza o comportamento de exportação de perfis para o destino da API HTTP, a fim de exportar dados somente para o endpoint da API quando atualizações relevantes para um perfil tiverem ocorrido após a qualificação de público-alvo ou outros eventos significativos. Os perfis são exportados para seu destino nas seguintes situações:

* A atualização do perfil foi determinada por uma alteração na associação de público-alvo para pelo menos um dos públicos-alvo mapeados para o destino. Por exemplo, o perfil se qualificou para um dos públicos mapeados para o destino ou saiu de um dos públicos mapeados para o destino.
* A atualização do perfil foi determinada por uma alteração no [mapa de identidade](/help/xdm/field-groups/profile/identitymap.md). Por exemplo, um perfil que já se qualificou para um dos públicos-alvo mapeados para o destino recebeu uma nova identidade no atributo de mapa de identidade.
* A atualização do perfil foi determinada por uma alteração nos atributos de pelo menos um dos atributos mapeados para o destino. Por exemplo, um dos atributos mapeados para o destino na etapa de mapeamento é adicionado a um perfil.

Em todos os casos descritos acima, somente os perfis em que ocorreram atualizações relevantes são exportados para o seu destino. Por exemplo, se um público-alvo mapeado para o fluxo de destino tiver cem membros e cinco novos perfis se qualificarem para o segmento, a exportação para o destino será incremental e incluirá apenas os cinco novos perfis.

Observe que todos os atributos mapeados são exportados para um perfil, independentemente de onde estejam as alterações. Portanto, no exemplo acima, todos os atributos mapeados para esses cinco novos perfis serão exportados mesmo se os atributos em si não tiverem sido alterados.

### O que determina uma exportação de dados e o que está incluído na exportação {#what-determines-export-what-is-included}

Com relação aos dados exportados para um determinado perfil, é importante entender os dois conceitos diferentes de *o que determina uma exportação de dados para seu destino de API HTTP* e *quais dados são incluídos na exportação*.

| O que determina uma exportação de destino | O que está incluído na exportação de destino |
|---------|----------|
| <ul><li>Atributos e segmentos mapeados servem como dica para uma exportação de destino. Isso significa que se o status `segmentMembership` de um perfil for alterado para `realized` ou `exiting` ou qualquer atributo mapeado for atualizado, uma exportação de destino será iniciada.</li><li>Como as identidades não podem ser mapeadas para destinos da API HTTP no momento, as alterações em qualquer identidade em um determinado perfil também determinam as exportações de destino.</li><li>Uma alteração em um atributo é definida como qualquer atualização no atributo, seja ou não o mesmo valor. Isso significa que uma substituição em um atributo é considerada uma alteração, mesmo que o valor em si não tenha sido alterado.</li></ul> | <ul><li>O objeto `segmentMembership` inclui o segmento mapeado no fluxo de dados de ativação, para o qual o status do perfil foi alterado após um evento de qualificação ou saída de segmento. Observe que outros segmentos não mapeados para os quais o perfil se qualificou podem fazer parte da exportação de destino, se esses segmentos pertencerem à mesma [política de mesclagem](/help/profile/merge-policies/overview.md) que o segmento mapeado no fluxo de dados de ativação. <br> **Importante**: quando a opção **[!UICONTROL Include Segment Names]** está habilitada, os nomes de segmentos são incluídos apenas para segmentos mapeados para o destino. Os segmentos não mapeados exibidos na exportação não incluirão o campo `name`, mesmo que a opção esteja habilitada. </li><li>Todas as identidades no objeto `identityMap` também estão incluídas (no momento, o Experience Platform não oferece suporte ao mapeamento de identidade no destino da API HTTP).</li><li>Somente os atributos mapeados são incluídos na exportação de destino.</li></ul> |

{style="table-layout:fixed"}

Por exemplo, considere esse fluxo de dados para um destino HTTP, onde três públicos-alvo são selecionados no fluxo de dados e quatro atributos são mapeados para o destino.

![Um exemplo de fluxo de dados de destino da API HTTP.](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Uma exportação de perfil para o destino pode ser determinada por um perfil qualificado para ou saindo dos *três segmentos mapeados*. No entanto, na exportação de dados, no objeto `segmentMembership` (consulte a seção [Dados Exportados](#exported-data) abaixo), outros públicos não mapeados poderão ser exibidos se esse perfil específico for membro deles e se eles compartilharem a mesma política de mesclagem que o público-alvo que acionou a exportação. Se um perfil se qualificar para o segmento **Cliente com carros DeLoree**, mas também for membro dos segmentos **Filme &quot;De volta para o futuro&quot;** assistido e **Fãs de ficção científica**, esses outros dois públicos-alvo também estarão presentes no objeto `segmentMembership` da exportação de dados, mesmo que eles não estejam mapeados no fluxo de dados, se eles compartilharem a mesma política de mesclagem com o segmento **Cliente com carros DeLorea**.

Do ponto de vista dos atributos de perfil, qualquer alteração nos quatro atributos mapeados acima determinará uma exportação de destino e qualquer um dos quatro atributos mapeados presentes no perfil estará presente na exportação de dados.

## Preenchimento retroativo de dados históricos {#historical-data-backfill}

Quando você adiciona um novo público a um destino existente ou cria um novo destino e mapeia públicos a ele, o Experience Platform exporta dados históricos de qualificação de público para o destino. Os perfis qualificados para o público-alvo *antes* de o público-alvo ser adicionado ao destino são exportados para o destino em aproximadamente uma hora.

## Dados exportados {#exported-data}

Os dados exportados do [!DNL Experience Platform] chegam ao destino [!DNL HTTP] no formato JSON. Por exemplo, a exportação abaixo contém um perfil que se qualificou para um determinado segmento, é um membro de outros dois segmentos e saiu de outro segmento. A exportação também inclui o nome, sobrenome, data de nascimento e endereço de email pessoal do atributo de perfil. As identidades para esse perfil são ECID e email.

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

Abaixo estão mais exemplos de dados exportados, dependendo das configurações de interface do usuário que você selecionar no fluxo de destino de conexão para as opções **[!UICONTROL Include Segment Names]** e **[!UICONTROL Include Segment Timestamps]**:

+++ A amostra de exportação de dados abaixo inclui nomes de público na seção `segmentMembership`

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
          },
          "354e086f-2e11-49a2-9e39-e5d9a76be683": {
            "lastQualificationTime": "2020-04-15T02:41:50+0000",
            "status": "realized"
          }
        }
      }
```

**Observação**: neste exemplo, o primeiro segmento (`5b998cb9-9488-4ec3-8d95-fa8338ced490`) é mapeado para o destino e inclui o campo `name`. O segundo segmento (`354e086f-2e11-49a2-9e39-e5d9a76be683`) não é mapeado para o destino e não inclui o campo `name`, mesmo que a opção **[!UICONTROL Include Segment Names]** esteja habilitada.

+++

+++ A amostra de exportação de dados abaixo inclui carimbos de data/hora de público-alvo na seção `segmentMembership`

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

Em 95% das vezes, o Experience Platform tenta oferecer uma latência de taxa de transferência de menos de 10 minutos para mensagens enviadas com êxito, com uma taxa de menos de 10 mil solicitações por segundo para cada fluxo de dados a um destino HTTP.

No caso de solicitações com falha para o destino da API HTTP, o Experience Platform armazena as solicitações com falha e tenta enviar as solicitações duas vezes para o seu endpoint.

## Solução de problemas {#troubleshooting}

Para garantir a entrega de dados confiável e evitar problemas de tempo limite, verifique se o seu ponto de extremidade HTTP responde em 2 segundos às solicitações do Experience Platform, conforme especificado na seção [pré-requisitos](#prerequisites). Respostas que demoram mais resultarão em erros de tempo limite.
