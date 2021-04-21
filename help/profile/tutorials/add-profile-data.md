---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API, ativar perfil, Ativar perfil
title: Adicionar dados ao perfil do cliente em tempo real
topic-legacy: tutorial
type: Tutorial
description: Este tutorial descreve as etapas necessárias para adicionar dados ao Perfil do cliente em tempo real.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Adicionar dados a [!DNL Real-time Customer Profile]

Este tutorial descreve as etapas necessárias para adicionar dados a [!DNL Real-time Customer Profile].

## Habilitar um esquema para [!DNL Real-time Customer Profile]

Os dados assimilados em [!DNL Experience Platform] para uso por [!DNL Real-time Customer Profile] devem estar em conformidade com um esquema [!DNL Experience Data Model] (XDM) habilitado para [!DNL Profile]. Para que um schema seja ativado para o Perfil, ele deve implementar a classe [!DNL XDM Individual Profile] ou [!DNL XDM ExperienceEvent].

Você pode habilitar um schema para usar em [!DNL Real-time Customer Profile] usando a API [!DNL Schema Registry] ou a interface do usuário [!DNL Schema Editor]. Para começar, siga os tutoriais para [criar um esquema usando APIs](../../xdm/tutorials/create-schema-api.md) ou [criar um esquema usando a interface do Editor de esquemas](../../xdm/tutorials/create-schema-ui.md).

## Adicionar dados usando a assimilação em lote

Todos os dados carregados em [!DNL Platform] usando a assimilação em lote são carregados em conjuntos de dados individuais. Antes que esses dados possam ser usados por [!DNL Real-time Customer Profile], o conjunto de dados em questão deve ser configurado especificamente. Para obter instruções completas, consulte o tutorial em [configurar um conjunto de dados para o Perfil e o Serviço de identidade](dataset-configuration.md).

Após configurar o conjunto de dados, você pode começar a assimilar dados nele. Consulte o [guia do desenvolvedor de assimilação em lote](../../ingestion/batch-ingestion/api-overview.md) para obter etapas detalhadas sobre como fazer upload de arquivos em diferentes formatos.

## Adicionar dados usando a assimilação de streaming

Todos os dados assimilados de fluxo compatíveis com um esquema XDM habilitado para [!DNL Profile] adicionarão ou substituirão automaticamente o registro apropriado em [!DNL Real-time Customer Profile]. Se mais de uma identidade for fornecida no registro ou se os dados da série forem consumidos, essas identidades serão mapeadas no gráfico de identidade sem configuração adicional. Consulte o [guia do desenvolvedor de assimilação de streaming](../../ingestion/tutorials/streaming-record-data.md) para saber mais.

## Confirme se o upload foi bem-sucedido

Ao fazer upload de dados para um novo conjunto de dados pela primeira vez ou como parte de um processo que envolve um novo ETL ou fonte de dados, é recomendável verificar cuidadosamente os dados para garantir que eles tenham sido carregados corretamente.

Usando a API de acesso [!DNL Real-time Customer Profile], é possível recuperar dados em lote à medida que eles são carregados em um conjunto de dados. Se não conseguir recuperar nenhuma das entidades esperadas, o conjunto de dados pode não estar habilitado para [!DNL Profile]. Depois de confirmar que seu conjunto de dados foi ativado, verifique se o formato e os identificadores de dados de origem são compatíveis com suas expectativas.

Para obter instruções detalhadas sobre como acessar entidades usando a API [!DNL Real-time Customer Profile], consulte o [guia do ponto de extremidade de entidades](../api/entities.md), também conhecido como &quot;[!DNL Profile Access] API&quot;.
