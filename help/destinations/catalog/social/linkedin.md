---
keywords: link-in-connection;linkedin connection;linkedin targets;linkedin;
title: Conexão de Audiência correspondente do LinkedIn
description: Ative perfis para suas campanhas do LinkedIn para definição de metas, personalização e supressão de audiências, com base em emails com hash.
translation-type: tm+mt
source-git-commit: d51de1ab4b2d4e91232166657466e597093f22ef
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---


# [!DNL LinkedIn Matched Audience] conexão

Ative perfis para suas [!DNL LinkedIn] campanhas para definição de metas, personalização e supressão de audiências, com base em emails com hash e IDs móveis.

![Destino do LinkedIn na interface do usuário do Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Casos de uso

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL LinkedIn Matched Audience], este é um caso de uso que os clientes da Adobe Experience Platform podem resolver usando esse recurso.

Uma empresa de software organiza uma conferência e quer manter contato com os participantes e mostrar-lhes ofertas personalizadas com base em seu status de participação na conferência. A empresa pode assimilar endereços de email ou IDs de dispositivos móveis de seu próprio [!DNL CRM] no Adobe Experience Platform, criar segmentos a partir de seus próprios dados offline e enviar esses segmentos para a plataforma social [!DNL LinkedIn], otimizando seus gastos com publicidade.

## Especificações de destino {#destination-specs}

[!DNL LinkedIn Matched Audience] apoia a ativação das seguintes identidades: e-mails com hash,  [!DNL GAID]e  [!DNL IDFA].

### Tipo de exportação {#export-type}

**Exportação**  de segmento - você está exportando todos os membros de um segmento (audiência) com os identificadores (nome, número de telefone etc.) usado no destino [!DNL LinkedIn Matched Audience].

### Pré-requisitos da conta do LinkedIn {#LinkedIn-account-prerequisites}

Antes de poder usar o destino [!UICONTROL Audiência Correspondente do LinkedIn], verifique se sua conta [!DNL LinkedIn Campaign Manager] tem o nível de permissão [!DNL Creative Manager] ou superior.

Para saber como editar suas [!DNL LinkedIn Campaign Manager] permissões de usuário, consulte [Adicionar, editar e remover permissões de usuário em contas de publicidade](https://www.linkedin.com/help/lms/answer/5753) na documentação do LinkedIn.

### Requisitos de correspondência de ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audience] requer que nenhuma informação pessoal identificável (PII) seja enviada de forma clara. Portanto, as audiências ativadas para [!DNL LinkedIn Matched Audience] podem ser desconectadas dos identificadores *hash*, como endereços de email ou IDs de dispositivos móveis.

Dependendo do tipo de IDs ingeridas no Adobe Experience Platform, é necessário atender aos requisitos correspondentes.

#### Requisitos de hash de email {#email-hashing-requirements}

Você pode optar por hash de endereços de email antes de ingressá-los no Adobe Experience Platform ou pode optar por trabalhar com endereços de email claramente no Experience Platform e fazer com que nosso algoritmo os coloque em hash na ativação.

Para saber mais sobre como ingerir endereços de email no Experience Platform, consulte [visão geral de ingestão em lote](/help/ingestion/batch-ingestion/overview.md) e a [visão geral de ingestão em streaming](/help/ingestion/streaming-ingestion/overview.md).

Se você optar por hash nos endereços de email, certifique-se de cumprir os seguintes requisitos:

- Aparar todos os espaços à esquerda e à direita da string de email. Por exemplo: `johndoe@example.com`, não `<space>johndoe@example.com<space>`;
- Ao executar o hash das strings de email, certifique-se de executar o hash da string em minúsculas;
   - Exemplo: `example@email.com`, não `EXAMPLE@EMAIL.COM`;
- Certifique-se de que a cadeia de caracteres com hash esteja toda em minúsculas
   - Exemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, não `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- Não salve a corda.

>[!NOTE]
>
>Os dados de namespaces sem hash são automaticamente hash por [!DNL Platform] na ativação.
> Os dados da fonte do atributo não são automaticamente hash.
> 
> Durante a etapa [Mapeamento de identidade](../../ui/activate-destinations.md#identity-mapping), quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Aplicar transformação]** para que [!DNL Platform] faça hash automático dos dados na ativação.
> 
> A opção **[!UICONTROL Aplicar transformação]** só é exibida quando você seleciona atributos como campos de origem. Ele não é exibido quando você escolhe namespaces.

![Transformação de mapeamento de identidade](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Conectar ao destino {#connect-destination}

Para se conectar ao destino [!DNL LinkedIn Matched Audience], consulte [Fluxo de trabalho de autenticação de destinos de rede social](./workflow.md).

## Ativar segmentos para [!DNL LinkedIn Matched Audience] {#activate-segments}

Para obter instruções sobre como ativar segmentos para [!DNL LinkedIn Matched Audience], consulte [Ativar dados para destinos](../../ui/activate-destinations.md).

## Dados exportados {#exported-data}

Uma ativação bem-sucedida significa que uma audiência personalizada [!DNL LinkedIn] seria criada programaticamente em [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). A associação de segmento na audiência seria adicionada e removida, pois os usuários são qualificados ou desqualificados para os segmentos ativados.

>[!TIP]
>
>A integração entre o Adobe Experience Platform e [!DNL LinkedIn Matched Audience] oferece suporte a preenchimentos retroativos históricos de audiência. Todas as qualificações de segmento histórico são enviadas para [!DNL LinkedIn] quando você ativa os segmentos para o destino.