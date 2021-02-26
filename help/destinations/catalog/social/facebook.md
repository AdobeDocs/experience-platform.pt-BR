---
keywords: conexão do Facebook;conexão do Facebook;destinos do facebook;facebook;instagram;mensageiro;facebook messenger
title: Conexão do Facebook
description: Ative perfis para suas campanhas do Facebook para definição de metas, personalização e supressão de audiências com base em emails com hash.
translation-type: tm+mt
source-git-commit: bec44832a235dd3f9e2ee0f3ffc77854ee5784d7
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 3%

---


# [!DNL Facebook] conexão

Ative perfis para suas [!DNL Facebook] campanhas para definição de metas, personalização e supressão de audiências com base em emails com hash.

Você pode usar esse destino para direcionamento de audiência na família [!DNL Facebook’s] de aplicativos compatíveis com [!DNL Custom Audiences], incluindo [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] e [!DNL Messenger]. A seleção do aplicativo no qual você deseja executar a campanha é indicada no nível de posicionamento no [!DNL Facebook Ads Manager].

![Destino do Facebook na interface do usuário do Adobe Experience Platform](../../assets/catalog/social/facebook/catalog.png)

## Casos de uso

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Facebook], há dois casos de uso de amostra que os clientes da Adobe Experience Platform podem resolver usando esse recurso.

### Caso de uso nº 1

Um varejista online quer atingir os clientes existentes por meio de plataformas sociais e mostrar-lhes ofertas personalizadas com base em seus pedidos anteriores. O varejista online pode assimilar endereços de email de seu próprio CRM para a Adobe Experience Platform, criar segmentos a partir de seus próprios dados offline e enviar esses segmentos para a plataforma social [!DNL Facebook], otimizando seus gastos com publicidade.

### Caso de uso nº 2

Uma companhia aérea tem níveis de clientes diferentes (Bronze, Prata e Ouro) e deseja fornecer a cada um dos níveis ofertas personalizadas por meio de plataformas sociais. No entanto, nem todos os clientes usam o aplicativo móvel da companhia aérea e alguns deles não fizeram logon no site da empresa. Os únicos identificadores que a empresa tem sobre esses clientes são IDs de associação e endereços de email.

Para público alvo em redes sociais, eles podem integrar os dados do cliente de seu CRM para o Adobe Experience Platform, usando os endereços de email como identificadores.

Em seguida, eles podem usar seus dados offline, incluindo as IDs de associação associadas e os níveis do cliente, para criar novos segmentos de audiência que possam público alvo pelo destino [!DNL Facebook].

## Especificações de destino {#destination-specs}

### Controle de dados para [!DNL Facebook] destinos {#data-governance}

>[!IMPORTANT]
>
>Os dados enviados para [!DNL Facebook] não devem incluir identidades pontilhadas. Você é responsável por cumprir essa obrigação e pode fazê-lo garantindo que os segmentos selecionados para ativação não usem uma opção de agrupamento em sua política de mesclagem. Saiba mais sobre [políticas de mesclagem](/help/profile/ui/merge-policies.md).

### Tipo de exportação {#export-type}

**Exportação**  de segmento - você está exportando todos os membros de um segmento (audiência) com os identificadores (nome, número de telefone etc.) usado no destino do Facebook.

### Pré-requisitos da conta do Facebook {#facebook-account-prerequisites}

Antes de enviar seus segmentos de audiência para [!DNL Facebook], certifique-se de atender aos seguintes requisitos:

