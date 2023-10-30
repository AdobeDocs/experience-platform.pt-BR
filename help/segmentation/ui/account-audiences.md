---
title: Públicos da conta
description: Saiba como criar e usar públicos-alvo da conta para direcionar perfis de conta em destinos downstream.
badgeLimitedAvailability: label="Disponibilidade limitada" type="Caution"
badgeB2B: label="Edição B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Públicos da conta

>[!AVAILABILITY]
>
>Os públicos-alvo da conta só estão disponíveis no [Edição B2B do Real-time Customer Data Platform](../../rtcdp/b2b-overview.md). Além disso, a funcionalidade de público-alvo da conta está atualmente em **disponibilidade limitada**. Entre em contato com o Atendimento ao cliente da Adobe ou com seu representante da Adobe para solicitar acesso a essa funcionalidade.

Com a segmentação de conta, o Adobe Experience Platform permite que você ofereça a total facilidade e sofisticação da experiência de segmentação de marketing de públicos com base em pessoas para públicos com base em conta.

Os públicos da conta podem ser usados como uma entrada para destinos baseados em conta, permitindo direcionar as pessoas nessas contas nos serviços downstream. Por exemplo, você pode usar públicos-alvo baseados em conta para recuperar registros de todas as contas que **não** ter informações de contato de qualquer pessoa com o título Diretor de Operações (COO) ou Diretor de Marketing (CMO).

## Terminologia {#terminology}

Antes de começar a usar públicos-alvo de conta, analise as diferenças entre os diferentes tipos de público-alvo:

- **Públicos da conta**: um público-alvo da conta é um público-alvo criado com o **account** dados do perfil. Os dados do perfil da conta podem ser usados para criar públicos-alvo que segmentem as pessoas nas contas downstream. Para obter mais informações sobre perfis de conta, leia a [visão geral do perfil da conta](../../rtcdp/accounts/account-profile-overview.md).
- **Públicos-alvo de pessoas**: um público-alvo de pessoas é um público-alvo criado com o **cliente** dados do perfil. Os dados do perfil do cliente podem ser usados para criar públicos-alvo que direcionem a clientela da sua empresa. Para obter mais informações sobre perfis de clientes, leia a [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).
- **Públicos-alvo potenciais**: um público-alvo potencial é um público-alvo criado com o uso de **potencial** dados do perfil. Os dados de perfil de cliente potencial podem ser usados para criar públicos-alvo de usuários não autenticados. Para obter mais informações sobre perfis de clientes potenciais, leia a [visão geral do perfil do cliente potencial](../../profile/ui/prospect-profile.md).

## Access {#access}

Para acessar os públicos-alvo da conta, selecione **[!UICONTROL Públicos-alvo]** no **[!UICONTROL Contas]** seção.

![O botão Audiences é realçado na seção Accounts (Contas).](../images/ui/account-audiences/select.png)

A variável [!UICONTROL Procurar] será exibida, mostrando uma lista de todos os públicos-alvo da conta da organização.

![Os públicos-alvo da conta pertencentes à organização são exibidos.](../images/ui/account-audiences/browse.png)

Essa exibição lista informações sobre o público-alvo, incluindo nome, contagem de perfis, origem, status do ciclo de vida, data de criação e data da última atualização.

## Criar público-alvo {#create}

Para criar um público-alvo para a conta, selecione **[!UICONTROL Criar público]** no [!UICONTROL Procurar] página.

![A variável [!UICONTROL Criar público] O botão é realçado na página de navegação do público-alvo da conta.](../images/ui/account-audiences/select-create-audience.png)

O Construtor de segmentos é exibido. Os atributos da conta são exibidos na barra de navegação esquerda.

![O Construtor de segmentos é exibido. Observe que somente os atributos são exibidos.](../images/ui/account-audiences/segment-builder.png)

Ao criar públicos-alvo de conta, observe que os eventos estão listados em **[!UICONTROL Pessoas]**, em vez de serem sua própria guia, já que esses atributos estão associados a pessoas.

![O local para localizar eventos, que está dentro da variável [!UICONTROL Pessoas] , está realçada.](../images/ui/account-audiences/attributes.png)

Para obter mais informações sobre como usar o Construtor de segmentos, leia as [Guia da interface do usuário do Construtor de segmentos](./segment-builder.md).

## Ativar público {#activate}

>[!NOTE]
>
>Somente um número limitado de destinos oferece suporte a públicos-alvo de contas. Verifique se o destino que você deseja ativar é compatível com os públicos-alvo da conta antes de continuar esse processo.

Depois de criar o público-alvo da sua conta, você pode ativá-lo para outros serviços downstream.

Selecione o público que deseja ativar, seguido por **[!UICONTROL Ativar para destino]**.

![A variável [!UICONTROL Ativar para destino] O botão é realçado no menu de ações rápidas para o público-alvo selecionado.](../images/ui/account-audiences/activate.png)

A variável [!UICONTROL Ativar destino] é exibida. Para obter mais informações sobre o processo de ativação, incluindo destinos compatíveis e detalhes sobre mapeamentos de campo, leia a [ativar públicos-alvo da conta](/help/destinations/ui/activate-account-audiences.md) tutorial.

## Próximas etapas {#next-steps}

Depois de ler este guia, você compreenderá melhor como criar e usar os públicos-alvo da sua conta no Adobe Experience Platform. Para saber como usar outros tipos de público-alvo na Platform, leia o [Guia da interface do usuário do serviço de segmentação](./overview.md).
