---
title: Conexão da Lista de clientes do pinterest
description: Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.
source-git-commit: dc7e43a16923cb17a39a8ddb4ba114c0e9c0cc39
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---


# Conexão da Lista de clientes do pinterest

## Visão geral {#overview}

Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.

>[!IMPORTANT]
>
>Esse destino foi criado pela equipe do Pinterest. Para quaisquer consultas ou pedidos de atualização, contacte-os diretamente em https://help.pinterest.com/en/contact.

## Pré-requisitos {#prerequisites}

* O usuário precisaria se autenticar com uma conta do Pinterest que tenha acesso à conta do anunciante à qual deseja adicionar um público-alvo. Detalhes sobre o compartilhamento de contas de anunciante podem ser encontrados [aqui](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Especificamente, o usuário precisaria dos níveis de acesso de &quot;público-alvo&quot;.
* Detalhes sobre os formatos de identidade da lista de clientes podem ser encontrados [aqui](https://help.pinterest.com/en/business/article/audience-targeting).


## Identidades suportadas {#supported-identities}

O destino Lista de clientes do Pinterest oferece suporte à ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

Na [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do workflow de ativação de destino, mapeie as identidades desejadas para o campo de destino *pinterest_audience*. As identidades são distintas e resolvidas após a assimilação de dados no Pinterest.

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| GAID | ID de publicidade do Google | Mapeie o namespace de identidade de origem *GAID* para o campo de identidade de destino *pinterest_audience*. As identidades são distintas e resolvidas após a assimilação de dados no Pinterest. |
| IDFA | Apple ID para anunciantes | Mapeie o namespace de identidade de origem *IDFA* para o campo de identidade de destino *pinterest_audience*. As identidades são distintas e resolvidas após a assimilação de dados no Pinterest. |
| EMAIL | Endereços de email (texto limpo ou com hash com o algoritmo SHA256) | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. <br> Mapeie o namespace de identidade de origem  ** Email_LC_ *SHA256* para o campo de identidade de destino  *pinterest_audience*. |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportação {#export-type}

**Exportar segmento**  - você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados no destino da Lista de clientes do Pinterest.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando usar o destino Lista de clientes da Pinterest, veja a seguir exemplos de casos de uso que os clientes da Adobe Experience Platform podem resolver usando esse destino.


### Caso de uso nº 1

Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.

## Ligar ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).



### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID]** da conta: Sua ID de conta de publicidade da Pinterest.

## Ativar segmentos para este destino {#activate}

Leia [Ativar perfis e segmentos para os destinos de exportação de segmentos de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte a [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Recursos adicionais {#additional-resources}

Consulte a página [Central de Ajuda do Pinterest](https://help.pinterest.com/en/business/article/audience-targeting) para obter mais informações.