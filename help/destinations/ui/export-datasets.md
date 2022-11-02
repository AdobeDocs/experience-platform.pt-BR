---
title: (Beta) Exportar conjuntos de dados para destinos de armazenamento na nuvem
type: Tutorial
description: Saiba como exportar conjuntos de dados do Adobe Experience Platform para o local de armazenamento de nuvem preferencial.
source-git-commit: 97a39e12d916e4fbd048c0fb9ddfa9bdfa10d438
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 1%

---

# (Beta) Exportar conjuntos de dados para destinos de armazenamento em nuvem

>[!IMPORTANT]
>
>* A funcionalidade para exportar conjuntos de dados está atualmente em Beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.
>* Essa funcionalidade beta é compatível com a exportação de dados de primeira geração, conforme definido na Real-time Customer Data Platform [descrição do produto](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* Essa funcionalidade está disponível para clientes que compraram o pacote Real-Time CDP Prime e Ultimate. Entre em contato com o representante da Adobe para obter mais informações.


Este artigo explica o workflow necessário para exportar [conjuntos de dados](/help/catalog/datasets/overview.md) do Adobe Experience Platform para o local de armazenamento em nuvem preferencial, como [!DNL Amazon S3], locais SFTP ou [!DNL Google Cloud Storage].

## Quando ativar segmentos ou exportar conjuntos de dados {#when-to-activate-segments-or-activate-datasets}

Alguns destinos baseados em arquivos no catálogo de Experience Platform suportam ativação de segmento e exportação de conjunto de dados.

* Considere ativar segmentos quando quiser que seus dados sejam estruturados em perfis agrupados por interesses ou qualificações do público-alvo.
* Como alternativa, considere as exportações de conjunto de dados quando você deseja exportar conjuntos de dados brutos, que não são agrupados ou estruturados por interesses ou qualificações do público-alvo. Você pode usar esses dados para relatórios, fluxos de trabalho da ciência de dados, para atender aos requisitos de conformidade e muitos outros casos de uso.

Este documento contém todas as informações necessárias para exportar conjuntos de dados. Se você deseja ativar segmentos para armazenamento na nuvem ou destinos de marketing por email, leia [Ativar dados do público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md).

## Pré-requisitos {#prerequisites}

Para exportar conjuntos de dados para destinos de armazenamento em nuvem, é necessário ter [conectado a um destino](./connect-destination.md). Se ainda não o fez, acesse o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar.

### Permissões necessárias {#permissions}

Para exportar conjuntos de dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]** e **[!UICONTROL Gerenciar e ativar destinos do conjunto de dados]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para garantir que você tenha as permissões necessárias para exportar conjuntos de dados e que o destino seja compatível com a exportação de conjuntos de dados, navegue pelo catálogo de destinos. Se um destino tiver uma **[!UICONTROL Ativar]** ou **[!UICONTROL Exportar conjuntos de dados]** , em seguida, você tem as permissões apropriadas.

## Selecione o destino {#select-destination}

Siga as instruções para selecionar um destino onde você pode exportar seus conjuntos de dados:

