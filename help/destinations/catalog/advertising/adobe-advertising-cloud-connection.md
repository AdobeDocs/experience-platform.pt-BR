---
title: Conexão com o Adobe Advertising Cloud DSP
description: O Adobe Advertising Cloud DSP é um destino integrado do Adobe Real-time Customer Data Platform, permitindo que você compartilhe segmentos primários autenticados com anunciantes e usuários aprovados para ativação de campanha.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: e67b3a6f9f57a3971a5bfa755db3b1043bebc96b
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 1%

---

# Conexão com o Adobe Advertising Cloud DSP

## Visão geral {#overview}

O ADOBE ADVERTISING CLOUD [!DNL Demand-Side Platform] (DSP) permite compartilhar segmentos primários autenticados com anunciantes e usuários aprovados para ativação de campanha com o DSP. Para saber mais sobre a integração do Real-Time CDP com o DSP, consulte [Sobre a ativação de segmentos autenticados de fontes de público-alvo](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Esta página foi criada pela equipe DSP. Para fazer consultas ou solicitações de atualização, entre em contato diretamente com o suporte da Advertising Cloud em `adcloud_support@adobe.com`.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino do Advertising Cloud DSP, veja a seguir exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso de anúncio de marca

Um varejista online deseja redirecionar seus clientes de alto valor por meio de uma campanha de exibição sem usar cookies para direcionamento. O varejista compartilha um segmento que consiste nas IDs de email com hash de seus clientes de alto valor, desde sua conta do Adobe Real-time Customer Data Platform (Real-Time CDP) até sua conta do DSP. O DSP converte as IDs de email com hash para autenticadas [!DNL RampIDs] por meio de uma parceria entre DSP e LiveRamp. O resultado [!DNL RampIDs] O pode ser usado em uma campanha de exibição para direcionar o público-alvo.

### Caso de uso de agência

Uma agência de mídia com uma conta DSP está realizando uma campanha de redirecionamento em nome de seu cliente, uma marca líder no setor de hotelaria e restauração. A marca quer redirecionar todos os seus convidados no último ano com uma nova oferta promocional. A marca hospeda todas as informações do convidado no [!DNL Real-Time CDP]. A marca pode compartilhar um segmento que consiste nas IDs de email com hash de seus convidados de sua [!DNL Real-Time CDP] para a conta DSP da agência de mídia para redirecionar os convidados por meio de uma campanha de mídia.

## Pré-requisitos {#prerequisites}

* Configurações no nível da conta e no nível da campanha do DSP para permitir o compartilhamento de segmentos com o [!DNL LiveRamp RampID], que traduzirá os dados do cliente para [!DNL RampIDs] para criar segmentos direcionáveis. Sua equipe de conta DSP executará essa configuração. [!DNL RampID] está disponível por meio de uma parceria entre o DSP e a [!DNL LiveRamp]e você não precisa de sua própria [!DNL LiveRamp] associação para usá-lo.
* A ID da organização Experience Cloud para a conta Experience Platform. Você pode encontrar sua ID no seu [!DNL Real-Time CDP] página de perfil do usuário.
* A [[!DNL Real-Time CDP] fonte no DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) para receber segmentos para ativação de campanha. Sua equipe de conta DSP criará a fonte usando sua ID de organização da Experience Cloud.
* A chave de origem da conta ou anunciante do DSP, que é gerada quando um [[!DNL Real-Time CDP] a origem é criada no DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Sua equipe de conta DSP compartilhará essa chave com você. Você o usará no Experience Platform para criar uma conexão de destino com o destino do Advertising Cloud DSP, como [explicado abaixo](#authenticate).
* Dados do cliente que consistem em emails ou emails com hash.

## Identidades suportadas {#supported-identities}

O destino do Adobe Advertising Cloud DSP é compatível com a ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Experience Platform é compatível com texto simples e endereços de email com hash SHA256. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** para que o Experience Platform coloque automaticamente os dados em hash na ativação. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela a seguir para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público) com os identificadores (email ou email com hash) usados no destino do Advertising Cloud DSP. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Quando um perfil é atualizado em Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions) para Experience Platform. Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar ao destino, siga as instruções para [criar uma conexão de destino](/help/destinations/ui/connect-destination.md) usando a interface de usuário do Experience Platform. No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para se conectar ao destino, forneça o seguinte parâmetro no [!UICONTROL Tipo de conexão] e selecione **[!UICONTROL Conectar ao destino]**.:

* **[!UICONTROL Chave da conta ou do anunciante]**: Isso [!UICONTROL Chave de origem] é gerado quando um [[!DNL Real-Time CDP] a origem é criada na interface do usuário do DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Sua equipe de conta do DSP compartilhará essa chave com você após criar a fonte.

![Campo de tipo de conexão](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.

![Campos de detalhes do destino](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmento de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

## Validar exportação de dados {#exported-data}

Para verificar se o segmento de dados foi compartilhado com o Advertising Cloud, verifique o seguinte:

* O fluxo de dados em seu [!DNL Real-Time CDP] destino bem-sucedido.

* No DSP, o segmento fica disponível ao criar ou editar um público-alvo no [!UICONTROL Públicos-alvo] > [!UICONTROL Todos os públicos-alvo] ou dentro de [!UICONTROL Direcionamento de público] seção de configurações de posicionamento. O segmento deve estar visível no [!UICONTROL Segmentos Adobe] na guia [!UICONTROL Real-Time CDP] pasta.

![Segmentos do Real-Time CDP nas configurações de público-alvo do DSP](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).
