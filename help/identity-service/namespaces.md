---
title: Visão geral do namespace de identidade
description: Os namespaces de identidade são um componente do Serviço de identidade que serve como indicadores do contexto ao qual uma identidade está relacionada. Por exemplo, eles distinguem um valor "name@email.com" como um endereço de email ou "443522" como uma ID de CRM numérica.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: fc886dc0d7abb1df76c12edc423bc788b443a788
workflow-type: tm+mt
source-wordcount: '1719'
ht-degree: 8%

---

# Visão geral do namespace de identidade

Os namespaces de identidade são um componente de [[!DNL Identity Service]](./home.md) que servem como indicadores do contexto ao qual uma identidade está relacionada. Por exemplo, eles distinguem um valor de &quot;name<span>@email.com&quot; como um endereço de email ou &quot;443522&quot; como uma ID de CRM numérica.

## Introdução

Trabalhar com namespaces de identidade requer uma compreensão dos vários serviços envolvidos da Adobe Experience Platform. Antes de começar a trabalhar com namespaces, reveja a documentação dos seguintes serviços:

- [[!DNL Real-Time Customer Profile]](../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Identity Service]](./home.md): obtenha uma melhor visualização dos clientes individuais e do comportamento deles ao unir as identidades de vários dispositivos e sistemas.
- [[!DNL Privacy Service]](../privacy-service/home.md): os namespaces de identidade são usados em solicitações de conformidade para regulamentos legais de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR). Cada solicitação de privacidade é feita em relação a um namespace para identificar quais dados dos consumidores devem ser afetados.

## Noções básicas sobre namespaces de identidade

Uma identidade totalmente qualificada inclui um valor de ID e um namespace. Ao corresponder dados de registro em fragmentos de perfil, como quando [!DNL Real-Time Customer Profile] mescla os dados do perfil, o valor da identidade e o namespace devem corresponder.

Por exemplo, dois fragmentos de perfil podem conter IDs primárias diferentes, mas compartilham o mesmo valor para o namespace &quot;Email&quot;, portanto [!DNL Platform] O é capaz de ver que esses fragmentos são realmente o mesmo indivíduo e reúne os dados no gráfico de identidade do indivíduo.

![](images/identity-service-stitching.png)

### Tipos de identidade {#identity-types}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="Especificar tipo de identidade"
>abstract="O tipo de identidade controla se os dados são armazenados ou não no gráfico de identidade. Identificadores que não sejam de pessoas não serão armazenados, e todos os outros tipos de identidade serão armazenados."
>text="Learn more in documentation"

Os dados podem ser identificados por vários tipos de identidade diferentes. O tipo de identidade é especificado no momento em que o namespace de identidade é criado e controla se os dados são ou não mantidos no gráfico de identidade e quaisquer instruções especiais sobre como esses dados devem ser tratados. Todos os tipos de identidade exceto **Identificador não pessoal** siga o mesmo comportamento de compilação de um namespace e seu valor de ID correspondente a um cluster de gráficos de identidade. Os dados não são compilados ao usar **Identificador não pessoal**.

Os seguintes tipos de identidade estão disponíveis no [!DNL Platform]:

| Tipo de identidade | Descrição |
| --- | --- |
| ID de cookies | As IDs de cookie identificam os navegadores da Web. Essas identidades são essenciais para a expansão e constituem a maioria do gráfico de identidade. No entanto, por natureza, eles decaem rapidamente e perdem seu valor ao longo do tempo. |
| ID entre dispositivos | As IDs entre dispositivos identificam um indivíduo e geralmente vinculam outras IDs. Os exemplos incluem uma ID de logon, uma ID de CRM e uma ID de fidelidade. Isso é uma indicação para [!DNL Identity Service] para lidar com o valor de forma sensível. |
| ID do dispositivo | As IDs de dispositivo identificam dispositivos de hardware, como IDFA (iPhone e iPad), GAID (Android) e RIDA (Roku), e podem ser compartilhadas por várias pessoas no domicílio. |
| Endereço de email | Os endereços de email são frequentemente associados a uma única pessoa e, portanto, podem ser usados para identificá-la em diferentes canais. Identidades desse tipo incluem informações de identificação pessoal (PII). Isso é uma indicação para [!DNL Identity Service] para lidar com o valor de forma sensível. |
| Identificador não de pessoas | IDs que não sejam de pessoas são usadas para armazenar identificadores que exigem namespaces, mas não estão conectados a um cluster de pessoas. Por exemplo, um SKU de produto, dados relacionados a produtos, organizações ou lojas. |
| ID do Parceiro [!BADGE Beta]{type=Informative} | IDs de parceiros são identificadores usados por parceiros de dados para representar pessoas. As IDs de parceiros geralmente são pseudônimas para não revelar a verdadeira identidade de uma pessoa e podem ser probabilísticas. No Real-time Customer Data Platform, as IDs de parceiros são usadas principalmente para ativação expandida do público-alvo e enriquecimento de dados, e não para criar vinculações determinísticas de gráficos de identidade. |
| Número de telefone | Os números de telefone são frequentemente associados a uma única pessoa e, portanto, podem ser usados para identificá-la em diferentes canais. As identidades desse tipo incluem PII. Isso é uma indicação para [!DNL Identity Service] para lidar com o valor de forma sensível. |

