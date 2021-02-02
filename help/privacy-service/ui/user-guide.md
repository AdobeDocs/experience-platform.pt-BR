---
keywords: Experience Platform;home;popular topics;export;Export
solution: Experience Platform
title: Guia do usuário do Privacy Service
topic: UI guide
description: Saiba como usar a interface do usuário do Privacy Service para coordenar e monitorar solicitações de privacidade em vários aplicativos do Experience Cloud.
translation-type: tm+mt
source-git-commit: 238a9200e4b43d41335bed0efab079780b252717
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 0%

---


# [!DNL Privacy Service] Guia do usuário

Este documento fornece etapas para criar e gerenciar solicitações de privacidade usando a interface do usuário [!DNL Privacy Service].

## Navegue pelo painel da interface do usuário [!DNL Privacy Service]

O painel para a interface de usuário [!DNL Privacy Service] fornece dois widgets que permitem visualização do status de seus trabalhos de privacidade: &quot;[!UICONTROL Relatório de status]&quot; e &quot;[!UICONTROL Solicitações de trabalho]&quot;. O painel também exibe a regra selecionada atual para as tarefas exibidas.

![Painel da interface](../images/user-guide/dashboard.png)

### Tipo de regulamento

[!DNL Privacy Service] suporta solicitações de trabalhos para várias regulamentações de privacidade:

* O [!DNL California Consumer Privacy Act] ([!UICONTROL CCPA])
* A União Europeia [!DNL General Data Protection Regulation] ([!UICONTROL RGPD])
* Tailândia [!DNL Personal Data Protection Act] ([!UICONTROL PDPA_THA])
* Brasil [!DNL Lei Geral de Proteção de Dados] ([!UICONTROL LGPD_BRA])
* A Nova Zelândia [!DNL Privacy Act] ([!UICONTROL NZPA_NZL])

Os trabalhos para cada tipo de regulamento são rastreados separadamente. Para alternar entre tipos de regulamento, selecione o menu suspenso **[!UICONTROL Tipo de regulamento]** e selecione a regra desejada na lista.

![Menu suspenso Tipo de regulamento](../images/user-guide/regulation.png)

Ao alterar o tipo de regulamento, o painel é atualizado para mostrar todos os diálogos de operações, filtros, widgets e criação de empregos que se aplicam ao regulamento selecionado.

![Painel atualizado](../images/user-guide/dashboard-update.png)

### Relatório de status

O gráfico no lado esquerdo do widget de Relatório de status acompanha trabalhos enviados contra quaisquer trabalhos que possam ter relatado erros. O gráfico no lado direito rastreia trabalhos próximos ao final da janela de conformidade de 30 dias.

Selecione um dos dois botões de alternância acima do gráfico para mostrar ou ocultar suas respectivas métricas.

![](../images/user-guide/hide-errors.png)

Você pode visualização o número exato de trabalhos associados a qualquer ponto de dados nos gráficos passando o mouse sobre o ponto de dados em questão.

![Pontos de dados do mouse sobre](../images/user-guide/mouse-over.png)

Para visualização de mais detalhes sobre um dado ponto de dados, selecione o ponto de dados em questão para exibir os trabalhos associados no widget Solicitações de trabalho. Anote o filtro aplicado logo acima da lista de trabalho.

