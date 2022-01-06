---
title: Conexão da Lista de clientes do pinterest
description: Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 90aa0d16851443255dd4828e9f28330a89a12692
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---

# [!DNL Pinterest Customer List] conexão

## Visão geral {#overview}

Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.

>[!IMPORTANT]
>
>Esse destino foi criado pela equipe do Pinterest. Para quaisquer consultas ou pedidos de atualização, contacte-os diretamente em https://help.pinterest.com/en/contact.

## Pré-requisitos {#prerequisites}

* O usuário precisaria se autenticar com uma conta do Pinterest que tenha acesso à conta do anunciante à qual deseja adicionar um público-alvo. Detalhes sobre o compartilhamento de contas de anunciante podem ser encontrados [here](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Especificamente, o usuário precisaria dos níveis de acesso de &quot;público-alvo&quot;.
* Detalhes sobre os formatos de identidade da lista de clientes podem ser encontrados [here](https://help.pinterest.com/en/business/article/audience-targeting).


## Identidades suportadas {#supported-identities}

O [!DNL Pinterest Customer List] O destino oferece suporte à ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

No [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do fluxo de trabalho de ativação de destino, mapeie as identidades desejadas para o campo de destino *pinterest_audience*. As identidades são distintas e resolvidas após a assimilação de dados no Pinterest.

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Mapeie o *GAID* namespace da identidade de origem para o campo de identidade de destino *pinterest_audience*. As identidades são distintas e resolvidas após a assimilação de dados no Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Mapeie o *IDFA* namespace da identidade de origem para o campo de identidade de destino *pinterest_audience*. As identidades são distintas e resolvidas após a assimilação de dados no Pinterest. |
| EMAIL | Endereços de email (texto limpo ou com hash com o algoritmo SHA256) | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. <br> Mapeie o *Email* ou *Email_LC_SHA256* namespace da identidade de origem para o campo de identidade de destino *pinterest_audience*. |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportação {#export-type}

**Exportar segmento** - você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados no destino da Lista de clientes do Pinterest.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar a variável [!DNL Pinterest Customer List] destino, aqui estão casos de uso de exemplo que os clientes do Adobe Experience Platform podem resolver usando esse destino.


### Caso de uso nº 1

Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.

## Ligar ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).


### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID do anunciante]**: Sua ID de anunciante da Pinterest.

## Ativar segmentos para este destino {#activate}

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Recursos adicionais {#additional-resources}

Consulte a [Página da Central de ajuda do pinterest](https://help.pinterest.com/en/business/article/audience-targeting) para obter mais informações.
