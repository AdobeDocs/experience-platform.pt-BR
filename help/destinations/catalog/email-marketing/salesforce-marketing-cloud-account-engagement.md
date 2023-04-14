---
title: Envolvimento da conta do Salesforce Marketing Cloud
description: Saiba como usar o destino do Salesforce Marketing Cloud Account Engagement (anteriormente conhecido como Pardot) para exportar seus dados de conta e ativá-los no Salesforce Marketing Cloud Account Engagement para suas necessidades comerciais.
last-substantial-update: 2023-04-14T00:00:00Z
source-git-commit: 65feb905bfa7d663d1d463d94af428a04dc55b01
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud Account Engagement] conexão

Use o [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(anteriormente conhecido como [!DNL Pardot])* destino para capturar, rastrear, pontuar e classificar leads. Você também pode projetar trilhas de leads para todos os estágios do pipeline para segmentos de mercado e grupos de clientes alvos por meio de campanhas de drip de email e gerenciamento de clientes potenciais com nutrição, pontuação e segmentação de campanha.

Comparado a [!DNL Salesforce Marketing Cloud Engagement] mais orientados para **B2C** marketing, [!DNL Marketing Cloud Account Engagement] é ideal para **B2B** casos de uso envolvendo vários departamentos e tomadores de decisão que exigem ciclos de vendas e decisões mais longos. Além disso, você também mantém uma proximidade e integração mais próximas com seu CRM para tomar as decisões apropriadas de vendas e marketing. *Observe que o Experience Platform também tem conexões para [!DNL Salesforce Marketing Cloud Engagement], você pode verificá-las no [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) e [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) páginas.*

Essa [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) endpoint, para **adicionar ou atualizar seus leads** depois de ativá-los em um novo [!DNL Marketing Cloud Account Engagement] segmento.

[!DNL Marketing Cloud Account Engagement] O usa o protocolo OAuth 2 com Código de Autorização para autenticar no [!DNL Account Engagement] API. Instruções para autenticação em seu [!DNL Marketing Cloud Account Engagement] são mais abaixo, na variável [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar a variável [!DNL Marketing Cloud Account Engagement] destino, aqui está um exemplo de caso de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Enviar emails para contatos para campanhas de marketing {#use-case-send-emails}

O departamento de marketing de uma plataforma online quer transmitir uma campanha de marketing baseada em email para um público com curadoria de leads B2B. A equipe de marketing da plataforma pode adicionar novos leads ou atualizar informações de leads existentes por meio do Adobe Experience Platform, criar segmentos a partir de seus próprios dados offline e enviar esses segmentos para [!DNL Marketing Cloud Account Engagement], que pode ser usada para enviar o email da campanha de marketing.

## Pré-requisitos {#prerequisites}

Consulte as seções abaixo para obter os pré-requisitos que você precisa configurar no Experience Platform e [!DNL Salesforce] e para obter informações que você precisa coletar antes de trabalhar com o [!DNL Marketing Cloud Account Engagement] destino.

### Pré-requisitos no Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados para o [!DNL Marketing Cloud Account Engagement] destino, você deve ter um [schema](/help/xdm/schema/composition.md), a [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) criado em [!DNL Experience Platform].

### Pré-requisitos em [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

Observe os seguintes pré-requisitos para exportar dados do Platform para seu [!DNL Marketing Cloud Account Engagement] conta:

#### Você precisa ter um [!DNL Marketing Cloud Account Engagement] account {#prerequisites-account}

A [!DNL Marketing Cloud Account Engagement] com uma assinatura para a [Envolvimento da conta do Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) produto é obrigatório para prosseguir.

Seu [!DNL Salesforce] deve ter a [!DNL Salesforce] `Account Engagement Administrator role`. Isso é necessário para [criar campos de prospecto personalizados](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5).

Por fim, sua conta também deve poder acessar o [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5).

Entre em contato com o [[!DNL Salesforce] Suporte](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) ou seu [!DNL Salesforce] administrador da conta se você não tiver uma conta ou a conta estiver faltando [!DNL Marketing Cloud Account Engagement] assinatura ou o [!DNL Account Engagement Administrator role].

#### Colete [!DNL Marketing Cloud Account Engagement] credenciais {#gather-credentials}

Anote os itens abaixo antes de autenticar para o [!DNL Marketing Cloud Account Engagement] destino.

| Credencial | Descrição |
| --- | --- |
| `Username` | Seu [!DNL Marketing Cloud Account Engagement] nome de usuário da conta. |
| `Password` | Seu [!DNL Marketing Cloud Account Engagement] senha da conta. |
| `Account Engagement Business Unit ID` | Para encontrar a ID da unidade de negócios do envolvimento da conta, use Configurar em [!DNL Salesforce]. Em Configurar, digite *Configuração da unidade de negócios* na caixa Localização rápida. A ID da unidade de negócios Envolvimento da conta começa com `0Uv` e tem 18 caracteres. Se não conseguir acessar as informações de Configuração da unidade de negócios, pergunte a sua [!DNL Salesforce] Administrador da conta para fornecer `Account Engagement Business Unit ID`. Se você precisar de orientação adicional consulte a [[!DNL Salesforce] Autenticação](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) página de orientação. |

{style="table-layout:auto"}

### Medidas de proteção {#guardrails}

Consulte a [!DNL Marketing Cloud Account Engagement] [limites de taxa](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) que detalha os limites impostos pelo seu plano e também se aplicaria às execuções de Experience Platform.

>[!IMPORTANT]
>
>Se o seu [!DNL Salesforce] o administrador da conta restringiu o acesso a intervalos IP confiáveis, é necessário contatá-los para obter [Experience Platform IP&#39;s](/help/destinations/catalog/streaming/ip-address-allow-list.md) incluir na lista de permissões. Consulte a [!DNL Salesforce] [Restringir o acesso a intervalos IP confiáveis para um aplicativo conectado](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) documentação se precisar de orientação adicional.

## Identidades suportadas {#supported-identities}

[!DNL Marketing Cloud Account Engagement] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| Email | Endereço de E-mail do cliente potencial | Obrigatório |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campo.</li><li> Para cada segmento selecionado na Plataforma, a variável correspondente [!DNL Salesforce Marketing Cloud Account Engagement] o status do segmento é atualizado com o status do segmento da Platform.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

Within **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, pesquisar por [!DNL Salesforce Marketing Cloud Account Engagement]. Como alternativa, você pode localizá-lo sob a variável **[!UICONTROL Marketing por email]** categoria .

### Autenticar para destino {#authenticate}

Para autenticar para o destino, selecione **[!UICONTROL Ligar ao destino]**. Você será navegado até o [!DNL Salesforce] página de logon. Insira seu [!DNL Marketing Cloud Account Engagement] credenciais da conta e selecione [!DNL Log In].

![Captura de tela da interface do usuário da plataforma que mostra como autenticar no Marketing Cloud Account Engagement.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

Em Seguida, Selecione [!UICONTROL Permitir] na janela subsequente para conceder permissões ao **Adobe Experience Platform** para acessar seu [!DNL Salesforce Marketing Cloud Account Engagement] conta. *Você precisará fazer isso apenas uma vez*.

![Pop-up de confirmação de captura de tela do aplicativo Salesforce para conceder permissões ao aplicativo do Experience Platform para o Marketing Cloud Account Engagement.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

Se os detalhes fornecidos forem válidos, a interface do usuário exibirá uma mensagem: *Você se conectou com êxito à conta de Envolvimento da Conta do Marketing Cloud do Salesforce* e uma **[!UICONTROL Conectado]** com uma marca de seleção verde, você pode prosseguir para a próxima etapa.

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório. Consulte a [Colete [!DNL Marketing Cloud Account Engagement] credenciais](#gather-credentials) para quaisquer orientações.

![Captura de tela da interface do usuário da plataforma que mostra os detalhes do destino.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| Campo | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | Um nome pelo qual você reconhecerá esse destino no futuro. |
| **[!UICONTROL Descrição]** | Uma descrição que ajudará a identificar esse destino no futuro. |
| **[!UICONTROL ID da unidade de negócios de envolvimento de conta]** | Seu [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
>
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente os dados de público-alvo do Adobe Experience Platform para a [!DNL Marketing Cloud Account Engagement] , é necessário percorrer a etapa de mapeamento de campo . O mapeamento consiste em criar um link entre os campos do esquema do Modelo de dados de experiência (XDM) na conta da plataforma e os equivalentes correspondentes do destino.

Para mapear corretamente os campos XDM para a variável [!DNL Marketing Cloud Account Engagement] campos de destino, siga as etapas abaixo.

1. No **[!UICONTROL Mapeamento]** etapa , selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.
1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar atributos]** e selecione o atributo XDM ou escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade.
1. No **[!UICONTROL Selecionar campo de destino]** escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade ou escolha **[!UICONTROL Selecionar atributos personalizados]** e especifique na lista de [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) do schema disponível.

   * Repita essas etapas para adicionar mapeamentos entre seu esquema de perfil XDM e [!DNL Marketing Cloud Account Engagement]: | Campo de origem | Campo de destino | Obrigatório | | — | — | — | |`IdentityMap: Email`|`Identity: email`| Sim | |`xdm: MailingAddress.city`|`xdm: city`| | |`xdm: person.name.firstName`|`Attribute: firstName`| |

   * Um exemplo com os mapeamentos acima é mostrado abaixo:
      ![Exemplo de captura de tela da interface do usuário da plataforma que mostra os mapeamentos do Target.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

Quando terminar de fornecer os mapeamentos para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Navegue até um dos segmentos selecionados. Selecione a guia **[!DNL Activation data]**. O **[!UICONTROL ID de mapeamento]** exibe o nome do campo personalizado que é gerado dentro do [!DNL Marketing Cloud Account Engagement Prospects] página.
   ![Exemplo de captura de tela da interface do usuário da plataforma que mostra a ID de mapeamento de um segmento selecionado.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. Faça logon no [[!DNL Salesforce]](https://login.salesforce.com/) site. Em seguida, navegue até o **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** e verificar se os prospetos do segmento foram adicionados/atualizados. Como alternativa, você também pode acessar [[!DNL Salesforce Pardot]](https://pi.pardot.com/) e acesse o **[!DNL Prospects]** página.
   ![Captura de tela da interface do usuário do Salesforce que mostra a página de Perspectivas.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. Para verificar se os prospetos foram atualizados, selecione um prospecto e verifique se o campo de prospecto personalizado foi atualizado com o status de Experience Platform segment .
   ![Captura de tela da interface do usuário do Salesforce que mostra a página de Prospecto selecionada, o campo de prospecto personalizado é atualizado com o status do segmento.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [Documentação da API](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).