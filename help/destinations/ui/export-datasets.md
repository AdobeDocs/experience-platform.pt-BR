---
title: Exportar conjuntos de dados para destinos de armazenamento na nuvem
type: Tutorial
description: Saiba como exportar conjuntos de dados do Adobe Experience Platform para o local de armazenamento em nuvem de sua preferência.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 4%

---

# Exportar conjuntos de dados para destinos de armazenamento na nuvem

>[!AVAILABILITY]
>
>* Essa funcionalidade está disponível para clientes que compraram o pacote Real-Time CDP Prime ou Ultimate, Adobe Journey Optimizer ou Customer Journey Analytics. Entre em contato com o representante da Adobe para obter mais informações.

Este artigo explica o workflow necessário para exportar [conjuntos de dados](/help/catalog/datasets/overview.md) do Adobe Experience Platform para o local de armazenamento em nuvem de sua preferência, como [!DNL Amazon S3], locais SFTP ou [!DNL Google Cloud Storage] usando a interface de usuário do Experience Platform.

Você também pode usar as APIs de Experience Platform para exportar conjuntos de dados. Leia o [exportar tutorial da API de conjuntos de dados](/help/destinations/api/export-datasets.md) para obter mais informações.

## Conjuntos de dados disponíveis para exportação {#datasets-to-export}

Os conjuntos de dados que você pode exportar variam com base no aplicativo Experience Platform (Real-Time CDP, Adobe Journey Optimizer), no nível (Prime ou Ultimate) e em qualquer complemento que você tenha adquirido (por exemplo: Data Distiller).

Entenda, na tabela abaixo, quais tipos de conjunto de dados você pode exportar dependendo do aplicativo, da camada do produto e de qualquer complemento adquirido:

<table>
<thead>
  <tr>
    <th>Aplicativo/Complemento</th>
    <th>Nível</th>
    <th>Conjuntos de dados disponíveis para exportação</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Real-Time CDP</td>
    <td>Prime</td>
    <td>Conjuntos de dados de Perfil e Evento de experiência criados na interface do Experience Platform após assimilar ou coletar dados por meio de Fontes, SDK da Web, SDK móvel, Conector de dados do Analytics e Audience Manager.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td><ul><li>Conjuntos de dados de Perfil e Evento de experiência criados na interface do Experience Platform após assimilar ou coletar dados por meio de Fontes, SDK da Web, SDK móvel, Conector de dados do Analytics e Audience Manager.</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets">Conjunto de dados Instantâneo do perfil gerado pelo sistema</a>.</li></td>
  </tr>
  <tr>
    <td rowspan="2">Adobe Journey Optimizer</td>
    <td>Prime</td>
    <td>Consulte a <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a> documentação.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td>Consulte a <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a> documentação.</td>
  </tr>
  <tr>
    <td>Distiller de dados</td>
    <td>Data Distiller (Complemento)</td>
    <td>Conjuntos de dados derivados criados por meio do Serviço de consulta.</td>
  </tr>
</tbody>
</table>

## Destinos compatíveis {#supported-destinations}

Atualmente, você pode exportar conjuntos de dados para os destinos de armazenamento na nuvem destacados na captura de tela e listados abaixo.

