---
keywords: Experience Platform, home, tópicos populares, monitorar identidades, monitorar fluxos de dados, fluxos de dados, identidades;
description: O serviço de identidade da Adobe Experience Platform fornece uma visão abrangente dos clientes e do comportamento deles ao unir identidades entre dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real. Este tutorial fornece instruções sobre como você pode monitorar fluxos de dados com identidades usando a interface do usuário do Experience Platform.
title: Monitorar fluxos de dados para identidades na interface do usuário
topic-legacy: overview
type: Tutorial
source-git-commit: 3018ee005c96e3905ae8dab24cca901cf48847ea
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 1%

---


# Monitorar fluxos de dados para identidades na interface do usuário

O serviço de identidade da Adobe Experience Platform fornece uma visão abrangente dos clientes e do comportamento deles ao unir identidades entre dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

O painel de monitoramento fornece uma representação visual da atividade dos dados nas identidades, incluindo o status das identidades dos dados. Este tutorial fornece instruções sobre como você pode usar o painel de monitoramento para monitorar as identidades de seus dados usando a interface do usuário do Experience Platform, permitindo rastrear o status do processamento de identidade.

## Introdução {#getting-started}

- [Fluxos de dados](../home.md): Os fluxos de dados são uma representação de trabalhos de dados que movem dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de destino, para [!DNL Identity] e [!DNL Profile]e para [!DNL Destinations].
   - [Execuções do fluxo de dados](../../sources/notifications.md): As execuções de fluxo de dados são trabalhos agendados recorrentes com base na configuração de frequência de fluxos de dados selecionados.
