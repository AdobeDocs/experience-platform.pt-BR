---
keywords: Experience Platform;página inicial;tópicos populares;
title: (Beta) Adobe Workfront Source
description: O Adobe Workfront é um aplicativo de gerenciamento de trabalho de marketing que ajuda você a gerenciar todo o ciclo de vida do trabalho em um único local. O Workfront inclui ferramentas de relatórios e análises que você pode usar para entender e otimizar melhor o fluxo de trabalho na sua organização.
exl-id: ea714278-d84d-4929-9a34-81fc5fb70871
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# (Beta) Fonte do Adobe Workfront

>[!NOTE]
>
>A fonte do Adobe Workfront está na versão beta. Consulte a [Visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

O Adobe Workfront é um aplicativo de gerenciamento de trabalho de marketing que ajuda você a gerenciar todo o ciclo de vida do trabalho em um único local. O Workfront inclui ferramentas de relatórios e análises que você pode usar para entender e otimizar melhor o fluxo de trabalho na sua organização.

A integração do Workfront com o catálogo de fontes do Adobe Experience Platform permite que você traga seus dados do Workfront para o Experience Platform e execute casos de uso como:

* Combine registros de trabalho com dados de terceiros.
* Aplique análises de histórico e de série temporal em registros de trabalho.
* Acessar registros de trabalho por meio de ferramentas de business intelligence de terceiros, como [!DNL PowerBI].
* Consultar dados de trabalho usando SQL padrão.

Os seguintes itens de trabalho e seus atributos correspondentes são qualificados para inclusão no Experience Platform por meio da fonte do Workfront:

* Portfólio
* Programa
* Projeto 
* Tarefa
* Tarefa Operacional (Problemas)
* Usuário

A origem do Workfront transmite todas as novas atualizações para esses atributos e faz o preenchimento retroativo de até um ano de eventos de alteração históricos. Assim que os dados do Workfront estiverem em um conjunto de dados da plataforma, você poderá utilizar [Serviço de consulta](../../../query-service/home.md) e outras ferramentas para analisar mais detalhadamente ou unir seus dados relacionados ao trabalho a outros conjuntos de dados, conforme necessário.

## Conectar o Workfront à Platform usando a interface

Para obter instruções detalhadas sobre como trazer seus dados do Workfront para a Platform, leia o guia em [criação de uma conexão de origem para trazer seus dados do Workfront para a Platform](../../tutorials/ui/create/adobe-applications/workfront.md).
