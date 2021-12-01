---
keywords: Conexão facebook; Conexão facebook; Destinos facebook; facebook; instagram; mensageiro; facebook Messenger
title: Conexão facebook
description: Ative perfis para suas campanhas do Facebook para direcionamento de público-alvo, personalização e supressão com base em emails com hash.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 357916aa925c7b3ada4abe64a2bc6ad090d70cc0
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 1%

---

# [!DNL Facebook] conexão

## Visão geral {#overview}

Ativar perfis para seu [!DNL Facebook] campanhas para segmentação, personalização e supressão de público-alvo com base em emails com hash.

Você pode usar esse destino para segmentação de público-alvo em [!DNL Facebook’s] família de aplicativos compatíveis com [!DNL Custom Audiences], incluindo [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network]e [!DNL Messenger]. A seleção do aplicativo no qual você deseja executar a campanha é indicada no nível de posicionamento no [!DNL Facebook Ads Manager].

![Destino do facebook na interface do usuário do Adobe Experience Platform](../../assets/catalog/social/facebook/catalog.png)

## Casos de uso

Para ajudá-lo a entender melhor como e quando usar a variável [!DNL Facebook] , aqui estão dois casos de uso de exemplo que os clientes do Adobe Experience Platform podem resolver usando esse recurso.

### Caso de uso nº 1

Um varejista online deseja alcançar clientes existentes por meio de plataformas sociais e mostrar a eles ofertas personalizadas com base em seus pedidos anteriores. O varejista online pode assimilar endereços de email de seu próprio CRM para o Adobe Experience Platform, criar segmentos a partir de seus próprios dados offline e enviar esses segmentos para a [!DNL Facebook] plataforma social, otimizando seus gastos com publicidade.

### Caso de uso nº 2

Uma companhia aérea tem níveis de clientes diferentes (Bronze, Prata e Ouro) e deseja fornecer a cada um dos níveis ofertas personalizadas por meio de plataformas sociais. No entanto, nem todos os clientes usam o aplicativo móvel da companhia aérea e alguns deles não fizeram logon no site da empresa. Os únicos identificadores que a empresa tem sobre esses clientes são IDs de associação e endereços de email.

Para direcioná-los em redes sociais, eles podem integrar os dados do cliente do CRM para o Adobe Experience Platform, usando os endereços de email como identificadores.

Em seguida, eles podem usar seus dados offline, incluindo as IDs de associação associadas e os níveis do cliente, para criar novos segmentos de público-alvo que podem ser direcionados por meio do [!DNL Facebook] destino.

## Identidades suportadas {#supported-identities}

