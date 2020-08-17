---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;enable profile;Enable profile
solution: Adobe Experience Platform
title: Adicionar dados ao Perfil do cliente em tempo real
topic: tutorial
description: Este tutorial descreve as etapas necessárias para adicionar dados ao Perfil do cliente em tempo real.
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Adicionar dados a [!DNL Real-time Customer Profile]

Este tutorial descreve as etapas necessárias para adicionar dados ao [!DNL Real-time Customer Profile].

## Ativar um schema para [!DNL Real-time Customer Profile]

Os dados sendo ingeridos [!DNL Experience Platform] para uso por [!DNL Real-time Customer Profile] devem estar em conformidade com um schema [!DNL Experience Data Model] (XDM) habilitado para [!DNL Profile]. Para que um schema seja habilitado para Perfil, ele deve implementar a classe [!DNL XDM Individual Profile] ou [!DNL XDM ExperienceEvent] .

Você pode ativar um schema para uso na [!DNL Real-time Customer Profile] API ou na interface do [!DNL Schema Registry] [!DNL Schema Editor] usuário. Para começar, siga os tutoriais para [criar um schema usando APIs](../../xdm/tutorials/create-schema-api.md) ou [criar um schema usando a interface do usuário](../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas.

## Adicionar dados usando a ingestão em lote

Todos os dados carregados para [!DNL Platform] usar a ingestão em lote são carregados em conjuntos de dados individuais. Antes que esses dados possam ser usados por [!DNL Real-time Customer Profile], o conjunto de dados em questão deve ser configurado especificamente. Para obter instruções completas, consulte o tutorial sobre como [configurar um conjunto de dados para o Perfil e o Serviço](dataset-configuration.md)de identidade.

Depois que o conjunto de dados for configurado, você poderá start a inserção de dados nele. Consulte o guia [do desenvolvedor de ingestão em](../../ingestion/batch-ingestion/api-overview.md) lote para obter etapas detalhadas sobre como fazer upload de arquivos em diferentes formatos.

## Adicionar dados usando a assimilação de fluxo

Todos os dados ingeridos em fluxo compatíveis com um schema XDM [!DNL Profile]habilitado adicionarão ou substituirão automaticamente o registro apropriado no [!DNL Real-time Customer Profile]. Se mais de uma identidade for fornecida no registro, ou se os dados da série cronológica forem consumidos, essas identidades serão mapeadas no gráfico de identidade sem configuração adicional. Consulte o guia [do desenvolvedor de ingestão de](../../ingestion/tutorials/streaming-record-data.md) streaming para saber mais.

## Confirme se o upload foi bem-sucedido

Ao fazer upload de dados para um novo conjunto de dados pela primeira vez, ou como parte de um processo que envolve um novo ETL ou fonte de dados, é recomendável verificar cuidadosamente os dados para garantir que eles tenham sido carregados corretamente.

Usando a API [!DNL Real-time Customer Profile] de acesso, é possível recuperar dados em lote à medida que eles são carregados em um conjunto de dados. Se você não conseguir recuperar nenhuma das entidades esperadas, seu conjunto de dados pode não estar habilitado para [!DNL Profile]. Depois de confirmar que o conjunto de dados foi ativado, verifique se o formato e os identificadores dos dados de origem suportam suas expectativas.

Para obter instruções detalhadas sobre como acessar entidades usando a [!DNL Real-time Customer Profile] API, consulte o guia [de ponto de extremidade de](../api/entities.md)entidades, também conhecido como &quot;[!DNL Profile Access] API&quot;.