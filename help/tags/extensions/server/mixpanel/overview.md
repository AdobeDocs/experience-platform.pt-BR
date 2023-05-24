---
keywords: extensão de encaminhamento de eventos;mixpanel;extensão de encaminhamento de eventos do mixpanel
title: Extensão de encaminhamento de eventos da API de rastreamento do Mixpanel
description: Essa extensão de encaminhamento de eventos do Adobe Experience Platform envia eventos da Rede de borda do Adobe Experience para o Mixpanel.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] Extensão de encaminhamento de eventos de API

[[!DNL Mixpanel]](https://www.mixpanel.com) O é uma ferramenta de análise de produtos que permite capturar dados sobre como os usuários interagem com um produto digital. É possível analisar dados de produtos com relatórios simples e interativos que permitem consultar e visualizar os dados com apenas alguns cliques. [!DNL Mixpanel] projetado para tornar as equipes mais eficientes, permitindo que todos analisem os dados do usuário em tempo real para identificar tendências, entender o comportamento do usuário e tomar decisões sobre o seu produto.

[!DNL Mixpanel] A emprega um modelo centrado no usuário e baseado em eventos que conecta cada interação a um único usuário. A variável [!DNL Mixpanel] o modelo de dados é criado com base nos conceitos de usuários, eventos e propriedades.

>[!NOTE]
>
>Consulte a [!DNL Mixpanel] documentação sobre [gerenciamento de identidade](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) para entender como [!DNL Mixpanel] mescla eventos para criar clusters de identidade. Também é recomendável que você revise o documento em [IDs distintas](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) para entender como eles são usados para identificar usuários nos dados do evento.

## Casos de uso

Essa extensão deve ser usada se você quiser usar dados da Rede de borda no [!DNL Mixpanel] para aproveitar os recursos de análise de produtos.

Por exemplo, considere uma organização de varejo com presença multicanal (site e dispositivos móveis). A organização captura entradas transacionais ou conversacionais como dados do evento de suas plataformas e as carrega para o [!DNL Mixpanel] usar a extensão de encaminhamento de eventos.

As equipes de análise podem aproveitar [!DNL Mixpanel's] recursos para processar os conjuntos de dados e obter insights de negócios, que podem ser usados para gerar gráficos, painéis ou outras visualizações para informar as partes interessadas de negócios.

Para obter mais informações sobre casos de uso específicos do [!DNL Mixpanel], consulte a seguinte documentação:

* [Novo para [!DNL Mixpanel]](https://help.mixpanel.com/hc/en-us/sections/360008533532-New-to-Mixpanel)
* [O que é [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12 tentativas [!DNL Mixpanel] recursos](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] pré-requisitos {#prerequisites-mixpanel}

Você deve ter um válido [!DNL Mixpanel] para usar essa extensão. Vá para a [[!DNL Mixpanel] página de registro](https://mixpanel.com/register/) para registrar e criar uma conta se ainda não tiver uma.

Certifique-se de que o [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) está ativada para o seu projeto. Navegue até **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** e alterne a configuração.

### Noções básicas sobre clusters de identidade no [!DNL Mixpanel]

Entrada [!DNL Mixpanel], um cluster de identidade contém uma coleção de `distinct_id` que se conectam a um usuário individual. [!DNL Mixpanel] lida com o cluster de identidades de cada usuário, resolvendo um único problema `distinct_id` de cada cluster a ser usado em relatórios. Você também pode incluir seu próprio identificador (chamado de local `distinct_id`) para eventos anônimos que ocorrem antes de um evento de identificação do usuário.

[!DNL Mixpanel] O resolve clusters de identidade por meio de dois métodos:

* **Identificar** : [!DNL Mixpanel] conecta o identificador escolhido a um `distinct_id`. Se seu site tiver o [!DNL Mixpanel] SDK ativado, a Platform usará o `distinct_id` atribuído ao usuário que está conectado no momento.
* **Alias**: [!DNL Mixpanel] combina dois perfis não anônimos `distinct id`s juntos, se os critérios de mesclagem adicionais forem atendidos.

>[!NOTE]
>
>Consulte a [!DNL Mixpanel] documento ativado [gerenciamento de identidade](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) para obter mais detalhes sobre esses métodos.
>
>Confirme se você ativou o [[!DNL Mixpanel] recurso de mesclagem de identidades](#prerequisites-mixpanel) para garantir que os clusters de identidade sejam resolvidos adequadamente.

### Coletar detalhes de configuração necessários {#configuration-details}

Para conectar o Experience Platform a [!DNL Mixpanel] você deve ter as seguintes entradas:

| Tipo de chave | Descrição | Exemplo |
| --- | --- | --- |
| Token do projeto | O token do projeto associado à [!DNL Mixpanel] conta. Consulte a [!DNL Mixpanel] documentação sobre [localizar o token do projeto](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) para obter orientação. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Instale e configure o [!DNL Mixpanel] extensão {#install}

Para instalar a extensão, [criar uma propriedade de encaminhamento de eventos](../../../ui/event-forwarding/overview.md#properties) ou escolha uma propriedade existente para editar.

Selecionar **[!UICONTROL Extensões]** no painel de navegação esquerdo. No **[!UICONTROL Catálogo]** selecione **[!UICONTROL Instalar]** no cartão para o [!DNL Mixpanel] extensão.

![Instalação do [!DNL Mixpanel] extensão.](../../../images/extensions/server/mixpanel/install-extension.png)

## Criar um [!DNL Send Event] regra

Comece a criar uma nova regra na propriedade de encaminhamento de eventos. Em **[!UICONTROL Ações]**, adicione uma nova ação e defina a extensão para **[!UICONTROL Mixpanel]**. Em seguida, defina o tipo de ação como **[!UICONTROL Rastrear evento]** para enviar eventos da Adobe Experience Edge Network para [!DNL Mixpanel].

| Entrada | Descrição | Obrigatório |
| --- | --- | --- |
| [!UICONTROL Token do projeto] | Este campo deve ser mapeado para o token de projeto associado à [!DNL Mixpanel] conta. | Sim |
| [!UICONTROL Tipo de evento] | O nome do evento. | Sim |
| [!UICONTROL Hora do Evento] | A hora do evento. |  |
| [!UICONTROL ID distinta do Mixpanel] | O identificador exclusivo do usuário que executou o evento. |  |
| [!UICONTROL Inserir ID] | Um identificador exclusivo do evento, usado para desduplicação. |  |
| [!UICONTROL Propriedades do evento] | Um objeto JSON que contém propriedades personalizadas do evento. Escolha entre fornecer JSON bruto ou usar um conjunto simplificado de entradas de valores-chave. |  |

>[!NOTE]
>
>Para obter mais informações sobre os campos padrão de uma [!DNL Mixpanel] evento, consulte a [documentação oficial](https://developer.mixpanel.com/reference/import-events#event).

![Adicione uma configuração de ação de regra de encaminhamento de eventos.](../../../images/extensions/server/mixpanel/track-event-action.png)

Quando a variável [!UICONTROL Rastrear evento] for adicionada à regra, você poderá configurar as condições da regra para que ela só seja acionada para determinados eventos, ou poderá deixar a seção condições vazia para fazer com que a regra seja acionada para todos os eventos.

>[!IMPORTANT]
>
>Se seu site estiver usando o [!DNL Mixpanel] do SDK, você pode continuar com a próxima etapa do [validação dos dados no [!DNL Mixpanel]](#validate). Se você não estiver usando o [!DNL Mixpanel] SDK, é necessário [criar uma regra de rastreamento de identidade separada](#create-an-identity-tracking-rule) assegurar que eventos e eventos `distinct_id` os valores são enviados para [!DNL Mixpanel] quando ocorre um evento de identificação de usuário.

## Validar dados no [!DNL Mixpanel] {#validate}

Se a implementação for bem-sucedida e os eventos forem coletados, você verá eventos na [[!DNL Mixpanel] console](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Verificar se [!DNL Mixpanel] mesclou os eventos de pós-logon preenchidos com valores de email e os eventos criados ao usar o **[!UICONTROL Enviar evento]**. Se implementado corretamente, [!DNL Mixpanel] irá associá-los a um único [perfil do usuário](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Próximas etapas

Este guia abordou como enviar eventos de conversão para o [!DNL Mixpanel] usando o encaminhamento de eventos. Essa extensão de encaminhamento de eventos utiliza o [!DNL Mixpanel] SDK e API JavaScript. Para obter mais informações sobre essas tecnologias subjacentes, consulte a documentação oficial:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] API JavaScript](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Para obter mais informações sobre os recursos de encaminhamento de eventos no Experience Platform, consulte [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
