---
keywords: conexão facebook;conexão facebook;destinos do facebook;facebook;instagram;messenger;facebook messenger
title: Conexão com o facebook
description: Ative perfis para suas campanhas do Facebook para direcionamento de público, personalização e supressão com base em emails com hash.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 7%

---

# [!DNL Facebook] conexão

## Visão geral {#overview}

Ativar perfis para o [!DNL Facebook] campanhas para direcionamento de público, personalização e supressão com base em emails com hash.

Você pode usar esse destino para direcionamento de público-alvo em [!DNL Facebook's] família de aplicativos compatíveis com [!DNL Custom Audiences], incluindo [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], e [!DNL Messenger]. A seleção do aplicativo no qual você deseja executar a campanha é indicada no nível de posicionamento no [!DNL Facebook Ads Manager].

![Destino do facebook na interface do Adobe Experience Platform.](../../assets/catalog/social/facebook/catalog.png)

## Casos de uso

Para ajudá-lo a entender melhor como e quando usar o [!DNL Facebook] destino, aqui estão dois casos de uso de exemplo que os clientes do Adobe Experience Platform podem resolver usando esse recurso.

### Caso de uso #1

Um varejista online deseja alcançar os clientes existentes por meio de plataformas sociais e mostrar ofertas personalizadas com base em seus pedidos anteriores. O varejista online pode assimilar endereços de email de seu próprio CRM para o Adobe Experience Platform, criar públicos a partir de seus próprios dados offline e enviar esses públicos para a [!DNL Facebook] social, otimizando seus gastos com publicidade.

### Caso de uso #2

Uma companhia aérea tem diferentes níveis de clientes (Bronze, Prata e Ouro) e deseja fornecer ofertas personalizadas a cada um dos níveis por meio de plataformas sociais. No entanto, nem todos os clientes usam o aplicativo móvel da companhia aérea e alguns deles não fizeram logon no site da empresa. Os únicos identificadores que a empresa tem sobre esses clientes são IDs de associação e endereços de email.

Para direcioná-los nas redes sociais, eles podem integrar os dados do cliente do CRM no Adobe Experience Platform, usando os endereços de email como identificadores.

Em seguida, eles podem usar seus dados offline, incluindo IDs de associação associadas e camadas de clientes, para criar novos públicos-alvo que podem direcionar por meio da [!DNL Facebook] destino.

## Identidades suportadas {#supported-identities}

[!DNL Facebook Custom Audiences] O oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| GAID | ID de publicidade do Google | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando a identidade de origem for um namespace do IDFA. |
| phone_sha256 | Números de telefone com hash com o algoritmo SHA256 | Os números de telefone com hash SHA256 e texto sem formatação são compatíveis com o Adobe Experience Platform. Siga as instruções em [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para texto sem formatação e números de telefone com hash, respectivamente. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Siga as instruções em [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para texto simples e endereços de email com hash, respectivamente. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. |
| extern_id | IDs de usuário personalizadas | Selecione esta identidade de destino quando sua identidade de origem for um namespace personalizado. |

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | ✓ | Públicos-alvo [importado](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público com os identificadores (nome, número de telefone ou outros) usados no destino do Facebook. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Pré-requisitos da conta do facebook {#facebook-account-prerequisites}

Antes de enviar os públicos-alvo para [!DNL Facebook], certifique-se de atender aos seguintes requisitos:

* Seu [!DNL Facebook] a conta de usuário deve ter acesso total à [!DNL Facebook Business Account] que é proprietária da conta de anúncio que você está usando.
* Seu [!DNL Facebook] a conta de usuário deve ter o **[!DNL Manage campaigns]** permissão ativada para a conta de anúncio que você planeja usar.
* A variável **Adobe Experience Cloud** conta comercial deve ser adicionada como um parceiro de publicidade em sua [!DNL Facebook Ad Account]. Use `business ID=206617933627973`. Consulte [Adicionar parceiros ao seu gerente de negócios](https://www.facebook.com/business/help/1717412048538897) na documentação do Facebook para obter detalhes.
  >[!IMPORTANT]
  >
  > Ao configurar as permissões para o Adobe Experience Cloud, você deve ativar o **Gerenciar campanhas** permissão. A permissão é necessária para o [!DNL Adobe Experience Platform] integração.
* Leia e assine o [!DNL Facebook Custom Audiences] Termos de serviço. Para fazer isso, acesse `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, onde `accountID` é seu [!DNL Facebook Ad Account ID].
  >[!IMPORTANT]
  >
  >Ao assinar o [!DNL Facebook Custom Audiences] Termos de serviço, certifique-se de usar a mesma conta de usuário usada para autenticar na API do Facebook.

## Requisitos de correspondência de ID {#id-matching-requirements}

[!DNL Facebook] exige que nenhuma informação pessoal identificável (PII) seja enviada em claro. Portanto, os públicos-alvo foram ativados para [!DNL Facebook] pode ser desativado *com hash* identificadores, como endereços de email ou números de telefone.

Dependendo do tipo de IDs que você assimila no Adobe Experience Platform, é necessário seguir os requisitos correspondentes.

## Requisitos de hash de número de telefone {#phone-number-hashing-requirements}

Há dois métodos para ativar números de telefone no [!DNL Facebook]:

* **Inserir números de telefone brutos**: você pode assimilar números de telefone brutos na [!DNL E.164] formatar em [!DNL Platform]. Eles são atribuídos a hash automaticamente após a ativação. Se você escolher essa opção, sempre assimile seus números de telefone brutos na `Phone_E.164` namespace.
* **Inserir números de telefone com hash**: você pode adicionar seus números de telefone a um hash antes da assimilação em [!DNL Platform]. Se você escolher essa opção, sempre assimile seus números de telefone com hash na `Phone_SHA256` namespace.

>[!NOTE]
>
>Números de telefone assimilados na `Phone` o namespace não pode ser ativado em [!DNL Facebook].

## Requisitos de hash de email {#email-hashing-requirements}

Você pode aplicar hash a endereços de email antes de assimilá-los no Adobe Experience Platform ou usar endereços de email em limpar no Experience Platform e ter [!DNL Platform] coloque hash neles na ativação.

Para saber mais sobre a assimilação de endereços de email no Experience Platform, consulte o [visão geral da assimilação em lote](/help/ingestion/batch-ingestion/overview.md) e a variável [visão geral da assimilação por transmissão](/help/ingestion/streaming-ingestion/overview.md).

Se você optar por criar o hash dos endereços de email, não se esqueça de atender aos seguintes requisitos:

* Cortar todos os espaços à esquerda e à direita da cadeia de caracteres de email; exemplo: `johndoe@example.com`, não `<space>johndoe@example.com<space>`;
* Ao aplicar hash às cadeias de caracteres de email, certifique-se de aplicar hash à cadeia de caracteres em minúsculas;
   * Exemplo: `example@email.com`, não `EXAMPLE@EMAIL.COM`;
* Verifique se a cadeia de caracteres com hash está em minúsculas
   * Exemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, não `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Não salve a corda.

>[!NOTE]
>
>O hash automático é aplicado aos dados de namespaces sem hash [!DNL Platform] na ativação.
> Os dados de origem do atributo não são automaticamente transformados em hash. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação.
> A variável **[!UICONTROL Aplicar transformação]** é exibida somente quando você seleciona atributos como campos de origem. Ela não é exibida ao escolher namespaces.

![Aplique o controle de transformação destacado na etapa de mapeamento.](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Uso de namespaces personalizados {#custom-namespaces}

Antes de poder usar o `Extern_ID` namespace para enviar dados [!DNL Facebook], certifique-se de sincronizar seus próprios identificadores usando [!DNL Facebook Pixel]. Consulte a [Documentação oficial do facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) para obter informações detalhadas.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Exibir destinos]** e **[!UICONTROL Gerenciar destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

O vídeo abaixo também demonstra as etapas para configurar um [!DNL Facebook] direcionar e ativar públicos-alvo.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>A interface do usuário do Experience Platform é atualizada com frequência e pode ter mudado desde a gravação deste vídeo. Para obter as informações mais atualizadas, consulte as [tutorial de configuração de destino](../../ui/connect-destination.md).

### Autenticar para o destino {#authenticate}

1. Localize o destino do Facebook no catálogo de destino e selecione **[!UICONTROL Configurar]**.
2. Selecionar **[!UICONTROL Conectar ao destino]**.
   ![Etapa de autenticação para o Facebook mostrada no fluxo de trabalho de ativação.](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. Insira suas credenciais do Facebook e selecione **Fazer logon**.

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="ID da Conta"
>abstract="Sua ID de conta do anúncio do Facebook. Você pode encontrar essa ID na conta do Facebook Ads Manager. Ao inserir essa ID, sempre utilize o prefixo `act_`."

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL ID da conta]**: Seu [!DNL Facebook Ad Account ID]. Você pode encontrar essa ID em seu [!DNL Facebook Ads Manager] conta. Ao inserir essa ID, sempre utilize o prefixo `act_`.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="Origem do público-alvo"
>abstract="Escolha como os dados do cliente no público-alvo foram coletados originalmente. Os dados serão exibidos no Facebook quando um usuário for direcionado pelo segmento"

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

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados do público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

No **[!UICONTROL Programação de segmento]** etapa, você deve fornecer a [!UICONTROL Origem do público] ao enviar públicos-alvo para [!DNL Facebook Custom Audiences].

![Origem da lista suspensa de Público-alvo mostrada na etapa de ativação do Facebook.](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Exemplo de mapeamento: ativação de dados de público-alvo no [!DNL Facebook Custom Audience] {#example-facebook}

Veja abaixo um exemplo do mapeamento de identidade correto ao ativar dados de público-alvo no [!DNL Facebook Custom Audience].

Selecionar campos de origem:

* Selecione o `Email` namespace como identidade de origem se os endereços de email que você estiver usando não tiverem hash.
* Selecione o `Email_LC_SHA256` namespace como identidade de origem se você tiver hash dos endereços de email do cliente na assimilação de dados no [!DNL Platform], segundo [!DNL Facebook] [requisitos de hash de email](#email-hashing-requirements).
* Selecione o `PHONE_E.164` namespace como identidade de origem se seus dados consistirem em números de telefone sem hash. [!DNL Platform] usará hash nos números de telefone para estar em conformidade com [!DNL Facebook] requisitos.
* Selecione o `Phone_SHA256` namespace como identidade de origem se você tiver hash de números de telefone na assimilação de dados no [!DNL Platform], segundo [!DNL Facebook] [requisitos de hash de número de telefone](#phone-number-hashing-requirements).
* Selecione o `IDFA` namespace como identidade de origem se seus dados consistirem em [!DNL Apple] IDs de dispositivo.
* Selecione o `GAID` namespace como identidade de origem se seus dados consistirem em [!DNL Android] IDs de dispositivo.
* Selecione o `Custom` namespace como identidade de origem se seus dados consistirem de outro tipo de identificadores.

Selecionar campos de destino:

* Selecione o `Email_LC_SHA256` namespace como identidade de destino quando os namespaces de origem `Email` ou `Email_LC_SHA256`.
* Selecione o `Phone_SHA256` namespace como identidade de destino quando os namespaces de origem `PHONE_E.164` ou `Phone_SHA256`.
* Selecione o `IDFA` ou `GAID` namespaces como identidade de destino quando os namespaces de origem são `IDFA` ou `GAID`.
* Selecione o `Extern_ID` namespace como identidade de destino quando o namespace de origem é personalizado.

>[!IMPORTANT]
>
>O hash automático é aplicado aos dados de namespaces sem hash [!DNL Platform] na ativação.
> 
>Os dados de origem do atributo não são automaticamente transformados em hash. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação.

![Aplique o controle de transformação destacado na etapa de mapeamento.](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Dados exportados {#exported-data}

Para [!DNL Facebook], uma ativação bem-sucedida significa que um [!DNL Facebook] o público-alvo personalizado seria criado programaticamente no [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). A associação de público-alvo seria adicionada e removida à medida que os usuários fossem qualificados ou desqualificados para os públicos ativados.

>[!TIP]
>
>A integração entre o Adobe Experience Platform e o [!DNL Facebook] O suporta preenchimentos retroativos de público-alvo histórico. Todas as qualificações históricas de público são enviadas para o [!DNL Facebook] quando você ativa os públicos-alvo para o destino.

## Solução de problemas {#troubleshooting}

### 400 Mensagem de erro de solicitação incorreta {#bad-request}

Ao configurar esse destino, você pode receber o seguinte erro:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Esse erro ocorre quando clientes estão usando contas recém-criadas e o [!DNL Facebook] As permissões do ainda não estão ativas.

Se você receber o `400 Bad Request` mensagem de erro depois de seguir as etapas em [Pré-requisitos da conta do facebook](#facebook-account-prerequisites), aguarde alguns dias para a [!DNL Facebook] para entrar em vigor.
