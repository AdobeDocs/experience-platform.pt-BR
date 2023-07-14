---
keywords: correspondência do cliente do google;correspondência do cliente do Google;Correspondência do cliente do Google
title: Conexão de Correspondência de cliente do Google
description: O Google Customer Match permite usar seus dados online e offline para acessar e reengajar com seus clientes nas propriedades próprias e operadas da Google, como Search, Shopping, Gmail e YouTube.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 1c9725c108d55aea5d46b086fbe010ab4ba6cf45
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 1%

---

# [!DNL Google Customer Match] conexão

## Visão geral {#overview}

[[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) O permite que você use seus dados online e offline para acessar e reengajar com seus clientes nas propriedades próprias e operadas da Google, como: [!DNL Search], [!DNL Shopping], [!DNL Gmail], e [!DNL YouTube].

![Destino da Correspondência de clientes do Google na interface do usuário do Adobe Experience Platform.](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando usar o [!DNL Google Customer Match] destino, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse recurso.

### Caso de uso #1

Uma marca de vestuário esportivo deseja alcançar clientes existentes por meio de [!DNL Google Search] e [!DNL Google Shopping] para personalizar ofertas e itens com base em suas compras anteriores e histórico de navegação. A marca apparel pode assimilar endereços de email de seu próprio CRM para o Experience Platform e criar públicos-alvo a partir de seus próprios dados offline. Em seguida, eles podem enviar esses públicos-alvo para [!DNL Google Customer Match] para ser usado em [!DNL Search] e [!DNL Shopping], otimizando seus gastos com publicidade.

### Caso de uso #2

Uma proeminente empresa de tecnologia lançou um novo telefone. Para promover esse novo modelo de telefone, eles estão procurando conscientizar os clientes sobre os novos recursos e funcionalidades do telefone para os clientes que possuem modelos anteriores de seus telefones.

Para promover a versão, eles carregam endereços de email do banco de dados do CRM no Experience Platform, usando os endereços de email como identificadores. Os públicos-alvo são criados com base nos clientes que possuem modelos de telefone mais antigos. Depois, os públicos-alvo são enviados para o [!DNL Google Customer Match], para que a empresa possa direcionar os clientes atuais, os clientes que possuem modelos de telefone mais antigos e clientes semelhantes no [!DNL YouTube].

## Governança de dados para [!DNL Google Customer Match] destinos {#data-governance}

Alguns destinos no Experience Platform têm determinadas regras e obrigações para dados enviados para a plataforma de destino ou recebidos dela. Você é responsável por entender as limitações e obrigações de seus dados e como usá-los no Adobe Experience Platform e na plataforma de destino. O Adobe Experience Platform fornece ferramentas de governança de dados para ajudar você a gerenciar algumas dessas obrigações de uso de dados. [Saiba mais](../../../data-governance/labels/overview.md) sobre as políticas e ferramentas de governança de dados.

## Identidades suportadas {#supported-identities}

[!DNL Google Customer Match] O oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| GAID | ID de publicidade do Google | Selecione essa identidade de destino quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione essa identidade de destino quando sua identidade de origem for um namespace IDFA. |
| phone_sha256_e.164 | Números de telefone no formato E164, com hash com o algoritmo SHA256 | Os números de telefone com hash SHA256 e texto sem formatação são compatíveis com o Adobe Experience Platform. Siga as instruções em [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para texto sem formatação e números de telefone com hash, respectivamente. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Siga as instruções em [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para texto simples e endereços de email com hash, respectivamente. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. |
| user_id | IDs de usuário personalizadas | Selecione esta identidade de destino quando sua identidade de origem for um namespace personalizado. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve todos os públicos-alvo que você pode exportar para esse destino.

Todos os destinos oferecem suporte à ativação de públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md).

Além disso, esse destino também suporta a ativação dos públicos-alvo descritos na tabela abaixo.

| Tipo de público | Descrição |
---------|----------|
| Uploads personalizados | Públicos-alvo assimilados em Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público-alvo com os identificadores (nome, número de telefone e outros) usados no [!DNL Google Customer Match] destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## [!DNL Google Customer Match] pré-requisitos da conta {#google-account-prerequisites}

Antes de configurar um [!DNL Google Customer Match] destino no Experience Platform, leia e siga a política da Google para uso de [!DNL Customer Match], delineado no [Documentação de suporte do Google](https://support.google.com/google-ads/answer/6299717).

Em seguida, verifique se [!DNL Google] a conta do está configurada para um [!DNL Standard] ou um nível de permissão superior. Consulte a [Documentação do Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) para obter detalhes.

### Lista de permissões {#allowlist}

Antes de criar o [!DNL Google Customer Match] destino no Experience Platform, verifique se o [!DNL Google Ads] conta está em conformidade com o [[!DNL Google Customer Match] política](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Os clientes com contas em conformidade são automaticamente permitidos listados pela Google.

## Requisitos de correspondência de ID {#id-matching-requirements}

[!DNL Google] exige que nenhuma informação pessoal identificável (PII) seja enviada em claro. Portanto, os públicos-alvo foram ativados para [!DNL Google Customer Match] pode ser desativado *com hash* identificadores, como endereços de email ou números de telefone.

Dependendo do tipo de IDs que você assimila no Adobe Experience Platform, é necessário seguir os requisitos correspondentes.

### Requisitos de hash de número de telefone {#phone-number-hashing-requirements}

Há dois métodos para ativar números de telefone no [!DNL Google Customer Match]:

* **Inserir números de telefone brutos**: você pode assimilar números de telefone brutos na [!DNL E.164] formatar em [!DNL Platform], e eles recebem hash automaticamente na ativação. Se você escolher essa opção, sempre assimile seus números de telefone brutos na `Phone_E.164` namespace.
* **Inserir números de telefone com hash**: você pode adicionar seus números de telefone a um hash antes da assimilação em [!DNL Platform]. Se você escolher essa opção, sempre assimile seus números de telefone com hash na `PHONE_SHA256_E.164` namespace.

>[!NOTE]
>
>Números de telefone assimilados na `Phone` o namespace não pode ser ativado em [!DNL Google Customer Match].

### Requisitos de hash de email {#hashing-requirements}

Você pode aplicar hash a endereços de email antes de assimilá-los no Adobe Experience Platform ou usar endereços de email em limpar no Experience Platform e ter [!DNL Platform] coloque hash neles na ativação.

Para obter mais informações sobre os requisitos de hash do Google e outras restrições na ativação, consulte as seguintes seções na documentação do Google:

* [[!DNL Customer Match] com endereço de email, endereço ou ID de usuário](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considerações](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] com número de telefone](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] com IDs de dispositivo móvel](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Para saber mais sobre a assimilação de endereços de email no Experience Platform, consulte o [visão geral da assimilação em lote](../../../ingestion/batch-ingestion/overview.md) e a variável [visão geral da assimilação por transmissão](../../../ingestion/streaming-ingestion/overview.md).

Se você optar por criar o hash dos endereços de email, certifique-se de cumprir os requisitos da Google, descritos nos links acima.

### Uso de namespaces personalizados {#custom-namespaces}

Antes de poder usar o `User_ID` para enviar dados ao Google, certifique-se de sincronizar seus próprios identificadores usando [!DNL gTag]. Consulte a [Documentação oficial do Google](https://support.google.com/google-ads/answer/9199250) para obter informações detalhadas.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configuração](../../ui/connect-destination.md) Para esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: forneça um nome para esta conexão de destino
* **[!UICONTROL Descrição]**: forneça uma descrição para esta conexão de destino
* **[!UICONTROL ID da conta]**: seu [ID de cliente do Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en). O formato da ID é xxx-xxx-xxxx. Se você estiver usando o [!DNL Google Ads Manager Account (My Client Center)], não use sua ID de conta de gerente. Use o [ID de cliente do Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en) em vez disso.

>[!IMPORTANT]
>
> * A variável **[!UICONTROL Combinar com PII]** a ação de marketing é selecionada por padrão para o [!DNL Google Customer Match] destino e não podem ser removidos.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

No **[!UICONTROL Programação de segmento]** etapa, você deve fornecer a [!UICONTROL ID do aplicativo] ao enviar [!DNL IDFA] ou [!DNL GAID] públicos-alvo para [!DNL Google Customer Match].

![ID do aplicativo de correspondência do cliente da Google](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Para obter detalhes sobre como encontrar o [!DNL App ID], consulte o [Documentação oficial do Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

### Exemplo de mapeamento: ativação de dados de público-alvo no [!DNL Google Customer Match] {#example-gcm}

Este é um exemplo de mapeamento de identidade correto ao ativar dados de público-alvo no [!DNL Google Customer Match].

Selecionar campos de origem:

* Selecione o `Email` namespace como identidade de origem se os endereços de email que você estiver usando não tiverem hash.
* Selecione o `Email_LC_SHA256` namespace como identidade de origem se você tiver hash dos endereços de email do cliente na assimilação de dados no [!DNL Platform], segundo [!DNL Google Customer Match] [requisitos de hash de email](#hashing-requirements).
* Selecione o `PHONE_E.164` namespace como identidade de origem se seus dados consistirem em números de telefone sem hash. [!DNL Platform] usará hash nos números de telefone para estar em conformidade com [!DNL Google Customer Match] requisitos.
* Selecione o `Phone_SHA256_E.164` namespace como identidade de origem se você tiver hash de números de telefone na assimilação de dados no [!DNL Platform], segundo [!DNL Facebook] [requisitos de hash de número de telefone](#phone-number-hashing-requirements).
* Selecione o `IDFA` namespace como identidade de origem se seus dados consistirem em [!DNL Apple] IDs de dispositivo.
* Selecione o `GAID` namespace como identidade de origem se seus dados consistirem em [!DNL Android] IDs de dispositivo.
* Selecione o `Custom` namespace como identidade de origem se seus dados consistirem de outro tipo de identificadores.

Selecionar campos de destino:

* Selecione o `Email_LC_SHA256` namespace como identidade de destino quando os namespaces de origem `Email` ou `Email_LC_SHA256`.
* Selecione o `Phone_SHA256_E.164` namespace como identidade de destino quando os namespaces de origem `PHONE_E.164` ou `Phone_SHA256_E.164`.
* Selecione o `IDFA` ou `GAID` namespaces como identidade de destino quando os namespaces de origem são `IDFA` ou `GAID`.
* Selecione o `User_ID` namespace como identidade de destino quando o namespace de origem é personalizado.

![Mapeamento de identidade](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

O hash automático é aplicado aos dados de namespaces sem hash [!DNL Platform] na ativação.

Os dados de origem do atributo não são automaticamente transformados em hash. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação.

![Transformação de mapeamento de identidade](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Verificar se a ativação do público-alvo foi bem-sucedida {#verify-activation}

Após concluir o fluxo de ativação, alterne para o **[!UICONTROL Anúncios do Google]** conta. Os públicos ativados são mostrados na sua conta do Google como listas de clientes. Observe que, dependendo do tamanho do público, alguns públicos-alvo não são preenchidos, a menos que haja mais de 100 usuários ativos para atender.

Ao mapear um público-alvo para ambos [!DNL IDFA] e [!DNL GAID] IDs móveis, [!DNL Google Customer Match] O cria um público-alvo separado para cada mapeamento de ID. Seu [!DNL Google Ads] mostra dois segmentos diferentes, um para o [!DNL IDFA], e um para o [!DNL GAID] mapeamento.

## Solução de problemas {#troubleshooting}

### 400 Mensagem de erro de solicitação incorreta {#bad-request}

Ao configurar esse destino, você pode receber o seguinte erro:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Esse erro ocorre quando as contas do cliente não estão em conformidade com os [pré-requisitos](#google-account-prerequisites). Para corrigir esse problema, entre em contato com a Google e verifique se sua conta está incluída na lista de permissões e configurada para um [!DNL Standard] ou um nível de permissão superior. Consulte a [Documentação do Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) para obter detalhes.

## Recursos adicionais {#additional-resources}

* [Integrar [!DNL Google Customer Match] - Tutorial em vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html?lang=pt-BR)

