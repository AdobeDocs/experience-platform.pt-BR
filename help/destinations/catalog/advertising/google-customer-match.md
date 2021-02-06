---
keywords: correspondência de cliente do Google;Correspondência de cliente do Google;Correspondência de cliente do Google
title: Destino da conexão de correspondência de cliente do Google
description: A Correspondência de clientes do Google permite que você use seus dados online e offline para acessar e se envolver novamente com seus clientes em todas as propriedades operadas e pertencentes ao Google, como Search, Shopping, Gmail e YouTube.
translation-type: tm+mt
source-git-commit: aa2088d30716f56ac2909214badbb39c0ae97855
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 0%

---


# Conexão de correspondência de cliente do Google

>[!IMPORTANT]
>
>A migração do cliente para as novas versões de destino está em andamento. Até a migração ser concluída, você verá somente as identidades disponíveis [!UICONTROL EMAIL] e [!UICONTROL EMAIL_LC_SHA_256] para este destino.

[O Google Customer ](https://support.google.com/google-ads/answer/6379332?hl=en) Matchlets permite que você use seus dados online e offline para alcançar e se envolver novamente com seus clientes em todas as propriedades operadas e pertencentes ao Google, como:  [!DNL Search],  [!DNL Shopping],  [!DNL Gmail]e  [!DNL YouTube].

![Destino de Correspondência de Cliente do Google na interface do usuário CDP em tempo real](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Casos de uso

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Google Customer Match], veja a seguir exemplos de casos de uso que os clientes da Plataforma de dados do cliente em tempo real podem resolver usando esse recurso.

### Caso de uso nº 1

Uma marca de vestuário atlética quer atingir os clientes existentes por meio de [!DNL Google Search] e [!DNL Google Shopping] para personalizar ofertas e itens com base em suas compras passadas e no histórico de navegação. A marca apparel pode assimilar endereços de email de seu próprio CRM para CDP em tempo real, criar segmentos a partir de seus próprios dados offline e enviar esses segmentos para [!DNL Google Customer Match] a serem usados em [!DNL Search] e [!DNL Shopping], otimizando seus gastos com publicidade.

### Caso de uso nº 2

Uma empresa de tecnologia de destaque acabou de lançar um novo telefone. Em um esforço para promover esse novo modelo de telefone, eles estão buscando conscientizar sobre os novos recursos e funcionalidades do telefone para clientes que possuem modelos anteriores de seus telefones.

Para promover a versão, eles carregam endereços de email de seu banco de dados CRM para o CDP em tempo real, usando os endereços de email como identificadores. Os segmentos são criados com base em clientes que possuem modelos de telefone mais antigos e enviados para [!DNL Google Customer Match] para que possam público alvo clientes atuais, clientes que possuem modelos de telefone mais antigos, bem como clientes semelhantes em [!DNL YouTube].

## Especificações de destino {#destination-specs}

### Controle de dados para [!DNL Google Customer Match] destinos {#data-governance}

Os destinos da CDP em tempo real podem ter certas regras e obrigações para os dados enviados para a plataforma de destino ou recebidos dela. Você é responsável por entender as limitações e obrigações dos seus dados e como usa esses dados na Adobe Experience Platform e na plataforma de destino. A Adobe Experience Platform fornece ferramentas de controle de dados para ajudá-lo a gerenciar algumas dessas obrigações de uso de dados. [Saiba ](../../..//data-governance/labels/overview.md) mais sobre as ferramentas e políticas de controle de dados.

### Tipo de exportação e identidades {#export-type}

**Exportação**  de segmento - você está exportando todos os membros de um segmento (audiência) com os identificadores (nome, número de telefone etc.) usado no destino [!DNL Google Customer Match].

**Identidades**  - você pode usar emails brutos ou com hash como IDs de clientes no Google

### [!DNL Google Customer Match] pré-requisitos de conta  {#google-account-prerequisites}

Antes de configurar um destino [!DNL Google Customer Match] no CDP em tempo real, certifique-se de ler e seguir a política do Google para usar [!DNL Customer Match], descrita na [documentação de suporte do Google](https://support.google.com/google-ads/answer/6299717).

### Lista de permissões {#allowlist}

>[!NOTE]
>
>É obrigatório ser adicionado à lista de permissões do Google antes de configurar seu primeiro destino [!DNL Google Customer Match] no CDP em tempo real. Verifique se o processo de lista de permissões descrito abaixo foi concluído pelo Google antes de criar um destino.

Antes de criar o destino [!DNL Google Customer Match] no CDP em tempo real, você deve entrar em contato com o Google e seguir as instruções de lista de permissões em [Usar parceiros de correspondência do cliente para fazer upload dos seus dados](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507) na documentação do Google.

Além disso, há uma segunda lista de permissões do Google na qual você deve adicionar sua conta se estiver planejando carregar dados usando a [User_ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id) do Google. Entre em contato com seu gerente de contas do Google para verificar se você foi adicionado às listas de permissões.

### Requisitos de correspondência de ID {#id-matching-requirements}

[!DNL Google] requer que nenhuma informação pessoal identificável (PII) seja enviada de forma clara. Portanto, as audiências ativadas para [!DNL Google Customer Match] podem ser desconectadas dos identificadores *hash*, como endereços de email ou números de telefone.

Dependendo do tipo de IDs ingeridas no Adobe Experience Platform, é necessário atender aos requisitos correspondentes.

#### Requisitos de hash do número de telefone {#phone-number-hashing-requirements}

Existem dois métodos para ativar números de telefone em [!DNL Google Customer Match]:

* **Inserindo números** de telefone brutos: você pode assimilar números de telefone brutos no  [!DNL E.164] formato  [!DNL Platform], que serão automaticamente atribuídos a hash na ativação. Se você escolher essa opção, certifique-se de sempre assimilar seus números de telefone brutos na namespace `Phone_E.164`.
* **Assumir números** de telefone com hash: você pode pré-hash de seus números de telefone antes da ingestão para  [!DNL Platform]. Se você escolher essa opção, certifique-se de sempre assimilar seus números de telefone com hash na namespace `PHONE_SHA256_E.164`.

>[!NOTE]
>
>Os números de telefone ingeridos na namespace `Phone` não podem ser ativados em [!DNL Google Customer Match].

#### Requisitos de hash de email {#hashing-requirements}

Você pode optar por hash de endereços de email antes de ingressá-los no Adobe Experience Platform ou pode optar por trabalhar com endereços de email claramente no Experience Platform e fazer com que nosso algoritmo os coloque em hash na ativação.

Para obter mais informações sobre os requisitos de hash do Google e outras restrições à ativação, consulte as seguintes seções na documentação do Google:

* [[!DNL Customer Match] com endereço de email, endereço ou ID de usuário](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considerações](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Correspondência do cliente com o número de telefone](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Correspondência do cliente com IDs de dispositivo móvel](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Para saber mais sobre como ingerir endereços de email no Experience Platform, consulte [visão geral de ingestão em lote](../../../ingestion/batch-ingestion/overview.md) e a [visão geral de ingestão em streaming](../../../ingestion/streaming-ingestion/overview.md).

Se você optar por hash nos endereços de email, certifique-se de seguir os requisitos do Google, descritos nos links acima.

#### Usando namespaces personalizadas {#custom-namespaces}

Antes de usar a namespace `User_ID` para enviar dados ao Google, certifique-se de sincronizar seus próprios identificadores usando [!DNL gTag]. Consulte a [documentação oficial](https://support.google.com/google-ads/answer/9199250) para obter informações detalhadas.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

## Conectar ao destino {#connect-destination}

Em **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, vá até a categoria **[!UICONTROL Publicidade]**. Selecione [!DNL Google Customer Match] e selecione **[!UICONTROL Configurar]**.

![Conectar-se ao destino de Correspondência de clientes do Google](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>Se já existir uma conexão com esse destino, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativate]** e **[!UICONTROL Configure]**, consulte a seção [Catalog](../../ui/destinations-workspace.md#catalog) da documentação da área de trabalho de destino.

Na etapa **Account**, se você já tiver configurado uma conexão com o destino [!DNL Google Customer Match], selecione **[!UICONTROL Conta existente]** e selecione a conexão existente. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão com [!DNL Google Customer Match]. Selecione **[!UICONTROL Ligar ao destino]** para iniciar sessão e ligar o Adobe Experience Cloud à sua conta [!DNL Google Ad].

>[!NOTE]
>
>A CDP em tempo real oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas na conta [!DNL Google Ad]. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

![Conectar-se ao destino de Correspondência de clientes do Google - etapa de autenticação](../../assets/catalog/advertising/google-customer-match/connection.png)

Depois que suas credenciais forem confirmadas e o Adobe Experience Cloud estiver conectado à sua conta do Google, você poderá selecionar **[!UICONTROL Próximo]** para prosseguir para a etapa **[!UICONTROL Configuração]**.

![Credenciais confirmadas](../../assets/catalog/advertising/google-customer-match/connection-success.png)

Na etapa **[!UICONTROL Autenticação]**, digite um [!UICONTROL Nome] e um [!UICONTROL Descrição] para o fluxo de ativação e preencha o Google com a [!UICONTROL ID da conta].

Também nesta etapa, você pode selecionar qualquer **[!UICONTROL caso de uso de marketing]** que deve se aplicar a este destino. Os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar de casos de uso de marketing definidos pelo Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte a página [Data Governance em CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) em tempo real. Para obter informações sobre casos individuais de uso de marketing definidos pelo Adobe, consulte [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md#core-actions).

Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

>[!IMPORTANT]
>
> * O caso de uso de marketing **[!UICONTROL Combinar com PII]** está selecionado por padrão para o destino [!DNL Google Customer Match] e não pode ser removido.
> * Para destinos [!DNL Google Customer Match]. **[!UICONTROL A]** ID da conta é a ID do cliente com o Google. O formato da ID é xxx-xxx-xxxx.


![Correspondência de cliente do Connect Google - etapa de autenticação](../../assets/catalog/advertising/google-customer-match/authentication.png)

Seu destino agora é criado. Você pode selecionar **[!UICONTROL Salvar e Sair]** se quiser ativar segmentos posteriormente ou selecionar **[!UICONTROL Próximo]** para continuar o fluxo de trabalho e selecionar segmentos para ativação. Em ambos os casos, consulte a próxima seção, [Ativar segmentos para [!DNL Google Customer Match]](#activate-segments), para o restante do fluxo de trabalho.

## Ativar segmentos para [!DNL Google Customer Match] {#activate-segments}

Para obter instruções sobre como ativar segmentos para [!DNL Google Customer Match], consulte [Ativar dados para destinos](../../ui/activate-destinations.md).


Na etapa **[!UICONTROL Agendamento do segmento]**, você deve fornecer a [!UICONTROL ID do aplicativo] ao enviar os segmentos [!DNL IDFA] ou [!DNL GAID] para [!DNL Google Customer Match].

![ID do aplicativo de correspondência de cliente do Google](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Para obter detalhes sobre como localizar [!DNL App ID], consulte a [documentação oficial](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).







<!-- 
To activate segments to [!DNL Google Customer Match], follow the steps below: 

In **[!UICONTROL Destinations > Browse]**, select the [!DNL Google Customer Match] destination where you want to activate your segments.

Click the name of the destination. This takes you to the Activate flow.

![activate-flow](../../assets/catalog/advertising/google-customer-match/activate-flow.png)

Note that if an activation flow already exists for a destination, you can see the segments that are currently being sent to the destination. Select **[!UICONTROL Edit activation]** in the right rail and follow the steps below to modify the activation details.

Select **[!UICONTROL Activate]**. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to [!DNL Google Customer Match].

![segments-to-destination](../../assets/catalog/advertising/google-customer-match/activate-segments.png)

In the **[!UICONTROL Identity mapping]** step, select which attributes to be included as an identity in this destination. Select **[!UICONTROL Add new mapping]** and browse your schema, select email and/or hashed email, and map them to the corresponding target identity.

![identity mapping initial screen](../../assets/catalog/advertising/google-customer-match/identity-mapping.png) 

**Plain text email address as primary identity**: If you have plain text (unhashed) email addresses as primary identity in your schema, select the email field in your **[!UICONTROL Source Attributes]** and map to the Email field in the right column under **[!UICONTROL Target Identities]**, as shown below:

![select plain text emails identity](../../assets/catalog/advertising/google-customer-match/raw-email.gif) 

**Hashed email address as primary identity**: If you have hashed email addresses as primary identity in your schema, select the hashed email field in your **[!UICONTROL Source Attributes]** and map to the Email_LC_SHA256 field in the right column under **[!UICONTROL Target Identities]**, as shown below:

![select hashed emails identity](../../assets/catalog/advertising/google-customer-match/hashed-emails.gif)

On the **[!UICONTROL Segment schedule]** page, you can set the start date for sending data to the destination.

On the **[!UICONTROL Review]** page, you can see a summary of your selection. Select **[!UICONTROL Cancel]** to break up the flow, **[!UICONTROL Back]** to modify your settings, or **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

>[!IMPORTANT]
>
>In this step, Real-time CDP checks for data usage policy violations. Shown below is an example where a policy is violated. You cannot complete the segment activation workflow until you have resolved the violation. For information on how to resolve policy violations, see [Policy enforcement](../../../rtcdp/privacy/data-governance-overview.md#enforcement) in the data governance documentation section.
 
![confirm-selection](../../assets/common/data-policy-violation.png)

If no policy violations have been detected, select **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

![confirm-selection](../../assets/catalog/advertising/google-customer-match/review.png) -->

## Verifique se a ativação do segmento foi bem-sucedida {#verify-activation}

Após concluir o fluxo de ativação, alterne para sua conta **[!UICONTROL Google Ads]**. Os segmentos ativados serão exibidos em sua conta do Google como listas do cliente. Observe que, dependendo do tamanho do seu segmento, algumas audiências não serão preenchidas a menos que haja mais de 100 usuários ativos para servir.

Ao mapear um segmento para [!DNL IDFA] e [!DNL GAID] IDs móveis, [!DNL Google Customer Match] cria um segmento separado para cada mapeamento de ID. Sua conta [!DNL Google Ads] mostrará dois segmentos diferentes, um para [!DNL IDFA] e outro para o mapeamento [!DNL GAID].

## Recursos adicionais {#additional-resources}

* [Integração da correspondência de clientes do Google - tutorial em vídeo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)