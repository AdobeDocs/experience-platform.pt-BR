---
keywords: Conexão facebook; Conexão facebook; Destinos facebook; facebook; instagram; mensageiro; facebook Messenger
title: Conexão facebook
description: Ative perfis para suas campanhas do Facebook para direcionamento de público-alvo, personalização e supressão com base em emails com hash.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
translation-type: tm+mt
source-git-commit: 1e9e5831b19738285affeb0337985c7cb0d45ebf
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 2%

---

# [!DNL Facebook] conexão

## Visão geral {#overview}

Ative perfis para suas campanhas [!DNL Facebook] para segmentação, personalização e supressão de público-alvo com base em emails com hash.

Você pode usar esse destino para segmentação de público-alvo em [!DNL Facebook’s] família de aplicativos compatíveis com [!DNL Custom Audiences], incluindo [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] e [!DNL Messenger]. A seleção do aplicativo no qual você deseja executar a campanha é indicada no nível de posicionamento no [!DNL Facebook Ads Manager].

![Destino do facebook na interface do usuário do Adobe Experience Platform](../../assets/catalog/social/facebook/catalog.png)

## Casos de uso

Para ajudá-lo a entender melhor como e quando usar o destino [!DNL Facebook], aqui estão dois casos de uso de exemplo que os clientes do Adobe Experience Platform podem resolver usando esse recurso.

### Caso de uso nº 1

Um varejista online deseja alcançar clientes existentes por meio de plataformas sociais e mostrar a eles ofertas personalizadas com base em seus pedidos anteriores. O varejista online pode assimilar endereços de email de seu próprio CRM para o Adobe Experience Platform, criar segmentos a partir de seus próprios dados offline e enviar esses segmentos para a [!DNL Facebook] plataforma social, otimizando seus gastos com publicidade.

### Caso de uso nº 2

Uma companhia aérea tem níveis de clientes diferentes (Bronze, Prata e Ouro) e deseja fornecer a cada um dos níveis ofertas personalizadas por meio de plataformas sociais. No entanto, nem todos os clientes usam o aplicativo móvel da companhia aérea e alguns deles não fizeram logon no site da empresa. Os únicos identificadores que a empresa tem sobre esses clientes são IDs de associação e endereços de email.

Para direcioná-los em redes sociais, eles podem integrar os dados do cliente do CRM para o Adobe Experience Platform, usando os endereços de email como identificadores.

Em seguida, eles podem usar seus dados offline, incluindo as IDs de associação associadas e os níveis do cliente para criar novos segmentos de público-alvo que podem direcionar por meio do destino [!DNL Facebook].

## Identidades compatíveis {#supported-identities}

