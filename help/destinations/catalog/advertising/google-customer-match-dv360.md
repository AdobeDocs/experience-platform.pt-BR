---
title: Correspondência de cliente do Google + conexão de vídeo e exibição 360
description: Com o conector de destino do Google Customer Match + Display & Video 360, você pode usar seus dados online e offline do Experience Platform para acessar e reengajar com seus clientes nas propriedades próprias e operadas da Google, como Search, Shopping, Gmail e YouTube.
badge: Disponibilidade limitada
exl-id: f6da3eae-bf3f-401a-99a1-2cca9a9058d2
source-git-commit: 16192df76b618ed1d516b78f9c3191027140b8d3
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 3%

---

# [!DNL Google Customer Match + Display & Video 360] conexão

>[!NOTE]
>
>**Disponibilidade limitada do conector Google Customer Match + Display &amp; Video 360**<br> Como estamos passando pelo ciclo de vida completo da maturidade dessa integração com o Google, estamos vendo dados que apontam para fraquezas na implementação que precisam ser corrigidas antes que possa ocorrer uma adoção mais ampla. Dadas essas preocupações, a Adobe reduziu a visibilidade desse destino a um número limitado de clientes. Estamos em conversas ativas com a Google para melhorar a experiência com o produto. Entendemos que isso pode ser uma notícia decepcionante, mas acreditamos que seja a abordagem responsável para garantir uma experiência confiável e de alta qualidade para nossos clientes.</br>

