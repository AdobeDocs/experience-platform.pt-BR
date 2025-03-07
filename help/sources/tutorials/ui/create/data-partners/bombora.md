---
title: Conectar a intenção do Bombora ao Experience Platform usando a interface do usuário
description: Saiba como conectar o Bombora Intent ao Experience Platform
hide: true
hidefromtoc: true
source-git-commit: 81a615b9826ed69bb050cae9c074a4e457ba128a
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 11%

---

# Conectar o [!DNL Bombora Intent] ao Experience Platform usando a interface

Leia este guia para saber como conectar sua conta do [!DNL Bombora Intent] à Adobe Experience Platform usando a interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md): o Real-Time CDP B2B edition foi criado especificamente para profissionais de marketing que operam em um modelo de serviço business-to-business. A plataforma reúne dados de várias origens e os combina numa única exibição de perfis de pessoas e contas. Esses dados unificados permitem que profissionais de marketing direcionem públicos-alvo específicos com precisão e gerem engajamento em todos os canais disponíveis.
* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Navegar pelo catálogo de origens

Na interface da Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Selecione **[!DNL Bombora Intent]** na categoria *[!UICONTROL B2B]* e selecione **[!UICONTROL Configurar]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Configurar]** quando uma determinada origem ainda não tem uma conta autenticada. Quando uma conta autenticada existir, esta opção será alterada para **[!UICONTROL Adicionar dados]**.



## Usar uma conta existente {#existing}

## Criar uma nova conta {#create}

## Fornecer detalhes do fluxo de dados {#provide-dataflow-details}

>[!CONTEXTUALHELP]
>id="platform_sources_bombora_domain"
>title="Origem do domínio"
>abstract="Embora o Adobe use o site accountOrganization.XDM, pode haver clientes que usam campos personalizados para seus respectivos sites. Portanto, você deve garantir que a origem do seu domínio seja o campo domínio/site que corresponderá aos registros da sua conta Bombora em relação às contas da Experience Platform."

## Agendar fluxo de dados {#schedule-dataflow}

>[!CONTEXTUALHELP]
>id="platform_sources_bombora_schedule"
>title="Agendar seu fluxo de dados"
>abstract="Bombora solta dados uma vez por semana na manhã de segunda-feira às 17h UTC. Portanto, você deve configurar a hora de início da assimilação depois das 17h UTC. Além disso, você deve confirmar o tempo de assimilação com o Bombora, pois eles podem alterar a programação ao soltar arquivos no Adobe."


## Revisar fluxo de dados {#review-dataflow}
