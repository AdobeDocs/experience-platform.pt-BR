---
title: Conexão Adobe Advertising Cloud DSP
description: O Adobe Advertising Cloud DSP é um destino integrado para a variável [!DNL Adobe Real-time Customer Data Profile], permitindo compartilhar segmentos originais autenticados com anunciantes e usuários aprovados para ativação da campanha.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: 2b8c9d81b7d9eddbbed3119a496e9c8d37e6c415
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Conexão Adobe Advertising Cloud DSP

## Visão geral {#overview}

A Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) o destino permite compartilhar segmentos originais autenticados com anunciantes e usuários aprovados para ativação da campanha com o DSP. Para saber mais sobre a integração do Real-Time CDP com o DSP, consulte [Sobre a ativação de segmentos autenticados de fontes de público-alvo](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Esta página foi criada pela equipe de DSP. Para obter qualquer pergunta ou solicitação de atualização, entre em contato com o suporte da Advertising Cloud diretamente em `adcloud_support@adobe.com`.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando usar o destino do Advertising Cloud DSP, veja a seguir exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso de publicidade da marca

Uma varejista online quer redirecionar seus clientes de alto valor por meio de uma campanha de exibição sem usar cookies para segmentação. O varejista compartilha um segmento que consiste nas IDs de email com hash de seus clientes de alto valor de sua [!DNL Real-Time CDP] à sua conta DSP. DSP então converte as IDs de email com hash para autenticado [!DNL RampIDs] através de uma parceria entre o DSP e o LiveRamp. O resultado [!DNL RampIDs] pode ser usada em uma campanha de exibição para direcionar o público.

### Caso de uso de agência

Uma agência de mídia com uma conta DSP está realizando uma campanha de redefinição de metas em nome de seu cliente, uma marca de destaque no setor de hospitalidade. A marca quer redirecionar todos os seus convidados no ano passado com uma nova oferta promocional. A marca hospeda todas as informações do convidado em [!DNL Real-Time CDP]. A marca pode compartilhar um segmento que consiste nas IDs de email com hash de seus convidados de suas [!DNL Real-Time CDP] conta para a conta DSP da agência de mídia para redirecionar os convidados por meio de uma campanha de mídia.

## Pré-requisitos {#prerequisites}

* DSP configurações de nível de conta e campanha para permitir o compartilhamento de segmentos com a [!DNL LiveRamp RampID], que traduzirá os dados do cliente para o [!DNL RampIDs] para criar segmentos direcionáveis. Sua equipe de conta DSP executará essa configuração.
* A ID de organização do Experience Cloud para a conta do Experience Platform. Você pode encontrar sua ID no [!DNL Real-Time CDP] página de perfil do usuário.
* A [[!DNL Real-Time CDP] origem em DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) para receber segmentos para ativação da campanha. Sua equipe de conta DSP criará a fonte usando a ID de organização do Experience Cloud.
* A chave de origem da conta ou do anunciante do DSP, que é gerada quando um [[!DNL Real-Time CDP] fonte é criada no DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Sua equipe de conta DSP compartilhará essa chave com você. Você o usará no Experience Platform para criar uma conexão de destino com o destino Advertising Cloud DSP, como [explicado abaixo](#authenticate).
* Dados do cliente que consistem em emails com hash ou .

## Identidades suportadas {#supported-identities}

O destino Adobe Advertising Cloud DSP suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Experience Platform oferece suporte a texto sem formatação e a endereços de email com hash SHA256. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** para que o Experience Platform faça o hash automático dos dados na ativação. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela a seguir para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (email ou email com hash) usados no destino do Advertising Cloud DSP. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Quando um perfil é atualizado no Experience Platform com base na avaliação de segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions) para Experience Platform. Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar ao destino, siga as instruções para [criar uma conexão de destino](/help/destinations/ui/connect-destination.md) usando a interface do usuário do Experience Platform. No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para se conectar ao destino, forneça o seguinte parâmetro na função [!UICONTROL Tipo de conexão] e selecione **[!UICONTROL Ligar ao destino]**.:

* **[!UICONTROL Chave de conta ou anunciante]**: Essa [!UICONTROL Chave de Origem] é gerada quando um [[!DNL Real-Time CDP] A origem é criada na interface do usuário do DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Sua equipe de conta DSP compartilhará essa chave com você depois que ela criar a fonte.

![Campo de tipo de conexão](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios na guia [!UICONTROL Detalhes do destino] e selecione **[!UICONTROL Próximo]**.

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.

![Campos de detalhes do destino](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Validar exportação de dados {#exported-data}

Para verificar se o segmento de dados foi compartilhado com o Advertising Cloud, verifique o seguinte:

* O fluxo de dados em [!DNL Real-Time CDP] destino bem-sucedido.

* No DSP, o segmento fica disponível ao criar ou editar um público-alvo do [!UICONTROL Públicos-alvo] > [!UICONTROL Todos os públicos-alvo] ou a partir do [!UICONTROL Direcionamento de público-alvo] seção das configurações de posicionamento. O segmento deve estar visível no [!UICONTROL Adobe Segmentos] na guia [!UICONTROL Real-Time CDP] pasta.

![Segmentos do Real-Time CDP em DSP configurações do público-alvo](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).
