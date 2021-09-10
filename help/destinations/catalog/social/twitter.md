---
title: Conexão de públicos-alvo personalizados do twitter
description: Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform
source-git-commit: 3ea3f9ed156ba3a1fbc790153a4b8fa193d5e2da
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---


# [!DNL Twitter Custom Audiences] conexão

## Visão geral {#overview}

Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Antes de configurar o destino [!DNL Twitter Custom Audiences], verifique os pré-requisitos do Twitter a seguir que você precisa atender.

1. Sua conta [!DNL Twitter Ads] deve estar qualificada para publicidade. Novas contas [!DNL Twitter Ads] não estão qualificadas para publicidade nas primeiras 2 semanas após a sua criação.
2. Sua conta de usuário do Twitter para a qual você autorizou o acesso em [!DNL Twitter Audience Manager] deve ter a permissão *[!DNL Partner Audience Manager]* ativada.


## Identidades suportadas {#supported-identities}

[!DNL Twitter Custom Audiences] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| device_id | IDFA/AdID/Android ID | A ID de anúncio do Google (GAID) e a Apple ID para anunciantes (IDFA) são compatíveis com a Adobe Experience Platform. Mapeie esses namespaces e/ou atributos do esquema de origem de acordo com a [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do fluxo de trabalho de ativação de destino. |
| email | Endereço(s) de email do usuário | Mapeie seus endereços de email de texto simples e seus endereços de email com hash SHA256 para este campo. Quando o campo de origem contém atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para ter [!DNL Platform] hash automaticamente os dados na ativação. Caso envie hash nos endereços de email do cliente antes de carregá-los no Adobe Experience Platform, observe que essas identidades devem ser transformadas em hash usando SHA256, sem sal. |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportação {#export-type}

**Exportar segmentos**  - você está exportando todos os membros de um segmento (público-alvo) com os identificadores usados no destino Públicos-alvo personalizados do Twitter.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Twitter Custom Audiences], aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso nº 1

Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes, ativando seus públicos-alvo criados no Adobe Experience Platform como [!DNL List Custom Audiences] no Twitter.

## Ligar ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID]** da conta: Sua ID  [!DNL Twitter Ads] de conta. Isso pode ser encontrado nas configurações [!DNL Twitter Ads].

## Ativar segmentos para este destino {#activate}

Leia [Ativar perfis e segmentos para os destinos de exportação de segmentos de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte a [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Recursos adicionais {#additional-resources}

Ao mapear segmentos de público-alvo para o Twitter, atenda aos seguintes requisitos de nomenclatura de segmento:

1. Forneça nomes de mapeamento de segmentos legíveis ao ser humano. Recomendamos o uso do mesmo nome usado para os segmentos do Experience Platform.
2. Não use caracteres especiais (+ &amp; , % : ; @ / = ? $) em nomes de mapeamento de segmento e segmento. Se o nome do seu segmento de Experience Platform contém esses caracteres, remova-os antes de mapear o segmento para um destino Twitter.

Mais informações sobre [!DNL List Custom Audiences] no Twitter podem ser encontradas na [documentação do Twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).