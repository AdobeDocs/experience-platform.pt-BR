---
keywords: Experience Platform;página inicial;tópicos populares;monitorar identidades;monitorar fluxos de dados;fluxos de dados;identidades;
description: O serviço de identidade da Adobe Experience Platform fornece uma visão abrangente dos clientes e do comportamento deles ao unir as identidades de vários dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e de impacto em tempo real. Este tutorial fornece instruções sobre como monitorar fluxos de dados com identidades usando a interface do usuário Experience Platform.
title: Monitorar fluxos de dados para identidades na interface
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 9%

---

# Monitorar fluxos de dados para identidades na interface

O Serviço de identidade da Adobe Experience Platform fornece uma visão abrangente dos clientes e seu comportamento ao unir identidades entre dispositivos e sistemas, permitindo fornecer experiências digitais pessoais de impacto em tempo real.

O painel de monitoramento fornece uma representação visual da atividade dos dados nas identidades, incluindo o status das identidades dos seus dados. Este tutorial fornece instruções sobre como usar o painel de monitoramento para monitorar as identidades de seus dados usando a interface do usuário do Experience Platform, permitindo que você acompanhe o status do processamento de identidades.

## Introdução {#getting-started}

- [Fluxos de dados](../home.md): os fluxos de dados são uma representação de trabalhos de dados que movem dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para conjuntos de dados de destino, para [!DNL Identity] e [!DNL Profile] e para [!DNL Destinations].
   - [Execuções de fluxo de dados](../../sources/notifications.md): as execuções de fluxo de dados são os trabalhos agendados recorrentes com base na configuração de frequência dos fluxos de dados selecionados.
