---
keywords: Experience Platform;página inicial;tópicos populares;Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: conector Marketo Engage
description: Este documento fornece uma visão geral do conector de origem do Marketo Engage, incluindo informações sobre autenticação, mapeamento e latência de dados.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: f0a3486fc7df7b08a11ec7bfb041841bc2c1c9a3
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 5%

---

# [!DNL Marketo Engage] conector

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) é uma solução completa para o gerenciamento de clientes potenciais e para os profissionais de marketing B2B que procuram transformar as experiências dos clientes ao se envolverem em todas as jornadas de compras complexas.

Com o [!DNL Marketo Engage] conector de origem, é possível trazer dados B2B de [!DNL Marketo Engage] para a Platform e mantenha esses dados atualizados usando aplicativos conectados à Platform.

>[!IMPORTANT]
>
>Você deve ter acesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) para usar todos os conjuntos de dados do Marketo para segmentação com o [Perfil do cliente em tempo real](../../../../profile/home.md). Sem o Real-Time CDP B2B Edition, você ainda pode usar a fonte do Marketo para trazer dados dos conjuntos de dados de pessoas e atividades para o Perfil do cliente em tempo real para segmentação.

Este documento fornece uma visão geral do [!DNL Marketo Engage] conector de origem, incluindo informações sobre como autenticar o conector, como mapear [!DNL Marketo Engage] para o Experience Data Model (XDM) e a latência de dados do conector.

## Configurar o mapeamento da organização do Adobe

Antes de estabelecer conjuntos de mapeamento para [!DNL Marketo Engage], você deve primeiro configurar o Mapeamento da organização do Adobe. Para obter etapas detalhadas sobre como concluir isso, consulte o guia em [configuração do Adobe Organization Mapping para [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Autentique seu [!DNL Marketo Engage] conector

Para se conectar [!DNL Marketo Engage] para a Platform, primeiro você deve recuperar os valores de `munchkinId`, `clientId`, e `clientSecret`.

Veja as etapas descritas na seção [Autentique seu conector de origem do Marketo](./marketo-auth.md) documento para recuperar suas credenciais.

## Configurar namespaces B2B e o utilitário de geração automática de esquema

Em seguida, use o namespace B2B e o utilitário de geração automática de esquema para configurar seu console do desenvolvedor do Platform e o ambiente do Postman. Isso permite preencher automaticamente os namespaces e esquemas B2B. Para obter instruções detalhadas, consulte o guia no [configuração dos namespaces B2B e do utilitário de geração automática de esquema](./marketo-namespaces.md)

## Experience Data Model (XDM)

O XDM é uma especificação documentada publicamente que fornece estruturas e definições comuns que permitem assimilar dados de fontes de terceiros para uso nos serviços downstream da plataforma.

A adesão aos padrões XDM permite que os dados sejam incorporados uniformemente ao ecossistema da plataforma, facilitando a entrega de dados e a coleta de informações.

Para saber mais sobre o XDM e sua função na Platform, consulte o [Visão geral do sistema XDM](../../../../xdm/home.md).

## Mapeamento de campo de [!DNL Marketo Engage] ao XDM

Para estabelecer uma conexão de origem entre [!DNL Marketo Engage] e Platform, os campos de dados de origem do Marketo devem ser mapeados para os campos XDM de destino apropriados antes de serem assimilados na Platform.

Consulte o seguinte para obter informações detalhadas sobre as regras de mapeamento de campo entre [!DNL Marketo Engage] conjuntos de dados e plataforma:

* [Atividades](../mapping/marketo.md#activities)
* [Programas](../mapping/marketo.md#programs)
* [Associações ao programa](../mapping/marketo.md#program-memberships)
* [Empresas](../mapping/marketo.md#companies)
* [Listas estáticas](../mapping/marketo.md#static-lists)
* [Associações de lista estática](../mapping/marketo.md#static-list-memberships)
* [Contas Nomeadas](../mapping/marketo.md#named-accounts)
* [Oportunidades](../mapping/marketo.md#opportunities)
* [Funções do contato da oportunidade](../mapping/marketo.md#opportunity-contact-roles)
* [Pessoas](../mapping/marketo.md#persons)

## Latência esperada de [!DNL Marketo Engage] dados na plataforma

A tabela a seguir descreve a latência esperada para trazer [!DNL Marketo Engage] dados na Platform, com base na natureza da assimilação e no destino desejado:

| Destino | Latência esperada |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 1 minuto |
| Data lake | &lt; 60 minutos |

## Próximas etapas e recursos adicionais

A documentação a seguir fornece mais informações sobre a criação de um [!DNL Marketo Engage] conexão de origem:

* Para obter informações sobre como conectar seu [!DNL Marketo Engage] dados para a Platform, leia o tutorial em [criação de um [!DNL Marketo Engage] conexão de origem na interface](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * Para obter informações sobre como configurar seus esquemas e assimilar dados de atividade personalizados, leia o tutorial sobre [criação de uma conexão de origem e fluxo de dados para [!DNL Marketo Engage] dados de atividade personalizados](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
* Para obter informações sobre a configuração subjacente dos namespaces B2B e esquemas usados com [!DNL Marketo Engage], leia a documentação de [Namespaces e esquemas B2B](./marketo-namespaces.md).
* Para obter informações sobre como encontrar o [!DNL Marketo Engage] munchkin ID e gerando suas credenciais, leia o [[!DNL Marketo Engage] guia de autenticação](./marketo-auth.md).
* Para obter informações sobre as regras de mapeamento específicas aplicáveis a [!DNL Marketo Engage] conjuntos de dados, leia a documentação em [[!DNL Marketo Engage] mapeamentos de campo](../mapping/marketo.md).
* Para obter informações gerais sobre [!DNL Real-Time Customer Data Platform B2B Edition] e seus recursos, leia a documentação em [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