![Filtro aplicado do widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Quando um filtro é aplicado ao widget Solicitações de trabalho, você pode remover o filtro selecionando **X** no pílula de filtro. Solicitações de trabalho, em seguida, retornam à lista de rastreamento padrão.

### Solicitações de trabalho

O widget Solicitações de trabalho lista todas as solicitações de trabalho disponíveis em sua organização, incluindo detalhes como tipo de solicitação, status atual, data de vencimento e e-mail do solicitante.

>[!NOTE]
>
>Os dados para trabalhos criados anteriormente só podem ser acessados por 30 dias após a data de conclusão.

Você pode filtrar a lista digitando palavras-chave na barra de pesquisa abaixo do título Solicitações de trabalho. A lista é automaticamente filtros à medida que você digita, mostrando solicitações que contêm valores que correspondem aos seus termos de pesquisa. Você também pode usar o menu suspenso **[!UICONTROL Solicitado em]** para selecionar um intervalo de tempo para os trabalhos listados.

![Opções de pesquisa de solicitação de trabalho](../images/user-guide/job-search.png)

Para visualização dos detalhes de uma solicitação de trabalho específica, selecione a ID de trabalho da solicitação na lista para abrir a página **[!UICONTROL Detalhes do Trabalho]**.

![Detalhes do Trabalho de IU do RGPD](../images/user-guide/job-details.png)

Esta caixa de diálogo contém informações de status sobre cada [!DNL Experience Cloud] solução e seu estado atual em relação ao trabalho geral. Como cada tarefa de privacidade é assíncrona, a página exibe a data e a hora de comunicação mais recentes (GMT) de cada solução, já que algumas exigem mais tempo do que outras para processar a solicitação.

Se uma solução tiver fornecido dados adicionais, ela poderá ser visualizada nessa caixa de diálogo. É possível visualização desses dados selecionando linhas de produtos individuais.

Para baixar os dados completos do trabalho como um arquivo CSV, selecione **[!UICONTROL Exportar para CSV]** no canto superior direito da caixa de diálogo.

## Criar uma nova solicitação de trabalho de privacidade

>[!NOTE]
>
>Para criar uma solicitação de trabalho de privacidade, você deve fornecer informações de identidade para os clientes específicos cujos dados devem ser acessados ou excluídos. Revise o documento nos [dados de identidade para solicitações de privacidade](../identity-data.md) antes de continuar com esta seção.

A interface do usuário [!DNL Privacy Service] fornece dois métodos para criar novas solicitações de trabalho:

* [Usar o Construtor de solicitações](#request-builder)
* [Carregar um arquivo JSON](#json)

As etapas para usar cada um desses métodos são fornecidas nas seções a seguir.

### Usar o Construtor de solicitações {#request-builder}

Usando o Construtor de solicitações, é possível criar manualmente uma nova solicitação de trabalho de privacidade na interface do usuário. O Construtor de solicitações é melhor usado para conjuntos mais simples e menores de solicitações, pois o Construtor de solicitações limita as solicitações a terem apenas o tipo de ID por usuário. Para solicitações mais complicadas, talvez seja melhor [carregar um arquivo JSON](#json).

Para start usando o Construtor de solicitações, selecione **[!UICONTROL Criar solicitação]** abaixo do widget Relatório de status no lado direito da tela.

![Selecionar Criar solicitação](../images/user-guide/create-request.png)

A caixa de diálogo **[!UICONTROL Criar solicitação]** é aberta, exibindo as opções disponíveis para enviar uma solicitação de trabalho de privacidade para o tipo de regulamento atualmente selecionado.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Selecione **[!UICONTROL Tipo de Trabalho]** da solicitação (&quot;Excluir&quot; ou &quot;Acesso&quot;) e um ou mais produtos disponíveis da lista.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Em **[!UICONTROL tipo de Namespace]**, selecione o tipo de namespace apropriado para as IDs do cliente que estão sendo enviadas para [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Ao usar o tipo de namespace padrão, selecione uma namespace no menu suspenso (email, ECID ou AAID) e digite os valores de ID na caixa de texto à direita, pressionando **\&lt;enter>** para cada ID para adicioná-la à lista.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Ao usar o tipo de namespace personalizada, você deve digitar manualmente na namespace antes de fornecer os valores de ID abaixo.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Quando terminar, selecione **[!UICONTROL Criar]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

A caixa de diálogo desaparece e o novo trabalho (ou trabalhos) é listado no widget Solicitações de trabalho juntamente com seu status de processamento atual.

### Carregar um arquivo JSON {#json}

Ao criar solicitações mais complicadas, como aquelas que usam vários tipos de ID para cada pessoa de dados sendo processada, você pode criar uma solicitação carregando um arquivo JSON.

Selecione a seta ao lado de **[!UICONTROL Criar solicitação]**, abaixo do widget Relatório de status no lado direito da tela. Na lista de opções que é exibida, selecione **[!UICONTROL Carregar JSON]**.

![Opções de criação de solicitações](../images/user-guide/create-options.png)

A caixa de diálogo **[!UICONTROL Carregar JSON]** é exibida, fornecendo uma janela para arrastar e soltar seu arquivo JSON.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Se você não tiver um arquivo JSON para carregar, selecione **[!UICONTROL Baixar Adobe-GDPR-Request.json]** para baixar um modelo que você pode preencher de acordo com os valores coletados de suas pessoas de dados.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Localize o arquivo JSON no computador e arraste-o para a janela de diálogo. Se o upload for bem-sucedido, o nome do arquivo será exibido na caixa de diálogo. Você pode continuar a adicionar mais arquivos JSON, conforme necessário, arrastando-os e soltando-os na caixa de diálogo.

Quando terminar, selecione **[!UICONTROL Criar]**. A caixa de diálogo desaparece e o novo trabalho (ou trabalhos) é listado no widget Solicitações de trabalho juntamente com seu status de processamento atual.

### Próximas etapas

Ao ler este documento, você aprendeu a usar a interface do usuário [!DNL Privacy Service] para criar um trabalho de privacidade, visualização os detalhes de um trabalho e monitore seu status de processamento, e baixe os resultados após sua conclusão.

Para obter etapas sobre como executar essas operações de forma programática usando a API [!DNL Privacy Service], consulte o [guia do desenvolvedor](../api/getting-started.md).