- [Serviço de identidade](../../identity-service/home.md): obtenha uma melhor visão dos clientes individuais e de seu comportamento unindo as identidades de vários dispositivos e sistemas.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Painel de monitoramento de identidades {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="Processamento de identidade"
>abstract="A visualização do processamento de identidade contém informações sobre registros assimilados ao serviço de identidade, incluindo o número de identidades adicionadas, gráficos criados e gráficos atualizados. Consulte o guia de definição de métricas para saber mais sobre métricas e gráficos."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="Detalhes de execução do fluxo de dados"
>abstract="A página Detalhes de execução do fluxo de dados exibe mais informações sobre a execução do fluxo de dados de identidade, incluindo a ID da organização e a ID de execução do fluxo de dados."

Para acessar o painel **[!UICONTROL Identidades]**, selecione **[!UICONTROL Monitoramento]** na navegação à esquerda. Uma vez na página **[!UICONTROL Monitoramento]**, selecione o cartão **[!UICONTROL Identidades]**.

![O cartão de Identidades. Informações sobre o número de registros recebidos, o número de registros assimilados e a taxa de sucesso são mostradas.](../assets/ui/monitor-identities/focus-card.png)

No painel **[!UICONTROL Identidades]** principal, o cartão **[!UICONTROL Identidades]** mostra informações sobre o número total de registros recebidos, o número de registros assimilados, bem como a taxa de êxito da assimilação de registros.

O painel em si contém métricas sobre Processamento de identidade. Por padrão, o painel mostrará os detalhes do Processamento de identidade das fontes da sua organização nas últimas 24 horas.

![O painel Identidades. Informações sobre o número de registros recebidos por origem são exibidas.](../assets/ui/monitor-identities/sources.png)

A página [!UICONTROL Processamento de identidade] contém informações sobre registros assimilados em [!DNL Identity Service], incluindo o número de identidades adicionadas, gráficos criados e gráficos atualizados.

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métricas de identidade | Descrição |
| ---------------- | ----------- |
| **[!UICONTROL Registros recebidos]** | O número de registros recebidos do data lake. |
| **[!UICONTROL Registros com falha]** | O número de registros que não foram assimilados na Platform devido a erros nos dados. |
| **[!UICONTROL Registros ignorados]** | O número de registros que foram assimilados, mas não em [!DNL Identity Service] porque havia apenas um identificador na linha de registro. |
| **[!UICONTROL Registros assimilados]** | O número de registros assimilados em [!DNL Identity Service]. |
| **[!UICONTROL Identidades adicionadas]** | O número de novos identificadores de rede adicionados a [!DNL Identity Service]. |
| **[!UICONTROL Gráficos criados]** | O número de novos gráficos de identidade de rede criados em [!DNL Identity Service]. |
| **[!UICONTROL Gráficos atualizados]** | O número de gráficos de identidade existentes atualizados com novas bordas. |
| **[!UICONTROL Total de fluxos de dados com falha]** | O número de execuções de fluxo de dados que falharam. |

Você pode selecionar o ícone de filtro ![Ícone de filtro](/help/images/icons/filter.png) ao lado do nome de origem para ver as informações de processamento de identidade dos fluxos de dados da origem selecionada.

![O ícone de filtro está realçado. A seleção desse ícone permite exibir os fluxos de dados da origem selecionada.](../assets/ui/monitor-identities/sources-filter.png)

Como alternativa, você pode selecionar **[!UICONTROL Fluxos de dados]** no botão de alternância para ver os detalhes de processamento da identidade dos fluxos de dados de sua organização nas últimas 24 horas.

![O painel Identidades. São exibidas informações sobre o número de identidades recebidas por fluxo de dados.](../assets/ui/monitor-identities/dataflows.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| -------| ----------- |
| **[!UICONTROL Fluxo de dados]** | O nome do fluxo de dados. |
| **[!UICONTROL Conjunto de dados]** | O nome do conjunto de dados no qual o fluxo de dados está inserindo. |
| **[!UICONTROL Nome do Source]** | O nome da origem à qual o fluxo de dados pertence. |
| **[!UICONTROL Registros recebidos]** | O número de registros recebidos do data lake. |
| **[!UICONTROL Registros com falha]** | O número de registros que não foram assimilados na Platform devido a erros nos dados. |
| **[!UICONTROL Registros ignorados]** | O número de registros que foram assimilados, mas não em [!DNL Identity Service] porque havia apenas um identificador na linha de registro. |
| **[!UICONTROL Registros assimilados]** | O número de registros assimilados em [!DNL Identity Service]. |
| **[!UICONTROL Total de registros]** | A contagem total de todos os registros, incluindo registros com falha, registros ignorados, identidades adicionadas e registros duplicados. |
| **[!UICONTROL Identidades adicionadas]** | O número de novos identificadores de rede adicionados a [!DNL Identity Service]. |
| **[!UICONTROL Gráficos criados]** | O número de novos gráficos de identidade de rede criados em [!DNL Identity Service]. |
| **[!UICONTROL Gráficos atualizados]** | O número de gráficos de identidade existentes atualizados com novas bordas. |
| **[!UICONTROL Total de fluxos de dados com falha]** | O número de execuções de fluxo de dados que falharam. |

Selecione o ícone de filtro ![filtro](/help/images/icons/filter.png) ao lado da hora de início da execução do fluxo de dados para ver mais informações sobre sua execução do fluxo de dados [!DNL Identity].

![O ícone de filtro está realçado. Selecionar este ícone permite exibir detalhes sobre o fluxo de dados selecionado.](../assets/ui/monitor-identities/dataflows-filter.png)

A página [!UICONTROL Detalhes da execução do fluxo de dados] exibe mais informações sobre a execução do fluxo de dados [!DNL Identity], incluindo a ID da organização e a ID de execução do fluxo de dados. Esta página também exibe o código de erro e a mensagem de erro correspondentes fornecidos por [!DNL Identity Service], caso ocorram erros no processo de assimilação.

![Um painel que mostra informações detalhadas sobre o fluxo de dados selecionado é exibido.](../assets/ui/monitor-identities/dataflow-run-details.png)

As seguintes métricas estão disponíveis para essa visualização de painel:

| Métrica | Descrição |
| -------| ----------- |
| **[!UICONTROL Registros recebidos]** | O número de registros recebidos do data lake. |
| **[!UICONTROL Registros com falha]** | O número de registros que não foram assimilados na Platform devido a erros nos dados. |
| **[!UICONTROL Registros ignorados]** | O número de registros que foram assimilados, mas não em [!DNL Identity Service] porque havia apenas um identificador na linha de registro. |
| **[!UICONTROL Registros assimilados]** | O número de registros assimilados em [!DNL Identity Service]. |
| **[!UICONTROL Identidades adicionadas]** | O número de novos identificadores de rede adicionados a [!DNL Identity Service]. |
| **[!UICONTROL Gráficos criados]** | O número de novos gráficos de identidade de rede criados em [!DNL Identity Service]. |
| **[!UICONTROL Gráficos atualizados]** | O número de gráficos de identidade existentes atualizados com novas bordas. |
| **[!UICONTROL Status]** | Define o status geral de um fluxo de dados. Os valores possíveis de status são: <ul><li>`Success`: Indica que um fluxo de dados está ativo e está assimilando dados de acordo com o agendamento fornecido.</li><li>`Failed`: indica que o processo de ativação de um fluxo de dados foi interrompido devido a erros. </li><li>`Processing`: indica que o fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados.</li></ul> |
| **[!UICONTROL Início da execução do fluxo de dados]** | A data e a hora em que o fluxo de dados começou a ser executado. |
| **[!UICONTROL Última atualização]** | A data e a hora da última atualização do fluxo de dados. |
| **[!UICONTROL Resumo do erro]** | Se a execução do fluxo de dados falhar, isso exibirá um código de erro e um resumo do por que a execução do fluxo de dados falhou. |
| **[!UICONTROL ID de execução do fluxo de dados]** | A ID da execução do fluxo de dados. |
| **[!UICONTROL ID da Organização IMS]** | A ID da organização à qual a execução do fluxo de dados pertence. |

Além disso, você pode selecionar a opção para visualizar os registros com falha ou os registros ignorados. A seção de erros inclui detalhes sobre o código de erro e o número de registros com falha ou excluídos.
