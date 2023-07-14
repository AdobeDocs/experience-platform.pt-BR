---
keywords: conexão linkedin;conexão linkedin;destinos linkedin;linkedin;
title: Conexão de públicos correspondentes do Linkedin
description: Ative perfis para suas campanhas do LinkedIn para direcionamento de público, personalização e supressão, com base em emails com hash.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 2%

---

# [!DNL LinkedIn Matched Audiences] conexão

## Visão geral {#overview}

Ativar perfis para o [!DNL LinkedIn] campanhas para direcionamento, personalização e supressão de público com base em emails com hash e IDs móveis.

![Destino do linkedIn na interface do usuário do Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Casos de uso

Para ajudá-lo a entender melhor como e quando usar o [!DNL LinkedIn Matched Audiences] destino, este é um caso de uso que os clientes do Adobe Experience Platform podem resolver usando esse recurso.

Uma empresa de software organiza uma conferência e deseja manter contato com os participantes, além de mostrar ofertas personalizadas com base no status de participação na conferência. A empresa pode assimilar endereços de email ou IDs de dispositivos móveis por conta própria [!DNL CRM] no Adobe Experience Platform. Em seguida, eles podem criar públicos-alvo a partir de seus próprios dados offline e enviá-los para a [!DNL LinkedIn] social, otimizando seus gastos com publicidade.

## Identidades suportadas {#supported-identities}

[!DNL LinkedIn Matched Audiences] O oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| GAID | ID de publicidade do Google | Selecione essa identidade de destino quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione essa identidade de destino quando sua identidade de origem for um namespace IDFA. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Siga as instruções em [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para emails com texto sem formatação e hash, respectivamente. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. |

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
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público-alvo com os identificadores (nome, número de telefone e outros) usados no [!DNL LinkedIn Matched Audiences] destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Pré-requisitos da conta do linkedIn {#LinkedIn-account-prerequisites}

Antes de poder usar o [!UICONTROL Público-alvo correspondente do linkedIn] destino, verifique se [!DNL LinkedIn Campaign Manager] a conta tem o [!DNL Creative Manager] nível de permissão ou superior.

Para saber como editar suas [!DNL LinkedIn Campaign Manager] permissões do usuário, consulte [Adicionar, editar e remover permissões de usuário em contas publicitárias](https://www.linkedin.com/help/lms/answer/5753) na documentação do LinkedIn.

## Requisitos de correspondência de ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] exige que nenhuma informação pessoal identificável (PII) seja enviada em claro. Portanto, os públicos-alvo foram ativados para [!DNL LinkedIn Matched Audiences] pode ser desativado *com hash* identificadores, como endereços de email ou IDs de dispositivos móveis.

Dependendo do tipo de IDs que você assimila no Adobe Experience Platform, é necessário seguir os requisitos correspondentes.

## Requisitos de hash de email {#email-hashing-requirements}

Você pode aplicar hash a endereços de email antes de assimilá-los no Adobe Experience Platform ou usar endereços de email em limpar no Experience Platform e ter [!DNL Platform] coloque hash neles na ativação.

Para saber mais sobre a assimilação de endereços de email no Experience Platform, consulte o [visão geral da assimilação em lote](/help/ingestion/batch-ingestion/overview.md) e a variável [visão geral da assimilação por transmissão](/help/ingestion/streaming-ingestion/overview.md).

Se você optar por criar o hash dos endereços de email, não se esqueça de atender aos seguintes requisitos:

* Cortar todos os espaços à esquerda e à direita da cadeia de caracteres de email. Por exemplo: `johndoe@example.com`, não `<space>johndoe@example.com<space>`;
* Ao aplicar hash às cadeias de caracteres de email, certifique-se de aplicar hash à cadeia de caracteres em minúsculas;
   * Exemplo: `example@email.com`, não `EXAMPLE@EMAIL.COM`;
* Verifique se a cadeia de caracteres com hash está em minúsculas
   * Exemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, não `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Não salve a corda.

>[!NOTE]
>
>O hash automático é aplicado aos dados de namespaces sem hash [!DNL Platform] na ativação.
> Os dados de origem do atributo não são automaticamente transformados em hash.
> 
> Durante a [Mapeamento de identidade](../../ui/activate-segment-streaming-destinations.md#mapping) etapa, quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação.
> 
> A variável **[!UICONTROL Aplicar transformação]** é exibida somente quando você seleciona atributos como campos de origem. Ela não é exibida ao escolher namespaces.

![Transformação de mapeamento de identidade](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

O vídeo abaixo também demonstra as etapas para configurar um [!DNL LinkedIn Matched Audiences] direcionar e ativar públicos-alvo.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>A interface do usuário do Experience Platform é atualizada com frequência e pode ter mudado desde a gravação deste vídeo. Para obter as informações mais atualizadas, consulte as [tutorial de configuração de destino](../../ui/connect-destination.md).

### Autenticar para destino {#authenticate}

1. Localize o [!DNL LinkedIn Matched Audiences] no catálogo de destino e selecione **[!UICONTROL Configurar]**.
2. Selecionar **[!UICONTROL Conectar ao destino]**.
   ![Autenticar no LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Insira suas credenciais do LinkedIn e selecione **Fazer logon**.

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="ID da conta"
>abstract="Sua ID da conta do Campaign Manager no LinkedIn. Você pode encontrar essa ID na conta do Campaign Manager do LinkedIn."

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL ID da conta]**: Seu [!DNL LinkedIn Campaign Manager Account ID]. Você pode encontrar essa ID em seu [!DNL LinkedIn Campaign Manager] conta.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

## Dados exportados {#exported-data}

Uma ativação bem-sucedida significa que uma [!DNL LinkedIn] o público-alvo personalizado seria criado programaticamente no [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). A associação de público-alvo seria adicionada e removida à medida que os usuários fossem qualificados ou desqualificados para os públicos ativados.

>[!TIP]
>
>A integração entre o Adobe Experience Platform e o [!DNL LinkedIn Matched Audiences] O suporta preenchimentos retroativos de público-alvo histórico. Todas as qualificações históricas de público são enviadas para o [!DNL LinkedIn] quando você ativa os públicos-alvo para o destino.
