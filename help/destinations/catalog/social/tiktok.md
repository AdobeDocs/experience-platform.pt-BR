---
title: Conexão TikTok
description: Crie públicos personalizados no TikTok com seus dados para segmentação com suas campanhas de publicidade. Esses públicos-alvo podem ser de pessoas que visitaram seu site ou interagiram com seu conteúdo. Impulsione rapidamente e com segurança o segmento desejado do Adobe Experience Platform para o TikTok usando a integração em tempo real do Adobe com o TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
source-git-commit: 7bfcd0132380f0c847742ff05c1f334542adfba2
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 2%

---


# Conexão TikTok

## Visão geral {#overview}

Crie públicos personalizados no TikTok com seus dados para segmentação com suas campanhas de publicidade. Esses públicos-alvo podem ser de pessoas que visitaram seu site ou interagiram com seu conteúdo. Impulsione rapidamente e com segurança o segmento desejado do Adobe Experience Platform para o TikTok usando a integração em tempo real do Adobe com o TikTok Ads Manager. Visita [TikTok Business Help Center](https://ads.tiktok.com/help/article/audiences?lang=en) para obter mais informações.

>[!IMPORTANT]
>
>Esta página de documentação foi criada pela equipe da TikTok. Para quaisquer consultas ou pedidos de atualização, contacte-os diretamente em [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando usar o destino do TikTok, veja um exemplo de caso de uso para clientes do Adobe Experience Platform.

### Caso de uso {#use-case-1}

Uma marca de vestuário atlético quer alcançar clientes existentes por meio de suas contas de mídia social. A marca de vestuário pode assimilar endereços de email de seu próprio CRM para o Adobe Experience Platform, criar segmentos a partir de seus próprios dados offline e enviar esses segmentos para o TikTok para exibir anúncios nos feeds de mídia social de seus clientes.

## Pré-requisitos {#prerequisites}

Antes de enviar os dados para a [!DNL TikTok Ads Manager] , será necessário conceder permissão ao Adobe Experience Platform para acessar sua conta de anúncio para `Audience Management`. Essa permissão pode ser fornecida ao inserir a ID do anunciante no Experience Platform e seguir o redirecionamento para conceder a permissão. Você pode encontrar mais instruções na seção [Documentação da API do TikTok](https://ads.tiktok.com/marketing_api/docs?id=1738373141733378).

## Identidades suportadas {#supported-identities}

O TikTok oferece suporte à ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| GAID | Google Advertising ID | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando sua identidade de origem for um namespace do IDFA. |
| Número de telefone | Números de telefone com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e números de telefone com hash SHA256, e eles devem estar no formato E.164. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. |
| Email | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados no destino do TikTok. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para autenticar para o destino, você será redirecionado para fazer logon no seu [!DNL TikTok Ads Manager] e autorize o Adobe a gerenciar públicos-alvo em seu nome.

![Seleção de permissão do TikTok](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "Imagem da interface do usuário do TikTok para selecionar permissões")

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Detalhes da conexão de destino](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Imagem da interface do usuário da plataforma, mostrando os detalhes da conexão de destino a serem preenchidos")

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID do gerenciador de anúncios do TikTok]**: Seu [!DNL TikTok Ads Manager ID]. Você pode encontrar isso em seu [!DNL TikTok Ads manager] conta.

![ID do gerenciador de anúncios do TikTok](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "Imagem da interface do usuário do TikTok Ads Manager, mostrando como obter a ID do TikTok Ads Manager")

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Mapear identidades {#map}

Abaixo está um exemplo do mapeamento de identidade correto ao exportar segmentos para o TikTok Ads Manager.

Seleção de campos de origem:

* Selecione um identificador (por exemplo:` Email_LC_SHA256`) como identidade de origem que identifica exclusivamente um perfil no Adobe Experience Platform e [!DNL TikTok Ads Manager].

Seleção de campos de destino:

* Selecione o namespace de email como identidade de destino.

![Mapeamento de identidade](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Imagem da interface do usuário da plataforma, mapeamento de identidades")

## Dados exportados {#exported-data}

Verifique sua [!DNL TikTok Ads Manager] conta (sob **Ativos > Públicos-alvo**) para verificar se o segmento Experience Platform foi exportado com êxito. O público-alvo será preenchido como um tipo de público-alvo: `Partner Audience`.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, leia a [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

Consulte a [Página da Central de ajuda do TikTok](https://ads.tiktok.com/help/article/audiences?lang=en) para obter mais informações.
