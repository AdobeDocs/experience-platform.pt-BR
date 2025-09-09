---
keywords: correspondência do cliente do google;correspondência do cliente do Google;Correspondência do cliente do Google
title: Conexão de Correspondência de cliente do Google
description: O Google Customer Match permite usar seus dados online e offline para acessar e reengajar com seus clientes nas propriedades próprias e operadas da Google, como Search, Shopping e Gmail.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 4541e812ac1f44b5374b81685c1e41cb7f00993f
workflow-type: tm+mt
source-wordcount: '2451'
ht-degree: 0%

---

# [!DNL Google Customer Match] conexão

>[!IMPORTANT]
>
> A Google está lançando alterações na [API do Google Ads](https://developers.google.com/google-ads/api/docs/start), na [Correspondência do Cliente](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) e na [API de Exibição e Vídeo 360](https://developers.google.com/display-video/api/guides/getting-started/overview) para oferecer suporte aos requisitos de conformidade e consentimento definidos na [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) da União Europeia ([Política de Consentimento do Usuário](https://www.google.com/about/company/user-consent-policy/) da UE). A aplicação dessas alterações aos requisitos de consentimento estará em vigor a partir de 6 de março de 2024.
> &#x200B;><br/>
> &#x200B;>Para aderir à política de consentimento do usuário da UE e continuar criando listas de públicos-alvo para usuários no Espaço Econômico Europeu (EEE), anunciantes e parceiros devem garantir que eles transmitem o consentimento do usuário final ao fazer upload dos dados de público-alvo. Como parceiro da Google, a Adobe fornece as ferramentas necessárias para cumprir esses requisitos de consentimento de acordo com a DMA na União Europeia.
> &#x200B;><br/>
> &#x200B;>Os clientes que compraram o Adobe Privacy &amp; Security Shield e configuraram uma [política de consentimento](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar perfis não consentidos não precisam tomar nenhuma ação.
> &#x200B;><br/>
> &#x200B;>Os clientes que não compraram o Adobe Privacy &amp; Security Shield devem usar os recursos de [definição de segmento](../../../segmentation/home.md#segment-definitions) no [Construtor de segmentos](../../../segmentation/ui/segment-builder.md) para filtrar perfis não consentidos, a fim de continuar usando os Destinos do Real-Time CDP Google existentes sem interrupção.

O [[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) permite que você use seus dados online e offline para acessar e reengajar com seus clientes nas propriedades próprias e operadas da Google, como: [!DNL Search], [!DNL Shopping] e [!DNL Gmail].

>[!TIP]
>
>Para alcançar os clientes no inventário do [!DNL YouTube], use o destino [Google Customer Match + DV360](/help/destinations/catalog/advertising/google-customer-match-dv360.md), que usa a API do Google Audience Partner.

![Destino do Google Customer Match na interface do Adobe Experience Platform.](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando usar o destino [!DNL Google Customer Match], veja a seguir exemplos de casos de uso que os clientes da Adobe Experience Platform podem resolver usando esse recurso.

### Caso de uso #1

Uma marca de vestuário atlético deseja alcançar clientes existentes por meio de [!DNL Google Search] e [!DNL Google Shopping] para personalizar ofertas e itens com base em suas compras anteriores e histórico de navegação. A marca apparel pode assimilar endereços de email de seu próprio CRM para o Experience Platform e criar públicos-alvo a partir de seus próprios dados offline. Em seguida, eles podem enviar esses públicos-alvo para [!DNL Google Customer Match] para serem usados em [!DNL Search] e [!DNL Shopping], otimizando seus gastos com publicidade.

### Caso de uso #2

>[!TIP]
>
>Para executar este caso de uso no inventário do [!DNL YouTube], use o novo destino [Google Customer Match + DV360](/help/destinations/catalog/advertising/google-customer-match-dv360.md), que usa a API do Google Audience Partner.

Uma proeminente empresa de tecnologia lançou um novo telefone. Para promover esse novo modelo de telefone, eles estão procurando conscientizar os clientes sobre os novos recursos e funcionalidades do telefone para os clientes que possuem modelos anteriores de seus telefones.

Para promover a versão, eles carregam endereços de email do banco de dados do CRM na Experience Platform, usando os endereços de email como identificadores. Os públicos-alvo são criados com base nos clientes que possuem modelos de telefone mais antigos. Os públicos-alvo serão enviados para [!DNL Google Customer Match], para que a empresa possa direcionar os clientes atuais, os clientes que possuem modelos de telefone mais antigos e clientes semelhantes em [!DNL YouTube].

## Governança de dados para [!DNL Google Customer Match] destinos {#data-governance}

Alguns destinos no Experience Platform têm determinadas regras e obrigações para dados enviados para a plataforma de destino ou recebidos dela. Você é responsável por entender as limitações e obrigações de seus dados e como usá-los no Adobe Experience Platform e na plataforma de destino. O Adobe Experience Platform fornece ferramentas de governança de dados para ajudar você a gerenciar algumas dessas obrigações de uso de dados. [Saiba mais](../../../data-governance/labels/overview.md) sobre políticas e ferramentas de governança de dados.

## Identidades suportadas {#supported-identities}

[!DNL Google Customer Match] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| `GAID` | GOOGLE ADVERTISING ID | Selecione essa identidade de destino quando a identidade de origem for um namespace GAID. |
| `IDFA` | Apple ID para anunciantes | Selecione essa identidade de destino quando sua identidade de origem for um namespace IDFA. |
| `phone_sha256_e.164` | Números de telefone no formato E164, com hash com o algoritmo SHA256 | Os números de telefone com hash SHA256 e texto sem formatação são compatíveis com o Adobe Experience Platform. Siga as instruções na seção [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para texto sem formatação e números de telefone com hash, respectivamente. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Aplicar transformação]** para que [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |
| `email_lc_sha256` | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Siga as instruções na seção [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para texto sem formatação e endereços de email com hash, respectivamente. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Aplicar transformação]** para que [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |
| `user_id` | IDs de usuário personalizadas | Selecione esta identidade de destino quando sua identidade de origem for um namespace personalizado. |
| `address_info_first_name` | Nome do usuário | Esta identidade de destino deve ser usada com `address_info_last_name`, `address_info_country_code` e `address_info_postal_code` quando você quiser enviar dados de endereço de correspondência para seu destino. <br><br>Para garantir que o Google corresponda ao endereço, mapeie todos os quatro campos de endereço (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` e `address_info_postal_code`) e verifique se nenhum desses campos tem dados ausentes nos perfis exportados. <br> Se algum campo não estiver mapeado ou contiver dados ausentes, o Google não corresponderá ao endereço. |
| `address_info_last_name` | Sobrenome do usuário | Esta identidade de destino deve ser usada com `address_info_first_name`, `address_info_country_code` e `address_info_postal_code` quando você quiser enviar dados de endereço de correspondência para seu destino. <br><br>Para garantir que o Google corresponda ao endereço, mapeie todos os quatro campos de endereço (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` e `address_info_postal_code`) e verifique se nenhum desses campos tem dados ausentes nos perfis exportados. <br> Se algum campo não estiver mapeado ou contiver dados ausentes, o Google não corresponderá ao endereço. |
| `address_info_country_code` | Código do país do endereço do usuário | Esta identidade de destino deve ser usada com `address_info_first_name`, `address_info_last_name` e `address_info_postal_code` quando você quiser enviar dados de endereço de correspondência para seu destino. <br><br>Para garantir que o Google corresponda ao endereço, mapeie todos os quatro campos de endereço (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` e `address_info_postal_code`) e verifique se nenhum desses campos tem dados ausentes nos perfis exportados. <br> Se algum campo não estiver mapeado ou contiver dados ausentes, o Google não corresponderá ao endereço. <br><br>Formato aceito: códigos de país de duas letras em minúsculas no formato [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). |
| `address_info_postal_code` | CEP do endereço do usuário | Esta identidade de destino deve ser usada com `address_info_first_name`, `address_info_last_name` e `address_info_country_code` quando você quiser enviar dados de endereço de correspondência para seu destino. <br><br>Para garantir que o Google corresponda ao endereço, mapeie todos os quatro campos de endereço (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` e `address_info_postal_code`) e verifique se nenhum desses campos tem dados ausentes nos perfis exportados. <br> Se algum campo não estiver mapeado ou contiver dados ausentes, o Google não corresponderá ao endereço. |

{style="table-layout:auto"}

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
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público-alvo]** | Você está exportando todos os membros de um público com os identificadores (nome, número de telefone e outros) usados no destino [!DNL Google Customer Match]. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Pré-requisitos da conta de [!DNL Google Customer Match] {#google-account-prerequisites}

Antes de configurar um destino [!DNL Google Customer Match] no Experience Platform, leia e siga a política da Google para usar o [!DNL Customer Match], descrita na [documentação de suporte do Google](https://support.google.com/google-ads/answer/6299717).

Em seguida, verifique se a sua conta [!DNL Google] está configurada para um nível de permissão [!DNL Standard] ou superior. Consulte a [documentação do Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&rd=1) para obter detalhes.

### Lista de permissões {#allowlist}

Antes de criar o destino [!DNL Google Customer Match] no Experience Platform, verifique se a sua conta [!DNL Google Ads] está em conformidade com a [[!DNL Google Customer Match] política](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Incluir na lista de permissões Os clientes com contas em conformidade são automaticamente notificados pela Google.

## Requisitos de correspondência de ID {#id-matching-requirements}

[!DNL Google] exige que nenhuma informação pessoal identificável (PII) seja enviada em branco. Portanto, os públicos ativados para [!DNL Google Customer Match] podem ser digitados de *identificadores com hash*, como endereços de email ou números de telefone.

Dependendo do tipo de IDs que você assimila no Adobe Experience Platform, é necessário seguir os requisitos correspondentes.

### Requisitos de hash de número de telefone {#phone-number-hashing-requirements}

Há dois métodos para ativar números de telefone em [!DNL Google Customer Match]:

* **Ingestão de números de telefone brutos**: você pode assimilar números de telefone brutos no formato [!DNL E.164] no [!DNL Experience Platform], que são automaticamente transformados em hash após a ativação. Se você escolher essa opção, sempre assimile seus números de telefone brutos no namespace `Phone_E.164`.
* **Números de telefone com hash de assimilação**: você pode colocar seus números de telefone em hash antes de assimilar em [!DNL Experience Platform]. Se você escolher essa opção, sempre assimile seus números de telefone com hash no namespace `PHONE_SHA256_E.164`.

>[!NOTE]
>
>Os números de telefone assimilados no namespace `Phone` não podem ser ativados em [!DNL Google Customer Match].

### Requisitos de hash de email {#hashing-requirements}

Você pode aplicar hash a endereços de email antes de assimilá-los no Adobe Experience Platform, ou usar endereços de email em limpar no Experience Platform, e aplicar hash a [!DNL Experience Platform] neles na ativação.

Para obter mais informações sobre os requisitos de hash do Google e outras restrições na ativação, consulte as seguintes seções na documentação do Google:

* [[!DNL Customer Match] com endereço de email, endereço ou ID de usuário](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considerações](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] com número de telefone](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] com IDs de dispositivo móvel](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Para saber mais sobre a assimilação de endereços de email no Experience Platform, consulte a [visão geral da assimilação em lote](../../../ingestion/batch-ingestion/overview.md) e a [visão geral da assimilação de streaming](../../../ingestion/streaming-ingestion/overview.md).

Se você optar por criar o hash dos endereços de email, certifique-se de cumprir os requisitos da Google, descritos nos links acima.

### Requisitos de hash do campo de endereço {#address-field-hashing}

Ao mapear campos relacionados a endereços para [!DNL Google Customer Match], o Experience Platform **hash** automaticamente os valores `address_info_first_name` e `address_info_last_name` antes de enviá-los para o Google. Esse hash automático é necessário para estar em conformidade com os requisitos de segurança e privacidade da Google.

**não** forneça valores com hash para `address_info_first_name` ou `address_info_last_name`. Se você fornecer valores com hash, o processo correspondente falhará.

### Uso de namespaces personalizados {#custom-namespaces}

Antes de poder usar o namespace `User_ID` para enviar dados para o Google, sincronize seus próprios identificadores usando o [!DNL gTag]. Consulte a [documentação oficial da Google](https://support.google.com/google-ads/answer/9199250) para obter informações detalhadas.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Experience Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Experience Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Visão geral do vídeo {#video-overview}

Assista ao vídeo abaixo para obter uma explicação dos benefícios e como ativar os dados para o Google Customer Match.

>[!VIDEO](https://video.tv.adobe.com/v/326489?captions=por_br)

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: forneça um nome para esta conexão de destino
* **[!UICONTROL Descrição]**: forneça uma descrição para esta conexão de destino
* **[!UICONTROL ID da conta]**: sua [ID de cliente do Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en). O formato da ID é xxx-xxx-xxxx. Se você estiver usando o [!DNL Google Ads Manager Account (My Client Center)], não use sua ID de Conta de Gerente. Em vez disso, use a [ID de cliente do Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en).

>[!NOTE]
>
>Durante o processo de conexão OAuth2, você pode ver &quot;Marketo Test&quot; exibido como o nome do projeto OAuth do Google. Esse é um comportamento normal, pois a Adobe usa esse nome de projeto para a integração do Customer Match da Google. Isso não afeta a configuração de destino.

>[!IMPORTANT]
>
> * A ação de marketing **[!UICONTROL Combinar com PII]** está selecionada por padrão para o destino [!DNL Google Customer Match] e não pode ser removida.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades* para destinos, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados de público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

Na etapa **[!UICONTROL Agendamento de segmento]**, você deve fornecer a [!UICONTROL ID do aplicativo] ao enviar [!DNL IDFA] ou [!DNL GAID] públicos-alvo para [!DNL Google Customer Match].

![Campo de ID do aplicativo de correspondência do cliente do Google realçado na etapa de agendamento de segmento do fluxo de trabalho de ativação.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Para obter detalhes sobre como encontrar o [!DNL App ID], consulte a [documentação oficial do Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) ou pergunte ao representante da Google.

### Exemplo de mapeamento: ativação de dados de público-alvo em [!DNL Google Customer Match] {#example-gcm}

Este é um exemplo de mapeamento de identidade correto ao ativar dados de público-alvo em [!DNL Google Customer Match].

Selecionar campos de origem:

* Selecione o namespace `Email` como identidade de origem se os endereços de email que você está usando não tiverem hash.
* Selecione o namespace `Email_LC_SHA256` como identidade de origem se você tiver hash dos endereços de email do cliente na assimilação de dados no [!DNL Experience Platform], de acordo com os [!DNL Google Customer Match] [requisitos de hash de email](#hashing-requirements).
* Selecione o namespace `PHONE_E.164` como identidade de origem se seus dados consistirem em números de telefone sem hash. [!DNL Experience Platform] aplicará hash aos números de telefone para atender aos requisitos de [!DNL Google Customer Match].
* Selecione o namespace `Phone_SHA256_E.164` como identidade de origem se você tiver hash de números de telefone na assimilação de dados em [!DNL Experience Platform], de acordo com [!DNL Facebook] [requisitos de hash de número de telefone](#phone-number-hashing-requirements).
* Selecione o namespace `IDFA` como identidade de origem se seus dados consistirem de [!DNL Apple] IDs de dispositivo.
* Selecione o namespace `GAID` como identidade de origem se seus dados consistirem de [!DNL Android] IDs de dispositivo.
* Selecione o namespace `Custom` como identidade de origem se os dados consistirem de outro tipo de identificadores.

Selecionar campos de destino:

* Selecione o namespace `Email_LC_SHA256` como identidade de destino quando os namespaces de origem forem `Email` ou `Email_LC_SHA256`.
* Selecione o namespace `Phone_SHA256_E.164` como identidade de destino quando os namespaces de origem forem `PHONE_E.164` ou `Phone_SHA256_E.164`.
* Selecione os namespaces `IDFA` ou `GAID` como identidade de destino quando os namespaces de origem forem `IDFA` ou `GAID`.
* Selecione o namespace `User_ID` como identidade de destino quando o namespace de origem for personalizado.

![Mapeamento de identidade entre campos de origem e destino mostrado na etapa Mapeamento do fluxo de trabalho de ativação.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

O hash automático de dados de namespaces sem hash é criado por [!DNL Experience Platform] após a ativação.

Os dados de origem do atributo não são automaticamente transformados em hash. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Aplicar transformação]** para que [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação.

![Aplicar controle de transformação realçado na etapa Mapeamento do fluxo de trabalho de ativação.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Monitorar destino {#monitor-destination}

Depois de se conectar ao destino e estabelecer um fluxo de dados de destino, você pode usar a [funcionalidade de monitoramento](/help/dataflows/ui/monitor-destinations.md) do Real-Time CDP para obter informações abrangentes sobre os registros de perfil ativados para o destino em cada execução de fluxo de dados.

>[!IMPORTANT]
>
>Quando você mapeia as quatro identidades de destino relacionadas ao endereço (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` e `address_info_postal_code`), elas são contadas como identidades individuais separadas para cada perfil na página de monitoramento de fluxo de dados.

## Verificar se a ativação do público-alvo foi bem-sucedida {#verify-activation}

Após concluir o fluxo de ativação, alterne para sua conta do **[!UICONTROL Google Ads]**. Os públicos ativados são mostrados na sua conta do Google como listas de clientes. Dependendo do tamanho do público-alvo, alguns públicos-alvo não são preenchidos, a menos que haja mais de 100 usuários ativos para atender.

Ao mapear um público para as IDs móveis do [!DNL IDFA] e do [!DNL GAID], o [!DNL Google Customer Match] cria um público separado para cada mapeamento de ID. Sua conta do [!DNL Google Ads] mostra dois segmentos diferentes, um para o [!DNL IDFA] e um para o mapeamento do [!DNL GAID].

## Solução de problemas {#troubleshooting}

### 400 Mensagem de erro de solicitação incorreta {#bad-request}

Ao configurar esse destino, você pode receber o seguinte erro:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Este erro ocorre quando as contas de clientes não atendem aos [pré-requisitos](#google-account-prerequisites). Para corrigir esse problema, contate a Google e verifique se sua conta está incluída na lista de permissões e configurada para um nível de permissão [!DNL Standard] ou superior. Consulte a [documentação do Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&rd=1) para obter detalhes.