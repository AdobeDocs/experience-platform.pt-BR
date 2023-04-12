---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
title: Guia da API de Fontes de autoatendimento (SDK em lote)
description: Este documento fornece uma visão geral do processo de criação de uma nova fonte, incluindo etapas sobre como recuperar, gravar e enviar uma nova especificação de conexão usando a API do Serviço de Fluxo.
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Guia da API de Fontes de autoatendimento (SDK em lote)

Este documento fornece uma visão geral do processo de criação de uma nova fonte, incluindo etapas sobre como escrever e enviar uma nova especificação de conexão usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Platform. O serviço fornece uma interface de usuário e uma RESTful API que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar sistemas de terceiros, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

O [!DNL Flow Service] A API fornece vários endpoints que permitem gerenciar programaticamente as especificações de conexão e fluxo para uma nova fonte que você está integrando por meio de Fontes de autoatendimento (SDK em lote).

## Criar uma nova especificação de conexão

A primeira etapa na configuração de uma nova fonte é criar uma nova especificação de conexão.

As especificações de conexão retornam as propriedades do conector de origem. Eles incluem especificações de autenticação relacionadas à criação das conexões base e de origem e uma ID de especificação de conexão fixa que é atribuída a uma fonte específica. As especificações de conexão são independentes de locatários e organizações. Uma especificação de conexão típica contém informações básicas sobre uma determinada fonte, bem como três seções distintas: `authSpec`, `sourceSpec`e `exploreSpec`.

Para obter instruções detalhadas, consulte o guia em [criação de uma nova especificação de conexão](./create.md). Para obter informações sobre as propriedades e valores usados para uma especificação de conexão, incluindo detalhes sobre a configuração de autenticação, origem e especificações de exploração, consulte o [documento de opções de configuração](../config/config.md).

## Atualizar especificações de fluxo

Depois de criar uma especificação de conexão com êxito, você deve anexar a variável `RestStorageToAEP` especificação de fluxo para permitir que sua origem crie um fluxo de dados.

As especificações de fluxo contêm informações que definem um fluxo, incluindo as IDs de conexão de origem e de destino que ele suporta, as especificações de transformação que precisam ser aplicadas aos dados e os parâmetros de agendamento necessários para gerar um fluxo.

Para obter instruções detalhadas, consulte o guia em [atualização das especificações de fluxo](./update-flow-specs.md).

## Atualize suas especificações de conexão

Você pode fazer atualizações na sua especificação de conexão fazendo uma solicitação de PUT para a [!DNL Flow Service] API. Consulte o guia sobre [atualização das especificações de conexão](./update-connection-specs.md) para obter mais informações.

## Enviar sua fonte

Para enviar sua fonte para integração ao Experience Platform, primeiro complete o [!DNL Flow Service] Fluxo de trabalho da API para fontes para garantir que sua fonte funcione com sucesso. Se sua fonte for executada com êxito, você poderá prosseguir e entrar em contato com o representante do Adobe para verificação e promoção. Consulte o guia sobre [testar e enviar sua fonte](./submit.md) para obter mais informações

## Próximas etapas

Para começar a usar o [!DNL Flow Service] API e crie uma nova fonte por meio de Fontes de autoatendimento (SDK em lote), leia a [guia de introdução](./getting-started.md) em seguida, selecione um dos guias de endpoint para saber como usar endpoints específicos.
