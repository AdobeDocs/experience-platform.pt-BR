---
keywords: Experience Platform, home, tópicos populares, namespace, Namespace, Namespaces, namespace, namespace de identidade, namespace de identidade, identidade, identidade, serviço de identidade, serviço de identidade
solution: Experience Platform
title: Visão geral do Namespace de identidade
topic: overview
description: 'Os namespaces de identidade são um componente do Identity Service que serve como indicadores do contexto ao qual uma identidade está relacionada. Por exemplo, eles distinguem um valor de "name@email.com" como um endereço de email ou "443522" como uma ID de CRM numérica. '
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 2%

---


# Visão geral do namespace de identidade

Os namespaces de identidade são um componente de [[!DNL Identity Service]](./home.md) que serve como indicadores do contexto ao qual uma identidade está relacionada. Por exemplo, eles distinguem um valor de &quot;name<span>@email.com&quot; como um endereço de email ou &quot;443522&quot; como uma ID de CRM numérica.

## Introdução

Trabalhar com namespaces de identidade requer uma compreensão dos vários serviços da Adobe Experience Platform envolvidos. Antes de começar a trabalhar com namespaces, reveja a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../profile/home.md): Fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Identity Service]](./home.md): Obtenha uma melhor visão de clientes individuais e seu comportamento ao unir identidades em dispositivos e sistemas.
- [[!DNL Privacy Service]](../privacy-service/home.md): Os namespaces de identidade são usados para estar em conformidade com o Regulamento Geral sobre a Proteção de Dados (GDPR), em que as solicitações do GDPR podem ser feitas em relação a um namespace.

## Noções básicas sobre namespaces de identidade

Uma identidade totalmente qualificada inclui um valor de ID e um namespace. Ao corresponder dados de registro em fragmentos de perfil, como quando [!DNL Real-time Customer Profile] mescla dados de perfil, o valor de identidade e o namespace devem corresponder.

Por exemplo, dois fragmentos de perfil podem conter IDs primárias diferentes, mas compartilham o mesmo valor para o namespace &quot;Email&quot;. Portanto, [!DNL Platform] é capaz de ver que esses fragmentos são, na verdade, o mesmo indivíduo e reúne os dados no gráfico de identidade do indivíduo.

![](images/identity-service-stitching.png)

### Tipos de identidade

Os dados podem ser identificados por vários tipos de identidade diferentes. O tipo de identidade é especificado no momento em que o namespace de identidade é criado e controla se os dados persistem ou não no gráfico de identidade e quaisquer instruções especiais para como esses dados devem ser tratados.

Os seguintes tipos de identidade estão disponíveis em [!DNL Platform]:

| Tipo de identidade | Descrição |
| --- | --- |
| ID de cookies | As IDs de cookie identificam navegadores da Web. Essas identidades são essenciais para a expansão e constituem a maioria do gráfico de identidade. No entanto, por natureza, eles caem rapidamente e perdem seu valor ao longo do tempo. |
| ID entre dispositivos | As IDs entre dispositivos identificam um indivíduo e geralmente vinculam outras IDs. Os exemplos incluem uma ID de logon, uma ID de CRM e uma ID de fidelidade. Esta é uma indicação para [!DNL Identity Service] para manipular o valor de forma sensível. |
| ID do dispositivo | As IDs de dispositivo identificam dispositivos de hardware, como IDFA (iPhone e iPad), GAID (Android) e RIDA (Roku), e podem ser compartilhadas por várias pessoas em residências. |
| Endereço de email | Os endereços de email geralmente são associados a uma única pessoa e, portanto, podem ser usados para identificá-la em diferentes canais. Identidades desse tipo incluem informações de identificação pessoal (PII). Esta é uma indicação para [!DNL Identity Service] para manipular o valor de forma sensível. |
| Identificador de não pessoas | As IDs de não pessoas são usadas para armazenar identificadores que exigem namespaces, mas não estão conectadas a um cluster de pessoas. Por exemplo, um SKU de produto, dados relacionados a produtos, organizações ou lojas. |
| Número de telefone | Os números de telefone geralmente são associados a uma única pessoa e, portanto, podem ser usados para identificá-la em diferentes canais. Identidades desse tipo incluem PII. Essa é uma indicação para [!DNL Identity Service] para manipular o valor com sensibilidade. |

### Namespaces padrão

A Experience Platform fornece vários namespaces de identidade disponíveis para todas as organizações. Eles são conhecidos como namespaces padrão e são visíveis usando a API [!DNL Identity Service] ou por meio da interface do usuário da plataforma.

Os seguintes namespaces padrão são fornecidos para uso por todas as organizações na Platform:

