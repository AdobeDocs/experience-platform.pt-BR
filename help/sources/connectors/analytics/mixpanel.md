---
title: Visão geral do Conector Source do Mixpanel
description: Saiba como conectar o Mixpanel ao Adobe Experience Platform usando APIs ou a interface do usuário.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# [!DNL Mixpanel]

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de um aplicativo de análise de terceiros. O suporte para provedores de análise inclui [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) é uma ferramenta de análise de produto que permite capturar dados sobre como os usuários interagem com um produto digital. O Mixpanel permite analisar esses dados de produtos com relatórios simples e interativos que permitem consultar e visualizar os dados com apenas alguns cliques.

As fontes usam a [API de Exportação de Evento do Mixpanel > Baixar](https://developer.mixpanel.com/reference/raw-event-export) para baixar os dados do evento conforme são recebidos e armazenados em [!DNL Mixpanel], juntamente com todas as propriedades do evento (incluindo `distinct_id`) e o carimbo de data e hora exato em que o evento foi enviado para o Experience Platform. O Mixpanel usa tokens de portador como um mecanismo de autenticação para se comunicar com a API de exportação de eventos do Mixpanel.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Autentique sua conta do [!DNL Mixpanel]

Esta seção descreve as etapas de pré-requisito a serem concluídas para autenticar sua conta e trazer seus dados do [!DNL Mixpanel] para a Platform.

Para criar uma conexão de origem e um fluxo de dados [!DNL Mixpanel], primeiro você deve ter uma conta [!DNL Mixpanel] válida. Se você não tiver uma conta válida do [!DNL Mixpanel], consulte a página [Registro do Mixpanel](https://mixpanel.com/register/) para criar sua conta.

Depois de criar uma conta do [!DNL Mixpanel] com êxito, navegue até a guia [!DNL Project Details] na página [!DNL Project Seettings] da interface do usuário do [!DNL Mixpanel] para recuperar a ID do projeto e configurar o fuso horário.

![configurações-projeto-mixpanel](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Em seguida, navegue até a guia [!DNL Service Accounts] na página [!DNL Project Settings] da interface do usuário [!DNL Mixpanel] para recuperar as credenciais da conta de serviço.

>[!TIP]
>
>Para a prática recomendada, selecione uma conta de serviço que [não expira](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Conta de Serviço do Mixpanel](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Finalmente, crie um [esquema](../../../xdm/schema/composition.md) da Platform necessário para o [!DNL Mixpanel Event Export API]. Para obter mais informações sobre os mapeamentos necessários para o esquema, consulte o manual em [criando uma [!DNL Mixpanel] conexão de origem na interface](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![Criar Esquema](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Conectar [!DNL Mixpanel] à plataforma usando APIs

A documentação abaixo fornece informações sobre como conectar o [!DNL Mixpanel] à Plataforma usando APIs ou a interface do usuário:

* [Criar uma conexão de origem e um fluxo de dados para  [!DNL Mixpanel] usando a API de Serviço de Fluxo](../../tutorials/api/create/analytics/mixpanel.md)

## Conectar [!DNL Mixpanel] à Plataforma usando a interface

* [Criar uma conexão de origem  [!DNL Mixpanel]  na interface](../../tutorials/ui/create/analytics/mixpanel.md)
* [Criar um fluxo de dados para uma conexão de origem de sucesso do cliente na interface](../../tutorials/ui/dataflow/analytics.md)
