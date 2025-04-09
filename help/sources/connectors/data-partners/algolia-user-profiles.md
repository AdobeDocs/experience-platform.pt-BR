---
title: Visão geral do Source de perfis de usuário da Algólia
description: Saiba mais sobre a fonte de perfis de usuário da Algólia no Adobe Experience Platform
hide: true
hidefromtoc: true
source-git-commit: 1bde4b831f1b79de1a8292ad5f221f522e871d08
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# [!DNL Algolia User Profiles]

[[!DNL Algolia]](https://www.algolia.com/) é uma poderosa plataforma de API de pesquisa e descoberta que permite que as empresas ofereçam experiências de pesquisa rápidas, relevantes e personalizáveis. Ele fornece recursos de pesquisa em tempo real, como tolerância a erros de digitação, filtragem, facetas e ajuste de relevância baseado em IA. O [!DNL Algolia] ajuda as empresas a melhorar o engajamento do usuário, as taxas de conversão e a experiência geral do cliente, fornecendo soluções de pesquisa de alto desempenho para sites, plataformas de comércio eletrônico e aplicativos.

Alguns dos principais benefícios do [!DNL Algolia] incluem:

* Pesquisa ultrarrápida com resultados instantâneos.
* Recomendações altamente relevantes viabilizadas pela IA.
* Classificação personalizável para priorizar as necessidades empresariais.
* Escalabilidade para lidar com cargas altas de tráfego facilmente.

Para obter mais informações, visite a [[!DNL Algolia] documentação do produto](https://resources.algolia.com/).

## Arquitetura

As Fontes de autoatendimento (SDK em lote) fornecem todos os recursos necessários, como autenticação, paginação ou extração de dados completa e parcial. A origem [!DNL Algolia User Profiles] usa esses recursos para concluir a integração.

![Arquitetura da Integração da Algólia e da Experience Platform](../../images/tutorials/create/algolia/user-profiles/algolia-aep-user-profiles-arch.png)

## Pré-requisitos {#prerequisites}

Conclua as etapas de pré-requisito a seguir para conectar sua conta do [!DNL Algolia] à Experience Platform.

1. Use o [[!DNL Algolia] painel](https://dashboard.algolia.com/users/sign_up) para fazer logon em sua conta do [!DNL Algolia] ou criar uma nova conta.
2. [Prepare seu Índice](https://www.algolia.com/doc/guides/sending-and-managing-data/prepare-your-data/in-depth/prepare-data-in-depth/).
3. [Configurar seus aspectos](https://www.algolia.com/doc/guides/managing-results/refine-results/faceting/).
4. [Enviar eventos de usuário](https://www.algolia.com/doc/guides/sending-events/getting-started/).
5. [Personalize seu índice](https://www.algolia.com/doc/guides/personalization/advanced-personalization/configure/setup/indices/).

### Configurar permissões no Experience Platform

Você deve ter as permissões **[!UICONTROL Exibir Fontes]** e **[!UICONTROL Gerenciar Fontes]** habilitadas para sua conta a fim de conectar sua conta do [!DNL Algolia] à Experience Platform. Entre em contato com o administrador do produto para obter as permissões necessárias. Para obter mais informações, leia o [guia da interface do usuário de controle de acesso](../../../access-control/abac/ui/permissions.md).

### INCLUIR NA LISTA DE PERMISSÕES endereço IP

Uma lista de endereços IP deve ser adicionada a uma inclui na lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região ao seu incluo na lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [inclui na lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Conectar sua conta do [!DNL Algolia] à Experience Platform

Após concluir os pré-requisitos, você pode prosseguir para a próxima etapa e [conectar sua conta [!DNL Algolia] à Experience Platform](../../tutorials/ui/create/data-partners/algolia-user-profiles.md).
