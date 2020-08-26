---
keywords: facebook extensions;facebook extension;facebook destinations;facebook
title: Destino do Facebook
seo-title: Destino do Facebook
description: Ative perfis para suas campanhas do Facebook para definição de metas, personalização e supressão de audiências com base em emails com hash.
seo-description: Ative perfis para suas campanhas do Facebook para definição de metas, personalização e supressão de audiências com base em emails com hash.
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 2%

---


# [!DNL Facebook] Destino

## Visão geral {#overview}

Ative perfis para suas [!DNL Facebook] campanhas para definição de metas, personalização e supressão de audiências com base em emails com hash.

![Destino do Facebook na interface do usuário do CDP em tempo real](/help/rtcdp/destinations/assets/facebook-destination.png)

## Casos de uso

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL Facebook] destino, veja dois exemplos de casos de uso que os clientes da Plataforma de dados do cliente em tempo real podem resolver usando esse recurso.


### Caso de uso nº 1


Um varejista online quer atingir os clientes existentes por meio de plataformas sociais e mostrar-lhes ofertas personalizadas com base em seus pedidos anteriores. O varejista online pode assimilar endereços de email de seu próprio CRM para o Adobe Real-time CDP, criar segmentos a partir de seus próprios dados offline e enviar esses segmentos para a plataforma [!DNL Facebook] social, otimizando seus gastos com publicidade.


### Caso de uso nº 2


Uma companhia aérea tem níveis de clientes diferentes (Bronze, Prata e Ouro) e deseja fornecer a cada um dos níveis ofertas personalizadas por meio de plataformas sociais. No entanto, nem todos os clientes usam o aplicativo móvel da companhia aérea e alguns deles não fizeram logon no site da empresa. Os únicos identificadores que a empresa tem sobre esses clientes são IDs de associação e endereços de email.

Para público alvo-los nas mídias sociais, eles podem integrar os dados do cliente de seu CRM para o CDP em tempo real do Adobe, usando os endereços de email como identificadores.

Em seguida, eles podem usar seus dados offline, incluindo as IDs de associação associadas e os níveis do cliente, para criar novos segmentos de audiência que podem público alvo até o [!DNL Facebook] destino.

## Especificações de destino {#destination-specs}

### Controle de dados para [!DNL Facebook] destinos {#data-governance}

>[!IMPORTANT]
>
>Os dados enviados para [!DNL Facebook] não devem incluir identidades agrupadas. Você é responsável por cumprir essa obrigação e pode fazê-lo garantindo que os segmentos selecionados para ativação não usem uma opção de agrupamento em sua política de mesclagem. Saiba mais sobre as políticas [de](/help/profile/ui/merge-policies.md)mesclagem.

### Tipo de ativação {#activation-type}

**Exportação** de segmento - você está exportando todos os membros de um segmento (audiência) com os identificadores (nome, número de telefone etc.) usado no destino do Facebook.

### Pré-requisitos da conta do Facebook {#facebook-account-prerequisites}

Antes de enviar os segmentos de audiência para [!DNL Facebook], verifique se você atende aos seguintes requisitos:

1. Sua conta de [!DNL Facebook] usuário deve ter a **[!DNL Manage campaigns]** permissão ativada para a conta de anúncio que você planeja usar.
2. Add the **Adobe Experience Cloud** business account as an advertising partner in your [!DNL Facebook Ad Account]. Use `business ID=206617933627973`. Consulte [Adicionar parceiros ao seu gerente](https://www.facebook.com/business/help/1717412048538897) de negócios na documentação do Facebook para obter detalhes.
   >[!IMPORTANT]
   >
   > When configuring the permissions for Adobe Experience Cloud, you must enable the **Manage campaigns** permission. Isso é necessário para a integração de [!DNL Adobe Real-time CDP].
3. Leia e assine os [!DNL Facebook Custom Audiences] Termos de serviço. Para fazer isso, acesse `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, onde `accountID` é a sua [!DNL Facebook Ad Account ID].

### Requisitos de hash de email {#email-hashing-requirements}

[!DNL Facebook] requer que nenhuma informação pessoal identificável (PII) seja enviada de forma clara. Portanto, as audiências ativadas para [!DNL Facebook] devem ser desconectadas de endereços de email *com hash* . Você pode optar por hash de endereços de email antes de ingressá-los no Adobe Experience Platform ou pode optar por trabalhar com endereços de email claramente no Experience Platform e fazer com que nosso algoritmo os coloque em hash na ativação.

Para saber mais sobre como assimilar endereços de email no Experience Platform, consulte a visão geral [da ingestão em](/help/ingestion/batch-ingestion/overview.md) lote e a visão geral [da](/help/ingestion/streaming-ingestion/overview.md)ingestão em vapor.

Se você optar por hash nos endereços de email, certifique-se de cumprir os seguintes requisitos:

* Aparar todos os espaços à esquerda e à direita da string de email; exemplo: `johndoe@example.com`, não `<space>johndoe@example.com<space>`;
* Ao executar o hash das strings de email, certifique-se de executar o hash da string em minúsculas;
   * Exemplo: `example@email.com`, não `EXAMPLE@EMAIL.COM`;
* Certifique-se de que a cadeia de caracteres com hash esteja toda em minúsculas
   * Exemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, não `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Não salve a corda.


>[!IMPORTANT]
>
>Se você optar por não criar hash de endereços de email, o Adobe Real-time CDP fará isso para você ao ativar segmentos para [!DNL Facebook]. No fluxo de trabalho [da](/help/rtcdp/destinations/activate-destinations.md#activate-data) ativação (consulte a etapa 5), selecione a `Email` opção como mostrado abaixo para endereços *de email* brutos e `Email_LC_SHA256` endereços *de email* com hash.


![Ligação na ativação](/help/rtcdp/destinations/assets/identity-mapping.png)

## Conectar ao destino {#connect-destination}

Para se conectar ao [!DNL Facebook] destino, consulte Fluxo de trabalho [de autenticação de destinos de rede](/help/rtcdp/destinations/social-network-destinations-workflow.md)Social.


## Ativar segmentos para [!DNL Facebook] {#activate-segments}

Para obter instruções sobre como ativar segmentos para [!DNL Facebook], consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).

## Dados exportados {#exported-data}

Para [!DNL Facebook], uma ativação bem-sucedida significa que uma audiência [!DNL Facebook] personalizada seria criada programaticamente no [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). A associação de segmento na audiência seria adicionada e removida, pois os usuários são qualificados ou desqualificados para os segmentos ativados.

>[!TIP]
>
>A integração entre a CDP em tempo real do Adobe e [!DNL Facebook] suporta preenchimentos retroativos históricos de audiência. Todas as qualificações de segmento histórico são enviadas para [!DNL Facebook] quando você ativa os segmentos para o destino.