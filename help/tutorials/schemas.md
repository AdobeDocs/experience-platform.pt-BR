---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: schemas e descritores XDM
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# Trabalhar com schemas do Modelo de Dados de Experiência (XDM) e descritores de relacionamento

A padronização e a interoperabilidade são conceitos-chave por trás da Adobe Experience Platform. O Experience Data Model (XDM), desenvolvido pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente. Os Schemas são a forma padrão de descrever dados na plataforma da experiência, permitindo que todos os dados que estão em conformidade com os schemas sejam reutilizáveis sem conflitos em uma organização e até mesmo compartilháveis entre várias organizações. Para saber mais sobre os schemas XDM, start lendo a visão geral [do sistema](../xdm/home.md)XDM.

## Criar um schema usando o Registro do Schema

O Registro de Schemas fornece uma interface de usuário e uma RESTful API da qual você pode visualização e gerenciar todos os recursos na Biblioteca de Schemas da plataforma Adobe Experience. A Biblioteca de Schemas contém recursos disponibilizados pela Adobe, parceiros da plataforma de experiência e fornecedores cujos aplicativos você usa, bem como recursos que você define e salva no Registro de Schemas. Para saber como criar schemas para sua organização, siga os tutoriais para [criar um schema usando a API](../xdm/tutorials/create-schema-api.md) do Registro do Schema ou [criando um schema usando a interface](../xdm/tutorials/create-schema-ui.md)do usuário do Editor de Schemas.

## Definir uma relação entre dois schemas

A capacidade de entender as relações entre seus clientes e suas interações com a sua marca em vários canais é uma parte importante da plataforma Adobe Experience. A definição desses relacionamentos na estrutura dos schemas do Modelo de Dados de Experiência (XDM) permite que você obtenha insights complexos sobre os dados do cliente. Esses descritores de relação podem ser definidos usando a API de Registro do Schema e a interface do editor do Schema. Para obter mais informações, consulte os tutoriais para definir relações entre dois schemas [usando a API](../xdm/tutorials/relationship-api.md) ou [usando a interface do usuário](../xdm/tutorials/relationship-ui.md).

## Criar um schema ad-hoc

Em circunstâncias específicas, pode ser necessário criar um schema do Modelo de Dados de Experiência (XDM) com campos que são namespacados para uso somente por um único conjunto de dados. Isso é conhecido como um schema &quot;ad-hoc&quot;. schemas Ad-hoc são usados em vários workflows de ingestão [de](../ingestion/home.md) dados para a Experience Platform, incluindo a assimilação de arquivos CSV e a criação de certos tipos de conexões [de](../source-connectors/home.md)origem. A criação de um schema ad-hoc é feita usando a API do Registro do Schema e deve ser usada em conjunto com outros tutoriais da Plataforma de experiência que exigem a criação de um schema ad-hoc como parte de seu fluxo de trabalho. Para começar a criar um schema ad-hoc, consulte o tutorial para [criar um schema ad-hoc usando a API](../xdm/tutorials/ad-hoc.md).

## Próximas etapas

Depois de definir schemas para sua organização, você pode começar a criar conjuntos de dados nos quais os dados podem ser assimilados. Para começar, consulte a seguinte documentação:

* [Visão geral dos conjuntos de dados](../catalog/datasets/overview.md)
* [Visão geral da ingestão de dados](../ingestion/home.md)