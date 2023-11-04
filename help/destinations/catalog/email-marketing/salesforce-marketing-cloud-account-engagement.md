---
title: Envolvimento da conta de Marketing Cloud do Salesforce
description: Saiba como usar o destino Salesforce Marketing Cloud Account Engagement (antigo Pardot) para exportar os dados da sua conta e ativá-los no Salesforce Marketing Cloud Account Engagement para atender às suas necessidades comerciais.
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1620'
ht-degree: 2%

---

# Conexão com o [!DNL Salesforce Marketing Cloud Account Engagement]

Use o [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(anteriormente conhecido como [!DNL Pardot])* destino para capturar, rastrear, pontuar e classificar leads. Você também pode projetar faixas de clientes potenciais para todos os estágios do pipeline para públicos-alvo de mercado e grupos de clientes por meio de campanhas de queda de email e gerenciamento de clientes potenciais com promoção, pontuação e segmentação de campanha.

Comparado a [!DNL Salesforce Marketing Cloud Engagement] mais orientada para a **B2C** marketing, [!DNL Marketing Cloud Account Engagement] é ideal para **B2B** Casos de uso envolvendo vários departamentos e tomadores de decisão que exigem ciclos de vendas e decisões mais longos. Além disso, você também mantém maior proximidade e integração com seu CRM para tomar as decisões apropriadas de vendas e marketing. *Observe que o Experience Platform também tem conexões para [!DNL Salesforce Marketing Cloud Engagement], você pode verificá-los no [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) e [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) páginas.*

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) endpoint, para **adicionar ou atualizar seus leads** depois de ativá-los em um novo [!DNL Marketing Cloud Account Engagement] segmento.

