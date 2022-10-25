---
keywords: Experience Platform; home; tópicos populares;
title: (Beta) Origem do Adobe Workfront
description: O Adobe Workfront é um aplicativo de gerenciamento de trabalho de marketing que ajuda você a gerenciar todo o ciclo de vida do trabalho em um único local. O Workfront inclui ferramentas de relatórios e análises que você pode usar para entender melhor e otimizar o fluxo de trabalho em sua organização.
source-git-commit: 1af0863766e29c599e02f2a553d237bc62f455d2
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# (Beta) Fonte da Adobe Workfront

>[!NOTE]
>
>A fonte do Adobe Workfront está em beta. Consulte a [Visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

O Adobe Workfront é um aplicativo de gerenciamento de trabalho de marketing que ajuda você a gerenciar todo o ciclo de vida do trabalho em um único local. O Workfront inclui ferramentas de relatórios e análises que você pode usar para entender melhor e otimizar o fluxo de trabalho em sua organização.

A integração do Workfront com o catálogo de fontes do Adobe Experience Platform permite trazer seus dados do Workfront para o Experience Platform e executar casos de uso como:

* Combine registros de trabalho com dados de terceiros.
* Aplique análises históricas e de séries de tempo em registros de trabalho.
* Acesse registros de trabalho por meio de ferramentas de inteligência empresarial de terceiros, como [!DNL PowerBI].
* Consultar dados de trabalho usando SQL padrão.

Os seguintes itens de trabalho e seus atributos correspondentes são elegíveis para inclusão no Experience Platform por meio da fonte Workfront:

* Portfólio
* Programa
* Projeto
* Tarefa
* Tarefa Operacional (Problemas)
* Usuário

A fonte do Workfront transmite todas as novas atualizações para esses atributos e preenche até um ano dos eventos de alteração do histórico. Assim que seus dados do Workfront estiverem em um conjunto de dados da plataforma, você poderá utilizar [Serviço de query](../../../query-service/home.md) e outras ferramentas para analisar ou unir seus dados relacionados ao trabalho com outros conjuntos de dados, conforme necessário.

## Conectar o Workfront à plataforma usando a interface do usuário

Para obter instruções detalhadas sobre como trazer seus dados do Workfront para a Platform, leia o guia em [criação de uma conexão de origem para trazer seus dados do Workfront para a plataforma](../../tutorials/ui/create/adobe-applications/workfront.md).