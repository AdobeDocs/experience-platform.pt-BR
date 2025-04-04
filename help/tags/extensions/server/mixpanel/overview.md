---
keywords: extensão de encaminhamento de eventos;mixpanel;extensão de encaminhamento de eventos do mixpanel
title: Extensão de encaminhamento de eventos da API de rastreamento do Mixpanel
description: Essa extensão de encaminhamento de eventos do Adobe Experience Platform envia eventos do Edge Network para o Mixpanel.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 1%

---

# Extensão de encaminhamento de eventos de API [!DNL Mixpanel Track Events]

[[!DNL Mixpanel]](https://www.mixpanel.com) é uma ferramenta de análise de produto que permite capturar dados sobre como os usuários interagem com um produto digital. É possível analisar dados de produtos com relatórios simples e interativos que permitem consultar e visualizar os dados com apenas alguns cliques. O [!DNL Mixpanel] foi projetado para tornar as equipes mais eficientes, permitindo que todos analisem os dados do usuário em tempo real para identificar tendências, entender o comportamento do usuário e tomar decisões sobre o seu produto.

O [!DNL Mixpanel] emprega um modelo centrado no usuário e baseado em eventos que conecta cada interação a um único usuário. O modelo de dados [!DNL Mixpanel] é construído com base nos conceitos de usuários, eventos e propriedades.

>[!NOTE]
>
>Consulte a documentação [!DNL Mixpanel] em [gerenciamento de identidades](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) para entender como o [!DNL Mixpanel] mescla eventos para criar clusters de identidade. Também é recomendável que você revise o documento em [IDs distintas](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) para entender como elas são usadas para identificar usuários nos dados do evento.

## Casos de uso

Essa extensão deve ser usada se você quiser usar dados da Edge Network no [!DNL Mixpanel] para aproveitar seus recursos de análise de produtos.

Por exemplo, considere uma organização de varejo com presença multicanal (site e dispositivos móveis). A organização captura entradas transacionais ou conversacionais como dados do evento de suas plataformas e as carrega em [!DNL Mixpanel] usando a extensão de encaminhamento de eventos.

As equipes de análise podem aproveitar os recursos do [!DNL Mixpanel's] para processar os conjuntos de dados e obter insights de negócios, que podem ser usados para gerar gráficos, painéis ou outras visualizações para informar as partes interessadas.

Para obter mais informações sobre casos de uso específicos do [!DNL Mixpanel], consulte a seguinte documentação:

* [Novo para [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [O que é [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12}recursos](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/) de experimentação obrigatória [!DNL Mixpanel] 

## [!DNL Mixpanel] pré-requisitos {#prerequisites-mixpanel}

Você deve ter uma conta [!DNL Mixpanel] válida para usar esta extensão. Vá para a [[!DNL Mixpanel] página de registro](https://mixpanel.com/register/) para se registrar e criar uma conta, caso ainda não tenha uma.

Verifique se a configuração [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) está habilitada para o seu projeto. Navegue até **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** e alterne a configuração.

### Compreendendo clusters de identidade em [!DNL Mixpanel]

Em [!DNL Mixpanel], um cluster de identidade contém uma coleção de `distinct_id` valores que se conectam a um usuário individual. [!DNL Mixpanel] manipula o cluster de identidades para cada usuário, resolvendo um único `distinct_id` canônico de cada cluster a ser usado em relatórios. Você também pode incluir seu próprio identificador (chamado de `distinct_id` local) para eventos anônimos que ocorrem antes de um evento de identificação de usuário.

[!DNL Mixpanel] resolve clusters de identidade através de dois métodos:

* **Identificar** : [!DNL Mixpanel] conecta o identificador escolhido a um `distinct_id` anônimo. Se o seu site tiver o SDK [!DNL Mixpanel] habilitado, a Experience Platform usará o `distinct_id` atribuído ao usuário que está conectado no momento.
* **Alias**: [!DNL Mixpanel] combina dois `distinct id`s não anônimos se os critérios de mesclagem adicionais forem atendidos.

>[!NOTE]
>
>Consulte o documento [!DNL Mixpanel] sobre [gerenciamento de identidades](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) para obter mais detalhes sobre esses métodos.
>
>Confirme se você habilitou o [[!DNL Mixpanel] recurso de mesclagem de identidades](#prerequisites-mixpanel) para garantir que os clusters de identidade sejam resolvidos adequadamente.

### Coletar detalhes de configuração necessários {#configuration-details}

Para conectar o Experience Platform a [!DNL Mixpanel], você deve ter as seguintes entradas:

| Tipo de chave | Descrição | Exemplo |
| --- | --- | --- |
| Token do projeto | O token do projeto associado à sua conta [!DNL Mixpanel]. Consulte a documentação do [!DNL Mixpanel] em [localizando o token do projeto](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) para obter orientação. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Instalar e configurar a extensão [!DNL Mixpanel] {#install}

Para instalar a extensão, [crie uma propriedade de encaminhamento de eventos](../../../ui/event-forwarding/overview.md#properties) ou escolha uma propriedade existente para editar.

Selecione **[!UICONTROL Extensões]** na navegação à esquerda. Na guia **[!UICONTROL Catálogo]**, selecione **[!UICONTROL Instalar]** no cartão para a extensão [!DNL Mixpanel].

![Instalando a extensão [!DNL Mixpanel].](../../../images/extensions/server/mixpanel/install-extension.png)

## Criar uma regra [!DNL Send Event]

Comece a criar uma nova regra na propriedade de encaminhamento de eventos. Em **[!UICONTROL Ações]**, adicione uma nova ação e defina a extensão como **[!UICONTROL Mixpanel]**. Em seguida, defina o tipo de ação como **[!UICONTROL Rastrear Evento]** para enviar eventos Edge Network para [!DNL Mixpanel].

| Entrada | Descrição | Obrigatório |
| --- | --- | --- |
| [!UICONTROL Token do projeto] | Este campo deve ser mapeado para o token de projeto associado à sua conta [!DNL Mixpanel]. | Sim |
| [!UICONTROL Tipo de evento] | O nome do evento. | Sim |
| [!UICONTROL Hora do Evento] | A hora do evento. | |
| [!UICONTROL ID distinta do Mixpanel] | O identificador exclusivo do usuário que executou o evento. | |
| [!UICONTROL Inserir ID] | Um identificador exclusivo do evento, usado para desduplicação. | |
| [!UICONTROL Propriedades do Evento] | Um objeto JSON que contém propriedades personalizadas do evento. Escolha entre fornecer JSON bruto ou usar um conjunto simplificado de entradas de valores-chave. | |

>[!NOTE]
>
>Para obter mais informações sobre os campos padrão de um evento [!DNL Mixpanel], consulte a [documentação oficial](https://developer.mixpanel.com/reference/import-events#event).

![Adicionar uma configuração de ação de regra de encaminhamento de eventos.](../../../images/extensions/server/mixpanel/track-event-action.png)

Depois que a ação [!UICONTROL Rastrear evento] for adicionada à regra, você poderá configurar as condições da regra para que ela só seja acionada para determinados eventos, ou você poderá deixar a seção de condições vazia para que a regra seja acionada para todos os eventos.

>[!IMPORTANT]
>
>Se o seu site estiver usando o SDK [!DNL Mixpanel], você poderá continuar até a próxima etapa do [validação de dados [!DNL Mixpanel]](#validate). Se você não estiver usando o SDK [!DNL Mixpanel], deve [criar uma regra de rastreamento de identidade separada](#create-an-identity-tracking-rule) para garantir que os eventos apropriados e os valores de `distinct_id` sejam enviados para [!DNL Mixpanel] quando ocorrer um evento de identificação de usuário.

## Validar dados em [!DNL Mixpanel] {#validate}

Se a implementação for bem-sucedida e os eventos forem coletados, você verá eventos no [[!DNL Mixpanel] console](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Verifique se [!DNL Mixpanel] mesclou os eventos de pós-logon preenchidos com valores de email e com os eventos criados ao usar o **[!UICONTROL Enviar Evento]**. Se implementadas corretamente, [!DNL Mixpanel] as associará a um único [perfil de usuário](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Próximas etapas

Este guia abordou como enviar eventos de conversão para [!DNL Mixpanel] usando o encaminhamento de eventos. Esta extensão de encaminhamento de eventos aproveita a API do SDK e do JavaScript [!DNL Mixpanel]. Para obter mais informações sobre essas tecnologias subjacentes, consulte a documentação oficial:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] API JavaScript](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Para obter mais informações sobre os recursos de encaminhamento de eventos do Experience Platform, consulte a [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
