---
title: Estender programações de exportação do conjunto de dados para fluxos de dados criados antes de novembro de 2024
description: Saiba como estender a programação de exportação para fluxos de dados de exportação de conjunto de dados criados antes de novembro de 2024 que deixarão de funcionar em 1º de setembro de 2025.
type: Tutorial
exl-id: a756886b-3f4b-4427-bd26-817221ba68aa
source-git-commit: 0da592dd2846ed0f1eeb31102842c8895cac6952
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# Estender programações de exportação do conjunto de dados para fluxos de dados criados antes de novembro de 2024

>[!IMPORTANT]
>
>**Ação necessária**: se sua organização tiver [fluxos de dados de exportação do conjunto de dados](export-datasets.md) criados antes de novembro de 2024, esses fluxos de dados deixarão de funcionar em 1º de setembro de 2025. Este guia explica como estender a programação de exportação além dessa data para os fluxos de dados que você deseja manter.

## Visão geral {#overview}

Na versão de [setembro de 2024 do Experience Platform](/help/release-notes/2024/september-2024.md#destinations), a Adobe introduziu uma data de término padrão de **1º de maio de 2025** para todos os fluxos de dados de exportação do conjunto de dados criados antes da versão de setembro de 2024.

**Esta data foi atualizada para 1º de setembro de 2025** para todos os fluxos de dados de exportação do conjunto de dados que foram criados **antes de novembro de 2024**.

Os fluxos de dados de exportação do conjunto de dados criados antes de novembro de 2024 interromperão a exportação de dados em **1º de setembro de 2025**, a menos que você estenda manualmente a data de expiração desses fluxos.

Se precisar que os fluxos de dados continuem exportando dados após **1º de setembro de 2025**, você deverá estender os agendamentos para cada destino para o qual está exportando conjuntos de dados, seguindo as etapas deste guia.

## Destinos afetados {#affected-destinations}

Sua organização pode ter fluxos de dados ativos de exportação de conjunto de dados enviando dados para os destinos listados abaixo. Siga as etapas nas próximas seções e assista ao vídeo explicativo para saber como identificar quais conjuntos de dados estão definidos para expirar.

* [[!DNL Azure Data Lake Storage Gen2]](../catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../catalog/cloud-storage/sftp.md#changelog)
* [[!DNL Marketo Measure Ultimate]](../catalog/adobe/marketo-measure-ultimate.md)

## Tutorial em vídeo {#video}

Assista ao vídeo abaixo para obter uma demonstração passo a passo de como identificar exportações de conjunto de dados com datas de término futuras e estender a programação de exportação para os fluxos de dados que você deseja manter.

>[!VIDEO](https://video.tv.adobe.com/v/3470518/)

## Etapa 1: identificar fluxos de dados afetados {#identify-dataflows}

Antes de estender a programação de exportação para seus fluxos de dados de exportação do conjunto de dados, primeiro é necessário identificar quais fluxos de dados são afetados pela data de expiração futura. Siga as etapas abaixo para localizar fluxos de dados que exigem ação.

1. Vá para **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** na interface do Experience Platform.
2. Selecione **[!UICONTROL Ativar]** em um destino que tenha fluxos de dados de exportação de conjunto de dados ativos.

   >[!TIP]
   >
   >Use o filtro **[!UICONTROL Tipos de Dados]** no lado esquerdo do catálogo para filtrar os destinos disponíveis por **[!UICONTROL Conjuntos de Dados]**.

3. Selecione o tipo de dados **[!UICONTROL Conjuntos de dados]** para exibir apenas os fluxos de dados com exportações de conjuntos de dados.
   ![Captura de tela mostrando como filtrar fluxos de dados por tipo de dados.](/help/destinations/assets/ui/export-datasets/dataset-type.png)
4. Selecione o cabeçalho da coluna **[!UICONTROL Criado]** e escolha **[!UICONTROL Classificar em Ordem Crescente]** para ver os fluxos de dados mais antigos.
   ![Captura de tela mostrando como classificar fluxos de dados em ordem crescente.](/help/destinations/assets/ui/export-datasets/sort-ascending.png)
5. Identifique qual dos fluxos de dados criados antes de novembro de 2024 você deseja manter.

## Etapa 2: acessar o fluxo de trabalho dos conjuntos de dados de exportação {#access-workflow}

Para cada fluxo de dados que deseja manter, é necessário acessar o fluxo de trabalho Exportar conjuntos de dados para modificar o agendamento.

1. Selecione o nome do fluxo de dados na coluna **[!UICONTROL Name]**. Você será direcionado à página **[!UICONTROL Execuções de fluxo de dados]**.
2. Nesta página, selecione a opção **[!UICONTROL Exportar conjuntos de dados]**.
   ![Captura de tela mostrando a opção de exportação de conjuntos de dados na página de execuções de fluxo de dados.](/help/destinations/assets/ui/export-datasets/export-datasets-option.png)
3. Na página **[!UICONTROL Selecionar conjuntos de dados]**, selecione **[!UICONTROL Avançar]**. Não é necessário adicionar novos conjuntos de dados ao fluxo de dados.
4. Você será direcionado à página **[!UICONTROL Agendamento]**, na qual também poderá ver uma notificação informando a data de expiração da exportação do conjunto de dados.
   ![Fluxos de dados de exportação do conjunto de dados com notificação de expiração](/help/destinations/assets/ui/export-datasets/dataset-export-notification.png)

## Etapa 3: estender o agendamento de exportação {#extend-export-schedule}

Agora você pode modificar a programação de exportação para estender-se além de 1º de setembro de 2025.

1. Selecione **[!UICONTROL Editar agendamento]**.
   ![Captura de tela da etapa Agendamento mostrando o botão Editar agendamento.](/help/destinations/assets/ui/export-datasets/edit-schedule.png)
2. Selecione um novo cronograma de exportação e, em seguida, **[!UICONTROL Salvar]**.
   ![Captura de tela da etapa Agendamento mostrando as opções de agendamento.](/help/destinations/assets/ui/export-datasets/edit-schedule-calendar.png)

   >[!TIP]
   >
   >Consulte a [documentação de exportação do conjunto de dados](export-datasets.md#scheduling) para obter orientações detalhadas sobre como configurar agendamentos de exportação do conjunto de dados.

## O que acontece se eu perder o prazo final de 1º de setembro de 2025? {#missed-deadline}

Se os fluxos de dados de exportação do seu conjunto de dados expiraram em 1º de setembro de 2025 e você ainda deseja estendê-los, siga as etapas nas seções acima para estender sua programação.

Se você estender o agendamento de exportação em 30 dias (ou menos se o [tempo de vida definido no conjunto de dados exportado](/help/catalog/datasets/experience-event-dataset-retention-ttl-guide.md) for inferior a 30 dias), ainda será possível obter um preenchimento retroativo dos dados que não foram exportados entre 1º de setembro e a data em que você reabilitar a exportação. Ao definir uma nova hora de término, haverá *não* uma exportação de arquivo completa primeiro. Em vez disso, as exportações continuarão incrementalmente de onde pararam em 1º de setembro.