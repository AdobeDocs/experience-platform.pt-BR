---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;dataflows;destinations
description: Os destinos permitem ativar seus dados da Adobe Experience Platform para inúmeros parceiros externos. Este tutorial fornece instruções sobre como você pode monitorar os fluxos de dados para seus destinos usando a interface do usuário do Experience Platform.
solution: Experience Platform
title: Monitorar fluxos de dados
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 12a6682b6e28e656899aee5c38d3bb4a84bcdd2f
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---


# Monitorar fluxos de dados para destinos na interface do usuário

Os destinos permitem ativar seus dados da Adobe Experience Platform para inúmeros parceiros externos. Este tutorial fornece instruções sobre como você pode monitorar os fluxos de dados para seus destinos usando a interface do usuário do Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Destinos](../../destinations/home.md): Os destinos são integrações pré-criadas com aplicativos comumente usados que permitem a ativação contínua de dados da Plataforma para campanhas de marketing entre canais, campanhas de email, anúncios direcionados e muitos outros casos de uso.
- [Caixas de proteção](../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

## Monitorar fluxos de dados

Na área de trabalho **[!UICONTROL Destinos]** na interface do usuário da plataforma, navegue até a guia **[!UICONTROL Procurar]** e selecione o nome de um destino que deseja visualização.

![](../assets/ui/monitor-destinations/select-destination.png)

Uma lista de fluxos de dados existentes é exibida. Nesta página há uma lista de fluxos de dados visualizáveis, incluindo informações sobre seu destino, nome de usuário, número de fluxos de dados e status.

Consulte a tabela a seguir para obter mais informações sobre status:

| Status | Descrição |
| ------ | ----------- |
| Ativado | O `Enabled` status indica que um fluxo de dados está ativo e está ingerindo dados de acordo com o agendamento fornecido. |
| Desativado | O `Disabled` status indica que um fluxo de dados está inativo e não está ingerindo dados. |
| Processamento | O `Processing` status indica que um fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados. |
| Erro | O `Error` status indica que o processo de ativação de um fluxo de dados foi interrompido. |

## [!UICONTROL Execuções do Dataflow]

A guia [!UICONTROL Dataflow executa] fornece dados de métricas em suas execuções de fluxo de dados para destinos em lote. Uma lista de execuções individuais e suas métricas específicas é exibida, juntamente com os seguintes totais para registros de perfis:

- **[!UICONTROL Registros de perfil ativados]**: A contagem total de registros de perfis criados ou atualizados para ativação.
- **[!UICONTROL Registros de perfil ignorados]**:  A contagem total de registros de perfis ignorados para ativação com base em saídas de perfis ou atributos ausentes.

![](../assets/ui/monitor-destinations/dataflow-runs.png)

>[!NOTE]
>
>As execuções de fluxo de dados são geradas com base na frequência de programação do fluxo de dados de destino. Uma execução de fluxo de dados separada é realizada para cada política de mesclagem aplicada a um segmento.

Para visualização dos detalhes de uma execução específica do fluxo de dados, selecione o tempo de start da execução na lista. A página de detalhes de uma execução de fluxo de dados contém informações adicionais, como o tamanho dos dados processados e uma lista de erros que ocorreram com detalhes do diagnóstico de erros.

![](../assets/ui/monitor-destinations/dataflow.png)