### Namespaces padrão {#standard}

O Experience Platform fornece vários namespaces de identidade que estão disponíveis para todas as organizações. Eles são conhecidos como namespaces padrão e são visíveis usando o [!DNL Identity Service] ou por meio da interface do usuário da Platform.

Os seguintes namespaces padrão são fornecidos para uso por todas as organizações na Platform:

| Nome de exibição | Descrição |
| ------------ | ----------- |
| AdCloud | Um namespace que representa o Adobe AdCloud. |
| Adobe Analytics (ID herdada) | Um namespace que representa o Adobe Analytics. Consulte o seguinte documento em [Namespaces do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces) para obter mais informações. |
| Apple IDFA (ID para anunciantes) | Um namespace que representa a Apple ID para anunciantes. Consulte o seguinte documento em [anúncios baseados em interesses](https://support.apple.com/en-us/HT202074) para obter mais informações. |
| Serviço de notificação por push da Apple | Um namespace que representa identidades coletadas usando o serviço de notificação por push da Apple. Consulte o seguinte documento em [Serviço de notificação por push da Apple](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) para obter mais informações. |
| CORE | Um namespace que representa o Adobe Audience Manager. Esse namespace também pode ser chamado pelo nome herdado: &quot;Adobe AudienceManager&quot;. Consulte o seguinte documento em [IDs do Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids) para obter mais informações. |
| ECID | Um namespace que representa a ECID. Esse namespace também pode ser referenciado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte o seguinte documento em [ECID](./ecid.md) para obter mais informações. |
| Email | Um namespace que representa um endereço de email. Esse tipo de namespace é frequentemente associado a uma única pessoa e, portanto, pode ser usado para identificá-la em diferentes canais. |
| Emails (SHA256, em letras minúsculas) | Um namespace para o endereço de email com hash prévio. Os valores fornecidos neste namespace são convertidos em minúsculas antes do hash com SHA256. Espaços à esquerda e à direita precisam ser cortados antes da normalização de um endereço de email. Esta configuração não pode ser alterada retroativamente. Consulte o seguinte documento em [Suporte a hash SHA 256](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) para obter mais informações. |
| Firebase Cloud Messaging | Um namespace que representa identidades coletadas usando o Google Firebase Cloud Messaging para notificações por push. Consulte o seguinte documento em [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) para obter mais informações. |
| ID de anúncio do Google (GAID) | Um namespace que representa uma ID de anúncio do Google. Consulte o seguinte documento em [ID de publicidade do Google](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) para obter mais informações. |
| ID de cliques do Google | Um namespace que representa uma ID de clique Google. Consulte o seguinte documento em [Rastreamento de cliques no Google Ads](https://developers.google.com/adwords/api/docs/guides/click-tracking) para obter mais informações. |
| Telefone | Um namespace que representa um número de telefone. Esse tipo de namespace é frequentemente associado a uma única pessoa e, portanto, pode ser usado para identificá-la em diferentes canais. |
| Telefone (E.164) | Um namespace que representa números de telefone brutos que precisam ter hash no formato E.164. O formato E.164 inclui um sinal de mais (`+`), um código de chamada de país internacional, um código de área local e um número de telefone. Por exemplo: `(+)(country code)(area code)(phone number)`. |
| Telefone (SHA256) | Um namespace que representa números de telefone que precisam de hash usando SHA256. Você deve remover símbolos, letras e quaisquer zeros à esquerda. Você também deve adicionar o código de chamada do país como prefixo. |
| Telefone (SHA256_E.164) | Um namespace que representa números de telefone brutos que precisam de hash usando os formatos SHA256 e E.164. |
| TNTID | Um namespace que representa o Adobe Target. Consulte o seguinte documento em [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=pt-BR) para obter mais informações. |
| Windows AID | Um namespace que representa uma ID de anúncio do Windows. Consulte o seguinte documento em [ID de anúncio do Windows](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) para obter mais informações. |

### Exibir namespaces de identidade {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="Exibir identidades de integração"
>abstract="Identidades de integração são namespaces usados para se conectar com outros sistemas e não são usados na resolução de identidade ou para unir identidades. <br> Essas identidades estão ocultas por padrão. Use a alternância para exibir namespaces de integração."

Para exibir namespaces de identidade na interface, selecione **[!UICONTROL Identidades]** na navegação à esquerda e selecione **[!UICONTROL Procurar]**.

![navegar](./images/browse.png)

Uma lista de namespaces de identidade é exibida na interface principal da página, exibindo informações sobre seus nomes, símbolos de identidade, data da última atualização e se eles são um namespace padrão ou personalizado. O painel direito contém informações sobre [!UICONTROL Fortaleza do gráfico de identidade].

![identidades](./images/identities.png)

A Platform também fornece namespaces para fins de integração. Esses namespaces estão ocultos por padrão, pois são usados para se conectar a outros sistemas e não são usados para compilar identidades. Para exibir namespaces de integração, selecione **[!UICONTROL Exibir identidades de integração]**.

![view-integration-identities](./images/view-integration-identities.png)

Selecione um namespace de identidade na lista para exibir informações sobre um namespace específico. Selecionar um namespace de identidade atualiza a exibição no painel direito para mostrar metadados relacionados ao namespace de identidade que você selecionou, incluindo o número de identidades assimiladas e o número de registros que falharam e foram ignorados.

![select-namespace](./images/select-namespace.png)

## Gerenciar namespaces personalizados {#manage-namespaces}

Dependendo dos dados organizacionais e casos de uso, talvez você precise de namespaces personalizados. Os namespaces personalizados podem ser criados usando o [[!DNL Identity Service]](./api/create-custom-namespace.md) ou por meio da interface do usuário.

Para criar um namespace personalizado usando a interface do usuário, navegue até o **[!UICONTROL Identidades]** espaço de trabalho, selecione **[!UICONTROL Procurar]** e selecione **[!UICONTROL Criar namespace de identidade]**.

![select-create](./images/select-create.png)

A variável **[!UICONTROL Criar namespace de identidade]** é exibida. Forneça uma **[!UICONTROL Nome de exibição]** e **[!UICONTROL Símbolo de identidade]** e selecione o tipo de identidade que deseja criar. Você também pode adicionar uma descrição opcional para adicionar mais informações sobre o namespace. Todos os tipos de identidade, exceto **Identificador não pessoal** O segue o mesmo comportamento de compilação. Se você selecionar **Identificador não pessoal** como tipo de identidade ao criar um namespace, a compilação não ocorre. Para obter informações específicas sobre cada tipo de identidade, consulte a tabela em [tipos de identidade](#identity-types).

Quando terminar, selecione **[!UICONTROL Criar]**.

>[!IMPORTANT]
>
>Os namespaces definidos são privados para sua organização e exigem um símbolo de identidade exclusivo para serem criados com sucesso.

![create-identity-namespace](./images/create-identity-namespace.png)

Semelhante aos namespaces padrão, você pode selecionar um namespace personalizado na **[!UICONTROL Procurar]** para exibir seus detalhes. No entanto, com um namespace personalizado, também é possível editar o nome para exibição e a descrição na área de detalhes.

>[!NOTE]
>
>Depois que um namespace é criado, ele não pode ser excluído e seu símbolo e tipo de identidade não podem ser alterados.

## Namespaces em dados de identidade

O fornecimento do namespace para uma identidade depende do método usado para fornecer dados de identidade. Para obter detalhes sobre como fornecer dados de identidade de dados, consulte a seção sobre [fornecimento de dados de identidade](./home.md#supplying-identity-data-to-identity-service) no [!DNL Identity Service] visão geral.

## Próximas etapas

Agora que você entende os principais conceitos dos namespaces de identidade, pode começar a aprender a trabalhar com seu gráfico de identidade usando o [visualizador de gráficos de identidade](./ui/identity-graph-viewer.md).
