---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API;ativar perfil;Ativar perfil
title: Adicionar dados ao Perfil do cliente em tempo real
type: Tutorial
description: Este tutorial descreve as etapas necessárias para adicionar dados ao Perfil do cliente em tempo real.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Adicionar dados a [!DNL Real-Time Customer Profile]

Este tutorial descreve as etapas necessárias para adicionar dados ao [!DNL Real-Time Customer Profile].

## Ativar um esquema para [!DNL Real-Time Customer Profile]

Dados que estão sendo assimilados na [!DNL Experience Platform] para uso de [!DNL Real-Time Customer Profile] deve estar em conformidade com um [!DNL Experience Data Model] Esquema do (XDM) ativado para [!DNL Profile]. Para que um esquema seja ativado para o Perfil, ele deve implementar [!DNL XDM Individual Profile] ou [!DNL XDM ExperienceEvent] classe.

Você pode ativar um esquema para uso no [!DNL Real-Time Customer Profile] usando o [!DNL Schema Registry] API ou a variável [!DNL Schema Editor] interface do usuário. Para começar, siga os tutoriais do [criação de um esquema usando APIs](../../xdm/tutorials/create-schema-api.md) ou [criação de um esquema usando a interface do Editor de esquemas](../../xdm/tutorials/create-schema-ui.md).

## Adicionar dados usando assimilação em lote

Todos os dados carregados no [!DNL Platform] o uso da assimilação em lote é carregado para conjuntos de dados individuais. Antes que esses dados possam ser usados por [!DNL Real-Time Customer Profile], o conjunto de dados em questão deve ser configurado especificamente. Para obter instruções completas, consulte o tutorial em [configurar um conjunto de dados para o Perfil e o Serviço de identidade](dataset-configuration.md).

Após configurar o conjunto de dados, você pode começar a assimilar dados nele. Consulte a [guia do desenvolvedor de assimilação em lote](../../ingestion/batch-ingestion/api-overview.md) para obter etapas detalhadas sobre como fazer upload de arquivos em diferentes formatos.

## Adicionar dados usando assimilação por transmissão

Quaisquer dados assimilados por fluxo compatíveis com um [!DNL Profile]O esquema XDM habilitado para adicionará ou substituirá automaticamente o registro apropriado no [!DNL Real-Time Customer Profile]. Se mais de uma identidade for fornecida no registro ou se os dados de séries temporais forem consumidos, essas identidades serão mapeadas no gráfico de identidade sem configuração adicional. Consulte a [guia do desenvolvedor de assimilação por transmissão](../../ingestion/tutorials/streaming-record-data.md) para saber mais.

## Confirme se o upload foi bem-sucedido

Ao fazer upload de dados para um novo conjunto de dados pela primeira vez ou como parte de um processo que envolve um novo ETL ou fonte de dados, é recomendável verificar cuidadosamente os dados para garantir que tenham sido carregados corretamente.

Usar o [!DNL Real-Time Customer Profile] Acessar a API, é possível recuperar dados em lote à medida que são carregados em um conjunto de dados. Se não conseguir recuperar nenhuma das entidades esperadas, o conjunto de dados pode não estar habilitado para [!DNL Profile]. Depois de confirmar que o conjunto de dados foi ativado, verifique se o formato de dados de origem e os identificadores atendem às suas expectativas.

Para obter instruções detalhadas sobre como acessar entidades usando o [!DNL Real-Time Customer Profile] API, consulte a [manual de endpoint de entidades](../api/entities.md), também conhecido como &quot;[!DNL Profile Access] API&quot;.

## Atualizar dados da Loja de Perfis

Ocasionalmente, pode ser necessário atualizar os dados na Loja de perfis da sua organização. Por exemplo, talvez seja necessário corrigir registros ou alterar um valor de atributo. Isso pode ser feito por meio da assimilação em lote e requer um conjunto de dados habilitado para perfil configurado com uma tag upsert. Para obter mais informações sobre como configurar um conjunto de dados para atualizações de atributo, consulte o tutorial para [ativar um conjunto de dados para Perfil e substituição](../../catalog/datasets/enable-upsert.md).
