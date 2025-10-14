---
title: Engajamento com a conta do Salesforce Marketing Cloud
description: Saiba como usar o destino Salesforce Marketing Cloud Account Engagement (antigo Pardot) para exportar os dados da sua conta e ativá-los no Salesforce Marketing Cloud Account Engagement para atender às suas necessidades comerciais.
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 2%

---

# [!DNL Salesforce Marketing Cloud Account Engagement] conexão

Use o destino [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(anteriormente conhecido como [!DNL Pardot])* para capturar, rastrear, pontuar e pontuar clientes em potencial. Você também pode projetar faixas de clientes potenciais para todos os estágios do pipeline para públicos-alvo de mercado e grupos de clientes por meio de campanhas de queda de email e gerenciamento de clientes potenciais com promoção, pontuação e segmentação de campanha.

Em comparação ao [!DNL Salesforce Marketing Cloud Engagement], que é mais orientado para o marketing **B2C**, o [!DNL Marketing Cloud Account Engagement] é ideal para casos de uso de **B2B** que envolvem vários departamentos e tomadores de decisão que exigem ciclos de vendas e decisões mais longos. Além disso, você também mantém maior proximidade e integração com seu CRM para tomar as decisões apropriadas de vendas e marketing. *Observação: a Experience Platform também tem conexões para [!DNL Salesforce Marketing Cloud Engagement]. Você pode verificá-las nas páginas [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) e [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md).*

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) aproveita o ponto de extremidade [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) para **adicionar ou atualizar seus clientes potenciais** depois de ativá-los em um novo segmento [!DNL Marketing Cloud Account Engagement].

[!DNL Marketing Cloud Account Engagement] usa o protocolo OAuth 2 com Código de Autorização para autenticar na API [!DNL Account Engagement]. As instruções para autenticar na sua instância do [!DNL Marketing Cloud Account Engagement] estão mais abaixo, na seção [Autenticar no destino](#authenticate).

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Marketing Cloud Account Engagement], veja um exemplo de caso de uso que os clientes da Adobe Experience Platform podem resolver usando esse destino.

### Enviar emails para contatos de campanhas de marketing {#use-case-send-emails}

O departamento de marketing de uma plataforma online deseja transmitir uma campanha de marketing por email para um público-alvo com curadoria de leads B2B. A equipe de marketing da plataforma pode adicionar novos clientes potenciais ou atualizar informações de clientes potenciais existentes por meio do Adobe Experience Platform, criar públicos a partir de seus próprios dados offline e enviar esses públicos para [!DNL Marketing Cloud Account Engagement], que pode ser usado para enviar o email da campanha de marketing.

## Pré-requisitos {#prerequisites}

Consulte as seções abaixo para quaisquer pré-requisitos que você precise configurar no Experience Platform e [!DNL Salesforce] e para obter as informações que você precisa coletar antes de trabalhar com o destino [!DNL Marketing Cloud Account Engagement].

### Pré-requisitos no Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar dados para o destino [!DNL Marketing Cloud Account Engagement], você deve ter um [esquema](/help/xdm/schema/composition.md), um [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR) e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=pt-BR) criados em [!DNL Experience Platform].

### Pré-requisitos em [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

Observe os seguintes pré-requisitos para exportar dados do Experience Platform para sua conta do [!DNL Marketing Cloud Account Engagement]:

#### Você precisa ter uma conta [!DNL Marketing Cloud Account Engagement] {#prerequisites-account}

Uma conta do [!DNL Marketing Cloud Account Engagement] com uma assinatura do produto [Envolvimento da conta da Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) é obrigatória para continuar.

A conta [!DNL Salesforce] deve ter [!DNL Salesforce] `Account Engagement Administrator role`. Isso é necessário para [criar campos de cliente potencial personalizados](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&type=5).

Por fim, sua conta também pode acessar o [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&type=5).

Entre em contato com o [[!DNL Salesforce] Suporte](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) ou com o administrador de conta do [!DNL Salesforce] se você não tiver uma conta, ou se a conta não tiver a assinatura do [!DNL Marketing Cloud Account Engagement] ou o [!DNL Account Engagement Administrator role].

#### Obter credenciais de [!DNL Marketing Cloud Account Engagement] {#gather-credentials}

Anote os itens abaixo antes de autenticar no destino [!DNL Marketing Cloud Account Engagement].

| Credencial | Descrição |
| --- | --- |
| `Username` | Seu nome de usuário da conta [!DNL Marketing Cloud Account Engagement]. |
| `Password` | A senha da sua conta [!DNL Marketing Cloud Account Engagement]. |
| `Account Engagement Business Unit ID` | Para localizar a ID da Unidade de Negócios de Envolvimento da Conta, use a Instalação em [!DNL Salesforce]. Em Configuração, digite *Configuração da Unidade de Negócios* na caixa Localização Rápida. A ID da Unidade de Negócios Envolvimento da Conta começa com `0Uv` e tem 18 caracteres. Se você não puder acessar as informações de Configuração da Unidade de Negócios, peça ao Administrador da Conta [!DNL Salesforce] para fornecer a `Account Engagement Business Unit ID`. Se você precisar de orientação adicional, consulte a página de diretrizes [[!DNL Salesforce] Autenticação](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication). |

{style="table-layout:auto"}

### Medidas de proteção {#guardrails}

Consulte os [!DNL Marketing Cloud Account Engagement] [limites de taxa](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits), que detalham os limites impostos pelo seu plano e também se aplicam às execuções do Experience Platform.

