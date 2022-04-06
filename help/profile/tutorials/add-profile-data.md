---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API, ativar perfil, Ativar perfil
title: Adicionar dados ao perfil do cliente em tempo real
topic-legacy: tutorial
type: Tutorial
description: Este tutorial descreve as etapas necessárias para adicionar dados ao Perfil do cliente em tempo real.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 9f00bff31f9e7d2da1294d3d1f24cba7870a4614
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Adicionar dados a [!DNL Real-time Customer Profile]

Este tutorial descreve as etapas necessárias para adicionar dados a [!DNL Real-time Customer Profile].

## Habilitar um esquema para [!DNL Real-time Customer Profile]

Dados sendo assimilados em [!DNL Experience Platform] para utilização por [!DNL Real-time Customer Profile] deve estar em conformidade com uma [!DNL Experience Data Model] esquema (XDM) que está ativado para [!DNL Profile]. Para que um esquema seja ativado para o Perfil, ele deve implementar a variável [!DNL XDM Individual Profile] ou [!DNL XDM ExperienceEvent] classe .

Você pode ativar um esquema para usar em [!DNL Real-time Customer Profile] usando o [!DNL Schema Registry] API ou [!DNL Schema Editor] interface do usuário. Para começar, siga os tutoriais para [criação de um schema usando APIs](../../xdm/tutorials/create-schema-api.md) ou [criação de um esquema usando a interface do usuário do Editor de esquemas](../../xdm/tutorials/create-schema-ui.md).

## Adicionar dados usando a assimilação em lote

Todos os dados carregados no [!DNL Platform] o uso da assimilação em lote é carregado em conjuntos de dados individuais. Antes que esses dados possam ser usados por [!DNL Real-time Customer Profile], o conjunto de dados em questão deve ser configurado especificamente. Para obter instruções completas, consulte o tutorial em [configuração de um conjunto de dados para Perfil e serviço de identidade](dataset-configuration.md).

Após configurar o conjunto de dados, você pode começar a assimilar dados nele. Consulte a [guia do desenvolvedor de ingestão em lote](../../ingestion/batch-ingestion/api-overview.md) para obter etapas detalhadas sobre como fazer upload de arquivos em diferentes formatos.

## Adicionar dados usando a assimilação de streaming

Qualquer dado assimilado por fluxo compatível com um [!DNL Profile]O esquema XDM habilitado para o -enabled adicionará ou substituirá automaticamente o registro apropriado em [!DNL Real-time Customer Profile]. Se mais de uma identidade for fornecida no registro ou se os dados da série forem consumidos, essas identidades serão mapeadas no gráfico de identidade sem configuração adicional. Consulte a [guia do desenvolvedor de assimilação de streaming](../../ingestion/tutorials/streaming-record-data.md) para saber mais.

## Confirme se o upload foi bem-sucedido

Ao fazer upload de dados para um novo conjunto de dados pela primeira vez ou como parte de um processo que envolve um novo ETL ou fonte de dados, é recomendável verificar cuidadosamente os dados para garantir que eles tenham sido carregados corretamente.

Usar o [!DNL Real-time Customer Profile] Para acessar a API, é possível recuperar dados em lote à medida que eles são carregados em um conjunto de dados. Se não conseguir recuperar nenhuma das entidades esperadas, o conjunto de dados talvez não esteja habilitado para [!DNL Profile]. Depois de confirmar que seu conjunto de dados foi ativado, verifique se o formato e os identificadores de dados de origem são compatíveis com suas expectativas.

Para obter instruções detalhadas sobre como acessar entidades usando o [!DNL Real-time Customer Profile] Consulte a API [guia do endpoint de entidades](../api/entities.md), também conhecido como &quot;[!DNL Profile Access] API&quot;.

## Atualizar dados do armazenamento de perfis

Ocasionalmente, pode ser necessário atualizar os dados na Loja de perfis de sua organização. Por exemplo, talvez seja necessário corrigir registros ou alterar um valor de atributo. Isso pode ser feito por meio da assimilação em lote e requer um conjunto de dados habilitado para perfil configurado com uma tag de atualização. Para obter mais informações sobre como configurar um conjunto de dados para atualizações de atributos, consulte o tutorial para [ativação de um conjunto de dados para Perfil e Reformulação](../../catalog/datasets/enable-upsert.md).
