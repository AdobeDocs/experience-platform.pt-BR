---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do usuário do Privacy Service
topic: UI guide
translation-type: tm+mt
source-git-commit: 4b7cbfcbcbaa602d92f3dfe814b1269f770e3fe7

---


# Guia do usuário do Privacy Service

Este documento fornece etapas para criar e gerenciar solicitações de privacidade usando a interface do usuário do Privacy Service.

## Navegue pelo painel da interface do usuário do Privacy Service

O painel para a interface do usuário do Privacy Service fornece dois widgets que permitem que você visualização o status de seus trabalhos de privacidade: Relatório **de** Status e Solicitações **** de Job. O painel também exibe a regra selecionada atual para as tarefas exibidas.

![painel da interface](../images/user-guide/dashboard.png)

### Tipo de regulamento

O Privacy Service suporta solicitações de trabalho para dois tipos de regulamento:

* O Regulamento Geral sobre a Proteção de Dados (RGPD)
* The California Consumer Privacy Act (CCPA).

Os trabalhos para cada tipo de regulamento são rastreados separadamente. Para alternar entre tipos de regulamento, clique no menu suspenso Tipo **de** regulamento e selecione a regra desejada na lista.

![Menu suspenso Tipo de regulamento](../images/user-guide/regulation.png)

Ao alterar o tipo de regulamento, o painel é atualizado para mostrar todos os diálogos de operações, filtros, widgets e criação de empregos que se aplicam ao regulamento selecionado.

![painel atualizado](../images/user-guide/dashboard-update.png)

### Relatório de status

O gráfico no lado esquerdo do widget de Relatório de status acompanha trabalhos enviados contra quaisquer trabalhos que possam ter relatado erros. O gráfico no lado direito rastreia trabalhos próximos ao final da janela de conformidade de 30 dias.

Clique em um dos dois botões de alternância acima do gráfico para mostrar ou ocultar suas respectivas métricas.

![](../images/user-guide/hide-errors.png)

Você pode visualização o número exato de trabalhos associados a qualquer ponto de dados nos gráficos passando o mouse sobre o ponto de dados em questão.

![Pontos de dados do mouse sobre](../images/user-guide/mouse-over.png)

Para visualização de mais detalhes sobre um dado ponto de dados, clique no ponto de dados em questão para exibir os trabalhos associados no widget Solicitações de trabalho. Anote o filtro aplicado logo acima da lista de trabalho.

![Filtro aplicado do widget](../images/user-guide/apply-filter.png)

>[!NOTE] Quando um filtro é aplicado ao widget Solicitações de trabalho, você pode remover o filtro clicando no **X** no pílula de filtro. Solicitações de trabalho, em seguida, retornam à lista de rastreamento padrão.

### Solicitações de trabalho

O widget Solicitações de trabalho lista todas as solicitações de trabalho disponíveis em sua organização, incluindo detalhes como tipo de solicitação, status atual, data de vencimento e e-mail do solicitante.

>[!NOTE] Os dados para trabalhos criados anteriormente só podem ser acessados por 30 dias após a data de conclusão.

Você pode filtrar a lista digitando palavras-chave na barra de pesquisa abaixo do título Solicitações de trabalho. A lista é automaticamente filtros à medida que você digita, mostrando solicitações que contêm valores que correspondem aos seus termos de pesquisa. Você também pode usar o menu suspenso **Solicitado** para selecionar um intervalo de tempo para os trabalhos listados.

![Opções de pesquisa de solicitação de trabalho](../images/user-guide/job-search.png)

Para visualização dos detalhes de uma solicitação de trabalho específica, clique na ID de trabalho da solicitação na lista para abrir a página Detalhes *da* tarefa.

![Detalhes do Trabalho de IU do RGPD](../images/user-guide/job-details.png)

Essa caixa de diálogo contém informações de status sobre cada solução da Experience Cloud e seu estado atual em relação ao trabalho geral. Como cada tarefa de privacidade é assíncrona, a página exibe a data e a hora de comunicação mais recentes (GMT) de cada solução, já que algumas exigem mais tempo do que outras para processar a solicitação.

