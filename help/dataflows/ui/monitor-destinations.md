---
keywords: Experience Platform, home, tópicos populares, monitorar contas, monitorar fluxos de dados, fluxos de dados, destinos
description: Os destinos permitem ativar seus dados do Adobe Experience Platform para inúmeros parceiros externos. Este tutorial fornece instruções sobre como você pode monitorar os fluxos de dados para seus destinos usando a interface do usuário do Experience Platform.
solution: Experience Platform
title: Monitorar fluxos de dados para destinos na interface do usuário
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 1d40ef02bd0bdb48bb999c3308f78824f75e3459
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---

# Monitorar fluxos de dados para destinos na interface do usuário

Os destinos permitem ativar seus dados do Adobe Experience Platform para inúmeros parceiros externos. Este tutorial fornece instruções sobre como você pode monitorar os fluxos de dados para seus destinos usando a interface do usuário do Experience Platform.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Destinos](../../destinations/home.md): Os destinos são integrações pré-criadas com aplicativos comumente usados que permitem a ativação simplificada de dados da Platform para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.
- [Sandboxes](../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Monitorar fluxos de dados

Na área de trabalho **[!UICONTROL Destinations]** na interface do usuário da plataforma, navegue até a guia **[!UICONTROL Browse]** e selecione o nome de um destino que deseja visualizar.

![](../assets/ui/monitor-destinations/select-destination.png)

Uma lista de fluxos de dados existentes é exibida. Nesta página, há uma lista de fluxos de dados visualizáveis, incluindo informações sobre seu destino, nome de usuário, número de fluxos de dados e status.

Consulte a tabela a seguir para obter mais informações sobre status:

| Status | Descrição |
| ------ | ----------- |
| Ativado | O status `Enabled` indica que um fluxo de dados está ativo e assimila dados de acordo com o agendamento fornecido. |
| Desativado | O status `Disabled` indica que um fluxo de dados está inativo e não está assimilando dados. |
| Processamento | O status `Processing` indica que um fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados. |
| Erro | O status `Error` indica que o processo de ativação de um fluxo de dados foi interrompido. |

## O fluxo de dados é executado para destinos de transmissão

Para destinos de transmissão, a guia [!UICONTROL Dataflow executa] fornece uma atualização por hora para dados de métrica em suas execuções de fluxo de dados. As estatísticas mais proeminentes rotuladas são para identidades.

As identidades representam as diferentes facetas de um perfil. Por exemplo, se um perfil contiver um número de telefone e um endereço de email, esse perfil terá duas identidades.

Uma lista de execuções individuais e suas métricas específicas é exibida, juntamente com os seguintes totais para identidades:

- **[!UICONTROL Identidades ativadas]**: A contagem total de identidades de perfil que foram criadas ou atualizadas para ativação.
- **[!UICONTROL Identidades excluídas]**: O número total de identidades de perfil que são ignoradas para ativação com base em atributos ausentes e violação de consentimento.
- **[!UICONTROL Falha]** de identidades: O número total de identidades de perfil que não estão ativadas para o destino devido a erros.

![](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Cada execução de fluxo de dados individual mostra os seguintes detalhes:

- **[!UICONTROL Início]** da execução do fluxo de dados: A hora em que a execução do fluxo de dados começou.
- **[!UICONTROL Tempo]** de processamento: O tempo necessário para o processamento do fluxo de dados.
- **[!UICONTROL Perfis recebidos]**: O número total de perfis recebidos no fluxo de dados.
- **[!UICONTROL Identidades ativadas]**: O número total de identidades de perfil que foram ativadas com êxito para o destino selecionado.
- **[!UICONTROL Identidades excluídas]**: O número total de identidades de perfil que são excluídas para ativação com base em atributos ausentes e violação de consentimento.
- **[!UICONTROL Identidades]** falharam. O número total de identidades de perfil que não estão ativadas para o destino devido a erros.
- **[!UICONTROL Taxa]** de ativação: A porcentagem de identidades recebidas que foram ativadas ou ignoradas com êxito. A fórmula a seguir demonstra como esse valor é calculado:
   ![](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Status]**: Representa o estado em que o fluxo de dados está: Concluído   ou  [!UICONTROL Processando].  Concluído significa que todas as identidades para a execução do fluxo de dados correspondente foram assimiladas dentro do período de uma hora.  Processamento significa que a execução do fluxo de dados ainda não foi concluída.

Para exibir os detalhes de uma execução específica do fluxo de dados, selecione a hora de início da execução na lista.

A página de detalhes de uma execução do fluxo de dados contém informações adicionais, como o número de perfis recebidos, o número de identidades ativadas, o número de identidades falhadas e o número de identidades excluídas.

![](../assets/ui/monitor-destinations/dataflow-details-stream.png)

A página de detalhes também exibe uma lista de identidades que falharam e identidades que foram excluídas. As informações das identidades com falha e excluída são exibidas, incluindo código de erro, contagem de identidades e descrição. Por padrão, a lista exibe as identidades com falha. Para mostrar identidades ignoradas, selecione a opção **[!UICONTROL Identities excluded]**.

![](../assets/ui/monitor-destinations/dataflow-records-stream.png)

## O fluxo de dados é executado para destinos em lote

Para destinos em lote, a guia [!UICONTROL Dataflow executa] fornece dados de métrica sobre as execuções do fluxo de dados. Uma lista de execuções individuais e suas métricas específicas é exibida, juntamente com os seguintes totais para identidades:

- **[!UICONTROL Identidades ativadas]**: A contagem de identidades de perfil individuais ativadas com êxito para o destino selecionado.
- **[!UICONTROL Identidades excluídas]**: A contagem de identidades de perfil individuais excluídas para ativação do destino selecionado, com base nos atributos ausentes e na violação de consentimento.

![](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Cada execução de fluxo de dados individual mostra os seguintes detalhes:

- **[!UICONTROL Início]** da execução do fluxo de dados: A hora em que a execução do fluxo de dados começou.
- **[!UICONTROL Tempo]** de processamento: O tempo que levou para a execução do fluxo de dados ser processada.
- **[!UICONTROL Perfis recebidos]**: O número total de perfis recebidos no fluxo de dados. Esse valor é atualizado a cada 60 minutos.
- **[!UICONTROL Identidades ativadas]**: O número total de identidades de perfil que foram ativadas com êxito para o destino selecionado.
- **[!UICONTROL Identidades excluídas]**: O número total de identidades de perfil que são excluídas para ativação com base em atributos ausentes e violação de consentimento.
- **[!UICONTROL Status]**: Representa o estado em que o fluxo de dados está. Pode ser um dos três estados: [!UICONTROL Sucesso], [!UICONTROL Falha] e [!UICONTROL Processamento].  Sucesso significa que o fluxo de dados está ativo e está assimilando dados de acordo com o agendamento fornecido.  Falhou significa que a ativação de dados foi suspensa devido a erros.  Processamento significa que o fluxo de dados ainda não está ativo e geralmente é encontrado quando um novo fluxo de dados é criado.

Para exibir detalhes de uma execução específica do fluxo de dados, selecione a hora de início da execução na lista.

>[!NOTE]
>
>As execuções de fluxo de dados são geradas com base na frequência de agendamento do fluxo de dados de destino. Uma execução de fluxo de dados separada é feita para cada política de mesclagem aplicada a um segmento.

A página de detalhes de um fluxo de dados, além dos detalhes mostrados na lista de fluxos de dados, exibe informações mais específicas sobre o fluxo de dados:

- **[!UICONTROL Tamanho dos dados]**: O tamanho do fluxo de dados que está sendo assimilado.
- **[!UICONTROL Total de arquivos]**: O número total de arquivos assimilados no fluxo de dados.
- **[!UICONTROL Última atualização]**: A hora em que a execução do fluxo de dados foi atualizada pela última vez.

![](../assets/ui/monitor-destinations/dataflow-batch.png)

A página de detalhes também exibe uma lista de identidades que falharam e identidades que foram excluídas. As informações das identidades com falha e excluída são exibidas, incluindo o código de erro e a descrição. Por padrão, a lista exibe as identidades com falha. Para mostrar identidades excluídas, selecione a opção **[!UICONTROL Identities excluded]**.

![](../assets/ui/monitor-destinations/dataflow-records-batch.png)


## Próximas etapas

Seguindo este guia, agora você sabe como monitorar os fluxos de dados para destinos de lote e streaming, incluindo todas as informações relevantes, como tempo de processamento, taxa de ativação e status. Para saber mais sobre fluxos de dados na Platform, leia a [visão geral dos fluxos de dados](../home.md). Para saber mais sobre destinos, leia a [visão geral de destinos](../../destinations/home.md).