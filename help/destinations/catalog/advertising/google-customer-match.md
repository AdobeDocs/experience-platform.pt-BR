---
keywords: correspondência de cliente do google, correspondência de cliente do Google, Correspondência de cliente do Google
title: Conexão Google Customer Match
description: A Correspondência de clientes do Google permite que você use seus dados online e offline para acessar e reengajar seus clientes em propriedades próprias e operadas da Google, como Pesquisa, Compras, Gmail e YouTube.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 1%

---

# [!DNL Google Customer Match] conexão

## Visão geral {#overview}

[Correspondência de cliente do Google](https://support.google.com/google-ads/answer/6379332?hl=en) O permite usar seus dados online e offline para acessar e reengajar seus clientes em propriedades próprias e operadas da Google, como: [!DNL Search], [!DNL Shopping], [!DNL Gmail]e [!DNL YouTube].

![Destino de correspondência do cliente da Google na interface do usuário do Adobe Experience Platform](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando usar a variável [!DNL Google Customer Match] , aqui estão casos de uso de exemplo que os clientes do Adobe Experience Platform podem resolver usando esse recurso.

### Caso de uso nº 1

Uma marca de vestuário atlético deseja alcançar clientes existentes por meio de [!DNL Google Search] e [!DNL Google Shopping] para personalizar ofertas e itens com base em suas compras anteriores e no histórico de navegação. A marca de vestuário pode assimilar endereços de email de seu próprio CRM para o Experience Platform e criar segmentos a partir de seus próprios dados offline. Em seguida, eles podem enviar esses segmentos para o [!DNL Google Customer Match] a utilizar em [!DNL Search] e [!DNL Shopping], otimizando seus gastos com publicidade.

### Caso de uso nº 2

Uma importante empresa de tecnologia lançou um novo telefone. Para promover esse novo modelo de telefone, eles estão buscando conscientizar sobre os novos recursos e funcionalidades do telefone para clientes que possuem modelos anteriores de seus telefones.

Para promover a versão, eles carregam endereços de email do banco de dados do CRM no Experience Platform, usando os endereços de email como identificadores. Os segmentos são criados com base em clientes que possuem modelos de telefone mais antigos. Em seguida, os segmentos são enviados para [!DNL Google Customer Match], para que a empresa possa direcionar os clientes atuais, os clientes que possuem modelos de telefone mais antigos e clientes semelhantes na [!DNL YouTube].

## Governança de dados para [!DNL Google Customer Match] destinos {#data-governance}

Alguns destinos no Experience Platform têm certas regras e obrigações para os dados enviados para a plataforma de destino ou recebidos dela. Você é responsável por entender as limitações e obrigações dos dados e como usá-los no Adobe Experience Platform e na plataforma de destino. O Adobe Experience Platform fornece ferramentas de governança de dados para ajudá-lo a gerenciar algumas dessas obrigações de uso de dados. [Saiba mais](../../../data-governance/labels/overview.md) sobre ferramentas e políticas de governança de dados.

## Identidades suportadas {#supported-identities}

[!DNL Google Customer Match] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| GAID | Google Advertising ID | Selecione essa identidade de destino quando sua identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione essa identidade de destino quando sua identidade de origem for um namespace IDFA. |
| phone_sha256_e.164 | Números de telefone no formato E164, com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e números de telefone com hash SHA256. Siga as instruções em [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para números de telefone sem formatação e com hash, respectivamente. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. Siga as instruções em [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e usar os namespaces apropriados para endereços de email de texto simples e com hash, respectivamente. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. |
| user_id | IDs de usuário personalizadas | Selecione essa identidade de destino quando sua identidade de origem for um namespace personalizado. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone e outros) usados na [!DNL Google Customer Match] destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## [!DNL Google Customer Match] pré-requisitos da conta {#google-account-prerequisites}

Antes de configurar um [!DNL Google Customer Match] destino no Experience Platform, certifique-se de ler e seguir a política do Google para usar [!DNL Customer Match], descritas na [Documentação de suporte do Google](https://support.google.com/google-ads/answer/6299717).

Em seguida, verifique se [!DNL Google] está configurada para uma [!DNL Standard] ou nível de permissão superior. Consulte a [Documentação do Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) para obter detalhes.

### Lista de permissões {#allowlist}

Antes de criar a [!DNL Google Customer Match] no Experience Platform, verifique se [!DNL Google Ads] A conta cumpre os requisitos [Política de correspondência de clientes do Google](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Os clientes com contas compatíveis são autorizados automaticamente pela Google.

## Requisitos de correspondência de ID {#id-matching-requirements}

[!DNL Google] exige que nenhuma informação pessoal identificável (PII) seja enviada de forma clara. Portanto, os públicos-alvo ativados para [!DNL Google Customer Match] pode ser desligado *hash* identificadores, como endereços de email ou números de telefone.

Dependendo do tipo de IDs assimiladas no Adobe Experience Platform, é necessário seguir os requisitos correspondentes.

### Requisitos de hash do número de telefone {#phone-number-hashing-requirements}

Há dois métodos para ativar números de telefone em [!DNL Google Customer Match]:

* **Inserir números de telefone brutos**: você pode assimilar números de telefone brutos no [!DNL E.164] formatar em [!DNL Platform]e são automaticamente atribuídos a hash na ativação. Se você escolher essa opção, certifique-se sempre de assimilar seus números de telefone brutos no `Phone_E.164` namespace.
* **Inserir números de telefone com hash**: você pode fazer o hash prévio dos números de telefone antes da ingestão no [!DNL Platform]. Se você escolher essa opção, certifique-se sempre de assimilar seus números de telefone com hash no `PHONE_SHA256_E.164` namespace.

>[!NOTE]
>
>Números de telefone assimilados no `Phone` o namespace não pode ser ativado em [!DNL Google Customer Match].

### Requisitos de hash de email {#hashing-requirements}

Você pode fazer hash nos endereços de email antes de assimilá-los no Adobe Experience Platform ou usar endereços de email limpos no Experience Platform e ter [!DNL Platform] coloque hash na ativação.

Para obter mais informações sobre os requisitos de hash do Google e outras restrições à ativação, consulte as seguintes seções na documentação de  do Google:

* [[!DNL Customer Match] com endereço de email, endereço ou ID do usuário](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considerações](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Correspondência de cliente com número de telefone](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Correspondência do cliente com IDs de dispositivo móvel](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Para saber mais sobre como assimilar endereços de email no Experience Platform, consulte o [visão geral da ingestão em lote](../../../ingestion/batch-ingestion/overview.md) e [visão geral da assimilação de streaming](../../../ingestion/streaming-ingestion/overview.md).

Se você optar por hash nos endereços de email, certifique-se de estar em conformidade com os requisitos do Google, descritos nos links acima.

### Uso de namespaces personalizados {#custom-namespaces}

Antes de usar a variável `User_ID` namespace para enviar dados ao Google, certifique-se de sincronizar seus próprios identificadores usando [!DNL gTag]. Consulte a [Documentação oficial do Google](https://support.google.com/google-ads/answer/9199250) para obter informações detalhadas.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: fornecer um nome para esta conexão de destino
* **[!UICONTROL Descrição]**: forneça uma descrição para esta conexão de destino
* **[!UICONTROL ID da conta]**: sua ID de cliente do Google. O formato da ID é xxx-xxx-xxxx.

>[!IMPORTANT]
>
> * O **[!UICONTROL Combinar com PII]** a ação de marketing é selecionada por padrão para a variável [!DNL Google Customer Match] e não pode ser removido.


## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

No **[!UICONTROL Agendamento do segmento]** , você deve fornecer a variável [!UICONTROL ID do aplicativo] ao enviar [!DNL IDFA] ou [!DNL GAID] segmentos para [!DNL Google Customer Match].

![Google Customer Match App ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Para obter detalhes sobre como encontrar a variável [!DNL App ID], consulte o [Documentação oficial do Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

### Exemplo de mapeamento: como ativar os dados do público-alvo no [!DNL Google Customer Match] {#example-gcm}

Este é um exemplo do mapeamento de identidade correto ao ativar os dados do público-alvo no [!DNL Google Customer Match].

Seleção de campos de origem:

* Selecione o `Email` namespace como identidade de origem se os endereços de email que você está usando não tiverem hash.
* Selecione o `Email_LC_SHA256` namespace como identidade de origem se você tiver enviado com hash endereços de email do cliente na assimilação de dados em [!DNL Platform], de acordo com [!DNL Google Customer Match] [requisitos de hash de email](#hashing-requirements).
* Selecione o `PHONE_E.164` namespace como identidade de origem se seus dados consistem em números de telefone sem hash. [!DNL Platform] hash os números de telefone para estar em conformidade com [!DNL Google Customer Match] requisitos.
* Selecione o `Phone_SHA256_E.164` namespace como identidade de origem se você tiver hash de números de telefone na assimilação de dados em [!DNL Platform], de acordo com [!DNL Facebook] [requisitos de hash do número de telefone](#phone-number-hashing-requirements).
* Selecione o `IDFA` namespace como identidade de origem se seus dados consistem em [!DNL Apple] IDs de dispositivo.
* Selecione o `GAID` namespace como identidade de origem se seus dados consistem em [!DNL Android] IDs de dispositivo.
* Selecione o `Custom` namespace como identidade de origem se os dados consistem em outro tipo de identificador.

Seleção de campos de destino:

* Selecione o `Email_LC_SHA256` namespace como identidade de destino quando os namespaces de origem forem `Email` ou `Email_LC_SHA256`.
* Selecione o `Phone_SHA256_E.164` namespace como identidade de destino quando os namespaces de origem forem `PHONE_E.164` ou `Phone_SHA256_E.164`.
* Selecione o `IDFA` ou `GAID` namespaces como identidade de destino quando os namespaces de origem são `IDFA` ou `GAID`.
* Selecione o `User_ID` namespace como identidade de destino quando seu namespace de origem é personalizado.

![Mapeamento de identidade](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Os dados de namespaces sem hash são automaticamente atribuídos a hash por [!DNL Platform] após a ativação.

Os dados da fonte de atributo não são automaticamente transformados em hash. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação.

![Transformação de mapeamento de identidade](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Verificar se a ativação de segmentos foi bem-sucedida {#verify-activation}

Após concluir o fluxo de ativação, mude para seu **[!UICONTROL Anúncios do Google]** conta. Os segmentos ativados são mostrados em sua conta do Google como listas de clientes. Observe que, dependendo do tamanho do seu segmento, alguns públicos-alvo não são preenchidos a menos que haja mais de 100 usuários ativos para serem atendidos.

Ao mapear um segmento para ambos [!DNL IDFA] e [!DNL GAID] IDs móveis, [!DNL Google Customer Match] cria um segmento separado para cada mapeamento de ID. Seu [!DNL Google Ads] A conta mostra dois segmentos diferentes, um para a variável [!DNL IDFA]e um para o [!DNL GAID] mapeamento.

## Solução de problemas {#troubleshooting}

### 400 Mensagem de erro de solicitação incorreta {#bad-request}

Ao configurar esse destino, você pode receber o seguinte erro:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Esse erro ocorre quando as contas do cliente não estão em conformidade com a [pré-requisitos](#google-account-prerequisites). Para corrigir esse problema, entre em contato com a Google e verifique se sua conta está incluída na lista de permissões e está configurada para um [!DNL Standard] ou nível de permissão superior. Consulte a [Documentação do Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) para obter detalhes.

## Recursos adicionais {#additional-resources}

* [Integração da correspondência do cliente do Google - Tutorial em vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)

