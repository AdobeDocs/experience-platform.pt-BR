---
title: Conexão de públicos-alvo personalizados do twitter
description: Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: c5d2427635d90f3a9551e2a395d01d664005e8bc
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 3%

---

# [!DNL Twitter Custom Audiences] conexão

## Visão geral {#overview}

Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Antes de configurar o [!DNL Twitter Custom Audiences] de destino, verifique os pré-requisitos do Twitter a seguir que você precisa atender.

1. Seu [!DNL Twitter Ads] deve ser elegível para publicidade. Novo [!DNL Twitter Ads] as contas não são elegíveis para publicidade nas primeiras 2 semanas após a sua criação.
2. Sua conta de usuário do Twitter para a qual você autorizou o acesso no [!DNL Twitter Audience Manager] deve ter o *[!DNL Partner Audience Manager]* permissão ativada.


## Identidades suportadas {#supported-identities}

[!DNL Twitter Custom Audiences] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| device_id | IDFA/AdID/Android ID | A Google Advertising ID (GAID) e a Apple ID for Advertisers (IDFA) são compatíveis com o Adobe Experience Platform. Mapeie esses namespaces e/ou atributos do esquema de origem de acordo com a variável [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do fluxo de trabalho de ativação de destino. |
| email | Endereço(s) de email do usuário | Mapeie seus endereços de email de texto simples e seus endereços de email com hash SHA256 para este campo. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. Caso envie hash nos endereços de email do cliente antes de carregá-los no Adobe Experience Platform, observe que essas identidades devem ser transformadas em hash usando SHA256, sem sal. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores usados no destino Públicos-alvo personalizados do Twitter. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar a variável [!DNL Twitter Custom Audiences] destino, aqui estão casos de uso de exemplo que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso nº 1

Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform as [!DNL List Custom Audiences] no Twitter.

## Ligar ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID da conta]**: Seu [!DNL Twitter Ads] ID da conta. Isso pode ser encontrado no [!DNL Twitter Ads] configurações.

## Ativar segmentos para este destino {#activate}

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Recursos adicionais {#additional-resources}

Ao mapear segmentos de público-alvo para o Twitter, atenda aos seguintes requisitos de nomenclatura de segmento:

1. Forneça nomes de mapeamento de segmentos legíveis ao ser humano. Recomendamos o uso do mesmo nome usado para os segmentos do Experience Platform.
2. Não use caracteres especiais (+ &amp; , % : ; @ / = ? $) em nomes de mapeamento de segmento e segmento. Se o nome do seu segmento de Experience Platform contém esses caracteres, remova-os antes de mapear o segmento para um destino Twitter.

Mais informações sobre [!DNL List Custom Audiences] no Twitter , é possível encontrar no [Documentação do twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
