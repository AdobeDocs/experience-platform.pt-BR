---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Esquemas e descritores XDM
topic-legacy: tutorial
type: Tutorial
description: A padronização e a interoperabilidade são conceitos-chave por trás do Adobe Experience Platform. O Experience Data Model (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente. Os esquemas são a maneira padrão de descrever dados no Experience Platform, permitindo que todos os dados que estão em conformidade com os esquemas sejam reutilizáveis sem conflitos em uma organização e até mesmo compartilháveis entre várias organizações.
exl-id: 1cdc45d7-57ca-4a2d-99a4-9a8cd885a511
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Trabalhar com esquemas [!DNL Experience Data Model] (XDM) e descritores de relacionamento

A padronização e a interoperabilidade são conceitos-chave por trás do Adobe Experience Platform. [!DNL Experience Data Model] O (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente. Os esquemas são a maneira padrão de descrever dados em [!DNL Experience Platform], permitindo que todos os dados que estão em conformidade com os esquemas sejam reutilizáveis sem conflitos em uma organização e até mesmo compartilháveis entre várias organizações. Para saber mais sobre os esquemas XDM, comece lendo a [Visão geral do sistema XDM](../xdm/home.md).

## Criar um esquema usando o Registro de esquema

O Registro de esquema fornece uma interface de usuário e uma RESTful API da qual é possível visualizar e gerenciar todos os recursos na Biblioteca de esquemas da Adobe Experience Platform. A Biblioteca de Esquemas contém recursos disponibilizados para você pelo Adobe, [!DNL Experience Platform] parceiros e fornecedores cujos aplicativos você usa, bem como recursos que você define e salva no Registro de Esquema. Para saber como criar schemas para sua organização, siga os tutoriais para [criar um schema usando a API do Registro de Schema](../xdm/tutorials/create-schema-api.md) ou [criar um schema usando a interface de usuário do Editor de Schema](../xdm/tutorials/create-schema-ui.md).

## Definir uma relação entre dois esquemas

A capacidade de entender os relacionamentos entre seus clientes e suas interações com a marca em vários canais é uma parte importante do Adobe Experience Platform. Definir esses relacionamentos dentro da estrutura de seus esquemas [!DNL Experience Data Model] (XDM) permite que você obtenha insights complexos sobre os dados do cliente. Esses descritores de relação podem ser definidos usando a API do Registro de Schema e a interface do Editor de Schema. Para obter mais informações, consulte os tutoriais para definir relações entre dois schemas [usando a API](../xdm/tutorials/relationship-api.md) ou [usando a interface do usuário](../xdm/tutorials/relationship-ui.md).

## Criar um esquema ad-hoc

Em circunstâncias específicas, pode ser necessário criar um esquema [!DNL Experience Data Model] (XDM) com campos que são namespacados para uso somente por um único conjunto de dados. Isso é chamado de schema &quot;ad-hoc&quot;. Esquemas ad-hoc são usados em vários [workflows de assimilação de dados](../ingestion/home.md) para [!DNL Experience Platform], incluindo a assimilação de arquivos CSV e a criação de determinados tipos de [conexões de origem](../sources/home.md). A criação de um schema ad hoc é feita usando a API do Registro de Schema e deve ser usada em conjunto com outros tutoriais [!DNL Experience Platform] que exigem a criação de um schema ad hoc como parte de seu fluxo de trabalho. Para começar a criar um schema ad-hoc, consulte o tutorial para [criar um schema ad-hoc usando a API](../xdm/tutorials/ad-hoc.md).

## Próximas etapas

Após definir os esquemas para sua organização, você pode começar a criar conjuntos de dados nos quais os dados podem ser assimilados. Para começar, consulte a seguinte documentação:

* [Visão geral dos conjuntos de dados](../catalog/datasets/overview.md)
* [Visão geral da assimilação de dados](../ingestion/home.md)
