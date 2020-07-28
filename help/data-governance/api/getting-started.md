---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor da API do serviço de política DULE
topic: developer guide
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---


# Guia do desenvolvedor da API DULE [!DNL Policy Service]

O DULE (Data Usage Labeling and Implementation, Rotulação e Aplicação de Uso de Dados) é o mecanismo principal do Adobe Experience Platform [!DNL Data Governance]. O DULE [!DNL Policy Service] fornece uma RESTful API que permite criar e gerenciar políticas de uso de dados para determinar quais ações de marketing podem ser tomadas em relação aos dados rotulados com determinados rótulos de uso de dados.

Este documento fornece instruções para executar as operações principais disponíveis na [!DNL Policy Service] API. Caso ainda não o tenha feito, comece por revisar a visão geral [do](../home.md) Data Governance para se familiarizar com a estrutura DULE. Para obter instruções passo a passo sobre como criar e aplicar políticas DULE, consulte o tutorial [da política](../policies/create.md)DULE.

Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a [!DNL Policy Service] API.

## Getting started with DULE [!DNL Policy Service]

Antes de começar a trabalhar com o [!DNL Policy Service], os dados em [!DNL Experience Platform] devem ter etiquetas DULE apropriadas aplicadas. As instruções passo a passo completas para aplicar rótulos de uso de dados a conjuntos de dados e campos podem ser encontradas no guia [do usuário de rótulos](../labels/user-guide.md)DULE.

## Pré-requisitos

Este guia exige uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [!DNL Data Governance](../home.md): A estrutura pela qual [!DNL Experience Platform] aplica a conformidade de uso de dados.
   * [Rótulos](../labels/overview.md)DULE: Os rótulos de uso de dados são aplicados aos campos de dados [!DNL Experience Data Model] (XDM), especificando restrições para como esses dados podem ser acessados.
* [!DNL Experience Data Model (XDM) System](../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [!DNL Real-time Customer Profile](../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

## Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

## Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Data Governance], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Recursos principais vs. personalizados

Na [!DNL Policy Service] API, todas as políticas e ações de marketing são referidas como `core` `custom` recursos.

Os `core` recursos são definidos e mantidos pela Adobe, enquanto `custom` os recursos são criados e mantidos por clientes individuais e, portanto, são únicos e visíveis apenas para a organização IMS que os criou. Dessa forma, as operações de listagem e pesquisa (`GET`) são as únicas operações permitidas em `core` recursos, enquanto as operações de listagem, pesquisa e atualização (`POST`, `PUT`, `PATCH`e `DELETE`) estão disponíveis para `custom` recursos.

## Status da política

As políticas de uso de dados podem ter um de três status possíveis: `DRAFT`, `ENABLED`ou `DISABLED`.

Por padrão, somente as políticas &quot;ATIVADAS&quot; participam da avaliação de políticas.

As políticas &quot;RASCUNHO&quot; também podem ser consideradas na avaliação das políticas, mas apenas através da definição do parâmetro &quot;query&quot; `?includeDraft=true`. Na seção documento sobre a aplicação [das](../enforcement/overview.md) políticas, pode obter - se mais informações sobre a avaliação das políticas no final deste documento.

## Nomes de ação de marketing {#marketing-actions}

Nomes de ações de marketing são identificadores exclusivos para ações de marketing. Cada ação `core` de marketing tem um nome exclusivo que se aplica a todas as Organizações IMS. Esses nomes são definidos e mantidos por Adobe. Enquanto isso, todas as ações de marketing definidas pelo cliente (`custom` recursos) são exclusivas em sua organização individual e não são visíveis nem compartilhadas com outras Organizações IMS.

As etapas para trabalhar com ações de marketing na [!DNL Policy Service] API são descritas na seção Ações [de](#marketing-actions) marketing posteriormente neste documento.

## Próximas etapas

Agora que você tem o conhecimento e as credenciais pré-requisito, pode continuar a ler as chamadas de API de amostra fornecidas neste guia do desenvolvedor:

* [Ações de marketing](marketing-actions.md)
* [Políticas](policies.md)