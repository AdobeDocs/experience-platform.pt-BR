---
title: Assimilação sob demanda para fluxos de dados de origens na interface
description: Saiba como criar fluxos de dados sob demanda para suas conexões de origem usando a interface do usuário do Experience Platform.
exl-id: e5a70044-2484-416a-8098-48e6d99c2d98
source-git-commit: fabacf273fb5774ddcee42d0cdcf12281eb0216b
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# Assimilação sob demanda para fluxos de dados de origens na interface

Você pode usar a assimilação sob demanda para acionar uma iteração de execução de fluxo de um fluxo de dados existente usando o espaço de trabalho de origens na interface do usuário do Adobe Experience Platform.

Este documento fornece etapas sobre como criar fluxos de dados sob demanda para origens, bem como sobre como repetir execuções de fluxo que foram processadas ou que falharam.

>[!BEGINSHADEBOX]

**O que é uma execução de fluxo?**

As execuções de fluxo representam uma instância da execução do fluxo de dados. Por exemplo, se um fluxo de dados estiver agendado para ser executado por hora às 9h00, 10h10 e 11h20, você terá três instâncias de um fluxo em execução. :00:00:00 As execuções de fluxo são específicas para sua organização específica.

>[!ENDSHADEBOX]

## Introdução

>[!NOTE]
>
>Para criar uma execução de fluxo, primeiro você deve ter a ID de fluxo de um fluxo de dados programado para assimilação única.

Este documento requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Fluxos de dados](../../../dataflows/home.md): um fluxo de dados é uma representação de trabalhos de dados que movem dados pela Experience Platform. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para conjuntos de dados de destino, para o Serviço de identidade, o Perfil do cliente em tempo real e para Destinos.
* [Sandboxes](../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Criar um fluxo de dados sob demanda {#create-a-dataflow-on-demand}

Navegue até a guia *[!UICONTROL Fluxos de Dados]* do espaço de trabalho de fontes. Aqui, localize o fluxo de dados que você deseja executar sob demanda e selecione as reticências (**`...`**) ao lado do nome do fluxo de dados.

![Uma lista de fluxos de dados no espaço de trabalho de fontes.](../../images/tutorials/on-demand/select-dataflow.png)

Em seguida, selecione **[!UICONTROL Executar sob demanda]** no menu suspenso exibido.

![Um menu suspenso com a opção Executar sob demanda selecionada.](../../images/tutorials/on-demand/run-on-demand.png)

Configure a programação da sua assimilação sob demanda. Selecione a **[!UICONTROL Hora de início da assimilação]**, a **[!UICONTROL Hora de início do intervalo de datas]** e a **[!UICONTROL Hora de término do intervalo de datas]**.

| Configuração de agendamento | Descrição |
| --- | --- |
| [!UICONTROL Hora de início da assimilação] | O horário agendado para o início da execução do fluxo por demanda. |
| [!UICONTROL Hora de início do intervalo de datas] | A data e a hora a partir das quais os dados serão recuperados. |
| [!UICONTROL Hora de término do intervalo de datas] | A data e a hora em que os dados serão recuperados. |

Selecione **[!UICONTROL Agendar]** e aguarde alguns momentos para o fluxo de dados sob demanda ser acionado.

![A janela de configuração de agendamento para assimilação sob demanda.](../../images/tutorials/on-demand/configure-schedule.png)

Selecione o nome do fluxo de dados para exibir a atividade do fluxo de dados. Aqui você verá uma lista de execuções de fluxo de dados que foram processadas. Você pode executar novamente iterações individuais das execuções do fluxo de dados, independentemente de terem falhado ou sido bem-sucedidas. Para iterações de execução que falharam, você pode usar **[!UICONTROL Repetir]** para iniciar a execução novamente após diagnosticar e resolver quaisquer erros que tenham sido encontrados durante o processo de criação.

>[!TIP]
>
>A repetição de uma execução de fluxo processará somente arquivos com carimbos de data e hora que se enquadrem na faixa da execução original.

![Uma lista de execuções de fluxo processadas para um fluxo de dados selecionado.](../../images/tutorials/on-demand/processed.png)

Selecione **[!UICONTROL Agendado]** para ver uma lista de execuções de fluxo de dados agendadas para assimilação futura.

![Uma lista de execuções de fluxo agendadas para um fluxo de dados selecionado.](../../images/tutorials/on-demand/scheduled.png)

## Próximas etapas

Ao ler este documento, você aprendeu a criar execuções de fluxo sob demanda para fluxos de dados de fontes existentes. Para obter mais informações sobre fontes, leia a [visão geral das fontes](../../home.md)