![Destinos que oferecem suporte a exportações de conjunto de dados](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Quando ativar públicos ou exportar conjuntos de dados {#when-to-activate-audiences-or-activate-datasets}

Alguns destinos baseados em arquivo no catálogo do Experience Platform são compatíveis com a ativação de público-alvo e a exportação de conjunto de dados.

* Considere ativar públicos-alvo quando quiser que seus dados sejam estruturados em perfis agrupados por interesses ou qualificações de público-alvo.
* Como alternativa, considere as exportações de conjunto de dados ao procurar exportar conjuntos de dados brutos, que não são agrupados ou estruturados por interesses ou qualificações de público-alvo. Você pode usar esses dados para relatórios, fluxos de trabalho de ciência de dados e muitos outros casos de uso. Por exemplo, como administrador, engenheiro de dados ou analista, você pode exportar dados do Experience Platform para sincronizar com o data warehouse, usar em ferramentas de análise de BI, ferramentas de aprendizado de máquina na nuvem externas ou armazenar em seu sistema para necessidades de armazenamento de longo prazo.

Este documento contém todas as informações necessárias para exportar conjuntos de dados. Se desejar ativar *públicos* para destinos de marketing por email ou armazenamento na nuvem, leia [Ativar dados do público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md).

## Pré-requisitos {#prerequisites}

Para exportar conjuntos de dados para destinos de armazenamento na nuvem, é necessário ter o [conectado a um destino](./connect-destination.md). Se ainda não tiver feito isso, acesse o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar.

### Permissões necessárias {#permissions}

Para exportar conjuntos de dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Exibir conjuntos de dados]**, e **[!UICONTROL Gerenciar e ativar destinos do conjunto de dados]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para garantir que você tenha as permissões necessárias para exportar conjuntos de dados e que o destino seja compatível com a exportação de conjuntos de dados, navegue pelo catálogo de destinos. Se um destino tiver um **[!UICONTROL Ativar]** ou um **[!UICONTROL Exportar conjuntos de dados]** , você terá as permissões apropriadas.

## Selecione seu destino {#select-destination}

Siga as instruções para selecionar um destino em que você possa exportar seus conjuntos de dados:

1. Ir para **[!UICONTROL Conexões > Destinos]** e selecione a variável **[!UICONTROL Catálogo]** guia.

   ![Guia Catálogo de destino com Controle de catálogo realçado.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Selecionar **[!UICONTROL Ativar]** ou **[!UICONTROL Exportar conjuntos de dados]** no cartão correspondente ao destino para o qual você deseja exportar conjuntos de dados.

   ![Guia Destination catalog com Ativate control realçado.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Selecionar **[!UICONTROL Conjuntos de dados do tipo de dados]** e selecione a conexão de destino para a qual deseja exportar conjuntos de dados, em seguida, selecione **[!UICONTROL Próxima]**.

>[!TIP]
> 
>Se quiser configurar um novo destino para exportar conjuntos de dados, selecione **[!UICONTROL Configurar novo destino]** para acionar o [Conectar ao destino](/help/destinations/ui/connect-destination.md) fluxo de trabalho.

![Fluxo de trabalho de ativação de destino com controle de Conjuntos de dados realçado.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. A variável **[!UICONTROL Selecionar conjuntos de dados]** é exibida. Prossiga para a próxima seção até [selecionar seus conjuntos de dados](#select-datasets) para exportação.

## Selecione seus conjuntos de dados {#select-datasets}

Use as caixas de seleção à esquerda dos nomes dos conjuntos de dados para selecionar os conjuntos de dados que você deseja exportar para o destino e, em seguida, selecione **[!UICONTROL Próxima]**.

![Fluxo de trabalho de exportação do conjunto de dados mostrando a etapa Selecionar conjuntos de dados, onde é possível selecionar quais conjuntos de dados serão exportados.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Programar exportação do conjunto de dados {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Opções de exportação de arquivo para conjuntos de dados"
>abstract="Selecione **Exportar arquivos incrementais** para exportar apenas os dados que foram adicionados ao conjunto de dados desde a última exportação. <br> A primeira exportação de arquivo incremental inclui todos os dados no conjunto de dados, atuando como um preenchimento retroativo. Os arquivos incrementais futuros incluem apenas os dados que foram adicionados ao conjunto de dados desde a primeira exportação."

No **[!UICONTROL Agendamento]** etapa, é possível definir uma data de início e uma cadência de exportação para suas exportações do conjunto de dados.

A variável **[!UICONTROL Exportar arquivos incrementais]** é selecionada automaticamente. Isso aciona uma exportação em que o primeiro arquivo é um instantâneo completo do conjunto de dados, e os arquivos subsequentes são adições incrementais ao conjunto de dados desde a exportação anterior.

>[!IMPORTANT]
>
>O primeiro arquivo incremental exportado inclui todos os dados existentes no conjunto de dados, funcionando como um preenchimento retroativo.

![Fluxo de trabalho de exportação do conjunto de dados mostrando a etapa de agendamento.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Use o **[!UICONTROL Frequência]** seletor para selecionar a frequência de exportação:

   * **[!UICONTROL Diariamente]**: programe as exportações de arquivos incrementais uma vez por dia, todos os dias, na hora especificada.
   * **[!UICONTROL Por hora]**: agende exportações de arquivos incrementais a cada 3, 6, 8 ou 12 horas.

2. Use o **[!UICONTROL Hora]** seletor para escolher a hora do dia, em [!DNL UTC] formato, quando a exportação deve ocorrer.

3. Use o **[!UICONTROL Data]** seletor para escolher o intervalo em que a exportação deve ocorrer. No momento, não é possível definir uma data final para as exportações. Para obter mais informações, consulte [limitações conhecidas](#known-limitations) seção.

4. Selecionar **[!UICONTROL Próxima]** para salvar o cronograma e prosseguir para a **[!UICONTROL Revisão]** etapa.

>[!NOTE]
> 
>Para exportações de conjunto de dados, os nomes de arquivo têm um formato padrão predefinido que não pode ser modificado. Consulte a seção [Verificar se o conjunto de dados foi exportado com êxito](#verify) para obter mais informações e exemplos de arquivos exportados.

## Consulte a seção {#review}

No **[!UICONTROL Revisão]** você poderá ver um resumo da sua seleção. Selecionar **[!UICONTROL Cancelar]** para interromper o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações ou **[!UICONTROL Concluir]** para confirmar a seleção e começar a exportar conjuntos de dados para o destino.

![Fluxo de trabalho de exportação do conjunto de dados mostrando a etapa de revisão.](/help/destinations/assets/ui/export-datasets/review.png)

## Verificar se o conjunto de dados foi exportado com êxito {#verify}

Ao exportar conjuntos de dados, o Experience Platform cria uma `.json` ou `.parquet` no local de armazenamento fornecido. Espere que um novo arquivo seja depositado no local de armazenamento de acordo com o agendamento de exportação fornecido.

O Experience Platform cria uma estrutura de pastas no local de armazenamento especificado, onde deposita os arquivos exportados do conjunto de dados. Uma nova pasta é criada para cada exportação, seguindo o padrão abaixo:

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

O nome de arquivo padrão é gerado aleatoriamente e garante que os nomes de arquivo exportados sejam exclusivos.

### Arquivos de conjunto de dados de exemplo {#sample-files}

A presença desses arquivos no local de armazenamento é a confirmação de uma exportação bem-sucedida. Para entender como os arquivos exportados são estruturados, é possível baixar uma amostra [arquivo .parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) ou [arquivo .json](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

#### Arquivos de conjunto de dados compactados {#compressed-dataset-files}

No [conectar ao fluxo de trabalho de destino](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options), você pode selecionar os arquivos do conjunto de dados exportados a serem compactados, conforme mostrado abaixo:

![Seleção de compactação e tipo de arquivo ao conectar-se a um destino para exportar conjuntos de dados.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

Observe a diferença no formato de arquivo entre os dois tipos de arquivo, quando compactados:

* Ao exportar arquivos JSON compactados, o formato de arquivo exportado é `json.gz`
* Ao exportar arquivos parquet compactados, o formato de arquivo exportado é `gz.parquet`

## Remover conjunto de dados do destino {#remove-dataset}

Para remover um conjunto de dados de um fluxo de dados existente, siga as etapas abaixo:

1. Faça logon no [IU DO EXPERIENCE PLATFORM](https://experience.adobe.com/platform/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Selecionar **[!UICONTROL Procurar]** no cabeçalho superior para exibir os fluxos de dados de destino existentes.

   ![Exibição de navegação de destino com uma conexão de destino mostrada e o restante desfocado.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Selecione o ícone de filtro ![Ícone de filtro](../assets/ui/edit-activation/filter.png) na parte superior esquerda para iniciar o painel classificar. O painel de classificação fornece uma lista de todos os seus destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de fluxos de dados associados ao destino selecionado.

1. No **[!UICONTROL Dados de ativação]** selecione o controle de conjuntos de dados para exibir todos os conjuntos de dados mapeados para esse fluxo de dados de exportação.

   ![A opção de navegação dos conjuntos de dados disponíveis é realçada na coluna de dados Ativation.](../assets/ui/export-datasets/go-to-datasets-data.png)

1. A variável **[!UICONTROL Dados de ativação]** para o destino é exibida. Selecionar **[!UICONTROL Remover conjunto de dados]** no painel direito para acionar a caixa de diálogo de confirmação remover conjunto de dados.

   ![Caixa de diálogo Remover conjunto de dados mostrando o controle Remover conjunto de dados no painel direito.](../assets/ui/export-datasets/remove-dataset-control.png)

1. Na caixa de diálogo de confirmação, selecione **[!UICONTROL Remover]** para remover imediatamente o conjunto de dados das exportações para o destino.

   ![Caixa de diálogo mostrando a opção Confirmar remoção do conjunto de dados do fluxo de dados.](../assets/ui/export-datasets/remove-dataset-confirm.png)


## Direitos de exportação do conjunto de dados {#licensing-entitlement}

Consulte os documentos de descrição do produto para entender quantos dados você está autorizado a exportar para cada aplicativo Experience Platform, por ano. Por exemplo, você pode exibir a Descrição do produto Real-Time CDP [aqui](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

Observe que os direitos de exportação de dados para diferentes aplicativos não são aditivos. Por exemplo, isso significa que, se você comprar o Real-Time CDP Ultimate e o Adobe Journey Optimizer Ultimate, o direito de exportação do perfil será o maior dos dois direitos, de acordo com as descrições do produto. Os direitos de volume são calculados calculando o número total de perfis licenciados e multiplicando por 500 KB para o Real-Time CDP Prime ou 700 KB para o Real-Time CDP Ultimate para determinar o volume de dados ao qual você tem direito.

Por outro lado, se você comprar complementos como o Data Distiller, o limite de exportação de dados ao qual você está habilitado representa a soma da camada do produto e do complemento.

Você pode visualizar e rastrear as exportações de perfil em relação aos limites contratuais no painel de licenciamento.

## Limitações conhecidas {#known-limitations}

Lembre-se das seguintes limitações da versão de disponibilidade geral das exportações do conjunto de dados:

* Atualmente, você só pode exportar arquivos incrementais e uma data de término não pode ser selecionada para suas exportações de conjunto de dados.
* Os nomes de arquivos exportados não podem ser personalizados no momento.
* No momento, os conjuntos de dados criados por meio da API não estão disponíveis para exportação.
* No momento, a interface não impede que você exclua um conjunto de dados que está sendo exportado para um destino. Não exclua conjuntos de dados que estejam sendo exportados para destinos. [Remover o conjunto de dados](#remove-dataset) de um fluxo de dados de destino antes de excluí-lo.
* Atualmente, as métricas de monitoramento para exportações de conjunto de dados estão misturadas com números para exportações de perfil, de modo que não refletem os números reais exportados.