Se uma solução tiver fornecido dados adicionais, ela poderá ser visualizada nessa caixa de diálogo. É possível visualização desses dados clicando em linhas de produtos individuais.

Para baixar os dados completos do job como um arquivo CSV, clique em **Exportar para CSV** na parte superior direita da caixa de diálogo.

## Criar uma nova solicitação de trabalho de privacidade

A interface do usuário do Privacy Service fornece dois métodos para criar novas solicitações de trabalho:

* Usar o Construtor de solicitações
* Carregar um arquivo JSON

As etapas para usar cada um desses métodos são fornecidas nas seções a seguir.

### Usar o Construtor de solicitações

Usando o Construtor de solicitações, é possível criar manualmente uma nova solicitação de trabalho de privacidade na interface do usuário. O Construtor de solicitações é melhor usado para conjuntos mais simples e menores de solicitações, pois o Construtor de solicitações limita as solicitações a terem apenas o tipo de ID por usuário. Para solicitações mais complicadas, talvez seja melhor [carregar um arquivo](#upload-a-json-file) JSON.

Para start usando o Construtor de solicitações, clique em **Criar solicitação** abaixo do widget Relatório de status no lado direito da tela.

![Clique em Criar solicitação](../images/user-guide/create-request.png)

A caixa de diálogo *Criar solicitação* é aberta, exibindo as opções disponíveis para enviar uma solicitação de trabalho de privacidade para o tipo de regulamento atualmente selecionado.

![](../images/user-guide/request-builder.png)

Selecione o Tipo **de** trabalho da solicitação (&quot;Excluir&quot; ou &quot;Acesso&quot;) e um ou mais **Produtos** disponíveis na lista. Em IDs **do** cliente, selecione um tipo de ID no menu suspenso (email, ECID ou AAID). Digite os valores da ID na caixa de texto à direita, pressionando **\&lt;enter>** para cada ID para adicioná-la à lista.

![](../images/user-guide/request-builder-fillout.png)

As IDs incluídas nesta lista receberão uma cópia de todas as notificações por email do Privacy Service, que são enviadas quando um trabalho é concluído, concluído com erros ou expira. Quando terminar, clique em **Criar**.

![](../images/user-guide/request-builder-create.png)

A caixa de diálogo desaparece e o novo trabalho (ou trabalhos) é listado no widget Solicitações de trabalho juntamente com seu status de processamento atual.

### Carregar um arquivo JSON

Ao criar solicitações mais complicadas, como aquelas que usam vários tipos de ID para cada pessoa de dados sendo processada, você pode criar uma solicitação carregando um arquivo JSON.

Clique na seta ao lado de **Criar solicitação**, abaixo do widget Relatório de status, no lado direito da tela. Na lista de opções que é exibida, selecione **Carregar JSON**.

![Opções de criação de solicitações](../images/user-guide/create-options.png)

A caixa de diálogo *Carregar JSON* é exibida, fornecendo uma janela para que você arraste e solte seu arquivo JSON.

![](../images/user-guide/upload-json.png)

Se você não tiver um arquivo JSON para carregar, clique em **Baixar Adobe-GDPR-Request.json** para baixar um modelo que você pode preencher de acordo com os valores coletados de suas pessoas de dados.


![](../images/user-guide/privacy-template.png)


Localize o arquivo JSON no computador e arraste-o para a janela de diálogo. Se o upload for bem-sucedido, o nome do arquivo será exibido na caixa de diálogo. Você pode continuar a adicionar mais arquivos JSON, conforme necessário, arrastando-os e soltando-os na caixa de diálogo.

Quando terminar, clique em **Criar**. A caixa de diálogo desaparece e o novo trabalho (ou trabalhos) é listado no widget Solicitações _de_ trabalho junto com seu status de processamento atual.

### Próximas etapas

Ao ler este documento, você aprendeu a usar a interface do usuário do Privacy Service para criar um trabalho de privacidade, visualização os detalhes de um trabalho e monitorar seu status de processamento, além de baixar os resultados após sua conclusão.

Para obter etapas sobre como executar essas operações de forma programática usando a API Privacy Service, consulte o guia [do](../api/getting-started.md)desenvolvedor.