[!DNL Facebook Custom Audiences] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| GAID | ID de publicidade do Google | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando sua identidade de origem for um namespace do IDFA. |
| phone_sha256 | Números de telefone com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e números de telefone com hash SHA256. Siga as instruções na seção [ID correspondente a requirements](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para texto sem formatação e números de telefone com hash, respectivamente. Quando o campo de origem contém atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para ter [!DNL Platform] hash automaticamente os dados na ativação. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. Siga as instruções na seção [ID correspondente a requirements](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para texto sem formatação e endereços de email com hash, respectivamente. Quando o campo de origem contém atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para ter [!DNL Platform] hash automaticamente os dados na ativação. |
| external_id | IDs de usuário personalizadas | Selecione essa identidade de destino quando sua identidade de origem for um namespace personalizado. |

## Tipo de exportação {#export-type}

**Exportar segmento**  - você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados no destino do Facebook.

## Pré-requisitos da conta do facebook {#facebook-account-prerequisites}

Antes de enviar seus segmentos de público-alvo para [!DNL Facebook], verifique se você atende aos seguintes requisitos:

- Sua conta de usuário [!DNL Facebook] deve ter a permissão **[!DNL Manage campaigns]** ativada para a conta de anúncio que você planeja usar.
- A conta comercial **Adobe Experience Cloud** deve ser adicionada como um parceiro de publicidade em seu [!DNL Facebook Ad Account]. Use `business ID=206617933627973`. Consulte [Adicionar parceiros ao seu gerente de negócios](https://www.facebook.com/business/help/1717412048538897) na documentação do Facebook para obter detalhes.
   >[!IMPORTANT]
   >
   > Ao configurar as permissões para o Adobe Experience Cloud, você deve habilitar a permissão **Gerenciar campanhas**. A permissão é necessária para a integração [!DNL Adobe Experience Platform].
- Leia e assine os [!DNL Facebook Custom Audiences] Termos de serviço. Para fazer isso, vá para `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, onde `accountID` é seu [!DNL Facebook Ad Account ID].

## Requisitos de correspondência de ID {#id-matching-requirements}

[!DNL Facebook] exige que nenhuma informação pessoal identificável (PII) seja enviada de forma clara. Portanto, os públicos-alvo ativados para [!DNL Facebook] podem ser desconectados dos identificadores com hash *como endereços de email ou números de telefone.*

Dependendo do tipo de IDs assimiladas no Adobe Experience Platform, é necessário seguir os requisitos correspondentes.

## Requisitos de hash do número de telefone {#phone-number-hashing-requirements}

Há dois métodos para ativar números de telefone em [!DNL Facebook]:

- **Inserir números** de telefone brutos: você pode assimilar números de telefone brutos no  [!DNL E.164] formato  [!DNL Platform]. Eles passam automaticamente por hash na ativação. Se você escolher essa opção, certifique-se sempre de assimilar seus números de telefone brutos no namespace `Phone_E.164`.
- **Inserir números** de telefone com hash: você pode fazer o hash prévio dos números de telefone antes da ingestão no  [!DNL Platform]. Se você escolher essa opção, certifique-se sempre de assimilar seus números de telefone com hash no namespace `Phone_SHA256`.

>[!NOTE]
>
>Os números de telefone assimilados no namespace `Phone` não podem ser ativados em [!DNL Facebook].


## Requisitos de hash de email {#email-hashing-requirements}

Você pode fazer hash de endereços de email antes de assimilá-los no Adobe Experience Platform ou usar endereços de email limpos no Experience Platform e fazer com que [!DNL Platform] faça hash na ativação.

Para saber mais sobre como assimilar endereços de email no Experience Platform, consulte a [visão geral de assimilação de lote](/help/ingestion/batch-ingestion/overview.md) e a [visão geral de assimilação de streaming](/help/ingestion/streaming-ingestion/overview.md).

Se você optar por hash nos endereços de email, certifique-se de estar em conformidade com os seguintes requisitos:

- Cortar todos os espaços à esquerda e à direita da string de email; exemplo: `johndoe@example.com`, não `<space>johndoe@example.com<space>`;
- Ao fazer o hash das cadeias de caracteres de email, certifique-se de fazer hash na cadeia de caracteres de minúsculas;
   - Exemplo: `example@email.com`, não `EXAMPLE@EMAIL.COM`;
- Certifique-se de que a cadeia de caracteres com hash esteja em letras minúsculas
   - Exemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, não `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- Não salve a corda.

>[!NOTE]
>
>Os dados de namespaces sem hash são automaticamente atribuídos a hash por [!DNL Platform] após a ativação.
> Os dados da fonte de atributo não são automaticamente transformados em hash. Quando o campo de origem contém atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para ter [!DNL Platform] hash automaticamente os dados na ativação.
> A opção **[!UICONTROL Apply transformation]** só é exibida quando você seleciona atributos como campos de origem. Ele não é exibido quando você escolhe namespaces.

![Transformação de mapeamento de identidade](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Uso de namespaces personalizados {#custom-namespaces}

Antes de usar o namespace `Extern_ID` para enviar dados a [!DNL Facebook], sincronize seus próprios identificadores usando [!DNL Facebook Pixel]. Consulte a [documentação oficial do Facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) para obter informações detalhadas.

## Conecte-se ao destino {#connect-destination}

Para se conectar ao destino [!DNL Facebook], consulte [Fluxo de trabalho de autenticação de destinos sociais](./workflow.md).

O vídeo abaixo também demonstra as etapas para configurar um destino [!DNL Facebook] e ativar segmentos.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Ativar segmentos para [!DNL Facebook] {#activate-segments}

Para obter instruções sobre como ativar segmentos para [!DNL Facebook], consulte [Ativar dados para destinos](../../ui/activate-destinations.md).

Na etapa **[!UICONTROL Segment schedule]**, você deve fornecer o [!UICONTROL Origin of audience] ao enviar segmentos para [!DNL Facebook Custom Audiences].

![Origem do público-alvo do facebook](../../assets/catalog/social/facebook/facebook-origin-audience.png)

## Dados exportados {#exported-data}

Para [!DNL Facebook], uma ativação bem-sucedida significa que um público-alvo personalizado [!DNL Facebook] seria criado programaticamente em [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). A associação de segmento no público-alvo seria adicionada e removida, pois os usuários eram qualificados ou desqualificados para os segmentos ativados.

>[!TIP]
>
>A integração entre o Adobe Experience Platform e [!DNL Facebook] oferece suporte a preenchimentos retroativos de público-alvo históricos. Todas as qualificações de segmento histórico são enviadas para [!DNL Facebook] quando você ativa os segmentos para o destino.
