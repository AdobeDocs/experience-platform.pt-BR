---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Adicionar dados ao Perfil do cliente em tempo real
topic: tutorial
translation-type: tm+mt
source-git-commit: 93aae0e394e1ea9b6089d01c585a94871863818e
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---


# Adicionar dados ao Perfil do cliente em tempo real

Este tutorial descreve as etapas necessárias para adicionar dados ao Perfil do cliente em tempo real.

## Ative um schema para o Perfil do cliente em tempo real

Os dados sendo ingeridos no Experience Platform para uso pelo Perfil de cliente em tempo real devem estar em conformidade com um schema do Modelo de dados de experiência (XDM) habilitado para Perfil. Para que um schema seja ativado para o Perfil, ele deve implementar o Perfil XDM Individual ou a classe XDM ExperienceEvent.

Você pode ativar um schema para uso no Perfil do cliente em tempo real usando a API do Registro do Schema ou a interface do usuário do Editor de Schemas. Para começar, siga os tutoriais para [criar um schema usando APIs](../../xdm/tutorials/create-schema-api.md) ou [criar um schema usando a interface do usuário](../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas.

## Adicionar dados usando a ingestão em lote

Todos os dados carregados para a Platform usando a ingestão em lote são carregados em conjuntos de dados individuais. Antes que esses dados possam ser usados pelo Perfil do cliente em tempo real, o conjunto de dados em questão deve ser configurado especificamente. Para obter instruções completas, consulte o tutorial sobre como [configurar um conjunto de dados para o Perfil e o Serviço](dataset-configuration.md)de identidade.

Depois que o conjunto de dados for configurado, você poderá start a inserção de dados nele. Consulte o guia [do desenvolvedor de ingestão em](../../ingestion/batch-ingestion/api-overview.md) lote para obter etapas detalhadas sobre como fazer upload de arquivos em diferentes formatos.

## Adicionar dados usando a assimilação de fluxo

Todos os dados ingeridos em fluxo compatíveis com um schema XDM habilitado para Perfis adicionarão ou substituirão automaticamente o registro apropriado no Perfil do cliente em tempo real. Se mais de uma identidade for fornecida no registro, ou se os dados da série cronológica forem consumidos, essas identidades serão mapeadas no gráfico de identidade sem configuração adicional. Consulte o guia [do desenvolvedor de ingestão de](../../ingestion/tutorials/streaming-record-data.md) streaming para saber mais.

## Confirme se o upload foi bem-sucedido

Ao fazer upload de dados para um novo conjunto de dados pela primeira vez, ou como parte de um processo que envolve um novo ETL ou fonte de dados, é recomendável verificar cuidadosamente os dados para garantir que eles tenham sido carregados corretamente.

Usando a API de acesso de Perfil do cliente em tempo real, é possível recuperar dados em lote à medida que eles são carregados em um conjunto de dados. Se você não conseguir recuperar nenhuma das entidades esperadas, seu conjunto de dados pode não estar habilitado para o Perfil. Depois de confirmar que o conjunto de dados foi ativado, verifique se o formato e os identificadores dos dados de origem suportam suas expectativas.

Para obter instruções detalhadas sobre como acessar entidades usando a API de Perfil do cliente em tempo real, consulte o guia [de ponto de extremidade de](../api/entities.md)entidades, também conhecido como &quot;API de acesso ao Perfil&quot;.