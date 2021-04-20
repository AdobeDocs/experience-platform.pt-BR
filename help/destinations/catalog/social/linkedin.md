---
keywords: conexão do linkedin; conexão do linkedin; destinos do linkedin; linkedin;
title: Conexão de públicos-alvo correspondentes do Linkedin
description: Ative perfis para suas campanhas do LinkedIn para direcionamento de público-alvo, personalização e supressão, com base em emails com hash.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
translation-type: tm+mt
source-git-commit: 95ca7112d1f2655bf33e8a1c549e886ced244a5d
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 1%

---

# [!DNL LinkedIn Matched Audiences] conexão

## Visão geral {#overview}

Ative perfis para suas campanhas [!DNL LinkedIn] para segmentação, personalização e supressão de público-alvo, com base em emails com hash e IDs móveis.

![Destino do linkedIn na interface do usuário do Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Casos de uso

Para ajudá-lo a entender melhor como e quando usar o destino [!DNL LinkedIn Matched Audiences], aqui está um caso de uso que os clientes do Adobe Experience Platform podem resolver usando esse recurso.

Uma empresa de software organiza uma conferência e deseja manter contato com os participantes e mostrar a eles ofertas personalizadas com base em seu status de presença em conferência. A empresa pode assimilar endereços de email ou IDs de dispositivo móvel de seu próprio [!DNL CRM] para o Adobe Experience Platform. Em seguida, eles podem criar segmentos a partir de seus próprios dados offline e enviar esses segmentos para a [!DNL LinkedIn] plataforma social, otimizando seus gastos com publicidade.

## Identidades compatíveis {#supported-identities}

[!DNL LinkedIn Matched Audiences] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| GAID | ID de publicidade do Google | Selecione essa identidade de destino quando sua identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione essa identidade de destino quando sua identidade de origem for um namespace IDFA. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. Siga as instruções na seção [ID correspondente a requirements](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para texto sem formatação e emails com hash, respectivamente. Quando o campo de origem contém atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para ter [!DNL Platform] hash automaticamente os dados na ativação. |


## Tipo de exportação {#export-type}

**Exportar segmento**  - você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone e outros) usados no  [!DNL LinkedIn Matched Audiences] destino.

## Pré-requisitos da conta do linkedIn {#LinkedIn-account-prerequisites}

Antes de usar o destino [!UICONTROL LinkedIn Matched Audience], verifique se a conta [!DNL LinkedIn Campaign Manager] tem o nível de permissão [!DNL Creative Manager] ou superior.

Para saber como editar suas permissões de usuário [!DNL LinkedIn Campaign Manager], consulte [Adicionar, editar e remover permissões de usuário em contas publicitárias](https://www.linkedin.com/help/lms/answer/5753) na documentação do LinkedIn.

## Requisitos de correspondência de ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] exige que nenhuma informação pessoal identificável (PII) seja enviada de forma clara. Portanto, os públicos-alvo ativados para [!DNL LinkedIn Matched Audiences] podem ser desmarcados com identificadores *com hash*, como endereços de email ou IDs de dispositivo móvel.

Dependendo do tipo de IDs assimiladas no Adobe Experience Platform, é necessário seguir os requisitos correspondentes.

## Requisitos de hash de email {#email-hashing-requirements}

Você pode fazer hash de endereços de email antes de assimilá-los no Adobe Experience Platform ou usar endereços de email limpos no Experience Platform e fazer com que [!DNL Platform] faça hash na ativação.

Para saber mais sobre como assimilar endereços de email no Experience Platform, consulte a [visão geral de assimilação de lote](/help/ingestion/batch-ingestion/overview.md) e a [visão geral de assimilação de streaming](/help/ingestion/streaming-ingestion/overview.md).

Se você optar por hash nos endereços de email, certifique-se de estar em conformidade com os seguintes requisitos:

- Cortar todos os espaços à esquerda e à direita da string de email. Por exemplo: `johndoe@example.com`, não `<space>johndoe@example.com<space>`;
- Ao fazer o hash das cadeias de caracteres de email, certifique-se de fazer hash na cadeia de caracteres de minúsculas;
   - Exemplo: `example@email.com`, não `EXAMPLE@EMAIL.COM`;
- Certifique-se de que a cadeia de caracteres com hash esteja em letras minúsculas
   - Exemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, não `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- Não salve a corda.

>[!NOTE]
>
>Os dados de namespaces sem hash são automaticamente atribuídos a hash por [!DNL Platform] após a ativação.
> Os dados da fonte de atributo não são automaticamente transformados em hash.
> 
> Durante a etapa [Mapeamento de identidade](../../ui/activate-destinations.md#identity-mapping), quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para ter [!DNL Platform] automaticamente hash os dados na ativação.
> 
> A opção **[!UICONTROL Apply transformation]** só é exibida quando você seleciona atributos como campos de origem. Ele não é exibido quando você escolhe namespaces.

![Transformação de mapeamento de identidade](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Conecte-se ao destino {#connect-destination}

Para se conectar ao destino [!DNL LinkedIn Matched Audiences], consulte [Fluxo de trabalho de autenticação de destinos de rede social](./workflow.md).

O vídeo abaixo também demonstra as etapas para configurar um destino [!DNL LinkedIn Matched Audiences] e ativar segmentos.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Ativar segmentos para [!DNL LinkedIn Matched Audiences] {#activate-segments}

Para obter instruções sobre como ativar segmentos para [!DNL LinkedIn Matched Audiences], consulte [Ativar dados para destinos](../../ui/activate-destinations.md).

## Dados exportados {#exported-data}

Uma ativação bem-sucedida significa que um público-alvo personalizado [!DNL LinkedIn] seria criado programaticamente em [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). A associação de segmento no público-alvo seria adicionada e removida, pois os usuários eram qualificados ou desqualificados para os segmentos ativados.

>[!TIP]
>
>A integração entre o Adobe Experience Platform e [!DNL LinkedIn Matched Audiences] oferece suporte a preenchimentos retroativos de público-alvo históricos. Todas as qualificações de segmento histórico são enviadas para [!DNL LinkedIn] quando você ativa os segmentos para o destino.
