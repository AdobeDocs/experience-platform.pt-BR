---
keywords: Experience Platform;página inicial;tópicos populares;mapear csv;mapear arquivo csv;mapear arquivo csv para xdm;mapear csv para xdm;guia de interface do usuário;mapeador;mapeamento;preparação de dados;preparação de dados;
title: Guia da interface de preparação de dados
description: Saiba como usar as funções de preparação de dados na interface do usuário do Experience Platform para mapear arquivos CSV para um esquema XDM.
exl-id: fafa4aca-fb64-47ff-a97d-c18e58ae4dae
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 1%

---

# Guia da interface de preparação de dados

Leia este guia para saber como usar as funções de mapeamento [preparação de dados](../home.md) na interface do usuário do Adobe Experience Platform para mapear arquivos CSV para um esquema [Experience Data Model (XDM)](../../xdm/home.md).

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [Serviço de identidade](../../identity-service/home.md): obtenha uma melhor visão dos clientes individuais e de seu comportamento unindo as identidades de vários dispositivos e sistemas.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [Fontes](../../sources/home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.

## Acessar a interface de mapeamento na interface do

Você pode acessar a interface de mapeamento na interface por dois caminhos diferentes.

1. Na interface do usuário do Experience Platform, selecione **[!UICONTROL Workflows]** no menu de navegação esquerdo e selecione **[!UICONTROL Mapear CSV para esquema XDM]**. Em seguida, forneça os detalhes do fluxo de dados e selecione os dados que deseja assimilar. Quando terminar, você é levado para a interface de mapeamento, onde é possível configurar o mapeamento entre os dados de origem e um esquema XDM.
2. Também é possível acessar a interface de mapeamento por meio do espaço de trabalho de origens.

## Mapear arquivos CSV em um esquema XDM

Use a interface de mapeamento e o conjunto de ferramentas abrangente fornecido para mapear com êxito os campos de dados do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

![A interface de mapeamento na interface do Experience Platform.](../images/ui/mapping/base_mapping.png)

### Noções básicas sobre a interface de mapeamento {#mapping-interface}

Consulte o painel na parte superior da interface para obter informações sobre a integridade dos campos de mapeamento no contexto do workflow de assimilação. O painel exibe os seguintes detalhes em relação aos campos de mapeamento:

| Propriedade | Descrição |
| --- | --- |
| [!UICONTROL Campos mapeados] | Exibe o número total de campos de origem que foram mapeados para um campo XDM de destino, independentemente de erros. |
| [!UICONTROL Campos obrigatórios] | Exibe o número de campos de mapeamento necessários. |
| [!UICONTROL Campos de identidade] | Exibe o número total de campos de mapeamento definidos como identidade. Esses campos de mapeamento são representados por um ícone de impressão digital. |
| [!UICONTROL Erros] | Exibe o número de campos de mapeamento incorretos. |

{style="table-layout:auto"}

Em seguida, você pode usar as opções listadas no cabeçalho para interagir ou filtrar melhor pelos campos de mapeamento.

| Opção | Descrição |
| --- | --- |
| [!UICONTROL Pesquisar campos de origem] | Use a barra de pesquisa para navegar até um campo de origem específico. |
| [!UICONTROL Todos os campos] | Selecione **[!UICONTROL Todos os campos]** para exibir um menu suspenso de opções para filtrar seus mapeamentos. As opções de filtro disponíveis incluem:<ul><li>**[!UICONTROL Campos obrigatórios]**: filtra a interface para exibir somente os campos necessários para concluir o fluxo de trabalho.</li><li> **[!UICONTROL Campos de identidade]**: filtra a interface para exibir somente campos marcados como identidades.</li><li>**[!UICONTROL Campos mapeados]**: filtra a interface para exibir somente os campos que já foram mapeados.</li><li>**[!UICONTROL Campos não mapeados]**: filtra a interface para exibir somente os campos que ainda não foram mapeados.</li><li>**[!UICONTROL Campos com erros]**: filtra a interface para exibir somente campos com erros.</li></ul> |
| [!UICONTROL Novo tipo de campo] | Selecione **[!UICONTROL Novo tipo de campo]** para adicionar um novo campo ou um campo calculado. Para obter mais informações, leia a seção sobre [adição de um novo tipo de campo](#add-a-new-field-type). |
| [!UICONTROL Importar mapeamentos] | Selecione **[!UICONTROL Importar mapeamentos]** para importar mapeamentos de um arquivo ou fluxo de dados existente. Para obter mais informações, leia a seção sobre [importação de mapeamentos](#import-mapping). |
| [!UICONTROL Validar] | Selecione **[!UICONTROL Validar]** para verificar se há erros nos mapeamentos. |
| [!UICONTROL Baixar modelo] | Selecione **[!UICONTROL Baixar modelo]** para exportar e baixar um arquivo CSV de seus mapeamentos. |
| [!UICONTROL Visualizar dados] | Selecione **[!UICONTROL Visualizar dados]** para usar o painel de visualização e inspecionar a estrutura e o conteúdo do conjunto de dados de origem. |
| [!UICONTROL Limpar tudo] | Selecione **[!UICONTROL Limpar tudo]** para excluir todos os mapeamentos da interface. |

{style="table-layout:auto"}

### Adicionar um novo tipo de campo {#add-a-new-field-type}

Você pode adicionar um novo campo de mapeamento ou um campo calculado selecionando **[!UICONTROL Novo tipo de campo]**.

#### Novo campo de mapeamento

Para adicionar um novo campo de mapeamento, selecione **[!UICONTROL Novo tipo de campo]** e **[!UICONTROL Adicionar novo campo]** no menu suspenso exibido.

![A interface de mapeamento com o botão &quot;adicionar novo campo&quot; selecionado.](../images/ui/mapping/add_new_field.png)

Em seguida, selecione o campo de origem que deseja adicionar da árvore de esquema de origem exibida e selecione **[!UICONTROL Selecionar]**.

![O esquema de origem com &quot;país&quot; selecionado como um novo campo adicional.](../images/ui/mapping/source_field.png)

A interface de mapeamento é atualizada com o campo de origem selecionado e um campo de destino vazio. Selecione **[!UICONTROL Mapear campo de destino]** para começar a mapear o novo campo de origem para seu campo XDM de destino apropriado.

![A interface de mapeamento com um campo de origem novo e não mapeado.](../images/ui/mapping/new_field_added.png)

Uma árvore de esquema de destino interativa é exibida, permitindo navegar manualmente pelo esquema de destino e localizar o campo XDM de destino apropriado para o campo de origem.

![A árvore de esquema de destino interativa com um novo campo de destino selecionado.](../images/ui/mapping/add_target_field.png)

#### Campos calculados {#calculated-fields}

Os campos calculados permitem que valores sejam criados com base nos atributos no esquema de entrada. Esses valores podem ser atribuídos a atributos no esquema de destino e receber um nome e uma descrição para facilitar a referência. Os campos calculados têm um comprimento máximo de 4096 caracteres.

Para criar um campo calculado, selecione **[!UICONTROL Novo tipo de campo]** e **[!UICONTROL Adicionar campo calculado]**

![A interface de mapeamento com o botão &quot;adicionar campo calculado&quot; selecionado.](../images/ui/mapping/new_calculated_field.png)

A janela **[!UICONTROL Criar campo calculado]** é exibida. Use a interface para inserir seus campos calculados e consulte a caixa de diálogo à esquerda para obter campos, funções e operadores compatíveis.

| Tabulação | Descrição |
| --- | ----------- |
| [!UICONTROL Função] | A guia functions lista as funções disponíveis para transformar os dados. Para saber mais sobre as funções que você pode usar em campos calculados, leia o guia em [usando funções de Preparo de Dados (Mapeador)](../functions.md). |
| [!UICONTROL Campo] | A guia fields lista campos e atributos disponíveis no schema de origem. |
| [!UICONTROL Operador] | A guia operators lista os operadores disponíveis para transformar os dados. |

![A interface de campo calculado](../images/ui/mapping/calculated_field.png)

Você pode adicionar campos, funções e operadores manualmente usando o editor de expressão no centro. Selecione o editor para começar a criar uma expressão. Depois de concluir, selecione **[!UICONTROL Salvar]** para continuar.

### Importar mapeamento {#import-mapping}

Você pode reduzir o tempo de configuração manual do processo de assimilação de dados e limitar erros usando a funcionalidade de mapeamento de importação do preparo de dados. Você pode importar mapeamentos de um fluxo existente ou de um arquivo exportado.

>[!BEGINTABS]

>[!TAB Importar mapeamento do fluxo]

Se você tiver vários fluxos de dados com base em arquivos de origem e esquemas de destino semelhantes, poderá importar o mapeamento existente e reutilizá-los para novos fluxos de dados.

Para importar o mapeamento de um fluxo de dados existente, selecione **[!UICONTROL Importar mapeamentos]** e **[!UICONTROL Importar mapeamento do fluxo]**.

![A interface de mapeamento com &quot;mapeamento de importação&quot; e &quot;mapeamento de importação do fluxo&quot; selecionada.](../images/ui/mapping/import_from_flow.png)

Em seguida, use a janela pop-up para localizar o fluxo de dados cujo mapeamento você deseja importar. Durante essa etapa, você também pode usar a função de pesquisa para isolar um fluxo de dados específico e recuperar seus mapeamentos. Quando terminar, selecione **[!UICONTROL Selecionar]**.

![Uma lista de fluxos de dados existentes cujos mapeamentos correspondentes podem ser importados.](../images/ui/mapping/import_flow_window.png)

>[!TAB Importar mapeamento do arquivo]

Em alguns casos, pode ser necessário implementar um grande número de mapeamentos para seus dados. Você pode fazer isso manualmente com a interface de mapeamento, mas também pode exportar seu modelo de mapeamento e configurar os mapeamentos em uma planilha offline para economizar tempo e evitar tempos limite do usuário no Experience Platform.

Para importar o mapeamento de um arquivo exportado, selecione **[!UICONTROL Importar mapeamentos]** e **[!UICONTROL Importar mapeamento do arquivo]**.

![A interface de mapeamento com &quot;mapeamento de importação&quot; e &quot;mapeamento de importação do arquivo&quot; selecionada.](../images/ui/mapping/import_from_file.png)

Em seguida, use a janela [!UICONTROL Carregar modelo] para baixar uma cópia CSV de seus mapeamentos. Em seguida, você pode configurar os mapeamentos localmente no dispositivo, usando qualquer software que suporte a edição de tipos de arquivos CSV. Durante essa etapa, você deve garantir que esteja usando apenas os campos fornecidos no arquivo de origem e no esquema de destino.

![A janela de modelo de carregamento que exibe opções para baixar e carregar um arquivo csv exportado dos mapeamentos.](../images/ui/mapping/upload_template.png)

+++Selecione para exibir um exemplo de um arquivo de mapeamento exportado

![O arquivo csv baixado do modelo de mapeamento.](../images/ui/mapping/mapping_csv_file.png)

+++

Quando terminar, selecione **[!UICONTROL Carregar arquivo]** e selecione o arquivo csv atualizado de seus mapeamentos. Aguarde um breve momento para que o sistema seja processado e selecione **[!UICONTROL Concluído]**.

![A janela de modelo de carregamento com um novo arquivo carregado.](../images/ui/mapping/upload_successful.png)

>[!ENDTABS]

Com os mapeamentos concluídos, agora é possível selecionar **[!UICONTROL Concluir]** e prosseguir para a próxima etapa para concluir o fluxo de dados.

![A interface de mapeamento com um conjunto completo de mapeamentos.](../images/ui/mapping/completed_mappings.png)

## Próximas etapas

Agora é possível mapear com êxito um arquivo CSV para um esquema XDM de destino usando a interface de mapeamento na interface do Experience Platform. Para obter mais informações, leia os seguintes documentos:

* [Visão geral do Preparo de dados](../home.md)
* [Visão geral das fontes](../../sources/home.md)
* [Monitorar fluxos de dados de fontes na interface do usuário](../../dataflows/ui/monitor-sources.md)
