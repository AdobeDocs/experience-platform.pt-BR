---
title: LiveRamp - Conexão de distribuição
description: Saiba como usar o LiveRamp - Conector de distribuição para ativar públicos-alvo integrados anteriormente no LiveRamp para outros destinos de publicidade.
hide: true
hidefromtoc: true
source-git-commit: c04c7ff4f1ab45d944f4ab516d7842df536fae40
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 40%

---


# Conexão com o [!DNL LiveRamp - Distribution] {#liveramp-onboarding}

A variável [!DNL LiveRamp - Distribution] conexão permite ativar públicos do Experience Platform para editores premium em mídias móveis, da web, de exibição e de TV conectada.

>[!IMPORTANT]
>
>Esse conector de destino e a página de documentação são criados e mantidos pelo LiveRamp. Para quaisquer consultas ou pedidos de atualização, entre em contato diretamente com o LiveRamp [aqui](mailto:example@email.com).

## Destinos compatíveis {#supported-destinations}

[!DNL LiveRamp - Distribution] O atualmente oferece suporte à ativação de público-alvo para as seguintes plataformas:

* [!DNL 4C Insights]
* [!DNL Acast]
* [!DNL Amobee]
* [!DNL Ampersand.tv]
* [!DNL Captify]
* [!DNL Cardlytics]
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [!DNL iHeartMedia]
* [!DNL Index Exchange]
* [!DNL Magnite CTV Platform]
* [!DNL Magnite DV+ (Rubicon Project)]
* [!DNL One Fox]
* [!DNL Pandora]
* [!DNL Reddit]
* [[!DNL Roku]](#roku)
* [!DNL Spotify]
* [!DNL Taboola]
* [!DNL TargetSpot]
* [!DNL Teads]
* [!DNL WB Discovery]

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL LiveRamp - Distribution] destino, este é um exemplo de caso de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

A equipe de marketing de um varejista de vestuário esportivo usou o [LiveRamp - Integração](liveramp-onboarding.md) conexão para enviar públicos do Experience Platform para sua conta do LiveRamp.

Por meio da [!DNL LiveRamp - Distribution] conexão que agora podem acionar a ativação dos públicos-alvo integrados para os destinos mencionados na parte superior desta página, para que possam direcionar usuários em dispositivos móveis, Web abertos, sociais e [!DNL CTV] plataformas.

## Integração de públicos ao LiveRamp {#onboarding}

Antes de ativar os públicos-alvo por meio da variável [!DNL LiveRamp - Distribution] conexão, use o [LiveRamp - Integração](liveramp-onboarding.md) conexão para exportar seus públicos-alvo do Experience Platform para o LiveRamp.

