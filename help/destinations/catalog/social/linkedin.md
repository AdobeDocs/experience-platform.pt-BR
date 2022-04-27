---
keywords: conexão do linkedin; conexão do linkedin; destinos do linkedin; linkedin;
title: Conexão de públicos-alvo correspondentes do Linkedin
description: Ative perfis para suas campanhas do LinkedIn para direcionamento de público-alvo, personalização e supressão, com base em emails com hash.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 2%

---

# [!DNL LinkedIn Matched Audiences] conexão

## Visão geral {#overview}

Ativar perfis para seu [!DNL LinkedIn] campanhas para direcionamento, personalização e supressão de público-alvo, com base em emails com hash e IDs móveis.

![Destino do linkedIn na interface do usuário do Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Casos de uso

Para ajudá-lo a entender melhor como e quando usar a variável [!DNL LinkedIn Matched Audiences] , este é um caso de uso que os clientes do Adobe Experience Platform podem resolver usando esse recurso.

Uma empresa de software organiza uma conferência e deseja manter contato com os participantes e mostrar a eles ofertas personalizadas com base em seu status de presença em conferência. A empresa pode assimilar endereços de email ou IDs de dispositivo móvel por conta própria [!DNL CRM] no Adobe Experience Platform. Em seguida, eles podem criar segmentos a partir de seus próprios dados offline e enviar esses segmentos para a [!DNL LinkedIn] plataforma social, otimizando seus gastos com publicidade.

## Identidades suportadas {#supported-identities}

[!DNL LinkedIn Matched Audiences] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| GAID | Google Advertising ID | Selecione essa identidade de destino quando sua identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione essa identidade de destino quando sua identidade de origem for um namespace IDFA. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. Siga as instruções em [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para texto sem formatação e emails com hash, respectivamente. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone e outros) usados na [!DNL LinkedIn Matched Audiences] destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Pré-requisitos da conta do linkedIn {#LinkedIn-account-prerequisites}

Antes de usar a variável [!UICONTROL Público-alvo correspondente do linkedIn] de destino, verifique se [!DNL LinkedIn Campaign Manager] tem a [!DNL Creative Manager] nível de permissão ou superior.

Para saber como editar seu [!DNL LinkedIn Campaign Manager] permissões do usuário, consulte [Adicionar, editar e remover permissões de usuário em contas publicitárias](https://www.linkedin.com/help/lms/answer/5753) na documentação do LinkedIn.

## Requisitos de correspondência de ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] exige que nenhuma informação pessoal identificável (PII) seja enviada de forma clara. Portanto, os públicos-alvo ativados para [!DNL LinkedIn Matched Audiences] pode ser desligado *hash* identificadores, como endereços de email ou IDs de dispositivo móvel.

Dependendo do tipo de IDs assimiladas no Adobe Experience Platform, é necessário seguir os requisitos correspondentes.

## Requisitos de hash de email {#email-hashing-requirements}

Você pode fazer hash nos endereços de email antes de assimilá-los no Adobe Experience Platform ou usar endereços de email limpos no Experience Platform e ter [!DNL Platform] coloque hash na ativação.

Para saber mais sobre como assimilar endereços de email no Experience Platform, consulte o [visão geral da ingestão em lote](/help/ingestion/batch-ingestion/overview.md) e [visão geral da assimilação de streaming](/help/ingestion/streaming-ingestion/overview.md).

Se você optar por hash nos endereços de email, certifique-se de estar em conformidade com os seguintes requisitos:

* Cortar todos os espaços à esquerda e à direita da string de email. Por exemplo: `johndoe@example.com`, não `<space>johndoe@example.com<space>`;
* Ao fazer o hash das cadeias de caracteres de email, certifique-se de fazer hash na cadeia de caracteres de minúsculas;
   * Exemplo: `example@email.com`, não `EXAMPLE@EMAIL.COM`;
* Certifique-se de que a cadeia de caracteres com hash esteja em letras minúsculas
   * Exemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, não `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Não salve a corda.

>[!NOTE]
>
>Os dados de namespaces sem hash são automaticamente atribuídos a hash por [!DNL Platform] após a ativação.
> Os dados da fonte de atributo não são automaticamente transformados em hash.
> 
> Durante os [Mapeamento de identidade](../../ui/activate-segment-streaming-destinations.md#mapping) , quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação.
> 
> O **[!UICONTROL Aplicar transformação]** A opção é exibida somente quando você seleciona atributos como campos de origem. Ele não é exibido quando você escolhe namespaces.

![Transformação de mapeamento de identidade](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

O vídeo abaixo também demonstra as etapas para configurar um [!DNL LinkedIn Matched Audiences] e ativar segmentos.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>A interface do usuário do Experience Platform é atualizada com frequência e pode ter sido alterada desde a gravação deste vídeo. Para obter as informações mais atualizadas, consulte o [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID da conta]**: your [!DNL LinkedIn Campaign Manager Account ID]. Você pode encontrar essa ID em seu [!DNL LinkedIn Campaign Manager] conta.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Dados exportados {#exported-data}

Uma ativação bem-sucedida significa que uma [!DNL LinkedIn] o público-alvo personalizado seria criado programaticamente em [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). A associação de segmento no público-alvo seria adicionada e removida, pois os usuários eram qualificados ou desqualificados para os segmentos ativados.

>[!TIP]
>
>A integração entre o Adobe Experience Platform e o [!DNL LinkedIn Matched Audiences] O suporta preenchimentos retroativos de público-alvo históricos. Todas as qualificações de segmento histórico são enviadas para [!DNL LinkedIn] ao ativar os segmentos para o destino.