[!DNL Marketing Cloud Account Engagement] O usa o protocolo OAuth 2 com código de autorização para autenticar no [!DNL Account Engagement] API. Instruções para autenticar em seu [!DNL Marketing Cloud Account Engagement] exemplo, são apresentados mais abaixo, no [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL Marketing Cloud Account Engagement] destino, este é um exemplo de caso de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Enviar emails para contatos de campanhas de marketing {#use-case-send-emails}

O departamento de marketing de uma plataforma online deseja transmitir uma campanha de marketing por email para um público-alvo com curadoria de leads B2B. A equipe de marketing da plataforma pode adicionar novos leads ou atualizar informações de leads existentes por meio do Adobe Experience Platform, criar públicos a partir de seus próprios dados offline e enviar esses públicos para [!DNL Marketing Cloud Account Engagement], que pode ser usado para enviar o email da campanha de marketing.

## Pré-requisitos {#prerequisites}

Consulte as seções abaixo para obter os pré-requisitos que você precisa configurar no Experience Platform e [!DNL Salesforce] e para obter as informações que você precisa coletar antes de trabalhar com a [!DNL Marketing Cloud Account Engagement] destino.

### Pré-requisitos no Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados para o [!DNL Marketing Cloud Account Engagement] destino, você deve ter um [schema](/help/xdm/schema/composition.md), um [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR), e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) criado em [!DNL Experience Platform].

### Pré-requisitos no [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

Observe os seguintes pré-requisitos para exportar dados da Platform para o seu [!DNL Marketing Cloud Account Engagement] conta:

#### Você precisa ter um [!DNL Marketing Cloud Account Engagement] account {#prerequisites-account}

A [!DNL Marketing Cloud Account Engagement] conta com uma assinatura do [Engajamento com a conta do Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) o produto é obrigatório para continuar.

Seu [!DNL Salesforce] a conta deve ter o [!DNL Salesforce] `Account Engagement Administrator role`. Isso é necessário para [criar campos de cliente potencial personalizados](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5).

Por fim, sua conta também deve poder acessar o [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5).

Entre em contato com [[!DNL Salesforce] Suporte](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) ou seu [!DNL Salesforce] administrador da conta, se você não tiver uma conta, ou se a conta não tiver a [!DNL Marketing Cloud Account Engagement] assinatura ou a [!DNL Account Engagement Administrator role].

#### Coletar [!DNL Marketing Cloud Account Engagement] credenciais {#gather-credentials}

Anote os itens abaixo antes de autenticar na [!DNL Marketing Cloud Account Engagement] destino.

| Credencial | Descrição |
| --- | --- |
| `Username` | Seu [!DNL Marketing Cloud Account Engagement] usuário da conta. |
| `Password` | Seu [!DNL Marketing Cloud Account Engagement] senha da conta. |
| `Account Engagement Business Unit ID` | Para encontrar a ID da unidade de negócios Account Engagement, use a Configuração no [!DNL Salesforce]. Em Configuração, insira *Configuração da unidade de negócios* na caixa Localização Rápida. A ID da unidade de negócios Engajamento da conta começa com `0Uv` e tem 18 caracteres. Se você não conseguir acessar as informações de Configuração da Unidade de Negócios, pergunte ao [!DNL Salesforce] Administrador da conta para fornecer a você a `Account Engagement Business Unit ID`. Se precisar de orientação adicional, consulte o [[!DNL Salesforce] Autenticação](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) página de diretrizes. |

{style="table-layout:auto"}

### Medidas de proteção {#guardrails}

Consulte a [!DNL Marketing Cloud Account Engagement] [limites de taxa](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) que detalha os limites impostos pelo seu plano e também se aplicaria às execuções Experience Platform.

>[!IMPORTANT]
>
>Se o seu [!DNL Salesforce] administrador da conta restringiu o acesso a intervalos IP confiáveis, você precisa contatá-los para obter [IPs Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) incluído na lista de permissões. Consulte a [!DNL Salesforce] [Restringir o acesso a intervalos IP confiáveis para um aplicativo conectado](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) se precisar de orientação adicional.

## Identidades suportadas {#supported-identities}

[!DNL Marketing Cloud Account Engagement] O oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| Email | Endereço de email do cliente potencial | Obrigatório |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campo.</li><li> Para cada público selecionado na Platform, a variável correspondente [!DNL Salesforce Marketing Cloud Account Engagement] O status do segmento é atualizado com o status de público-alvo da Platform.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

Dentro de **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, pesquisar [!DNL Salesforce Marketing Cloud Account Engagement]. Como alternativa, você pode localizá-lo na **[!UICONTROL Marketing por email]** categoria.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, selecione **[!UICONTROL Conectar ao destino]**. Você será direcionado para o [!DNL Salesforce] página de logon. Insira seu [!DNL Marketing Cloud Account Engagement] credenciais da conta e selecione [!DNL Log In].

![Captura de tela da interface do usuário da plataforma que mostra como realizar a autenticação para o Envolvimento da conta do Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

Próximo, Selecionar [!UICONTROL Permitir] na janela subsequente para conceder permissões ao **Adobe Experience Platform** aplicativo para acessar seu [!DNL Salesforce Marketing Cloud Account Engagement] conta. *Você precisará fazer isso apenas uma vez*.

![Pop-up de confirmação da captura de tela do aplicativo Salesforce para conceder permissões ao aplicativo Experience Platform acesso ao Envolvimento da conta do Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

Se os detalhes fornecidos forem válidos, a interface exibirá uma mensagem: *Você se conectou com sucesso à conta de Envolvimento da conta do Salesforce Marketing Cloud* e uma **[!UICONTROL Conectado]** com uma marca de seleção verde, você pode prosseguir para a próxima etapa.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório. Consulte a [Coletar [!DNL Marketing Cloud Account Engagement] credenciais](#gather-credentials) para obter orientação.

![Captura de tela da interface do usuário da plataforma mostrando os detalhes do destino.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| Campo | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | Um nome pelo qual você reconhecerá este destino no futuro. |
| **[!UICONTROL Descrição]** | Uma descrição que ajudará você a identificar esse destino no futuro. |
| **[!UICONTROL ID da Unidade de Negócios de Envolvimento da Conta]** | Seu [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Ler [Ativar perfis e públicos para destinos de exportação de público de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente os dados do público-alvo do Adobe Experience Platform para a [!DNL Marketing Cloud Account Engagement] destino, é necessário passar pela etapa de mapeamento de campos. O mapeamento consiste em criar um link entre os campos do esquema do Experience Data Model (XDM) na sua conta da Platform e seus equivalentes correspondentes no destino.

Para mapear corretamente os campos XDM para o [!DNL Marketing Cloud Account Engagement] campos de destino, siga as etapas abaixo.

1. No **[!UICONTROL Mapeamento]** etapa, selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.
1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar atributos]** e selecione o atributo XDM ou escolha o atributo **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade.
1. No **[!UICONTROL Selecionar campo de destino]** escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade ou escolha **[!UICONTROL Selecionar atributos personalizados]** categoria e especifique na lista de [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) do schema disponível.

   * Repita essas etapas para adicionar mapeamentos entre o esquema de perfil XDM e [!DNL Marketing Cloud Account Engagement]: | Campo de origem | Campo de destino | Obrigatório | | — | — | — | |`IdentityMap: Email`|`Identity: email`| Sim | |`xdm: MailingAddress.city`|`xdm: city`| | |`xdm: person.name.firstName`|`Attribute: firstName`| |

   * Um exemplo com os mapeamentos acima é mostrado abaixo:
     ![Exemplo de captura de tela da interface do Platform mostrando os mapeamentos do Target.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

Quando terminar de fornecer os mapeamentos para sua conexão de destino, selecione **[!UICONTROL Próxima]**.

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Navegue até um dos públicos-alvo selecionados. Selecione a guia **[!DNL Activation data]**. A variável **[!UICONTROL ID do mapeamento]** exibe o nome do campo personalizado que é gerado na variável [!DNL Marketing Cloud Account Engagement Prospects] página.
   ![Exemplo de captura de tela da interface do usuário do Platform mostrando a ID de mapeamento para um segmento selecionado.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. Faça logon no [[!DNL Salesforce]](https://login.salesforce.com/) site. Em seguida, navegue até o **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** e verifique se os prospetos do público-alvo foram adicionados/atualizados. Como alternativa, você também pode acessar [[!DNL Salesforce Pardot]](https://pi.pardot.com/) e acesse o **[!DNL Prospects]** página.
   ![Captura de tela da interface do usuário do Salesforce que mostra a página de clientes potenciais.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. Para verificar se os clientes potenciais foram atualizados, selecione um cliente potencial e verifique se o campo personalizado de cliente potencial foi atualizado com o status do público-alvo Experience Platform.
   ![Captura de tela da interface do usuário do Salesforce que mostra a página de cliente potencial selecionada, o campo de cliente potencial personalizado é atualizado com o status do público-alvo.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [Documentação da API](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).
