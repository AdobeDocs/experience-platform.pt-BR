---
title: Visão geral do conector de origem do Mixpanel
description: Saiba como conectar o Mixpanel ao Adobe Experience Platform usando APIs ou a interface do usuário.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# [!DNL Mixpanel]

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de um aplicativo de análise de terceiros. O suporte para provedores de análise inclui [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) O é uma ferramenta de análise de produtos que permite capturar dados sobre como os usuários interagem com um produto digital. O Mixpanel permite analisar esses dados de produtos com relatórios simples e interativos que permitem consultar e visualizar os dados com apenas alguns cliques.

Origens aproveitam o [API de exportação de eventos do Mixpanel > Baixar](https://developer.mixpanel.com/reference/raw-event-export) para baixar os dados do evento conforme são recebidos e armazenados no [!DNL Mixpanel], juntamente com todas as propriedades do evento (incluindo `distinct_id`) e o carimbo de data e hora exato em que o evento foi enviado ao Experience Platform. O Mixpanel usa tokens de portador como um mecanismo de autenticação para se comunicar com a API de exportação de eventos do Mixpanel.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Autentique seu [!DNL Mixpanel] account

Esta seção descreve as etapas de pré-requisito a serem concluídas para autenticar sua conta e trazer sua [!DNL Mixpanel] dados para a Platform.

Para criar um [!DNL Mixpanel] conexão de origem e fluxo de dados, você deve primeiro ter um [!DNL Mixpanel] conta. Se você não tiver um [!DNL Mixpanel] conta, consulte o [Registro do Mixpanel](https://mixpanel.com/register/) página para criar sua conta.

Depois de criar um [!DNL Mixpanel] conta, navegue até o [!DNL Project Details] na guia [!DNL Project Seettings] página do [!DNL Mixpanel] Interface para recuperar a ID do projeto e configurar o fuso horário.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Em seguida, navegue até o [!DNL Service Accounts] na guia [!DNL Project Settings] página no [!DNL Mixpanel] Interface para recuperar as credenciais da conta de serviço.

>[!TIP]
>
>Para a prática recomendada, selecione uma conta de serviço que [não expira](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Conta de serviço do Mixpanel](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Por fim, crie uma plataforma [schema](../../../xdm/schema/composition.md) necessário para o [!DNL Mixpanel Event Export API]. Para obter mais informações sobre os mapeamentos necessários para o esquema, consulte o guia em [criação de um [!DNL Mixpanel] conexão de origem na interface](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![Criar esquema](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Conectar [!DNL Mixpanel] para a Platform usando APIs

A documentação abaixo fornece informações sobre como se conectar [!DNL Mixpanel] para a Platform usando APIs ou a interface do usuário:

* [Criar uma conexão de origem e um fluxo de dados para [!DNL Mixpanel] uso da API do Serviço de fluxo](../../tutorials/api/create/analytics/mixpanel.md)

## Conectar [!DNL Mixpanel] para a Platform usando a interface

* [Criar um [!DNL Mixpanel] conexão de origem na interface](../../tutorials/ui/create/analytics/mixpanel.md)
* [Criar um fluxo de dados para uma conexão de origem de sucesso do cliente na interface](../../tutorials/ui/dataflow/analytics.md)
