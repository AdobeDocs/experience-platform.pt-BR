---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API;ativar perfil;Ativar perfil
title: Adicionar dados ao Perfil do cliente em tempo real
type: Tutorial
description: Este tutorial descreve as etapas necessárias para adicionar dados ao Perfil do cliente em tempo real.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Adicionar dados a [!DNL Real-Time Customer Profile]

Este tutorial descreve as etapas necessárias para adicionar dados ao [!DNL Real-Time Customer Profile].

## Habilitar um esquema para [!DNL Real-Time Customer Profile]

Os dados assimilados em [!DNL Experience Platform] para uso por [!DNL Real-Time Customer Profile] devem estar em conformidade com um esquema [!DNL Experience Data Model] (XDM) habilitado para [!DNL Profile]. Para que um esquema seja habilitado para o Perfil, ele deve implementar a classe [!DNL XDM Individual Profile] ou [!DNL XDM ExperienceEvent].

Você pode habilitar um esquema para uso em [!DNL Real-Time Customer Profile] usando a API [!DNL Schema Registry] ou a interface do usuário [!DNL Schema Editor]. Para começar, siga os tutoriais de [criação de um esquema usando APIs](../../xdm/tutorials/create-schema-api.md) ou [criação de um esquema usando a interface do Editor de Esquemas](../../xdm/tutorials/create-schema-ui.md).

## Adicionar dados usando assimilação em lote

Todos os dados carregados para [!DNL Experience Platform] usando a assimilação em lote são carregados para conjuntos de dados individuais. Antes que esses dados possam ser usados por [!DNL Real-Time Customer Profile], o conjunto de dados em questão deve ser configurado especificamente. Para obter instruções completas, consulte o tutorial sobre [configuração de um conjunto de dados para o Perfil e o Serviço de Identidade](dataset-configuration.md).

Após configurar o conjunto de dados, você pode começar a assimilar dados nele. Consulte o [guia do desenvolvedor de assimilação em lote](../../ingestion/batch-ingestion/api-overview.md) para obter etapas detalhadas sobre como carregar arquivos em diferentes formatos.

## Adicionar dados usando assimilação por transmissão

Quaisquer dados assimilados por fluxo compatíveis com um esquema XDM habilitado para [!DNL Profile] adicionarão ou substituirão automaticamente o registro apropriado em [!DNL Real-Time Customer Profile]. Se mais de uma identidade for fornecida no registro ou se os dados de séries temporais forem consumidos, essas identidades serão mapeadas no gráfico de identidade sem configuração adicional. Consulte o [guia do desenvolvedor de assimilação de streaming](../../ingestion/tutorials/streaming-record-data.md) para saber mais.

## Confirme se o upload foi bem-sucedido

Ao fazer upload de dados para um novo conjunto de dados pela primeira vez ou como parte de um processo que envolve um novo ETL ou fonte de dados, é recomendável verificar cuidadosamente os dados para garantir que tenham sido carregados corretamente.

Usando a API de Acesso [!DNL Real-Time Customer Profile], você pode recuperar dados em lote conforme eles são carregados em um conjunto de dados. Se você não conseguir recuperar nenhuma das entidades esperadas, seu conjunto de dados pode não estar habilitado para [!DNL Profile]. Depois de confirmar que o conjunto de dados foi ativado, verifique se o formato de dados de origem e os identificadores atendem às suas expectativas.

Para obter instruções detalhadas sobre como acessar entidades usando a API [!DNL Real-Time Customer Profile], consulte o [manual de ponto de extremidade de entidades](../api/entities.md), também conhecido como &quot;[!DNL Profile Access] API&quot;.

## Atualizar dados do repositório de perfis

Ocasionalmente, pode ser necessário atualizar os dados no armazenamento de perfil de sua organização. Por exemplo, talvez seja necessário corrigir registros ou alterar um valor de atributo. Isso pode ser feito por meio da assimilação em lote e requer um conjunto de dados habilitado para perfil configurado com uma tag upsert. Para obter mais informações sobre como configurar um conjunto de dados para atualizações de atributo, consulte o tutorial para [habilitar um conjunto de dados para Perfil e substituição](../../catalog/datasets/enable-upsert.md).