>[!IMPORTANT]
>
>Se o administrador da sua conta do [!DNL Salesforce] tiver restringido o acesso a intervalos IP confiáveis, você precisará contatá-los para obter [IPs do Experience Platform incluir na lista de permissões](/help/destinations/catalog/streaming/ip-address-allow-list.md). Consulte a documentação [!DNL Salesforce] [Restringir Acesso a Intervalos IP Confiáveis para um Aplicativo Conectado](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&type=5) se precisar de orientação adicional.

## Identidades suportadas {#supported-identities}

[!DNL Marketing Cloud Account Engagement] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| Email | Endereço de email do cliente potencial | Obrigatório |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campos.</li><li> Para cada público selecionado no Experience Platform, o status do segmento [!DNL Salesforce Marketing Cloud Account Engagement] correspondente é atualizado com seu status de público do Experience Platform.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

Em **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, procure por [!DNL Salesforce Marketing Cloud Account Engagement]. Como alternativa, você pode localizá-lo na categoria **[!UICONTROL Email marketing]**.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, selecione **[!UICONTROL Conectar ao destino]**. Você será direcionado à página de logon [!DNL Salesforce]. Insira suas credenciais de conta do [!DNL Marketing Cloud Account Engagement] e selecione [!DNL Log In].

![Captura de tela da interface do usuário do Experience Platform mostrando como autenticar para o Envolvimento da Conta da Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

Em seguida, selecione [!UICONTROL Permitir] na janela subsequente para conceder permissões ao aplicativo **Adobe Experience Platform** para acessar sua conta [!DNL Salesforce Marketing Cloud Account Engagement]. *Será necessário fazer isso apenas uma vez*.

![Pop-up de confirmação da captura de tela do aplicativo Salesforce para conceder permissões ao aplicativo Experience Platform para o Envolvimento da Conta do Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

Se os detalhes fornecidos forem válidos, a interface exibirá uma mensagem: *Você se conectou com êxito à mensagem da conta* do Salesforce Marketing Cloud Account Engagement e um status **[!UICONTROL Conectado]** com uma marca de seleção verde, você poderá prosseguir para a próxima etapa.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório. Consulte a seção [Coletar [!DNL Marketing Cloud Account Engagement] credenciais](#gather-credentials) para obter qualquer orientação.

![Captura de tela da interface do Experience Platform mostrando os detalhes do destino.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| Campo | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | Um nome pelo qual você reconhecerá este destino no futuro. |
| **[!UICONTROL Descrição]** | Uma descrição que ajudará você a identificar esse destino no futuro. |
| **[!UICONTROL ID da Unidade de Negócios de Envolvimento da Conta]** | Seu [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e públicos-alvo para destinos de exportação de público-alvo de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente seus dados de público-alvo do Adobe Experience Platform para o destino [!DNL Marketing Cloud Account Engagement], é necessário passar pela etapa de mapeamento de campos. O mapeamento consiste na criação de um link entre os campos do esquema do Experience Data Model (XDM) na sua conta do Experience Platform e seus equivalentes correspondentes no destino.

Para mapear corretamente os campos XDM para os campos de destino [!DNL Marketing Cloud Account Engagement], siga as etapas abaixo.

1. Na etapa **[!UICONTROL Mapeamento]**, selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.
1. Na janela **[!UICONTROL Selecionar campo de origem]**, escolha a categoria **[!UICONTROL Selecionar atributos]** e selecione o atributo XDM ou escolha o **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade.
1. Na janela **[!UICONTROL Selecionar campo de destino]**, escolha o **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade ou escolha a categoria **[!UICONTROL Selecionar atributos personalizados]** e especifique na lista de [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) do esquema disponível.

   * Repita essas etapas para adicionar mapeamentos entre seu esquema de perfil XDM e [!DNL Marketing Cloud Account Engagement]:

     | Campo de origem | Campo de público alvo | Obrigatório |
     | --- | --- | --- |
     | `IdentityMap: Email` | `Identity: email` | Sim |
     | `xdm: MailingAddress.city` | `xdm: city` | |
     | `xdm: person.name.firstName` | `Attribute: firstName` | |

   * Um exemplo com os mapeamentos acima é mostrado abaixo:

     ![Exemplo de captura de tela da interface do Experience Platform mostrando os mapeamentos do Target.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

Quando terminar de fornecer os mapeamentos para sua conexão de destino, selecione **[!UICONTROL Avançar]**.

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Navegue até um dos públicos-alvo selecionados. Selecione a guia **[!DNL Activation data]**. A coluna **[!UICONTROL ID de Mapeamento]** exibe o nome do campo personalizado gerado na página [!DNL Marketing Cloud Account Engagement Prospects].
   ![Exemplo de captura de tela da interface do Experience Platform mostrando a ID de Mapeamento para um segmento selecionado.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. Faça logon no site [[!DNL Salesforce]](https://login.salesforce.com/). Em seguida, navegue até a página **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** e verifique se os prospetos do público-alvo foram adicionados/atualizados. Como alternativa, você também pode acessar [[!DNL Salesforce Pardot]](https://pi.pardot.com/) e acessar a página **[!DNL Prospects]**.
   ![Captura de tela da interface do Salesforce mostrando a página de clientes potenciais.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. Para verificar se os clientes potenciais foram atualizados, selecione um cliente potencial e verifique se o campo personalizado de cliente potencial foi atualizado com o status do público-alvo do Experience Platform.
   ![Captura de tela da interface do Salesforce mostrando a página de cliente potencial selecionada, o campo de cliente potencial personalizado é atualizado com o status do público-alvo.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte a [visão geral da Governança de Dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [Documentação da API](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).
