---
title: Conexão com o TikTok
description: Crie públicos-alvo personalizados no TikTok com seus dados para direcionar com suas campanhas de publicidade. Esses públicos-alvo podem ser de pessoas que visitaram o site ou interagiram com o conteúdo. Empurre de maneira rápida e segura o público-alvo desejado do Adobe Experience Platform para o TikTok usando a integração em tempo real do Adobe com o TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 2%

---

# Conexão com o TikTok

## Visão geral {#overview}

Crie públicos-alvo personalizados no TikTok com seus dados para direcionar com suas campanhas de publicidade. Esses públicos-alvo podem ser de pessoas que visitaram o site ou interagiram com o conteúdo. Empurre de maneira rápida e segura o público-alvo desejado do Adobe Experience Platform para o TikTok usando a integração em tempo real do Adobe com o TikTok Ads Manager. Visita [Centro de ajuda empresarial da TikTok](https://ads.tiktok.com/help/article/audiences?lang=en) para obter mais informações.

>[!IMPORTANT]
>
>Esta página de documentação foi criada pela equipe do TikTok. Para qualquer consulta ou solicitação de atualização, entre em contato diretamente em [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino do TikTok, este é um exemplo de caso de uso para clientes do Adobe Experience Platform.

### Caso de uso {#use-case-1}

Uma marca de vestuário esportivo quer alcançar clientes existentes por meio de suas contas de mídia social. A marca de vestuário pode assimilar endereços de email de seu próprio CRM para o Adobe Experience Platform, criar públicos a partir de seus próprios dados offline e enviar esses públicos para o TikTok para exibir anúncios nos feeds de redes sociais de seus clientes.

## Pré-requisitos {#prerequisites}

Antes de enviar dados para o seu [!DNL TikTok Ads Manager] conta, será necessário conceder a permissão Adobe Experience Platform para acessar sua conta de anúncio para `Audience Management`. Essa permissão pode ser fornecida inserindo a ID do anunciante no Experience Platform e seguindo o redirecionamento para conceder a permissão. Você pode encontrar mais instruções em [Documentação da API do TikTok](https://ads.tiktok.com/marketing_api/docs?id=1738373141733378).

## Identidades suportadas {#supported-identities}

O TikTok é compatível com a ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| GAID | ID de publicidade do Google | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando a identidade de origem for um namespace do IDFA. |
| Número de telefone | Números de telefone com hash com o algoritmo SHA256 | Os números de telefone com hash SHA256 e texto sem formatação são compatíveis com o Adobe Experience Platform e devem estar no formato E.164. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. |
| Email | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público com os identificadores (nome, número de telefone ou outros) usados no destino do TikTok. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para autenticar no destino, você será redirecionado para fazer logon no [!DNL TikTok Ads Manager] e autorize o Adobe a gerenciar públicos-alvo em seu nome.

![Seleção de permissão do TikTok](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "Imagem da interface do usuário do TikTok para selecionar permissões")

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Detalhes da conexão de destino](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Imagem da interface do usuário da Platform mostrando os detalhes da conexão de destino a serem preenchidos")

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL ID do TikTok Ads Manager]**: Seu [!DNL TikTok Ads Manager ID]. Você pode encontrar isso em seu [!DNL TikTok Ads manager] conta.

![ID do TikTok Ads Manager](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "Imagem da interface do usuário do TikTok Ads Manager, mostrando como obter a ID do TikTok Ads Manager")

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e públicos para destinos de exportação de público de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Mapear identidades {#map}

Veja abaixo um exemplo do mapeamento de identidade correto ao exportar públicos para o TikTok Ads Manager.

Selecionar campos de origem:

* Selecione um identificador (por exemplo:` Email_LC_SHA256`) como identidade de origem que identifica exclusivamente um perfil no Adobe Experience Platform e [!DNL TikTok Ads Manager].

Selecionar campos de destino:

* Selecione o namespace do email como identidade de destino.

![Mapeamento de identidade](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Imagem da interface do usuário da plataforma, mapeamento de identidades")

## Dados exportados {#exported-data}

Verifique o seu [!DNL TikTok Ads Manager] conta (em **Ativos > Públicos**) para verificar se o público-alvo do Experience Platform foi exportado com êxito. O público será preenchido como um tipo de público: `Partner Audience`.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

Consulte a [Página Central de ajuda do TikTok](https://ads.tiktok.com/help/article/audiences?lang=en) para obter informações adicionais.
