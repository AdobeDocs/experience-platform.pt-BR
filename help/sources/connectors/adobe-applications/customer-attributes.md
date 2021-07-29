---
keywords: Experience Platform, home, tópicos populares, conector de atributos do cliente
solution: Experience Platform
title: Visão geral do conector de origem dos atributos do cliente
topic-legacy: overview
description: Saiba como conectar atributos do cliente ao Adobe Experience Platform usando APIs ou a interface do usuário
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 541cc87f218a6ef3dcca37573f6d0f9cf560edfb
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Conector de atributos do cliente

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) no Experience Cloud permite fazer upload dos dados corporativos capturados de um banco de dados de gerenciamento de relacionamento com o cliente (CRM). Você pode fazer upload dos dados em uma fonte de dados de Atributo do cliente no Experience Cloud e, em seguida, usar os dados no Adobe Analytics e no Adobe Target.

O Experience Platform fornece suporte para assimilar [!DNL Customer Attributes] dados de perfil no Adobe Experience Platform.

## Conjuntos de dados e esquemas

A fonte [!DNL Customer Attributes] cria automaticamente o conjunto de dados para que os dados chegam. Esse conjunto de dados criado automaticamente é fixo e não pode ser selecionado manualmente. A fonte também cria automaticamente o esquema para o conjunto de dados com base na fonte de dados de entrada. Esse processo também envolve a criação automática dos mapeamentos necessários entre o schema e os dados de origem.

## Identidades

A identidade primária de um conjunto de dados está contida na primeira coluna do arquivo CSV dos dados de origem. A fonte [!DNL Customer Attributes] presume que a identidade esteja sempre mapeada para o namespace [`CORE`](../../../identity-service/namespaces.md), um namespace gerado pelo sistema compatível com [[!DNL Identity Service]](../../../identity-service/home.md).

Não é possível selecionar um namespace existente para a identidade ao usar a fonte [!DNL Customer Attributes] porque [!DNL Customer Attributes] parte do princípio de que a identidade primária do schema está sempre no mapa de identidade. [!DNL Customer Attributes] em seguida, o cria o mapeamento da ID de origem para a UUID do mapa de identidade de maneira automatizada.

Para que os dados [!DNL Customer Attributes] se vinculem a outros conjuntos de dados [!DNL Profile], os dados e identidades devem ser correspondentes a uma ID de Experience Cloud.

Você pode estabelecer o namespace `CORE` definindo a ID do Experience Cloud para o visitante usando [SDK da Web](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [SDK móvel](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity) ou [API do serviço de ID do Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=en).

O arquivo [!DNL Customer Attributes] não preenche mais nenhum outro relacionamento de identidade. Por exemplo, se um conjunto de dados de origem [!DNL Customer Attributes] contiver um **Email** e um campo **Loyalty ID**, esses campos deverão ser rotulados como campos de identidade no esquema para serem processados em [!DNL Identity Service].

Consulte o tutorial em [criar uma conexão de origem [!DNL Customer Attributes] na interface do usuário](../../tutorials/ui/create/adobe-applications/customer-attributes.md) para obter mais informações.
