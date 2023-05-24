---
keywords: Experience Platform;página inicial;tópicos populares;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK
title: Guia da API de fontes de autoatendimento (SDK em lote)
description: Este documento fornece uma visão geral do processo de criação de uma nova origem, incluindo etapas sobre como recuperar, gravar e enviar uma nova especificação de conexão usando a API de Serviço de Fluxo.
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Guia da API de fontes de autoatendimento (SDK em lote)

Este documento fornece uma visão geral do processo de criação de uma nova origem, incluindo etapas sobre como gravar e enviar uma nova especificação de conexão usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes na Platform. O serviço fornece uma interface de usuário e API RESTful que permite configurar conexões de origem com vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar seus sistemas de terceiros, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

A variável [!DNL Flow Service] A API fornece vários endpoints que permitem gerenciar programaticamente as especificações de conexão e fluxo para uma nova fonte que você está integrando por meio de Fontes de autoatendimento (SDK em lote).

## Criar uma nova especificação de conexão

A primeira etapa na configuração de uma nova origem é criar uma nova especificação de conexão.

As especificações de conexão retornam as propriedades do conector de uma origem. Eles incluem especificações de autenticação relacionadas à criação de conexões de base e de origem e uma ID de especificação de conexão fixa que é atribuída a uma origem específica. As especificações de conexão são independentes de locatário e de organização. Uma especificação de conexão típica contém informações básicas sobre uma determinada fonte, bem como três seções distintas: `authSpec`, `sourceSpec`, e `exploreSpec`.

Para obter instruções detalhadas, consulte o guia no [criação de uma nova especificação de conexão](./create.md). Para obter informações sobre as propriedades e os valores usados para uma especificação de conexão, incluindo detalhes sobre a configuração de autenticação, origem e especificações de exploração, consulte [documento de opções de configuração](../config/config.md).

## Atualizar especificações de fluxo

Depois de criar uma especificação de conexão com êxito, você deverá anexar a variável `RestStorageToAEP` especificação de fluxo para permitir que sua origem crie um fluxo de dados.

As especificações de fluxo contêm informações que definem um fluxo, incluindo as IDs de conexão de origem e de destino que ele suporta, as especificações de transformação que precisam ser aplicadas aos dados e os parâmetros de programação necessários para gerar um fluxo.

Para obter instruções detalhadas, consulte o guia no [atualização das especificações de fluxo](./update-flow-specs.md).

## Atualizar a especificação de conexão

Você pode fazer atualizações nas especificações da conexão fazendo uma solicitação PUT para o [!DNL Flow Service] API. Consulte o guia sobre [atualizando suas especificações de conexão](./update-connection-specs.md) para obter mais informações.

## Enviar sua fonte

Para enviar sua origem para integração com o Experience Platform, primeiro complete todo o [!DNL Flow Service] Fluxo de trabalho de API para origens, para garantir que sua origem funcione com êxito. Se a origem for executada com êxito, você poderá continuar e entrar em contato com o representante da Adobe para verificação e promoção. Consulte o guia sobre [testar e enviar sua fonte](./submit.md) para obter mais informações

## Próximas etapas

Para começar a usar o [!DNL Flow Service] e criar uma nova fonte por meio de Fontes de autoatendimento (SDK em lote), leia o [guia de introdução](./getting-started.md) em seguida, selecione um dos manuais de endpoint para saber como usar endpoints específicos.