Use este destino para ativar suas listas [[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) com base em PII próprias diretamente para [!DNL Google Display & Video 360] propriedades como [!DNL Search], [!DNL YouTube], [!DNL Gmail] e [!DNL Google Display Network].

Determinados terceiros integrados à Google, como o Adobe Real-Time CDP, podem usar o [!DNL Google Audience Partner API] para criar [!DNL Customer Match] públicos-alvo diretamente na conta [!DNL Display & Video 360] dos clientes.

Com a capacidade recém-introduzida de utilizar o [!DNL Customer Matched] público-alvo através do [!DNL Display & Video 360], você agora pode direcionar públicos-alvo através de uma lista expandida de fontes de inventário.

![Correspondência de cliente do Google + destino DV360 na interface do usuário do Adobe Experience Platform.](/help/destinations/assets/catalog/advertising/gcm-dv360/catalog.png)

## Aviso importante sobre alterações nos destinos do Google relacionadas aos requisitos de consentimento atualizados na União Europeia

>[!IMPORTANT]
>
> A Google está lançando alterações na [API do Google Ads](https://developers.google.com/google-ads/api/docs/start), na [Correspondência do Cliente](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) e na [API de Exibição e Vídeo 360](https://developers.google.com/display-video/api/guides/getting-started/overview) para oferecer suporte aos requisitos de conformidade e consentimento definidos na [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) da União Europeia ([Política de Consentimento do Usuário](https://www.google.com/about/company/user-consent-policy/) da UE). A aplicação dessas alterações aos requisitos de consentimento estará em vigor a partir de 6 de março de 2024.
> &#x200B;><br/>
> &#x200B;>Para aderir à política de consentimento do usuário da UE e continuar criando listas de públicos-alvo para usuários no Espaço Econômico Europeu (EEE), anunciantes e parceiros devem garantir que eles transmitem o consentimento do usuário final ao fazer upload dos dados de público-alvo. Como parceiro da Google, a Adobe fornece as ferramentas necessárias para cumprir esses requisitos de consentimento de acordo com a DMA na União Europeia.
> &#x200B;><br/>
> &#x200B;>Os clientes que compraram o Adobe Privacy &amp; Security Shield e configuraram uma [política de consentimento](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar perfis não consentidos não precisam tomar nenhuma ação.
> &#x200B;><br/>
> &#x200B;>Os clientes que não compraram o Adobe Privacy &amp; Security Shield devem usar os recursos de [definição de segmento](../../../segmentation/home.md#segment-definitions) no [Construtor de segmentos](../../../segmentation/ui/segment-builder.md) para filtrar perfis não consentidos, a fim de continuar usando os Destinos do Real-Time CDP Google existentes sem interrupção.

## Quando usar este destino

Várias integrações com o Google estão disponíveis no catálogo de destinos e pode ser difícil entender quando usar cada um dos destinos do Google disponíveis. Compreenda os diferentes casos de uso lendo as informações na tabela abaixo:

| [Correspondência de cliente do Google](/help/destinations/catalog/advertising/google-customer-match.md) | [Vídeo e exibição do Google 360](/help/destinations/catalog/advertising/google-dv360.md) | [!DNL Google Customer Match] + [!DNL Display & Video 360] (este conector) |
|---------|----------|---------|
| Exporte seus públicos com base em PII e acesse-os no inventário disponível em [!DNL Google Customer Match]. | Alcance públicos-alvo com base em cookies no inventário disponível por meio do [!DNL Google Display & Video 360], em propriedades próprias e operadas do Google, como Youtube e [!DNL Search], e muito além. | Crie públicos com base em PII em [!DNL Google Customer Match] e alcance-os no inventário disponível em [!DNL Google Display & Video 360], somente em propriedades próprias e operadas da Google. |

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando usar esse destino, veja a seguir exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse recurso.

### Caso de uso #1

Uma marca de vestuário atlético deseja alcançar clientes existentes por meio de [!DNL Google Search] e [!DNL Google Shopping] para personalizar ofertas e itens com base em suas compras anteriores e histórico de navegação. A marca apparel pode assimilar endereços de email de seu próprio CRM para o Experience Platform e criar públicos-alvo a partir de seus próprios dados offline. Em seguida, eles podem enviar esses públicos-alvo para o destino [!DNL Google Customer Match + Display & Video 360] a ser usado nas propriedades [!DNL Google Display & Video 360], como [!DNL Search], [!DNL YouTube], [!DNL Gmail] e [!DNL Google Display Network].

### Caso de uso #2

Uma proeminente empresa de tecnologia lançou um novo telefone. Para promover esse novo modelo de telefone, eles estão procurando conscientizar os clientes sobre os novos recursos e funcionalidades do telefone para os clientes que possuem modelos anteriores de seus telefones.

Para promover a versão, eles carregam endereços de email do banco de dados do CRM na Experience Platform, usando os endereços de email como identificadores. Os públicos-alvo são criados com base nos clientes que possuem modelos de telefone mais antigos. Os públicos-alvo são enviados para [!DNL Google Customer Match], para que a empresa possa direcionar os clientes atuais, os clientes que possuem modelos de telefone mais antigos e clientes semelhantes em propriedades do [!DNL Google Display & Video 360], como [!DNL Search], [!DNL YouTube], [!DNL Gmail] e [!DNL Google Display Network].

## Identidades suportadas {#supported-identities}

[!DNL Google Customer Match] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando a identidade de origem for um namespace do IDFA. |
| phone_sha256_e.164 | Números de telefone no formato E164, com hash com o algoritmo SHA256 | Os números de telefone com hash SHA256 e texto sem formatação são compatíveis com o Adobe Experience Platform. Siga as instruções na seção [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para texto sem formatação e números de telefone com hash, respectivamente. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Aplicar transformação]** para que [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Siga as instruções na seção [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para texto sem formatação e endereços de email com hash, respectivamente. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Aplicar transformação]** para que [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |

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

### Requisitos de vinculação de contas {#linking}

Antes de configurar esse conector de destino, você deve vincular sua ID de conta da Google à ID de conta da Google da Adobe: `4641108541`.

As exportações de dados falharão se sua conta do Google não estiver vinculada corretamente à ID da conta da Adobe.

>[!NOTE]
>
>Para clientes que faziam parte do programa beta para este conector: a Adobe atualizou a ID da conta de parceiro da Google de `6219889373` para `4641108541`.
>
>**Se você fez parte do programa beta para o conector Google Customer Match + Display &amp; Video 360 e se sua conta do Google está atualmente vinculada à antiga ID de Conta de Parceiro da Adobe (`6219889373`), siga as etapas abaixo:**
>
>1. Desvincule sua conta da Google da ID de Conta de Parceiro da Adobe antiga (`6219889373`)
>2. Vincular sua conta da Google à nova ID de Conta de Parceiro da Adobe (`4641108541`)
>3. Remover todos os públicos-alvo dos fluxos de dados existentes
>4. Criar novos fluxos de dados e mapear seus públicos
>
>Se sua conta do Google já estiver vinculada à nova ID de Conta de Parceiro da Adobe (`4641108541`), nenhuma ação será necessária para usar esse conector.

**Para organizações com contas de gerente:**

Se sua organização usar uma [conta de gerente [!DNL Google] 2&rbrace; para gerenciar várias contas de cliente, siga estes requisitos específicos de vinculação:](https://support.google.com/google-ads/answer/6139186)

* **Para exportar para uma conta de cliente específica:** Vincule essa conta de cliente individual (não a conta de gerente) à ID de conta da Google da Adobe: `4641108541`
* **A vinculação de conta de gerente sozinha não é suficiente** e causará falhas de exportação de dados

### Lista de permissões {#allowlist}

Antes de criar o destino [!DNL Google Customer Match] no Experience Platform, verifique se a sua conta [!DNL Google Ads] está em conformidade com a [[!DNL Google Customer Match] política](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Incluir na lista de permissões Os clientes com contas em conformidade são automaticamente notificados pela Google.

## Requisitos de correspondência de ID {#id-matching-requirements}

[!DNL Google] exige que nenhuma informação pessoal identificável (PII) seja enviada em branco. Portanto, os públicos ativados para [!DNL Google Customer Match] devem ser destacados por *identificadores com hash*, como endereços de email com hash ou números de telefone.

Dependendo do tipo de IDs que você assimila no Adobe Experience Platform, é necessário seguir os requisitos correspondentes.

### Requisitos de hash de número de telefone {#phone-number-hashing-requirements}

Há dois métodos para ativar números de telefone em [!DNL Google Customer Match]:

* **Ingestão de números de telefone brutos**: você pode assimilar números de telefone brutos no formato [!DNL E.164] no [!DNL Experience Platform], que são automaticamente transformados em hash após a ativação. Se você escolher essa opção, sempre assimile seus números de telefone brutos no namespace `Phone_E.164`.
* **Números de telefone com hash de assimilação**: você pode colocar seus números de telefone em hash antes de assimilar em [!DNL Experience Platform]. Se você escolher essa opção, sempre assimile seus números de telefone com hash no namespace `PHONE_SHA256_E.164`.

>[!NOTE]
>
>Os números de telefone assimilados no namespace `Phone` não podem ser ativados para o destino [!DNL Google Customer Match + DV360].

### Requisitos de hash de email {#hashing-requirements}

Você pode aplicar hash a endereços de email antes de assimilá-los no Adobe Experience Platform, ou usar endereços de email em limpar no Experience Platform, e aplicar hash a [!DNL Experience Platform] neles na ativação.

Para obter mais informações sobre os requisitos de hash do Google e outras restrições na ativação, consulte as seguintes seções na documentação do Google:

* [[!DNL Customer Match] com endereço de email, endereço ou ID de usuário](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considerações](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] com número de telefone](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] com IDs de dispositivo móvel](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)

Para saber mais sobre a assimilação de endereços de email no Experience Platform, consulte a [visão geral da assimilação em lote](../../../ingestion/batch-ingestion/overview.md) e a [visão geral da assimilação de streaming](../../../ingestion/streaming-ingestion/overview.md).

Se você optar por criar o hash dos endereços de email, certifique-se de cumprir os requisitos da Google, descritos nos links acima.

<!-- ### Using custom namespaces {#custom-namespaces}

Before you can use the `User_ID` namespace to send data to Google, make sure you synchronize your own identifiers using [!DNL gTag]. Refer to the [Google official documentation](https://support.google.com/google-ads/answer/9199250) for detailed information. -->

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Experience Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Experience Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/3475118/?quality=12&learn=on&captions=por_br) -->

## Conectar ao destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_gcm_dv360_accountID"
>title="Vincular contas do Google e da Adobe"
>abstract="Verifique se a ID de conta do Google inserida aqui já está vinculada à sua conta da Adobe. Se você tiver uma conta de gerente do Google com várias contas de clientes e pretender exportar dados da Experience Platform para uma conta de cliente específica, vincule essa conta de cliente à sua conta da Adobe e insira a ID da conta aqui."

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: forneça um nome para esta conexão de destino
* **[!UICONTROL Descrição]**: forneça uma descrição para esta conexão de destino
* **[!UICONTROL ID da conta]**: sua [ID de cliente do Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en). O formato da ID é xxx-xxx-xxxx. Se você estiver usando o [!DNL Google Ads Manager Account (My Client Center)], não use sua ID de Conta de Gerente. Em vez disso, use a [ID de cliente do Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en).
* **[!UICONTROL Tipo de conta]**: seu tipo de conta do Google. Selecione uma opção, dependendo do tipo de conta publicitária com o Google:
   * **[!UICONTROL Exibir Parceiro de Vídeo]**
   * **[!UICONTROL Exibir Anunciante de Vídeo]**

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades* para destinos, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](../../assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados de público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

<!-- In the **[!UICONTROL Segment schedule]** step, you must provide the [!UICONTROL App ID] when sending [!DNL IDFA] or [!DNL GAID] audiences to [!DNL Google Customer Match].

![Google Customer Match App ID field highlighted in the Segment schedule step of the activation workflow.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

For details on how to find the [!DNL App ID], refer to the [Google official documentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) or ask your Google representative. -->

### Exemplo de mapeamento: ativação de dados de público-alvo em [!DNL Google Customer Match + Display & Video 360] {#example-gcm}

Este é um exemplo de mapeamento de identidade correto ao ativar dados de público-alvo em [!DNL Google Customer Match + Display & Video 360].

Selecionar campos de origem:

* Selecione o namespace `Email` como identidade de origem se os endereços de email que você está usando não tiverem hash.
* Selecione o namespace `Email_LC_SHA256` como identidade de origem se você tiver hash dos endereços de email do cliente na assimilação de dados no [!DNL Experience Platform], de acordo com os [!DNL Google Customer Match] [requisitos de hash de email](#hashing-requirements).
* Selecione o namespace `PHONE_E.164` como identidade de origem se seus dados consistirem em números de telefone sem hash. [!DNL Experience Platform] aplicará hash aos números de telefone para atender aos requisitos de [!DNL Google Customer Match].
* Selecione o namespace `Phone_SHA256_E.164` como identidade de origem se você tiver hash de números de telefone na assimilação de dados em [!DNL Experience Platform], de acordo com [!DNL Facebook] [requisitos de hash de número de telefone](#phone-number-hashing-requirements).

Selecionar campos de destino:

* Selecione o namespace `Email_LC_SHA256` como identidade de destino quando os namespaces de origem forem `Email` ou `Email_LC_SHA256`.
* Selecione o namespace `Phone_SHA256_E.164` como identidade de destino quando os namespaces de origem forem `PHONE_E.164` ou `Phone_SHA256_E.164`.

![Mapeamento de identidade entre campos de origem e destino mostrado na etapa Mapeamento do fluxo de trabalho de ativação.](../../assets/catalog/advertising/google-customer-match-dv360/identity-mapping-gcm-dv360.png)

O hash automático de dados de namespaces sem hash é criado por [!DNL Experience Platform] após a ativação.

Os dados de origem do atributo não são automaticamente transformados em hash. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Aplicar transformação]** para que [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação.

![Aplicar controle de transformação realçado na etapa Mapeamento do fluxo de trabalho de ativação.](../../assets/catalog/advertising/google-customer-match-dv360/transformation.png)

## Monitorar destino {#monitor-destination}

Depois de se conectar ao destino e estabelecer um fluxo de dados de destino, você pode usar a [funcionalidade de monitoramento](/help/dataflows/ui/monitor-destinations.md) do Real-Time CDP para obter informações abrangentes sobre os registros de perfil ativados para o destino em cada execução de fluxo de dados.

As informações de monitoramento da conexão [!DNL Google Customer Match + Display & Video 360] incluem informações de nível de público relacionadas a identidades ativadas, excluídas e com falha em cada execução de fluxo de dados e fluxo de dados. [Leia mais](/help/dataflows/ui/monitor-destinations.md#segment-level-view) sobre a funcionalidade.

## Verificar se a ativação do público-alvo foi bem-sucedida {#verify-activation}

Após concluir o fluxo de ativação, alterne para sua conta do **[!UICONTROL Google Ads]**. Os públicos ativados são mostrados na sua conta do Google como listas de clientes. Dependendo do tamanho do público-alvo, alguns públicos-alvo não são preenchidos, a menos que haja mais de 1000 usuários ativos para atender. Encontre mais informações na [documentação do Google Audience Partner](https://developers.google.com/audience-partner/api/docs/customer-match/get-started#verify-list). Observe que você precisa solicitar à Google acesso à documentação no link.

## Governança de dados

Alguns destinos no Experience Platform têm determinadas regras e obrigações para dados enviados para a plataforma de destino ou recebidos dela. Você é responsável por entender as limitações e obrigações de seus dados e como usá-los no Adobe Experience Platform e na plataforma de destino. O Adobe Experience Platform fornece ferramentas de governança de dados para ajudar você a gerenciar algumas dessas obrigações de uso de dados. [Saiba mais](../../../data-governance/labels/overview.md) sobre políticas e ferramentas de governança de dados.

## Solução de problemas {#troubleshooting}

### 400 Mensagem de erro de solicitação incorreta {#bad-request}

Ao configurar esse destino, você pode receber o seguinte erro:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Este erro ocorre quando as contas de clientes não atendem aos [pré-requisitos](#google-account-prerequisites). Para corrigir esse problema, contate a Google e verifique se sua conta está incluída na lista de permissões e configurada para um nível de permissão [!DNL Standard] ou superior. Consulte a [documentação do Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&rd=1) para obter detalhes.