Depois de ter integrado os públicos-alvo ao LiveRamp, continue o fluxo de trabalho de ativação a partir da [conectar ao destino](#connect) etapa.

## Conectar ao destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_identifier_settings"
>title="Configurações do identificador"
>abstract="Selecione os identificadores compatíveis com seu destino. Consulte a documentação para obter a lista completa dos identificadores compatíveis com cada destino."

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o LiveRamp {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

![Imagem da interface do usuário da Platform mostrando a tela de conexão de destino.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-new-connection.png)

* **[!UICONTROL URL do token]**: o URL do token do LiveRamp.
* **[!UICONTROL ID da organização do LiveRamp]**: a ID da organização da sua conta do LiveRamp.
* **[!UICONTROL Nome de usuário]**: Seu nome de usuário da conta do LiveRamp.
* **[!UICONTROL Senha]**: a senha da sua conta do LiveRamp.

### Configurar detalhes do destino {#destination-details}

Depois de se conectar com sucesso à sua conta do LiveRamp, insira as informações necessárias para se conectar ao destino no qual deseja ativar os públicos-alvo.

![Imagem da interface do usuário da Platform mostrando a tela de detalhes do destino.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-destination-details.png)

* **[!UICONTROL Nome]**: Preencha o nome preferencial para a conexão de destino.
* **[!UICONTROL Descrição]**: digite uma descrição para o destino. Use uma descrição que ajudará você a identificar facilmente a finalidade desse destino.
* **[!UICONTROL Destino]**: use o menu suspenso para selecionar o destino no qual deseja ativar os públicos-alvo. O destino selecionado aqui afeta diretamente o que você vê na [configurações específicas de destino](#destination-settings) tela.
* **[!UICONTROL Integração]**: selecione a conta de integração que deseja usar para o destino.
* **[!UICONTROL Identificador]**: selecione os identificadores compatíveis com seu destino. Atualmente, todos os destinos têm seus identificadores compatíveis preenchidos previamente no menu suspenso.

## Configurações específicas de destino {#destination-settings}

Cada um dos destinos [suportado](#supported-destinations) por [!DNL LiveRamp - Onboarding] exige que você preencha as opções de configuração específicas.

Consulte as seções abaixo para obter orientações detalhadas sobre como configurar cada destino.

### [!DNL 4C Insights] {#insights}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_4cinsights_profile_id"
>title="ID de perfil de marca 4C"
>abstract="Insira a ID numérica associada ao seu Perfil de marca 4C. Se você não tiver essa ID, entre em contato com o representante de serviços do cliente 4C."

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

### [!DNL Acast] {#acast}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_acast_client"
>title="Nome do cliente"
>abstract="O nome da sua conta de anunciante, da forma que você deseja que seja exibido para o parceiro de destino. Use o nome da sua empresa. Não use espaços ou caracteres especiais."

### [!DNL Amobee] {#amobee}

### [!DNL Ampersand.tv] {#ampersand-tv}

### [!DNL Captify] {#captify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_captify_client"
>title="Nome do cliente"
>abstract="O nome da sua conta de anunciante, da forma que você deseja que seja exibido para o parceiro de destino. Use o nome da sua empresa. Não use espaços ou caracteres especiais."

### [!DNL Cardlytics] {#cardlytics}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_cardlytics_client"
>title="Nome do cliente"
>abstract="O nome da sua conta de anunciante, da forma que você deseja que seja exibido para o parceiro de destino. Use o nome da sua empresa. Não use espaços ou caracteres especiais."

### [!DNL Disney (Hulu/ESPN/ABC)] {#disney}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_agreement"
>title="Contrato de termos de destino de dados do anunciante"
>abstract="Digite `I AGREE` para confirmar o reconhecimento e a aceitação dos termos de dados do anunciante Disney."
>additional-url="https://www.disneyadvertising.com/ADVERTISER-DATA-DESTINATION-TERMS/" text="Leia o contrato"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_client"
>title="Nome do cliente"
>abstract="O nome da sua conta de anunciante, da forma que você deseja que seja exibido para o parceiro de destino. Use o nome da sua empresa. Não use espaços ou caracteres especiais."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_email"
>title="Seu endereço de email"
>abstract="Insira um endereço de email vinculado a um indivíduo. Esse endereço de email serve como uma assinatura do contrato de termos de dados do anunciante. Esse endereço de email também será usado para entrar em contato com você, se necessário."

Para configurar detalhes para o destino, preencha os campos abaixo.

![Imagem da interface do usuário da Platform mostrando os campos de dados do cliente para o destino Disney.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-disney-fields.png)

* **[!UICONTROL Contrato de termos de destino de dados do anunciante]**: Digite `I AGREE` para confirmar o reconhecimento e a aceitação dos termos de dados do anunciante da Disney.
* **[!UICONTROL Nome do cliente]**: digite o nome da empresa como deseja que seja exibido ao parceiro de destino.
* **[!UICONTROL Endereço de email]**: insira um endereço de email vinculado a um indivíduo. Esse endereço de email serve como uma assinatura do contrato de termos de dados do anunciante.

### [!DNL iHeartMedia] {#iheartmedia}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_iheartmedia_client"
>title="Nome do cliente"
>abstract="O nome da sua conta de anunciante, da forma que você deseja que seja exibido para o parceiro de destino. Use o nome da sua empresa. Não use espaços ou caracteres especiais."

### [!DNL Index Exchange] {#index-exchange}

### [!DNL Magnite CTV Platform] {#magnite}

### [!DNL Magnite DV+ (Rubicon Project)] {#magnite-dv}

### [!DNL One Fox] {#fox}

### [!DNL Pandora] {#pandora}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_data_provider_name"
>title="Nome do provedor de dados"
>abstract="O nome da sua empresa da forma que você deseja que seja exibido para a Pandora. O nome pode incluir no máximo 40 caracteres minúsculos e alfanuméricos (por exemplo, Minha_Empresa)."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_rep_email"
>title="Endereço de email do(a) representante de conta"
>abstract="O endereço de email do(a) representante de conta Pandora. Esse endereço é usado para enviar atualizações de taxonomia. Para inserir vários endereços, separe-os por vírgulas."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_email"
>title="Endereço de email"
>abstract="Esse endereço é usado para enviar atualizações de taxonomia. Para inserir vários endereços, separe-os por vírgulas."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_account_name"
>title="Nome da conta"
>abstract="O nome da sua conta Pandora. Entre em contato com o(a) representante de conta Pandora, Caso não tenha certeza sobre qual é o nome da sua conta. Não use espaços ou caracteres especiais."

### [!DNL Reddit] {#reddit}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_id"
>title="ID de anunciante do Reddit"
>abstract="Sua ID de anunciante do Reddit. Precisa começar com “t2_” ou “a2_”. Entre em contato com o representante do Reddit caso não saiba sua ID de anunciante."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_name"
>title="Nome de anunciante do Reddit"
>abstract="Seu nome de anunciante do Reddit. Não use espaços ou caracteres especiais."

### Roku {#roku}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_email"
>title="Endereço de email da conta Roku"
>abstract="Insira o endereço de email vinculado à sua conta Roku."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_representative_email"
>title="Endereço de email do(a) representante de conta Roku"
>abstract="Insira o endereço de email do(a) representante de conta Roku. Esse endereço é usado para enviar atualizações de taxonomia. Para inserir vários endereços, separe-os por vírgulas."

Para configurar detalhes para o destino, preencha os campos abaixo.

![Imagem da interface do usuário da plataforma mostrando os identificadores compatíveis com o destino do Roku.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-roku-fields.png)

* **[!UICONTROL Endereço de email da conta do Roku]**: insira o endereço de email vinculado à sua conta Roku.
* **[!UICONTROL Endereço de email do representante de conta Roku]**: digite o endereço de email do representante de conta do Roku. Para inserir vários endereços, separe-os por vírgulas.

### [!DNL Spotify] {#spotify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_client"
>title="Nome do cliente"
>abstract="O nome da sua conta de anunciante, da forma que você deseja que seja exibido para o parceiro de destino. Use o nome da sua empresa. Não use espaços ou caracteres especiais."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_account_token"
>title="Token da conta"
>abstract="Um identificador alfanumérico que informa ao Spotify para onde portar os dados e que você está verificado(a) para usar esse fluxo de trabalho. Entre em contato com o(a) gerente de conta do Spotify para obter esse token."

### [!DNL Taboola] {#taboola}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_rep_email"
>title="Endereço de email do(a) gerente de conta"
>abstract="O endereço de email do(a) gerente de conta da Taboola."

### [!DNL TargetSpot] {#targetspot}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_targetspot_client"
>title="Nome do cliente"
>abstract="O nome da sua conta de anunciante, da forma que você deseja que seja exibido para o parceiro de destino. Use o nome da sua empresa. Não use espaços ou caracteres especiais."

### [!DNL Teads] {#teads}

### [!DNL WB Discovery] {#wb-discovery}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_wb_client"
>title="Nome do cliente"
>abstract="O nome da sua conta de anunciante, da forma que você deseja que seja exibido para o parceiro de destino. Use o nome da sua empresa. Não use espaços ou caracteres especiais."

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, leia o manual no [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

A variável [!DNL LiveRamp - Distribution] A conexão ativa públicos que já foram integrados à sua conta do LiveRamp por meio do [LiveRamp - Integração](liveramp-onboarding.md) conexão.

Para ativar os públicos-alvo com êxito, nesta etapa, selecione o **mesmos públicos-alvo** que você tenha integrado anteriormente ao LiveRamp.

>[!IMPORTANT]
>
>Selecionar públicos que não foram integrados anteriormente no LiveRamp não acionará a integração dos novos públicos.

## Dados exportados / Validar exportação de dados {#exported-data}

Para verificar e monitorar a ativação de seus públicos, faça logon em sua conta do LiveRamp e verifique as métricas de ativação.

Em caso de dúvidas sobre a ativação do público-alvo, entre em contato com o representante de conta do LiveRamp.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

Para obter mais detalhes sobre como configurar [!DNL LiveRamp - Onboarding] armazenamento, consulte a seção [documentação oficial](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