[!DNL Facebook Custom Audiences] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| GAID | Google Advertising ID | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando sua identidade de origem for um namespace do IDFA. |
| phone_sha256 | Números de telefone com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e números de telefone com hash SHA256. Siga as instruções em [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para números de telefone sem formatação e com hash, respectivamente. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. Siga as instruções em [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e usar os namespaces apropriados para endereços de email de texto simples e com hash, respectivamente. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. |
| external_id | IDs de usuário personalizadas | Selecione essa identidade de destino quando sua identidade de origem for um namespace personalizado. |

## Tipo de exportação {#export-type}

**Exportar segmento** - você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados no destino do Facebook.

## Pré-requisitos da conta do facebook {#facebook-account-prerequisites}

Antes de enviar segmentos de público-alvo para o [!DNL Facebook], certifique-se de atender aos seguintes requisitos:

* Seu [!DNL Facebook] a conta do usuário deve ter o **[!DNL Manage campaigns]** permissão ativada para a conta do anúncio que você planeja usar.
* O **Adobe Experience Cloud** A conta comercial deve ser adicionada como um parceiro de publicidade em seu [!DNL Facebook Ad Account]. Use `business ID=206617933627973`. Consulte [Adicionar parceiros ao seu gerente de negócios](https://www.facebook.com/business/help/1717412048538897) na documentação do Facebook para obter detalhes.
   >[!IMPORTANT]
   >
   > Ao configurar as permissões para o Adobe Experience Cloud, você deve ativar o **Gerenciar campanhas** permissão. A permissão é necessária para a variável [!DNL Adobe Experience Platform] integração.
* Leia e assine o [!DNL Facebook Custom Audiences] Termos de serviço. Para fazer isso, acesse `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, onde `accountID` é seu [!DNL Facebook Ad Account ID].
   >[!IMPORTANT]
   >
   >Ao assinar o [!DNL Facebook Custom Audiences] Termos de serviço, certifique-se de usar a mesma conta de usuário que você usou para autenticar na API do Facebook.

## Requisitos de correspondência de ID {#id-matching-requirements}

[!DNL Facebook] exige que nenhuma informação pessoal identificável (PII) seja enviada de forma clara. Portanto, os públicos-alvo ativados para [!DNL Facebook] pode ser desligado *hash* identificadores, como endereços de email ou números de telefone.

Dependendo do tipo de IDs assimiladas no Adobe Experience Platform, é necessário seguir os requisitos correspondentes.

## Requisitos de hash do número de telefone {#phone-number-hashing-requirements}

Há dois métodos para ativar números de telefone em [!DNL Facebook]:

* **Inserir números de telefone brutos**: você pode assimilar números de telefone brutos no [!DNL E.164] formatar em [!DNL Platform]. Eles passam automaticamente por hash na ativação. Se você escolher essa opção, certifique-se sempre de assimilar seus números de telefone brutos no `Phone_E.164` namespace.
* **Inserir números de telefone com hash**: você pode fazer o hash prévio dos números de telefone antes da ingestão no [!DNL Platform]. Se você escolher essa opção, certifique-se sempre de assimilar seus números de telefone com hash no `Phone_SHA256` namespace.

>[!NOTE]
>
>Números de telefone assimilados no `Phone` o namespace não pode ser ativado em [!DNL Facebook].


## Requisitos de hash de email {#email-hashing-requirements}

Você pode fazer hash nos endereços de email antes de assimilá-los no Adobe Experience Platform ou usar endereços de email limpos no Experience Platform e ter [!DNL Platform] coloque hash na ativação.

Para saber mais sobre como assimilar endereços de email no Experience Platform, consulte o [visão geral da ingestão em lote](/help/ingestion/batch-ingestion/overview.md) e [visão geral da assimilação de streaming](/help/ingestion/streaming-ingestion/overview.md).

Se você optar por hash nos endereços de email, certifique-se de estar em conformidade com os seguintes requisitos:

* Cortar todos os espaços à esquerda e à direita da string de email; exemplo: `johndoe@example.com`, não `<space>johndoe@example.com<space>`;
* Ao fazer o hash das cadeias de caracteres de email, certifique-se de fazer hash na cadeia de caracteres de minúsculas;
   * Exemplo: `example@email.com`, não `EXAMPLE@EMAIL.COM`;
* Certifique-se de que a cadeia de caracteres com hash esteja em letras minúsculas
   * Exemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, não `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Não salve a corda.

>[!NOTE]
>
>Os dados de namespaces sem hash são automaticamente atribuídos a hash por [!DNL Platform] após a ativação.
> Os dados da fonte de atributo não são automaticamente transformados em hash. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação.
> O **[!UICONTROL Aplicar transformação]** A opção é exibida somente quando você seleciona atributos como campos de origem. Ele não é exibido quando você escolhe namespaces.

![Transformação de mapeamento de identidade](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Uso de namespaces personalizados {#custom-namespaces}

Antes de usar a variável `Extern_ID` namespace para enviar dados para [!DNL Facebook], certifique-se de sincronizar seus próprios identificadores usando [!DNL Facebook Pixel]. Consulte a [Documentação oficial do facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) para obter informações detalhadas.

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

O vídeo abaixo também demonstra as etapas para configurar um [!DNL Facebook] e ativar segmentos.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>A interface do usuário do Experience Platform é atualizada com frequência e pode ter sido alterada desde a gravação deste vídeo. Para obter as informações mais atualizadas, consulte o [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID da conta]**: your [!DNL Facebook Ad Account ID]. Você pode encontrar essa ID em seu [!DNL Facebook Ads Manager] conta. Ao inserir essa ID, sempre coloque o prefixo nela com `act_`.

## Ativar segmentos para este destino {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="Origem do público"
>abstract="Escolha como os dados do cliente no segmento foram coletados originalmente. Os dados serão exibidos no Facebook quando um usuário for direcionado pelo segmento"
>additional-url="http://www.adobe.com/go/destinations-facebook-activate-section-en" text="Saiba mais na documentação"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customers"
>title="Origem do público"
>abstract="Os anunciantes coletaram dados diretamente dos clientes."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="Origem do público"
>abstract="Os anunciantes coletaram dados diretamente de seus parceiros."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="Origem do público"
>abstract="Os anunciantes coletaram dados diretamente de seus clientes e parceiros."

Consulte [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

No **[!UICONTROL Agendamento do segmento]** , você deve fornecer a variável [!UICONTROL Origem do público] ao enviar segmentos para [!DNL Facebook Custom Audiences].

![Origem do público-alvo do facebook](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Exemplo de mapeamento: como ativar os dados do público-alvo no [!DNL Facebook Custom Audience] {#example-facebook}

Abaixo está um exemplo do mapeamento de identidade correto ao ativar os dados do público-alvo em [!DNL Facebook Custom Audience].

Seleção de campos de origem:

* Selecione o `Email` namespace como identidade de origem se os endereços de email que você está usando não tiverem hash.
* Selecione o `Email_LC_SHA256` namespace como identidade de origem se você tiver enviado com hash endereços de email do cliente na assimilação de dados em [!DNL Platform], de acordo com [!DNL Facebook] [requisitos de hash de email](#email-hashing-requirements).
* Selecione o `PHONE_E.164` namespace como identidade de origem se seus dados consistem em números de telefone sem hash. [!DNL Platform] hash os números de telefone para estar em conformidade com [!DNL Facebook] requisitos.
* Selecione o `Phone_SHA256` namespace como identidade de origem se você tiver hash de números de telefone na assimilação de dados em [!DNL Platform], de acordo com [!DNL Facebook] [requisitos de hash do número de telefone](#phone-number-hashing-requirements).
* Selecione o `IDFA` namespace como identidade de origem se seus dados consistem em [!DNL Apple] IDs de dispositivo.
* Selecione o `GAID` namespace como identidade de origem se seus dados consistem em [!DNL Android] IDs de dispositivo.
* Selecione o `Custom` namespace como identidade de origem se os dados consistem em outro tipo de identificador.

Seleção de campos de destino:

* Selecione o `Email_LC_SHA256` namespace como identidade de destino quando os namespaces de origem forem `Email` ou `Email_LC_SHA256`.
* Selecione o `Phone_SHA256` namespace como identidade de destino quando os namespaces de origem forem `PHONE_E.164` ou `Phone_SHA256`.
* Selecione o `IDFA` ou `GAID` namespaces como identidade de destino quando os namespaces de origem são `IDFA` ou `GAID`.
* Selecione o `Extern_ID` namespace como identidade de destino quando seu namespace de origem é personalizado.

>[!IMPORTANT]
>
>Os dados de namespaces sem hash são automaticamente atribuídos a hash por [!DNL Platform] após a ativação.
> 
>Os dados da fonte de atributo não são automaticamente transformados em hash. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação.

![Mapeamento de identidade](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Dados exportados {#exported-data}

Para [!DNL Facebook], uma ativação bem-sucedida significa que uma [!DNL Facebook] o público-alvo personalizado seria criado programaticamente em [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). A associação de segmento no público-alvo seria adicionada e removida, pois os usuários eram qualificados ou desqualificados para os segmentos ativados.

>[!TIP]
>
>A integração entre o Adobe Experience Platform e o [!DNL Facebook] O suporta preenchimentos retroativos de público-alvo históricos. Todas as qualificações de segmento histórico são enviadas para [!DNL Facebook] ao ativar os segmentos para o destino.

## Solução de problemas {#troubleshooting}

### 400 Mensagem de erro de solicitação incorreta {#bad-request}

Ao configurar esse destino, você pode receber o seguinte erro:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Esse erro ocorre quando os clientes usam contas recém-criadas e a variável [!DNL Facebook] as permissões do ainda não estão ativas.

Se você receber a variável `400 Bad Request` mensagem de erro depois de seguir as etapas em [Pré-requisitos da conta do facebook](#facebook-account-prerequisites), permita alguns dias para o [!DNL Facebook] para entrar em vigor.