- [Serviço de identidade](../../identity-service/home.md): Obtenha uma melhor visão de clientes individuais e seu comportamento ao unir identidades em dispositivos e sistemas.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Painel de monitoramento de identidades {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="Processamento de identidade"
>abstract="A exibição de processamento de identidade contém informações sobre registros assimilados ao serviço de identidade, incluindo o número de identidades adicionadas, gráficos criados e gráficos atualizados. Consulte o guia de definição de métricas para saber mais sobre métricas e gráficos."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="Detalhes da execução do fluxo de dados"
>abstract="A página Detalhes de execução do fluxo de dados exibe mais informações sobre a execução do fluxo de dados de identidade, incluindo a ID da organização e a ID de execução do fluxo de dados."

Para acessar o **[!UICONTROL Identidades]** painel, selecione **[!UICONTROL Monitoramento]** no painel de navegação esquerdo. Uma vez no **[!UICONTROL Monitoramento]** selecione o **[!UICONTROL Identidades]** cartão.

![O cartão Identities . Informações sobre o número de registros recebidos, o número de registros assimilados e a taxa de sucesso são mostradas.](../assets/ui/monitor-identities/focus-card.png)

No principal **[!UICONTROL Identidades]** painel, o **[!UICONTROL Identidades]** cartão mostra informações sobre o número total de registros recebidos, o número de registros assimilados, bem como a taxa de sucesso da assimilação de registros.

O próprio painel contém métricas sobre o processamento de identidade. Por padrão, o painel mostrará os detalhes de processamento da identidade das fontes de sua organização nas últimas 24 horas.

![O painel Identidades. As informações sobre o número de registros recebidos por fonte são exibidas.](../assets/ui/monitor-identities/sources.png)

O [!UICONTROL Processamento de identidade] contém informações sobre registros assimilados a [!DNL Identity Service], incluindo o número de identidades adicionadas, gráficos criados e gráficos atualizados.

As métricas a seguir estão disponíveis para esta exibição de painel:

| Métricas de identidade | Descrição |
| ---------------- | ----------- |
| **[!UICONTROL Registros recebidos]** | O número de registros recebidos do lago de dados. |
| **[!UICONTROL Falha nos registros]** | O número de registros que não foram assimilados na Platform devido a erros nos dados. |
| **[!UICONTROL Registros ignorados]** | O número de registros que foram assimilados, mas não em [!DNL Identity Service] porque havia apenas um identificador na linha de registro. |
| **[!UICONTROL Registros assimilados]** | O número de registros assimilados em [!DNL Identity Service]. |
| **[!UICONTROL Identidades adicionadas]** | O número de novos identificadores líquidos adicionados a [!DNL Identity Service]. |
| **[!UICONTROL Gráficos criados]** | O número de novos gráficos de identidade líquidos criados em [!DNL Identity Service]. |
| **[!UICONTROL Gráficos atualizados]** | O número de gráficos de identidade existentes atualizados com novas bordas. |
| **[!UICONTROL Total de fluxos de dados com falha]** | O número de execuções de fluxo de dados que falharam. |

Você pode selecionar o ícone de filtro ![Ícone Filtro](../assets/ui/monitor-identities/filter.png) ao lado do nome da origem para ver as informações de processamento de identidade para os fluxos de dados da origem selecionada.

![O ícone de filtro é realçado. Selecionar esse ícone permite exibir os fluxos de dados da fonte selecionada.](../assets/ui/monitor-identities/sources-filter.png)

Como alternativa, você pode selecionar **[!UICONTROL Fluxos de dados]** no botão de alternância para ver os detalhes de processamento de identidade dos fluxos de dados da sua organização nas últimas 24 horas.

![O painel Identidades. São exibidas informações sobre o número de identidades recebidas por fluxo de dados.](../assets/ui/monitor-identities/dataflows.png)

As métricas a seguir estão disponíveis para esta exibição de painel:

| Métrica | Descrição |
| -------| ----------- |
| **[!UICONTROL Fluxo de dados]** | O nome do fluxo de dados. |
| **[!UICONTROL Conjunto de dados]** | O nome do conjunto de dados ao qual o fluxo de dados está sendo inserido. |
| **[!UICONTROL Nome da origem]** | O nome da origem à qual o fluxo de dados pertence. |
| **[!UICONTROL Registros recebidos]** | O número de registros recebidos do lago de dados. |
| **[!UICONTROL Falha nos registros]** | O número de registros que não foram assimilados na Platform devido a erros nos dados. |
| **[!UICONTROL Registros ignorados]** | O número de registros que foram assimilados, mas não em [!DNL Identity Service] porque havia apenas um identificador na linha de registro. |
| **[!UICONTROL Registros assimilados]** | O número de registros assimilados em [!DNL Identity Service]. |
| **[!UICONTROL Total de registros]** | A contagem total de todos os registros, incluindo registros com falha, registros ignorados, identidades adicionadas e registros duplicados. |
| **[!UICONTROL Identidades adicionadas]** | O número de novos identificadores líquidos adicionados a [!DNL Identity Service]. |
| **[!UICONTROL Gráficos criados]** | O número de novos gráficos de identidade líquidos criados em [!DNL Identity Service]. |
| **[!UICONTROL Gráficos atualizados]** | O número de gráficos de identidade existentes atualizados com novas bordas. |
| **[!UICONTROL Total de fluxos de dados com falha]** | O número de execuções de fluxo de dados que falharam. |

Selecione o ícone de filtro ![filter](../assets/ui/monitor-identities/filter.png) além do tempo de início da execução do fluxo de dados para ver mais informações sobre o [!DNL Identity] execução do fluxo de dados.

![O ícone de filtro é realçado. Selecionar esse ícone permite exibir detalhes sobre o fluxo de dados selecionado.](../assets/ui/monitor-identities/dataflows-filter.png)

O [!UICONTROL Detalhes da execução do fluxo de dados] página exibe mais informações sobre sua [!DNL Identity] execução do fluxo de dados, incluindo a ID da organização e a ID de execução do fluxo de dados. Esta página também exibe o código de erro e a mensagem de erro correspondentes fornecidos pelo [!DNL Identity Service], caso ocorra algum erro no processo de ingestão.

![Um painel que mostra informações detalhadas sobre o fluxo de dados selecionado é exibido.](../assets/ui/monitor-identities/dataflow-run-details.png)

As métricas a seguir estão disponíveis para esta exibição de painel:

| Métrica | Descrição |
| -------| ----------- |
| **[!UICONTROL Registros recebidos]** | O número de registros recebidos do lago de dados. |
| **[!UICONTROL Falha nos registros]** | O número de registros que não foram assimilados na Platform devido a erros nos dados. |
| **[!UICONTROL Registros ignorados]** | O número de registros que foram assimilados, mas não em [!DNL Identity Service] porque havia apenas um identificador na linha de registro. |
| **[!UICONTROL Registros assimilados]** | O número de registros assimilados em [!DNL Identity Service]. |
| **[!UICONTROL Identidades adicionadas]** | O número de novos identificadores líquidos adicionados a [!DNL Identity Service]. |
| **[!UICONTROL Gráficos criados]** | O número de novos gráficos de identidade líquidos criados em [!DNL Identity Service]. |
| **[!UICONTROL Gráficos atualizados]** | O número de gráficos de identidade existentes atualizados com novas bordas. |
| **[!UICONTROL Status]** | Define o status geral de um fluxo de dados. Os valores de status possíveis são: <ul><li>`Success`: Indica que um fluxo de dados está ativo e está assimilando dados de acordo com o cronograma que foi fornecido.</li><li>`Failed`: Indica que o processo de ativação de um fluxo de dados foi interrompido devido a erros. </li><li>`Processing`: Indica que o fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados.</li></ul> |
| **[!UICONTROL Início da execução do fluxo de dados]** | A data e a hora em que o fluxo de dados começou a ser executado. |
| **[!UICONTROL Última atualização]** | A data e a hora em que o fluxo de dados foi atualizado pela última vez. |
| **[!UICONTROL Resumo do erro]** | Se a execução do fluxo de dados falhar, isso exibirá um código de erro e um resumo de por que a execução do fluxo de dados falhou. |
| **[!UICONTROL ID de execução do fluxo de dados]** | A ID da execução do fluxo de dados. |
| **[!UICONTROL ID da organização IMS]** | A ID da organização à qual a execução do fluxo de dados pertence. |

Além disso, você pode selecionar a alternância para exibir os registros que falharam ou os registros ignorados. A seção errors inclui detalhes sobre o código de erro e o número de registros que falharam ou foram excluídos.