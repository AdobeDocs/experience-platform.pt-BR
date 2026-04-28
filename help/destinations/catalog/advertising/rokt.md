---
title: Rokt
description: Saiba como conectar públicos do Adobe Experience Platform ao Rokt para melhorar o desempenho da campanha por meio de direcionamento, supressão e personalização mais inteligentes.
source-git-commit: a281a7c961b8576105913feb7a7f8258c975e875
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 4%

---


# [!DNL Rokt] conexão {#rokt-destination}

## Visão geral {#overview}

[[!DNL Rokt]](https://www.rokt.com) desbloqueia valor no comércio eletrônico usando uma decisão em tempo real orientada por IA para tornar cada Transaction Moment™ mais relevante. Ele fornece experiências personalizadas e conecta anunciantes com clientes de alta intenção. Conecte [!DNL Adobe Experience Platform] públicos-alvo ao [!DNL Rokt] para melhorar o desempenho da campanha através de direcionamento, supressão e personalização mais inteligentes. Alcance os clientes certos no momento certo e, ao mesmo tempo, reduza o desperdício de gastos.

>[!IMPORTANT]
>
>O conector de destino e a página de documentação são criados e mantidos pela equipe [!DNL Rokt]. Para qualquer consulta ou solicitação de atualização, entre em contato com o Gerente de Conta do [!DNL Rokt] ou ligue para `support@rokt.com`.

## Casos de uso {#use-cases}

Os seguintes casos de uso mostram como [!DNL Experience Platform] clientes podem usar o destino [!DNL Rokt].

### Caso de uso #1: redirecionamento {#use-case-1}

Reenvolva clientes de alta intenção que visitaram seu site ou aplicativo, mas não fizeram a conversão. Crie uma audiência em [!DNL Experience Platform], incluindo usuários que navegaram em categorias de produtos específicas ou abandonaram um fluxo de check-out. Em seguida, encaminhe esse público-alvo para [!DNL Rokt] para apresentar ofertas personalizadas no ponto de compra em sites parceiros. [!DNL Rokt] opera no momento da transação, imediatamente após um cliente concluir uma compra em outro lugar. Os públicos-alvo redirecionados são atingidos quando a intenção de compra está no pico, gerando taxas de conversão mais altas do que o redirecionamento de exibição tradicional.

### Caso de uso #2: listas de supressão {#use-case-2}

Evite gastos desperdiçados e experiências irrelevantes suprimindo os públicos que não devem receber determinadas ofertas do [!DNL Rokt]. Casos de uso comuns de supressão incluem a exclusão de conversores recentes, membros de fidelidade em uma promoção ativa ou usuários que optaram por não participar do marketing. Por exemplo, exclua clientes que compraram nos últimos 30 dias. Sincronizar esses públicos de supressão de [!DNL Experience Platform] para [!DNL Rokt] em tempo real. Isso mantém as campanhas focadas em usuários novos ou reengajáveis. Isso melhora o ROI e protege a experiência do cliente.

## Pré-requisitos {#prerequisites}

Antes de configurar o destino [!DNL Rokt] em [!DNL Adobe Experience Platform], obtenha as credenciais a seguir do seu Gerente de Conta **[!DNL Rokt]**:

* **Chave de API**: use como **[!UICONTROL Username]** ao [autenticar a conexão de destino](#authenticate).
* **Segredo de API**: use como **[!UICONTROL Password]** ao [autenticar a conexão de destino](#authenticate).

O Gerente de Conta do [!DNL Rokt] provisionará essas credenciais na plataforma do [!DNL Rokt] antes da configuração. Entre em contato com o Gerente de contas, caso ainda não as tenha recebido.

## Identidades suportadas {#supported-identities}

[!DNL Rokt] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| email | Endereço de email de texto sem formatação | Recomendado. Usado para correspondência de perfil em [!DNL Rokt]. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | Há suporte para endereços de email com hash SHA256 e de texto sem formatação. Quando o campo de origem contiver atributos sem hash, selecione a opção **[!UICONTROL Apply transformation]** para fazer com que [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |
| telefone | Telefone de texto sem formatação | Usado para correspondência de perfil em [!DNL Rokt]. |
| phone_sha256 | Números de telefone com hash com o algoritmo SHA256 | Há suporte para números de telefone com hash SHA256 e texto sem formatação. Quando o campo de origem contiver atributos sem hash, selecione a opção **[!UICONTROL Apply transformation]** para fazer com que [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |
| GAID | [!DNL Google] Advertising ID | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | [!DNL Apple] ID para anunciantes | Selecione a identidade de destino do IDFA quando a identidade de origem for um namespace do IDFA. |
| aepProfileId | [!DNL Adobe Experience Platform] ID do perfil | Mapeia a ID do Perfil (`xdm:_id`) como um identificador de fallback. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sim | Públicos gerados através de [!DNL Experience Platform] [[!DNL Segmentation Service]](/help/segmentation/home.md). |
| Todas as outras origens de público-alvo | Sim | Esta categoria inclui todas as origens de público-alvo fora dos públicos-alvo gerados pelo [!DNL Segmentation Service]. Leia sobre as [várias origens do público-alvo](/help/segmentation/ui/audience-portal.md#customize). Alguns exemplos incluem: <ul><li> carregar audiências personalizadas [importadas](/help/segmentation/ui/audience-portal.md#import-audience) para [!DNL Experience Platform] de arquivos CSV,</li><li> públicos-alvo semelhantes, </li><li> públicos federados, </li><li> públicos-alvo gerados em outros aplicativos [!DNL Experience Platform], como [!DNL Adobe Journey Optimizer], </li><li> e muito mais. </li></ul> |

{style="table-layout:auto"}

Públicos-alvo compatíveis por tipo de dados de público-alvo:

| Tipo de dados de público | Suportado | Descrição | Casos de uso |
|--------------------|-----------|-------------|-----------|
| [Públicos-alvo](/help/segmentation/types/people-audiences.md) | Sim | Com base nos perfis de clientes. Use-os para direcionar grupos específicos de pessoas para campanhas de marketing. | Compradores frequentes, abandonadores de carrinho |
| [Públicos-alvo da conta](/help/segmentation/types/account-audiences.md) | Não | Direcione indivíduos em organizações específicas para estratégias de marketing baseadas em conta. | Marketing B2B |
| [Públicos-alvo potenciais](/help/segmentation/types/prospect-audiences.md) | Não | Direcione indivíduos que ainda não são clientes, mas compartilham características com seu público-alvo. | Prospecção com dados de terceiros |
| [Exportações do conjunto de dados](/help/catalog/datasets/overview.md) | Não | Coleções de dados estruturados armazenados no Data Lake [!DNL Adobe Experience Platform]. | Relatórios, fluxos de trabalho de ciência de dados |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público-alvo com os identificadores (email, telefone, ID de anúncio móvel ou outros) usados no destino [!DNL Rokt]. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado em [!DNL Experience Platform] com base na avaliação do público-alvo, o conector enviará a atualização downstream para [!DNL Rokt]. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](/help/destinations/ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Username]**: Sua chave de API, fornecida pelo seu gerente de conta [!DNL Rokt].
* **[!UICONTROL Password]**: Seu Segredo de API, fornecido pelo seu Gerente de Conta do [!DNL Rokt].

  ![A tela de configuração de destino [!DNL Rokt] em [!DNL Experience Platform], com detalhes de conta, campos de autenticação e detalhes de destino preenchidos.](/help/destinations/assets/catalog/advertising/rokt/aep-configure-destination.png)

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro (por exemplo, &quot;[!DNL Rokt] - Redirecionando Públicos-alvo&quot;).
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](/help/destinations/ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
>
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e públicos-alvo para destinos de exportação de público-alvo de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

### Mapear atributos e identidades {#map}

O destino [!DNL Rokt] oferece suporte ao mapeamento de namespaces de identidade de [!DNL Experience Platform] para [!DNL Rokt] campos de identidade. Você deve mapear pelo menos uma identidade para ativar um público-alvo com êxito. Os mapeamentos recomendados são mostrados na tabela abaixo.

| Campo de origem | Campo de destino | Considerações |
|---|---|---|
| `IdentityMap: Email` | `Identity: email` | Recomendado |
| `IdentityMap: Email_LC_SHA256` | `Identity: emailSha256` | Recomendado |
| `IdentityMap: Phone` | `Identity: phone` | Opcional |
| `IdentityMap: Phone_SHA256` | `Identity: phoneSha256` | Opcional |
| `IdentityMap: GAID` | `Identity: gaid` | Opcional |
| `IdentityMap: IDFA` | `Identity: idfa` | Opcional |
| `xdm: _id` | `Identity: aepProfileId` | Opcional |

{style="table-layout:auto"}

Este é um exemplo de um mapeamento completo:

![A etapa de mapeamento do fluxo de trabalho de ativação de destino [!DNL Rokt] em [!DNL Experience Platform], com campos de identidade de origem e destino configurados.](/help/destinations/assets/catalog/advertising/rokt/aep-identity-mapping.png)

>[!NOTE]
>
>Pelo menos um mapeamento de identidade baseado em email (`email` ou `emailSha256`) é altamente recomendado para maximizar as taxas de correspondência em [!DNL Rokt].

### Configurar programação de público {#audience-schedule}

Após concluir a etapa de mapeamento, configure um agendamento de público-alvo para cada público-alvo selecionado. Forneça um **[!UICONTROL Start date]** para quando o público-alvo deve começar a sincronizar e um **[!UICONTROL Mapping ID]** (um rótulo usado para identificar esse público-alvo em [!DNL Rokt]). Você pode usar o nome de público-alvo [!DNL Experience Platform] ou qualquer cadeia de caracteres descritiva que ajude você e seu Gerente de Contas [!DNL Rokt] a identificar o público-alvo.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

* [Documentação do desenvolvedor do [!DNL Rokt]](https://docs.rokt.com)
* [Visão geral dos destinos do Adobe Experience Platform](/help/destinations/home.md)
