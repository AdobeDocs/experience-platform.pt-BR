---
keywords: extensão de encaminhamento de eventos, mixpanel, extensão de encaminhamento de eventos mixpanel
title: Extensão de Encaminhamento de Eventos de API de Rastreamento de Mixpanel
description: Essa extensão de encaminhamento de eventos do Adobe Experience Platform envia eventos de rede do Adobe Experience Edge para o Mixpanel.
last-substantial-update: 2023-03-29T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] Extensão de encaminhamento de eventos de API

[[!DNL Mixpanel]](https://www.mixpanel.com) O é uma ferramenta de análise de produto que permite capturar dados sobre como os usuários interagem com um produto digital. Você pode analisar dados de produtos com relatórios simples e interativos que permitem consultar e visualizar os dados com apenas alguns cliques. [!DNL Mixpanel] criado para tornar as equipes mais eficientes, permitindo que todos analisem os dados do usuário em tempo real para identificar tendências, entender o comportamento do usuário e tomar decisões sobre seu produto.

[!DNL Mixpanel] O emprega um modelo baseado em eventos e centrado no usuário que conecta cada interação a um único usuário. O [!DNL Mixpanel] o modelo de dados é criado com base nos conceitos dos usuários, eventos e propriedades.

>[!NOTE]
>
>Consulte a [!DNL Mixpanel] documentação sobre [gerenciamento de identidade](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) para entender como [!DNL Mixpanel] mescla eventos para criar clusters de identidade. Também é recomendável que você revise o documento em [IDs distintas](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) para entender como eles são usados para identificar usuários nos dados do evento.

## Casos de uso

Essa extensão deve ser usada se você quiser usar dados da Edge Network em [!DNL Mixpanel] para aproveitar seus recursos de análise do produto.

Por exemplo, considere uma organização de varejo que tem uma presença de multicanal (site e dispositivo móvel). A organização captura entrada transacional ou conversacional como dados de evento de suas plataformas e a carrega em [!DNL Mixpanel] usando a extensão de encaminhamento de eventos.

As equipes de análise podem aproveitar [!DNL Mixpanel's] recursos para processar os conjuntos de dados e obter insights de negócios, que podem ser usados para gerar gráficos, painéis ou outras visualizações para informar às partes interessadas da empresa.

Para obter mais informações sobre casos de uso específicos de [!DNL Mixpanel], consulte a seguinte documentação:

* [Novo em [!DNL Mixpanel]](https://help.mixpanel.com/hc/en-us/sections/360008533532-New-to-Mixpanel)
* [O que é [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12 obrigatoriamente [!DNL Mixpanel] recursos](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] pré-requisitos {#prerequisites-mixpanel}

Você deve ter um [!DNL Mixpanel] para usar essa extensão. Vá para o [[!DNL Mixpanel] página de registro](https://mixpanel.com/register/) para registrar e criar uma conta, caso ainda não tenha uma.

Certifique-se de que [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) está ativada para o seu projeto. Navegar para **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** e alterne a configuração.

### Como entender os clusters de identidade em [!DNL Mixpanel]

Em [!DNL Mixpanel], um cluster de identidade contém uma coleção de `distinct_id` que se conectam a um usuário individual. [!DNL Mixpanel] lida com o cluster de identidades de cada usuário, resolvendo um único canônico `distinct_id` de cada cluster a ser usado em relatórios. Também é possível incluir seu próprio identificador (chamado de local `distinct_id`) para eventos anônimos que ocorrem antes de um evento de identificação de usuário.

[!DNL Mixpanel] resolve clusters de identidade por meio de dois métodos:

* **Identificar** : [!DNL Mixpanel] conecta seu identificador escolhido a um anônimo `distinct_id`. Se seu site tiver a variável [!DNL Mixpanel] SDK ativado, a Platform usará a variável `distinct_id` atribuído ao usuário que está conectado no momento.
* **Alias**: [!DNL Mixpanel] combina dois não-anônimos `distinct id`s junto, se os critérios de mesclagem adicionais forem atendidos.

>[!NOTE]
>
>Consulte a [!DNL Mixpanel] documento em [gerenciamento de identidade](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) para obter mais detalhes sobre esses métodos.
>
>Confirme se você ativou a variável [[!DNL Mixpanel] recurso de mesclagem de identidade](#prerequisites-mixpanel) para garantir que os agrupamentos de identidade sejam resolvidos adequadamente.

### Obter detalhes de configuração necessários {#configuration-details}

Para conectar o Experience Platform ao [!DNL Mixpanel] você deve ter as seguintes entradas:

| Tipo de chave | Descrição | Exemplo |
| --- | --- | --- |
| Token do projeto | O token do projeto associado à sua [!DNL Mixpanel] conta. Consulte a [!DNL Mixpanel] documentação sobre [encontrar o token do projeto](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) para orientação. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Instalar e configurar o [!DNL Mixpanel] extensão {#install}

Para instalar a extensão, [criar uma propriedade de encaminhamento de evento](../../../ui/event-forwarding/overview.md#properties) ou escolha uma propriedade existente para editar.

Selecionar **[!UICONTROL Extensões]** no painel de navegação esquerdo. No **[!UICONTROL Catálogo]** guia , selecione **[!UICONTROL Instalar]** no cartão para o [!DNL Mixpanel] extensão.

![Instalar o [!DNL Mixpanel] extensão.](../../../images/extensions/server/mixpanel/install-extension.png)

## Crie um [!DNL Send Event] regra

Comece a criar uma nova regra na propriedade de encaminhamento de eventos. Em **[!UICONTROL Ações]**, adicione uma nova ação e defina a extensão para **[!UICONTROL Mixpanel]**. Em seguida, defina o tipo de ação como **[!UICONTROL Rastrear evento]** para enviar eventos de rede do Adobe Experience Edge para [!DNL Mixpanel].

| Entrada | Descrição | Obrigatório |
| --- | --- | --- |
| [!UICONTROL Token do projeto] | Este campo deve ser mapeado para o token de projeto associado ao seu [!DNL Mixpanel] conta. | Sim |
| [!UICONTROL Tipo de evento] | O nome do evento. | Sim |
| [!UICONTROL Hora do evento] | A hora do evento. |  |
| [!UICONTROL ID distinta do painel misto] | O identificador exclusivo do usuário que executou o evento. |  |
| [!UICONTROL Inserir ID] | Um identificador exclusivo para o evento, usado para desduplicação. |  |
| [!UICONTROL Propriedades do evento] | Um objeto JSON que contém propriedades personalizadas do evento. Selecione entre fornecer JSON bruto ou usar um conjunto simplificado de entradas de valor chave. |  |

>[!NOTE]
>
>Para obter mais informações sobre os campos padrão de um [!DNL Mixpanel] , consulte [documentação oficial](https://developer.mixpanel.com/reference/import-events#event).

![Adicione uma configuração de ação da regra de encaminhamento de eventos.](../../../images/extensions/server/mixpanel/track-event-action.png)

Uma vez [!UICONTROL Rastrear evento] for adicionada à regra, você poderá configurar as condições da regra para que ela seja acionada somente para determinados eventos, ou poderá deixar a seção condições vazia para fazer com que a regra seja acionada para todos os eventos.

>[!IMPORTANT]
>
>Se seu site estiver usando a variável [!DNL Mixpanel] SDK, você pode continuar para a próxima etapa de [como validar seus dados no [!DNL Mixpanel]](#validate). Se você não estiver usando a variável [!DNL Mixpanel] SDK, você deve [criar uma regra de rastreamento de identidade separada](#create-an-identity-tracking-rule) assegurar que os eventos e `distinct_id` são enviados para [!DNL Mixpanel] quando ocorre um evento de identificação de usuário.

## Validar dados no [!DNL Mixpanel] {#validate}

Se sua implementação for bem-sucedida e os eventos forem coletados, você verá os eventos no [[!DNL Mixpanel] console](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Verificar se [!DNL Mixpanel] mesclou os eventos de logon posterior preenchidos com valores de email e os eventos criados ao usar **[!UICONTROL Enviar evento]**. Se implementado corretamente, [!DNL Mixpanel] associá-los a um único [perfil de usuário](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Próximas etapas

Este guia cobriu como enviar eventos de conversão para o [!DNL Mixpanel] utilizando o encaminhamento de eventos. Essa extensão de encaminhamento de eventos aproveita o [!DNL Mixpanel] SDK e API do JavaScript. Para obter mais informações sobre essas tecnologias subjacentes, consulte a documentação oficial:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] API JavaScript](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Para obter mais informações sobre os recursos de encaminhamento de eventos no Experience Platform, consulte o [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