- Sua conta de usuário [!DNL Facebook] deve ter a permissão **[!DNL Manage campaigns]** ativada para a conta de anúncio que você planeja usar.
- A conta comercial **Adobe Experience Cloud** deve ser adicionada como um parceiro publicitário em seu [!DNL Facebook Ad Account]. Use `business ID=206617933627973`. Consulte [Adicionar parceiros ao seu Business Manager](https://www.facebook.com/business/help/1717412048538897) na documentação do Facebook para obter detalhes.
   >[!IMPORTANT]
   >
   > Ao configurar as permissões para Adobe Experience Cloud, você deve ativar a permissão **Gerenciar campanha**. Isso é necessário para a integração de [!DNL Adobe Experience Platform].
- Leia e assine os [!DNL Facebook Custom Audiences] Termos de serviço. Para fazer isso, acesse `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, onde `accountID` é a sua [!DNL Facebook Ad Account ID].

### Requisitos de correspondência de ID {#id-matching-requirements}

[!DNL Facebook] requer que nenhuma informação pessoal identificável (PII) seja enviada de forma clara. Portanto, as audiências ativadas para [!DNL Facebook] podem ser desconectadas dos identificadores *hash*, como endereços de email ou números de telefone.

Dependendo do tipo de IDs ingeridas no Adobe Experience Platform, é necessário atender aos requisitos correspondentes.

#### Requisitos de hash do número de telefone {#phone-number-hashing-requirements}

Existem dois métodos para ativar números de telefone em [!DNL Facebook]:

- **Inserindo números** de telefone brutos: você pode assimilar números de telefone brutos no  [!DNL E.164] formato  [!DNL Platform], que serão automaticamente atribuídos a hash na ativação. Se você escolher essa opção, certifique-se de sempre assimilar seus números de telefone brutos na namespace `Phone_E.164`.
- **Assumir números** de telefone com hash: você pode pré-hash de seus números de telefone antes da ingestão para  [!DNL Platform]. Se você escolher essa opção, certifique-se de sempre assimilar seus números de telefone com hash na namespace `Phone_SHA256`.

>[!NOTE]
>
>Os números de telefone ingeridos na namespace `Phone` não podem ser ativados em [!DNL Facebook].


#### Requisitos de hash de email {#email-hashing-requirements}

Você pode optar por hash de endereços de email antes de ingressá-los no Adobe Experience Platform ou pode optar por trabalhar com endereços de email claramente no Experience Platform e fazer com que nosso algoritmo os coloque em hash na ativação.

Para saber mais sobre como ingerir endereços de email no Experience Platform, consulte [visão geral de ingestão em lote](/help/ingestion/batch-ingestion/overview.md) e a [visão geral de ingestão em streaming](/help/ingestion/streaming-ingestion/overview.md).

Se você optar por hash nos endereços de email, certifique-se de cumprir os seguintes requisitos:

- Aparar todos os espaços à esquerda e à direita da string de email; exemplo: `johndoe@example.com`, não `<space>johndoe@example.com<space>`;
- Ao executar o hash das strings de email, certifique-se de executar o hash da string em minúsculas;
   - Exemplo: `example@email.com`, não `EXAMPLE@EMAIL.COM`;
- Certifique-se de que a cadeia de caracteres com hash esteja toda em minúsculas
   - Exemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, não `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- Não salve a corda.

>[!NOTE]
>
>Os dados de namespaces sem hash são automaticamente hash por [!DNL Platform] na ativação.
> Os dados da fonte do atributo não são automaticamente hash. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Aplicar transformação]** para que [!DNL Platform] faça hash automático dos dados na ativação.
> A opção **[!UICONTROL Aplicar transformação]** só é exibida quando você seleciona atributos como campos de origem. Ele não é exibido quando você escolhe namespaces.

![Transformação de mapeamento de identidade](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

#### Usando namespaces personalizadas {#custom-namespaces}

Antes de usar a namespace `Extern_ID` para enviar dados para [!DNL Facebook], certifique-se de sincronizar seus próprios identificadores usando [!DNL Facebook Pixel]. Consulte a [documentação oficial](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) para obter informações detalhadas.

## Conectar ao destino {#connect-destination}

Para se conectar ao destino [!DNL Facebook], consulte [Fluxo de trabalho de autenticação de destinos de rede social](./workflow.md).

## Ativar segmentos para [!DNL Facebook] {#activate-segments}

Para obter instruções sobre como ativar segmentos para [!DNL Facebook], consulte [Ativar dados para destinos](../../ui/activate-destinations.md).

Na etapa **[!UICONTROL Agendamento do segmento]**, você deve fornecer a audiência [!UICONTROL ao enviar segmentos para [!DNL Facebook Custom Audiences].]

![Origem de Audiência do Facebook](../../assets/catalog/social/facebook/facebook-origin-audience.png)

## Dados exportados {#exported-data}

Para [!DNL Facebook], uma ativação bem-sucedida significa que uma [!DNL Facebook] audiência personalizada seria criada programaticamente em [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). A associação de segmento na audiência seria adicionada e removida, pois os usuários são qualificados ou desqualificados para os segmentos ativados.

>[!TIP]
>
>A integração entre o Adobe Experience Platform e [!DNL Facebook] oferece suporte a preenchimentos retroativos históricos de audiência. Todas as qualificações de segmento histórico são enviadas para [!DNL Facebook] quando você ativa os segmentos para o destino.