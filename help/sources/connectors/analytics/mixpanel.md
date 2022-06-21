---
keywords: Experience Platform; home; tópicos populares;
title: (Beta) Visão geral do conector de origem do Mixpanel
description: Saiba como conectar o Mixpanel ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: e44f6d5bb2fd891a3e3b3c5e4aed68e8d4687b53
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# (Beta) [!DNL Mixpanel]

>[!NOTE]
>
>O [!DNL Mixpanel] A fonte está em beta. Consulte a [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilar dados de um aplicativo analítico de terceiros. O suporte para provedores de análise inclui [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) O é uma ferramenta de análise de produto que permite capturar dados sobre como os usuários interagem com um produto digital. O Mixpanel permite analisar esses dados do produto com relatórios simples e interativos que permitem consultar e visualizar os dados com apenas alguns cliques.

As Fontes usam o [API de exportação de eventos do Mixpanel > Download](https://developer.mixpanel.com/reference/raw-event-export) para baixar os dados do evento à medida que são recebidos e armazenados em [!DNL Mixpanel], juntamente com todas as propriedades do evento (incluindo `distinct_id`) e o carimbo de data e hora exato em que o evento foi enviado para o Experience Platform. O Mixpanel usa tokens do portador como um mecanismo de autenticação para se comunicar com a API de exportação de eventos do Mixpanel.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Autentique seu [!DNL Mixpanel] account

Esta seção descreve as etapas de pré-requisito a serem concluídas para autenticar sua conta e trazer sua conta [!DNL Mixpanel] para a plataforma.

Para criar um [!DNL Mixpanel] conexão de origem e fluxo de dados, primeiro você deve ter um [!DNL Mixpanel] conta. Se você não tiver um [!DNL Mixpanel] consulte a [Registro de painel misto](https://mixpanel.com/register/) para criar sua conta.

Depois de criar uma [!DNL Mixpanel] , navegue até a [!DNL Project Details] na guia no [!DNL Project Seettings] da página [!DNL Mixpanel] Interface do usuário para recuperar a ID do projeto e configurar o fuso horário.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Em seguida, navegue até o [!DNL Service Accounts] na guia no [!DNL Project Settings] na página [!DNL Mixpanel] IU para recuperar as credenciais da conta de serviço.

>[!TIP]
>
>Para práticas recomendadas, selecione uma conta de serviço que [não expira](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Conta do Serviço Mixpanel](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Por fim, crie uma plataforma [schema](../../../xdm/schema/composition.md) para [!DNL Mixpanel Event Export API]. Para obter mais informações sobre os mapeamentos necessários para o esquema, consulte o guia em [criar um [!DNL Mixpanel] conexão de origem na interface do usuário](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![Criar esquema](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Connect [!DNL Mixpanel] para Plataforma usando APIs

A documentação abaixo fornece informações sobre como se conectar [!DNL Mixpanel] para Plataforma usando APIs ou a interface do usuário:

* [Criar uma conexão de origem e um fluxo de dados para [!DNL Mixpanel] usando a API do Serviço de Fluxo](../../tutorials/api/create/analytics/mixpanel.md)

## Connect [!DNL Mixpanel] para Plataforma usando a interface do usuário

* [Crie um [!DNL Mixpanel] conexão de origem na interface do usuário](../../tutorials/ui/create/analytics/mixpanel.md)
* [Criar um fluxo de dados para uma conexão de origem de sucesso do cliente na interface do usuário](../../tutorials/ui/dataflow/analytics.md)
