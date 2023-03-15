---
keywords: Experience Platform;página inicial;tópicos populares;Conector de atributos do cliente
solution: Experience Platform
title: Visão geral do conector de origem de atributos do cliente
description: Saiba como conectar atributos do cliente à Adobe Experience Platform usando APIs ou a interface do usuário
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 8%

---

# Conector de atributos do cliente

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) O no Experience Cloud permite fazer upload dos dados corporativos capturados de um banco de dados do gerenciamento de relacionamento com o cliente (CRM). Você pode fazer upload dos dados em uma fonte de dados de atributo do cliente no Experience Cloud e, em seguida, usar os dados no Adobe Analytics e no Adobe Target.

O Experience Platform fornece suporte para assimilação [!DNL Customer Attributes] dados de perfil no Adobe Experience Platform.

## Conjuntos de dados e esquemas

A variável [!DNL Customer Attributes] A origem cria automaticamente o conjunto de dados para o qual os dados chegam. Este conjunto de dados criado automaticamente é fixo e não pode ser selecionado manualmente. A fonte também cria automaticamente o esquema para o conjunto de dados com base na fonte de dados de entrada. Esse processo também envolve a criação automática dos mapeamentos necessários entre o esquema e os dados de origem.

## Identidades

A identidade principal de um conjunto de dados está contida na primeira coluna do arquivo CSV dos dados de origem. A variável [!DNL Customer Attributes] A origem presume que a identidade é sempre mapeada para o [`CORE` namespace](../../../identity-service/namespaces.md), um namespace gerado pelo sistema que é suportado pela [[!DNL Identity Service]](../../../identity-service/home.md).

Não é possível selecionar um namespace existente para a identidade ao usar [!DNL Customer Attributes] origem porque [!DNL Customer Attributes] O presume que a identidade primária do esquema está sempre no mapa de identidade. [!DNL Customer Attributes] Em seguida, o cria o mapeamento da ID de origem para a UUID do mapa de identidade de maneira automatizada.

Para [!DNL Customer Attributes] dados a serem vinculados a outros [!DNL Profile] conjuntos de dados, seus dados e identidades devem poder corresponder a uma ID de Experience Cloud.

É possível estabelecer a variável `CORE` definindo a ID do Experience Cloud para o visitante usando [SDK da Web](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [SDK móvel](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity)ou a variável [API do serviço de ID do Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR).

A variável [!DNL Customer Attributes] O arquivo não preenche ainda mais nenhuma outra relação de identidade. Por exemplo, se um [!DNL Customer Attributes] o conjunto de dados de origem contém um **E-mail** e uma **ID de fidelidade** , esses campos devem ser rotulados como campos de identidade no esquema para serem processados em [!DNL Identity Service].

Veja o tutorial sobre [criação de um [!DNL Customer Attributes] conexão de origem na interface](../../tutorials/ui/create/adobe-applications/customer-attributes.md) para obter mais informações.
