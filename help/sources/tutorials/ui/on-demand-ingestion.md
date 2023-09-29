---
title: Assimilação sob demanda para fluxos de dados de origens na interface
description: Saiba como criar fluxos de dados sob demanda para suas conexões de origem usando a interface do usuário Experience Platform.
source-git-commit: cea12160656ba0724789db03e62213022bacd645
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Assimilação sob demanda para fluxos de dados de origens na interface

Você pode usar a assimilação sob demanda para acionar uma iteração de execução de fluxo de um fluxo de dados existente usando o espaço de trabalho de origens na interface do usuário do Adobe Experience Platform.

Este documento fornece etapas sobre como criar fluxos de dados sob demanda para origens, bem como sobre como repetir execuções de fluxo que foram processadas ou que falharam.

>[!BEGINSHADEBOX]

**O que é uma execução de fluxo?**

As execuções de fluxo representam uma instância da execução do fluxo de dados. Por exemplo, se um fluxo de dados estiver programado para ser executado por hora às 9h, 10h e 11h, você terá três instâncias de um fluxo em execução. As execuções de fluxo são específicas para sua organização específica.

>[!ENDSHADEBOX]

## Introdução

Este documento requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Origens](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Fluxos de dados](../../../dataflows/home.md): um fluxo de dados é uma representação de trabalhos de dados que movem dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para conjuntos de dados de destino, para o Serviço de identidade, o Perfil do cliente em tempo real e para Destinos.
* [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Criar um fluxo de dados sob demanda {#create-a-dataflow-on-demand}

Navegue até a *[!UICONTROL Fluxos de dados]* do espaço de trabalho de origens. Aqui, localize o fluxo de dados que você deseja executar sob demanda e selecione as reticências (**`...`**) ao lado do nome do fluxo de dados.

![Uma lista de fluxos de dados no espaço de trabalho de origens.](../../images/tutorials/on-demand/select-dataflow.png)

Em seguida, selecione **[!UICONTROL Executar sob demanda]** no menu suspenso exibido.

![Um menu suspenso com a opção Executar sob demanda selecionada.](../../images/tutorials/on-demand/run-on-demand.png)

Configure a programação da sua assimilação sob demanda. Selecione o **[!UICONTROL Hora de início da assimilação]**, o **[!UICONTROL Hora inicial do intervalo de datas]**, e o **[!UICONTROL Hora final do intervalo de datas]**.

| Configuração de agendamento | Descrição |
| --- | --- |
| [!UICONTROL Hora de início da assimilação] | O horário agendado para o início da execução do fluxo por demanda. |
| [!UICONTROL Hora inicial do intervalo de datas] | A data e a hora a partir das quais os dados serão recuperados. |
| [!UICONTROL Hora final do intervalo de datas] | A data e a hora em que os dados serão recuperados. |

Selecionar **[!UICONTROL Agendar]** e aguarde alguns instantes para que seu fluxo de dados sob demanda seja acionado.

![A janela de configuração de programação para assimilação sob demanda.](../../images/tutorials/on-demand/configure-schedule.png)

Selecione o nome do fluxo de dados para exibir a atividade do fluxo de dados. Aqui você verá uma lista de execuções de fluxo de dados que foram processadas. Selecione uma execução de fluxo de dados e **[!UICONTROL Tentar novamente]** no painel direito para repetir a assimilação de uma iteração de execução de fluxo de dados selecionada.

![Uma lista de execuções de fluxo processadas para um fluxo de dados selecionado.](../../images/tutorials/on-demand/processed.png)

Selecionar **[!UICONTROL Agendado]** para ver uma lista de execuções de fluxo de dados programadas para assimilação futura.

![Uma lista de execuções de fluxo agendadas para um fluxo de dados selecionado.](../../images/tutorials/on-demand/scheduled.png)

## Próximas etapas

Ao ler este documento, você aprendeu a criar execuções de fluxo sob demanda para fluxos de dados de fontes existentes. Para obter mais informações sobre fontes, leia a [visão geral das origens](../../home.md)