1. Ir para **[!UICONTROL Conexões > Destinos]** e selecione o **[!UICONTROL Catálogo]** guia .

   ![Guia Catálogo de destino com Controle de catálogo destacado.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Selecionar **[!UICONTROL Ativar]** ou **[!UICONTROL Exportar conjuntos de dados]** no cartão correspondente ao destino para o qual você deseja exportar conjuntos de dados.

   ![Guia Destination catalog com Ativate control destacado.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Selecionar **[!UICONTROL Conjuntos de dados do tipo de dados]** e selecione a conexão de destino para a qual deseja exportar conjuntos de dados, em seguida, selecione **[!UICONTROL Próximo]**.

>[!TIP]
> 
>Para configurar um novo destino para exportar conjuntos de dados, selecione **[!UICONTROL Configurar novo destino]** para acionar a [Ligar ao destino](/help/destinations/ui/connect-destination.md) fluxo de trabalho.

![Destino do fluxo de trabalho de ativação com controle de Conjuntos de dados realçado.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. O **[!UICONTROL Selecionar conjuntos de dados]** é exibida. Prossiga para a próxima seção de [selecione seus conjuntos de dados](#select-datasets) para exportação.

## Selecionar seus conjuntos de dados {#select-datasets}

Use as caixas de seleção à esquerda dos nomes dos conjuntos de dados para selecionar os conjuntos de dados que deseja exportar para o destino e selecione **[!UICONTROL Próximo]**.

![Fluxo de trabalho de exportação do conjunto de dados que mostra a etapa Selecionar conjuntos de dados, onde é possível selecionar quais conjuntos de dados exportar.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Agendar exportação de conjunto de dados {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Opções de exportação de arquivo para conjuntos de dados"
>abstract="Selecionar **Exportar arquivos incrementais** para exportar apenas os dados que foram adicionados ao conjunto de dados desde a última exportação. <br> A primeira exportação de arquivo incremental inclui todos os dados no conjunto de dados, atuando como um preenchimento retroativo. Os arquivos incrementais futuros incluem apenas os dados que foram adicionados ao conjunto de dados desde a primeira exportação."

No **[!UICONTROL Agendamento]** , é possível definir uma data de início e uma cadência de exportação para as exportações do conjunto de dados.

O **[!UICONTROL Exportar arquivos incrementais]** é selecionada automaticamente. Isso aciona uma exportação onde o primeiro arquivo é um instantâneo completo do conjunto de dados e os arquivos subsequentes são adições incrementais ao conjunto de dados desde a exportação anterior.

>[!IMPORTANT]
>
>O primeiro arquivo incremental exportado inclui todos os dados existentes no conjunto de dados, funcionando como um preenchimento retroativo.

![Fluxo de trabalho de exportação do conjunto de dados que mostra a etapa de agendamento.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Use o **[!UICONTROL Frequência]** seletor para selecionar a frequência de exportação:

   * **[!UICONTROL Diariamente]**: Programe exportações de arquivo incrementais uma vez por dia, todos os dias, no momento especificado.
   * **[!UICONTROL Por hora]**: Agendar exportações de arquivos incrementais a cada 3, 6, 8 ou 12 horas.

2. Use o **[!UICONTROL Hora]** seletor para escolher a hora do dia, em [!DNL UTC] , quando a exportação deve ocorrer.

3. Use o **[!UICONTROL Data]** seletor para escolher o intervalo em que a exportação deve ocorrer. Observe que na versão beta do recurso, não é possível definir uma data de término para as exportações. Para obter mais informações, visualize o [limitações conhecidas](#known-limitations) seção.

4. Selecionar **[!UICONTROL Próximo]** para salvar o agendamento e prosseguir para o **[!UICONTROL Revisão]** etapa.

>[!NOTE]
> 
>Para exportações do conjunto de dados, os nomes dos arquivos têm um formato predefinido e padrão, que não pode ser modificado. Consulte a seção [Verificar exportação bem-sucedida do conjunto de dados](#verify) para obter mais informações e exemplos de arquivos exportados.

## Revisão {#review}

No **[!UICONTROL Revisão]** você pode ver um resumo da sua seleção. Selecionar **[!UICONTROL Cancelar]** para quebrar o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações, ou **[!UICONTROL Concluir]** para confirmar a seleção e começar a exportar conjuntos de dados para o destino.

![Fluxo de trabalho de exportação do conjunto de dados que mostra a etapa de revisão.](/help/destinations/assets/ui/export-datasets/review.png)

## Verificar exportação bem-sucedida do conjunto de dados {#verify}

Ao exportar conjuntos de dados, o Experience Platform cria um `.json` ou `.parquet` no local de armazenamento fornecido. Espere que um novo arquivo seja depositado no local de armazenamento de acordo com a programação de exportação que você forneceu.

O Experience Platform cria uma estrutura de pastas no local de armazenamento especificado, onde deposita os arquivos de conjunto de dados exportados. Uma nova pasta é criada para cada momento de exportação, seguindo o padrão abaixo:

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

O nome de arquivo padrão é gerado aleatoriamente e garante que os nomes de arquivo exportados sejam exclusivos.

### Arquivos de conjunto de dados de amostra {#sample-files}

A presença desses arquivos no local de armazenamento é a confirmação de uma exportação bem-sucedida. Para entender como os arquivos exportados são estruturados, é possível baixar uma amostra [Arquivo .parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) ou [arquivo .json](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

## Remover conjunto de dados do destino {#remove-dataset}

Para remover um conjunto de dados de um fluxo de dados existente, siga as etapas abaixo:

1. Faça logon no [Interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Selecionar **[!UICONTROL Procurar]** no cabeçalho superior para exibir os fluxos de dados de destino existentes.

   ![Exibição de navegação de destino com uma conexão de destino exibida e o restante esmaecido.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Selecione o ícone de filtro ![Ícone Filtro](../assets/ui/edit-activation/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de fluxos de dados associada ao destino selecionado.

1. No **[!UICONTROL Dados de ativação]** selecione o controle de conjuntos de dados para exibir todos os conjuntos de dados mapeados para esse fluxo de dados de exportação.

   ![A opção disponível de navegação dos conjuntos de dados realçada na coluna Dados de ativação .](../assets/ui/export-datasets/go-to-datasets-data.png)

1. O **[!UICONTROL Dados de ativação]** será exibida a página de destino. Selecionar **[!UICONTROL Remover conjunto de dados]** no painel direito para acionar a caixa de diálogo de confirmação de remover conjunto de dados.

   ![Caixa de diálogo Remover conjunto de dados mostrando o controle Remover conjunto de dados no painel direito.](../assets/ui/export-datasets/remove-dataset-control.png)

1. Na caixa de diálogo de confirmação, selecione **[!UICONTROL Remover]** para remover imediatamente o conjunto de dados das exportações para o destino.

   ![Caixa de diálogo que mostra a opção de remoção Confirmar conjunto de dados do fluxo de dados.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Limitações conhecidas {#known-limitations}

Lembre-se das seguintes limitações da versão beta das exportações de conjunto de dados:

* No momento, há uma única permissão (**[!UICONTROL Gerenciar e ativar destinos do conjunto de dados]**) que inclui o gerenciamento e a ativação de permissões em destinos de conjuntos de dados. Esses controles serão divididos no futuro em permissões mais granulares. Revise o [permissões necessárias](#permissions) para obter uma lista completa de permissões que você precisa exportar conjuntos de dados.
* Atualmente, você só pode exportar arquivos incrementais e uma data final não pode ser selecionada para suas exportações de conjunto de dados.
* Nomes de arquivo exportados não são personalizáveis no momento.
* No momento, a interface do usuário não impede que você exclua um conjunto de dados que está sendo exportado para um destino. Não exclua nenhum conjunto de dados que esteja sendo exportado para destinos do . [Remover o conjunto de dados](#remove-dataset) de um fluxo de dados de destino antes de excluí-lo.
* As métricas de monitoramento para exportações de conjunto de dados estão atualmente misturadas aos números para exportações de perfil, de modo que não refletem os números de exportação verdadeiros.
