---
title: Visão geral do namespace de identidade
description: Saiba mais sobre namespaces de identidade no Serviço de identidade.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1848'
ht-degree: 17%

---

# Visão geral do namespace de identidade

Leia o documento a seguir para saber mais sobre o que você pode fazer com namespaces de identidade no serviço de identidade da Adobe Experience Platform.

## Introdução

Os namespaces de identidade exigem uma compreensão de vários serviços da Adobe Experience Platform. Antes de começar a trabalhar com namespaces, reveja a documentação dos seguintes serviços:

* [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Identity Service]](../home.md): obtenha uma melhor visão de clientes individuais e de seu comportamento ao unir as identidades de vários dispositivos e sistemas.
* [[!DNL Privacy Service]](../../privacy-service/home.md): os namespaces de identidade são usados em solicitações de conformidade para regulamentos legais de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR). Cada solicitação de privacidade é feita em relação a um namespace para identificar quais dados dos consumidores devem ser afetados.

## Compreensão dos namespaces de identidade {#understanding-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="Namespaces de identidade"
>abstract="Um namespace de identidade é o contexto de uma determinada identidade. Por exemplo, um namespace de `Email` pode ser **nome<span>@acme.com**. Da mesma forma, um namespace de `Phone` pode ser `555-555-1234`."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="Valores de identidade"
>abstract="Um valor de identidade é um identificador que representa uma pessoa, uma organização ou um ativo exclusivo. O contexto ou tipo de identidade que o valor representa é definido por um namespace de identidade correspondente. Ao corresponder dados de registro em fragmentos de perfil, o namespace e o valor de identidade devem coincidir. Ao corresponder dados de registro em fragmentos de perfil, o namespace e o valor da identidade devem coincidir."
>text="Learn more in documentation"

Uma identidade totalmente qualificada inclui dois componentes: um **valor de identidade** e um **namespace de identidade**. Por exemplo, se o valor de uma identidade for `scott@acme.com`, então um namespace fornecerá contexto para esse valor, diferenciando-o como um endereço de email. Da mesma forma, um namespace pode distinguir `555-123-456` como um número de telefone e `3126ABC` como um CRMID. Essencialmente, **um namespace fornece contexto a uma determinada identidade**. Ao corresponder dados de registro entre fragmentos de perfil, como quando [!DNL Real-Time Customer Profile] mescla dados de perfil, o valor de identidade e o namespace devem corresponder.

Por exemplo, dois fragmentos de perfil podem conter IDs primárias diferentes, mas compartilham o mesmo valor para o namespace &quot;Email&quot;. Portanto, o Experience Platform pode ver que esses fragmentos são realmente o mesmo indivíduo e reúne os dados no gráfico de identidade do indivíduo.

>[!BEGINSHADEBOX]

**Namespace de identidade explicado**

Outra maneira de entender melhor o conceito de namespace é considerar exemplos do mundo real, como cidades e seus estados correspondentes. Por exemplo, Portland, Maine e Portland, no Oregon, são dois lugares diferentes nos Estados Unidos. Enquanto as cidades compartilham o mesmo nome, o estado opera como um namespace e fornece o contexto necessário que distingue as duas cidades uma da outra.

Aplicar a mesma lógica ao Serviço de identidade:

* Acesso rápido, o valor de identidade de: `1-234-567-8900` pode parecer um número de telefone. No entanto, de uma perspectiva do sistema, esse valor poderia ter sido configurado como uma CRMID. O Serviço de identidade não teria como aplicar o contexto necessário a esse valor de identidade sem um namespace correspondente.
* Outro exemplo é o valor de identidade de: `john@gmail.com`. Embora seja possível presumir facilmente que esse valor de identidade seja um email, é totalmente possível que ele esteja configurado como um CRMID de namespace personalizado. Com o namespace, você pode distinguir `Email:john@gmail.com` de `CRMID:john@gmail.com`.

>[!ENDSHADEBOX]

### Componentes de um namespace

Um namespace consiste nos seguintes componentes:

* **Nome de exibição**: o nome amigável para um determinado namespace.
* **Símbolo de identidade**: um código usado internamente pelo Serviço de identidade para representar um namespace.
* **Tipo de identidade**: a classificação de um determinado namespace.
* **Descrição**: (opcional) todas as informações complementares que você pode fornecer em relação a um determinado namespace.

### Tipo de identidade {#identity-type}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="Especificar tipo de identidade"
>abstract="O tipo de identidade controla se os dados são armazenados ou não no gráfico de identidade. Os gráficos de identidade não são gerados para os seguintes tipos de identidade: identificadores não pessoais e ID de parceiro."
>text="Learn more in documentation"

Um elemento de um namespace de identidade é o **tipo de identidade**. O tipo de identidade determina:

* Se um gráfico de identidade será gerado:
   * Os gráficos de identidade não são gerados para os seguintes tipos de identidade: identificadores não pessoais e ID de parceiro.
   * Os gráficos de identidade são gerados para todos os outros tipos de identidade.
* Quais identidades são removidas do gráfico de identidade quando os limites do sistema são atingidos. Para obter mais informações, leia as [medidas de proteção para dados de identidade](../guardrails.md).

Os seguintes tipos de identidade estão disponíveis no Experience Platform:

| Tipo de identidade | Descrição |
| --- | --- |
| ID do cookie | As IDs de cookie identificam os navegadores da Web. Essas identidades são essenciais para a expansão e constituem a maioria do gráfico de identidade. No entanto, por natureza, eles decaem rapidamente e perdem seu valor ao longo do tempo. |
| ID entre dispositivos | As IDs entre dispositivos identificam um indivíduo e geralmente vinculam outras IDs. Os exemplos incluem uma ID de logon, CRMID e ID de fidelidade. Esta é uma indicação para [!DNL Identity Service] manipular o valor de forma sensível. |
| ID do dispositivo | As IDs de dispositivo identificam dispositivos de hardware, como IDFA (iPhone e iPad), GAID (Android) e RIDA (Roku), e podem ser compartilhadas por várias pessoas do domicílio. |
| Endereço de email | Os endereços de email são frequentemente associados a uma única pessoa e, portanto, podem ser usados para identificá-la em diferentes canais. Identidades desse tipo incluem informações de identificação pessoal (PII). Esta é uma indicação para [!DNL Identity Service] manipular o valor de forma sensível. |
| Identificador não pessoal | IDs que não sejam de pessoas são usadas para armazenar identificadores que exigem namespaces, mas não estão conectados a um conjunto de pessoas. Por exemplo, um SKU de produto, dados relacionados a produtos, organizações ou lojas. |
| ID de parceiro | <ul><li>IDs de parceiro são identificadores usados por parceiros de dados para representar pessoas. As IDs de parceiros geralmente são pseudônimas para não revelar a verdadeira identidade de uma pessoa e podem ser probabilísticas. No Real-Time Customer Data Platform, as IDs de parceiros são usadas principalmente para ativação expandida do público-alvo e enriquecimento de dados, e não para criar vinculações de gráficos de identidade.</li><li>Os gráficos de identidade não são gerados ao assimilar uma identidade que inclui um namespace de identidade especificado como tipo de ID do parceiro.</li><li>A falha na assimilação de dados do parceiro usando o tipo de identidade da ID do parceiro pode resultar no alcance das limitações de gráfico do sistema no Serviço de identidade, bem como na mesclagem indesejada de perfis.</li><ul> |
| Número de telefone | Os números de telefone são frequentemente associados a uma única pessoa e, portanto, podem ser usados para identificá-la em diferentes canais. As identidades desse tipo incluem PII. Esta é uma indicação para [!DNL Identity Service] manipular o valor de forma sensível. |

{style="table-layout:auto"}

### Namespaces padrão {#standard}

A Experience Platform fornece vários namespaces de identidade que estão disponíveis para todas as organizações. Eles são conhecidos como namespaces padrão e são visíveis usando a API [!DNL Identity Service] ou por meio da interface do usuário do Experience Platform.

Os seguintes namespaces padrão são fornecidos para uso por todas as organizações no Experience Platform:

| Nome de exibição | Descrição |
| ------------ | ----------- |
| AdCloud | Um namespace que representa o Adobe AdCloud. |
| Adobe Analytics (ID legada) | Um namespace que representa o Adobe Analytics. Consulte o seguinte documento em [namespaces do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=pt-BR#namespaces) para obter mais informações. |
| Apple IDFA (ID para anunciantes) | Um namespace que representa a Apple ID para anunciantes. Consulte o seguinte documento em [anúncios baseados em interesses](https://support.apple.com/en-us/HT202074) para obter mais informações. |
| Serviço de notificação por push da Apple | Um namespace que representa identidades coletadas usando o serviço de notificação por push da Apple. Consulte o seguinte documento no [Serviço de notificação por push do Apple](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) para obter mais informações. |
| ECID | Um namespace que representa a ECID. Esse namespace também pode ser referenciado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte o seguinte documento no [ECID](./ecid.md) para obter mais informações. |
| Email | Um namespace que representa um endereço de email. Esse tipo de namespace é frequentemente associado a uma única pessoa e, portanto, pode ser usado para identificá-la em diferentes canais. |
| Emails (SHA256, em letras minúsculas) | Um namespace para o endereço de email com hash prévio. Os valores fornecidos neste namespace são convertidos em minúsculas antes do hash com SHA256. Espaços à esquerda e à direita precisam ser cortados antes da normalização de um endereço de email. Esta configuração não pode ser alterada retroativamente. Consulte o seguinte documento sobre [suporte a hash SHA256](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=pt-BR#hashing-support) para obter mais informações. |
| Firebase Cloud Messaging | Um namespace que representa identidades coletadas usando o Google Firebase Cloud Messaging para notificações por push. Consulte o seguinte documento em [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) para obter mais informações. |
| ID de anúncio do Google (GAID) | Um namespace que representa uma Google Advertising ID. Consulte o seguinte documento no [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) para obter mais informações. |
| Telefone | Um namespace que representa um número de telefone. Esse tipo de namespace é frequentemente associado a uma única pessoa e, portanto, pode ser usado para identificá-la em diferentes canais. |
| Telefone (E.164) | Um namespace que representa números de telefone brutos que precisam ter hash no formato E.164. O formato E.164 inclui um sinal de adição (`+`), um código de chamada de país internacional, um código de área local e um número de telefone. Por exemplo: `(+)(country code)(area code)(phone number)`. |
| Telefone (SHA256) | Um namespace que representa números de telefone que precisam de hash usando SHA256. Você deve remover símbolos, letras e quaisquer zeros à esquerda. Você também deve adicionar o código de chamada do país como prefixo. |
| Telefone (SHA256_E.164) | Um namespace que representa números de telefone brutos que precisam ser transformados em hash, utilizando os formatos SHA256 e E.164. |
| TNTID | Um namespace que representa o Adobe Target. Consulte o seguinte documento no [Target](https://docs.adobe.com/content/help/pt-BR/experience-cloud/user-guides/home.translate.html) para obter mais informações. |
| Windows AID | Um namespace que representa uma Advertising ID do Windows. Consulte o seguinte documento no [Windows Advertising ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) para obter mais informações. |

### Exibir namespaces de identidade {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="Exibir identidades de integração"
>abstract="Identidades de integração são namespaces usados para se conectar com outros sistemas e não são usados na resolução de identidade ou para unir identidades. <br> Essas identidades estão ocultas por padrão. Use o botão de alternância para exibir namespaces de integração."

Para exibir namespaces de identidade na interface do usuário, selecione **[!UICONTROL Identities]** na navegação à esquerda e **[!UICONTROL Browse]**.

Um diretório de namespaces na organização é exibido, exibindo informações sobre nomes, símbolos de identidade, datas da última atualização, tipos de identidade correspondentes e descrição.

![Um diretório de namespaces de identidade personalizados em sua organização.](../images/namespace/browse.png)

## Criar namespaces personalizados {#create-namespaces}

Dependendo dos dados organizacionais e casos de uso, talvez você precise de namespaces personalizados. Os namespaces personalizados podem ser criados usando a API [[!DNL Identity Service]](../api/create-custom-namespace.md) ou por meio da interface do usuário.

Para criar um namespace personalizado, selecione **[!UICONTROL Create identity namespace]**.

>[!TIP]
>
>As identidades de integração são namespaces usados para se conectar a outros sistemas. Não são usados na resolução de identidades, nem são usados para compilar identidades. Selecione **[!UICONTROL View integration identities]** para atualizar a lista e incluir identidades de integração. No entanto, as identidades de integração estão ocultas por padrão, pois são somente visualização e não é necessário configurá-las.

![O botão criar namespace de identidade no espaço de trabalho de identidades.](../images/namespace/create-identity-namespace.png)

A janela [!UICONTROL Create identity namespace] é exibida. Primeiro, você deve fornecer um nome de exibição e um símbolo de identidade para o namespace personalizado que deseja criar. Opcionalmente, também é possível fornecer uma descrição para adicionar mais contexto ao namespace personalizado que você está criando.

![Uma janela pop-up na qual você pode inserir informações relacionadas ao seu namespace de identidade personalizado.](../images/namespace/name-and-symbol.png)

Em seguida, selecione o tipo de identidade que deseja atribuir ao namespace personalizado. Quando terminar, selecione **[!UICONTROL Create]**.

![Uma seleção de tipos de identidade que você pode escolher e atribuir ao seu namespace de identidade personalizado.](../images/namespace/select-identity-type.png)

>[!IMPORTANT]
>
>* Os namespaces definidos são privados para sua organização e exigem um símbolo de identidade exclusivo para serem criados com sucesso.
>
>* Depois que um namespace é criado, ele não pode ser excluído e seu símbolo e tipo de identidade não podem ser alterados.
>
>* Não há suporte para namespaces duplicados. Não é possível usar um nome para exibição existente e um símbolo de identidade ao criar um novo namespace.

## Namespaces em dados de identidade

O fornecimento do namespace para uma identidade depende do método usado para fornecer dados de identidade. Para obter detalhes sobre como fornecer dados de identidade, leia o [[!DNL Identity Service] guia de implementação](../implementation.md).

## Próximas etapas

Agora que você entende os principais conceitos dos namespaces de identidade, pode começar a aprender a trabalhar com seu gráfico de identidade usando o [visualizador de gráficos de identidade](../features/identity-graph-viewer.md).