| Nome de exibição | Descrição |
| ------------ | ----------- |
| AdCloud | Um namespace que representa a Adobe AdCloud. |
| Adobe Analytics (ID herdada) | Um namespace que representa o Adobe Analytics. Consulte o seguinte documento em [namespaces do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces) para obter mais informações. |
| Apple IDFA (ID para anunciantes) | Um namespace que representa Apple ID para anunciantes. Consulte o seguinte documento sobre [anúncios baseados em juros](https://support.apple.com/en-us/HT202074) para obter mais informações. |
| Serviço de notificação por push da Apple | Um namespace que representa identidades coletadas usando o serviço de Notificação por push da Apple. Consulte o documento a seguir em [Apple Push Notification service](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) para obter mais informações. |
| CORE | Um namespace que representa o Adobe Audience Manager. Esse namespace também pode ser mencionado pelo nome herdado: &quot;Adobe AudienceManager&quot;. Consulte o seguinte documento em [IDs do Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids) para obter mais informações. |
| ECID | Um namespace que representa ECID. Esse namespace também pode ser mencionado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte o seguinte documento em [ECID](./ecid.md) para obter mais informações. |
| Email | Um namespace que representa um endereço de email. Esse tipo de namespace geralmente é associado a uma única pessoa e, portanto, pode ser usado para identificá-la em diferentes canais. |
| Emails (SHA256, em minúsculas) | Um namespace para endereço de email com hash prévio. Os valores fornecidos neste namespace são convertidos em minúsculas antes do hash com SHA256. Os espaços à esquerda e à direita precisam ser cortados antes que um endereço de email seja normalizado. Esta configuração não pode ser alterada retroativamente. Consulte o seguinte documento em [SHA256 hash support](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) para obter mais informações. |
| Firebase Cloud Messaging | Um namespace que representa identidades coletadas usando o Google Firebase Cloud Messaging para notificações por push. Consulte o documento a seguir em [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) para obter mais informações. |
| ID de anúncio do Google (GAID) | Um namespace que representa uma ID de publicidade do Google. Consulte o seguinte documento em [ID de anúncio do Google](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) para obter mais informações. |
| ID de clique do Google | Um namespace que representa uma ID de clique do Google. Consulte o seguinte documento sobre [Rastreamento de cliques no Google Ads](https://developers.google.com/adwords/api/docs/guides/click-tracking) para obter mais informações. |
| Telefone | Um namespace que representa um número de telefone. Esse tipo de namespace geralmente é associado a uma única pessoa e, portanto, pode ser usado para identificá-la em diferentes canais. |
| Telefone (E.164) | Um namespace que representa números brutos de telefone que precisam ser atribuídos a hash no formato E.164. O formato E.164 inclui um sinal de mais (`+`), um código de chamada internacional de país, um código de área local e um número de telefone. Por exemplo: `(+)(country code)(area code)(phone number)`. |
| Telefone (SHA256) | Um namespace que representa números de telefone que precisam ser atribuídos a hash usando SHA256. Você deve remover símbolos, letras e quaisquer zeros à esquerda. Você também deve adicionar o código de chamada do país como um prefixo. |
| Telefone (SHA256_E.164) | Um namespace que representa números brutos de telefone que precisam ser atribuídos a hash usando os formatos SHA256 e E.164. |
| TNTID | Um namespace que representa o Adobe Target. Consulte o seguinte documento no [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en) para obter mais informações. |
| Windows AID | Um namespace que representa uma ID de publicidade do Windows. Consulte o seguinte documento em [ID de publicidade do Windows](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) para obter mais informações. |

Para exibir namespaces padrão na interface do usuário, selecione **[!UICONTROL Identities]** na navegação esquerda e selecione a guia **[!UICONTROL Browse]** para exibir uma lista de namespaces de identidade padrão acessíveis à sua organização. Você pode classificar os namespaces alfabeticamente por seu **[!UICONTROL Nome de exibição]**, **[!UICONTROL Símbolo de identidade]** ou **[!UICONTROL Proprietário]**. Como alternativa, você pode classificar os namespaces cronologicamente pela data de atualização mais recente.

Selecione um namespace para ver informações mais específicas no painel direito.

>[!NOTE]
>
>A Platform também fornece namespaces para fins de integração. Esses namespaces são ocultos por padrão, pois são usados para se conectar com outros sistemas e não são usados para unir identidades. Para exibir namespaces de integração, selecione **[!UICONTROL Exibir identidades de integração]**.

![](./images/browse-namespaces.png)

## Gerenciamento de namespaces personalizados {#manage-namespaces}

Dependendo dos dados organizacionais e dos casos de uso, pode ser necessário criar namespaces personalizados. Os namespaces personalizados podem ser criados usando a API [[!DNL Identity Service]](./api/create-custom-namespace.md) ou por meio da interface do usuário.

Para criar um namespace personalizado usando a interface do usuário, navegue até o espaço de trabalho **[!UICONTROL Identidades]**, selecione **[!UICONTROL Procurar]** e selecione **[!UICONTROL Criar namespace de identidade]**.

![](./images/create.png)

A caixa de diálogo **[!UICONTROL Criar namespace de identidade]** é exibida. Forneça um **[!UICONTROL Nome de exibição]** e **[!UICONTROL Símbolo de identidade]** exclusivos e selecione o tipo de identidade que deseja criar. Você também pode adicionar uma descrição opcional para obter mais informações sobre o namespace. Quando terminar, selecione **[!UICONTROL Criar]**.

>[!IMPORTANT]
>
>Os namespaces definidos são privados de sua organização e exigem um símbolo de identidade exclusivo para serem criados com êxito.

![](./images/create-namespace.png)

Semelhante aos namespaces padrão, você pode selecionar um namespace personalizado na guia **[!UICONTROL Browse]** para exibir seus detalhes. No entanto, com um namespace personalizado, também é possível editar o nome de exibição e a descrição na área de detalhes.

>[!NOTE]
>
>Depois que um namespace é criado, ele não pode ser excluído e seu símbolo de identidade e tipo não podem ser alterados.

## Namespaces nos dados de identidade

Fornecer o namespace para uma identidade depende do método usado para fornecer dados de identidade. Para obter detalhes sobre como fornecer dados de identidade, consulte a seção [fornecendo dados de identidade](./home.md#supplying-identity-data-to-identity-service) na visão geral [!DNL Identity Service].

## Próximas etapas

Agora que você entende os principais conceitos dos namespaces de identidade, pode começar a aprender a trabalhar com o gráfico de identidade usando o [visualizador de gráfico de identidade](./ui/identity-graph-viewer.md).
