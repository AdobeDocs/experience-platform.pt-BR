---
keywords: Experience Platform;página inicial;tópicos populares;Conector de atributos do cliente
solution: Experience Platform
title: Visão geral do conector do Source para atributos do cliente
description: Saiba como conectar atributos do cliente à Adobe Experience Platform usando APIs ou a interface do usuário
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 7%

---

# Conector de atributos do cliente

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=pt-BR) no Experience Cloud permite que você carregue os dados corporativos capturados de um banco de dados do gerenciamento de relacionamento com o cliente (CRM). Você pode fazer upload dos dados em uma fonte de dados de atributo do cliente no Experience Cloud e, em seguida, usar os dados no Adobe Analytics e no Adobe Target.

A Experience Platform oferece suporte para assimilação de dados de perfil do [!DNL Customer Attributes] na Adobe Experience Platform.

## Conjuntos de dados e esquemas

A fonte [!DNL Customer Attributes] cria automaticamente o conjunto de dados para o qual os dados são direcionados. Este conjunto de dados criado automaticamente é fixo e não pode ser selecionado manualmente. A fonte também cria automaticamente o esquema para o conjunto de dados com base na fonte de dados de entrada. Esse processo também envolve a criação automática dos mapeamentos necessários entre o esquema e os dados de origem.

## Identidades

A identidade principal de um conjunto de dados está contida na primeira coluna do arquivo CSV dos dados de origem. A origem [!DNL Customer Attributes] presume que a identidade sempre está mapeada para o namespace [`CORE` &#x200B;](../../../identity-service/features/namespaces.md), um namespace gerado pelo sistema com suporte de [[!DNL Identity Service]](../../../identity-service/home.md).

Não é possível selecionar um namespace existente para a identidade ao usar a origem [!DNL Customer Attributes] porque [!DNL Customer Attributes] presume que a identidade primária para o esquema está sempre no mapa de identidade. [!DNL Customer Attributes] em seguida, cria o mapeamento da ID de origem para a UUID do mapa de identidade de maneira automatizada.

Para que os dados do [!DNL Customer Attributes] sejam vinculados a outros conjuntos de dados do [!DNL Profile], é necessário que os respectivos dados e identidades possam ser vinculados a uma Experience Cloud ID.

É possível estabelecer o namespace `CORE` definindo a Experience Cloud ID para o visitante por meio da [Web SDK](/help/web-sdk/identity/overview.md), do [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/) ou da [API do Serviço Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR).

O arquivo [!DNL Customer Attributes] não preenche mais nenhuma outra relação de identidade. Por exemplo, se um conjunto de dados de origem [!DNL Customer Attributes] contiver um campo **Email** e uma **ID de fidelidade**, esses campos deverão ser rotulados como campos de identidade no esquema para serem processados em [!DNL Identity Service].

Consulte o tutorial sobre [criação de uma [!DNL Customer Attributes] conexão de origem na interface](../../tutorials/ui/create/adobe-applications/customer-attributes.md) para obter mais informações.
