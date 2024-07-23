---
keywords: Experience Platform;início;tópicos populares;exportar;Exportar;;home;popular topics;export;Export
solution: Experience Platform
title: Gerenciar processos de privacidade na interface do Privacy Service
description: Saiba como usar a interface do usuário do Privacy Service para coordenar e monitorar solicitações de privacidade em vários aplicativos Experience Cloud.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 341cc4cb150717f08b2e59412ef58fbd6f7b3450
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 12%

---

# Gerenciamento de processos de privacidade na interface do Privacy Service {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="Respeitar solicitações de privacidade do titular de dados"
>abstract="<h2>Descrição</h2><p>O Serviço de Privacidade da Adobe Experience Platform permite criar e gerenciar solicitações de privacidade em nome de clientes que desejam acessar ou excluir seus dados pessoais de acordo com as normas legais de privacidade.</p>"

Este documento fornece etapas para criar e gerenciar solicitações de privacidade usando a interface do usuário do [!DNL Privacy Service].

>[!IMPORTANT]
>
>O Privacy Service se destina apenas a solicitações de titulares de dados e de direitos do consumidor. Qualquer outro uso do Privacy Service para limpeza ou manutenção de dados não é suportado ou permitido. A Adobe tem a obrigação legal de os cumprir em tempo útil. Dessa forma, o teste de carga no Privacy Service não é permitido, pois é um ambiente somente de produção e cria um backlog desnecessário de solicitações de privacidade válidas.
>
>Um limite rígido de upload diário está em vigor para ajudar a evitar o abuso do serviço. Os usuários que abusam do sistema terão o acesso ao serviço desativado. Uma reunião subsequente será realizada com eles para abordar suas ações e discutir o uso aceitável do Privacy Service.

## Navegar no painel da interface do usuário [!DNL Privacy Service]

O painel da interface do usuário do [!DNL Privacy Service] fornece dois widgets que permitem exibir o status dos seus trabalhos de privacidade: &quot;[!UICONTROL Relatório de Status]&quot; e &quot;[!UICONTROL Solicitações de Trabalho]&quot;. O painel também exibe o regulamento selecionado atual para os trabalhos exibidos.

![painel da interface](../images/user-guide/dashboard.png)

### Tipo de regulação

O [!DNL Privacy Service] dá suporte a solicitações de trabalho para vários regulamentos de privacidade. A tabela a seguir lista os regulamentos compatíveis e seus rótulos correspondentes, conforme representados na interface do usuário:

| Rótulo da interface | Regulação |
| --- | --- |
| [!UICONTROL APA_AUS] | O [!DNL Australia Privacy Act (Privacy Act)] |
| [!UICONTROL CPA] | O [!DNL Colorado Privacy Act] |
| [!UICONTROL CCPA] | O [!DNL California Consumer Privacy Act] |
| [!UICONTROL CPRA_USA] | O [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL CTDPA] | O [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL FDBR_USA] | O [!DNL Florida Digital Bill of Rights] |
| [!UICONTROL GDPR] | O [!DNL General Data Protection Regulation] da União Europeia |
| [!UICONTROL HIPAA_AUS] | O [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL LGPD_BRA] | Do Brasil: [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL MHMDA] | O [!DNL Washington My Health My Data Act] |
| [!UICONTROL NZPA_NZL] | Nova Zelândia [!DNL Privacy Act] |
| [!UICONTROL OCPA_USA] | O [!DNL Oregon Consumer Privacy Act] |
| [!UICONTROL PDPA_THA] | Da Tailândia: [!DNL Personal Data Protection Act] |
| [!UICONTROL TDPSA_USA] | O [!DNL Texas Data Privacy and Security Act] |
| [!UICONTROL UCPA] | O [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_USA] | O [!DNL Virginia Consumer Data Protection Act] |

{style="table-layout:auto"}

>[!NOTE]
>
>Consulte a visão geral em [regulamentos de privacidade compatíveis](../regulations/overview.md) para obter mais informações sobre o contexto legal de cada regulamento.

As ordens de produção para cada tipo de regulamento são rastreadas separadamente. Para alternar entre tipos de regulamentos, selecione o menu suspenso **[!UICONTROL Tipo de Regulamento]** e selecione o regulamento desejado na lista.

![O console Privacy Service com a lista suspensa Tipo de Regulamento.](../images/user-guide/regulation.png)

Ao alterar o tipo de regulamento, o painel é atualizado para mostrar todas as operações, filtros, widgets e caixas de diálogo de criação de trabalho que se aplicam ao regulamento selecionado.

![Painel atualizado](../images/user-guide/dashboard-update.png)

### Status do relatório

O gráfico no lado esquerdo do widget Relatório de status rastreia as tarefas enviadas em relação às tarefas que foram relatadas com erros. O gráfico no lado direito rastreia os trabalhos próximos ao final da janela de conformidade de 30 dias.

Selecione um dos dois botões de alternância acima do gráfico para mostrar ou ocultar suas respectivas métricas.

![](../images/user-guide/hide-errors.png)

Você pode visualizar o número exato de tarefas associadas a qualquer ponto de dados nos gráficos, passando o mouse sobre o ponto de dados em questão.

![Passe o mouse sobre os pontos de dados](../images/user-guide/mouse-over.png)

Para exibir mais detalhes sobre determinado ponto de dados, selecione o ponto de dados em questão para exibir as tarefas associadas no widget Solicitações de trabalho. Anote o filtro que é aplicado logo acima da lista de tarefas.

![Filtro aplicado do widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Quando um filtro é aplicado ao widget Solicitações de trabalho, é possível removê-lo selecionando **X** no preenchimento de filtro. As solicitações de tarefa retornam à lista de rastreamento padrão.

### Solicitações de tarefa {#job-requests}

O espaço de trabalho [!UICONTROL Solicitações de Trabalho] lista detalhes sobre as solicitações de trabalho recentes na sua organização. Os detalhes incluem tipo de solicitação, status atual, data de vencimento, email do solicitante e assim por diante. Conjuntos de 100 registros são carregados de cada vez. Por padrão, os trabalhos criados mais recentemente são exibidos na parte superior com mais conjuntos de registros carregados à medida que você rolar a tela para baixo para navegar.

>[!NOTE]
>
>Os dados de trabalhos criados anteriormente só podem ser acessados por 30 dias após a data de conclusão.

Você pode filtrar a lista digitando palavras-chave na barra de pesquisa abaixo do título [!UICONTROL Solicitações de trabalho]. A lista filtra automaticamente à medida que você digita, mostrando solicitações que contêm valores correspondentes aos termos da pesquisa. O campo de pesquisa executa uma pesquisa &quot;rápida&quot; que corresponde IDs de trabalho de privacidade aos trabalhos renderizados/carregados atualmente na interface do usuário. Não é uma pesquisa abrangente de todas as tarefas submetidas. Em vez disso, é um filtro aplicado aos resultados carregados. Use a API de Privacy Service para [retornar trabalhos com base em um regulamento específico, intervalos de datas ou um único trabalho](../api/privacy-jobs.md#list).

>[!TIP]
>
>Para carregar registros na interface dos últimos 30 dias, role a tabela para baixo e carregue mais lotes de registros.

![A seção Solicitação de Trabalho do Console de Privacidade com o campo de pesquisa realçado.](../images/user-guide/job-search.png)

Como alternativa, use o botão de pesquisa para executar uma consulta de trabalho de privacidade que abrange um intervalo de datas específico. Essa ação retorna todas as tarefas de privacidade enviadas por sua organização durante o período determinado. Selecione o menu suspenso **[!UICONTROL Solicitado em]** para escolher uma data de início e término para a consulta. As opções disponíveis incluem [!UICONTROL Hoje], [!UICONTROL Últimos 7 Dias], [!UICONTROL Últimas 2 Semanas], [!UICONTROL Últimos 30 Dias] ou [!UICONTROL Personalizado]. Quando usado com a opção [!UICONTROL Solicitado em], o recurso de pesquisa exibe somente as solicitações de trabalho que foram enviadas entre os intervalos de datas escolhidos.

![A seção Solicitação de Trabalho com o campo de pesquisa, Solicitado no menu suspenso, e o botão Pesquisar realçado.](../images/user-guide/requested-on-dropdown-menu.png)

Para exibir os detalhes de uma solicitação de trabalho específica, selecione a ID do trabalho da solicitação na lista para abrir a página **[!UICONTROL Detalhes do trabalho]**.

![Detalhes do Trabalho da Interface do GDPR](../images/user-guide/job-details.png)

Esta caixa de diálogo contém informações de status sobre cada solução [!DNL Experience Cloud] e seu estado atual em relação ao trabalho geral. Como cada trabalho de privacidade é assíncrono, a página exibe a data e a hora da comunicação mais recente (GMT) de cada solução, pois algumas exigem mais tempo do que outras para processar a solicitação.

Se uma solução tiver fornecido dados adicionais, ela será exibida nessa caixa de diálogo. Você pode visualizar esses dados selecionando linhas de produto individuais.

Para baixar os dados completos do trabalho como um arquivo CSV, selecione **[!UICONTROL Exportar para CSV]** na parte superior direita da caixa de diálogo.

## Criar uma nova solicitação de processo de privacidade {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="Instruções"
>abstract="<ul><li>Selecione <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=pt-BR#logging-in-from-experience-platform">Solicitações</a> na navegação à esquerda para abrir a Interface de privacidade e, em seguida, selecione <b>Criar solicitação</b>.</li><li>Aqui, você pode usar o construtor de solicitações ou fazer upload de um arquivo JSON de titulares de dados.</li><li>Se estiver usando o construtor de solicitações, selecione o tipo de tarefa (acesso e/ou exclusão) e escolha o tipo de identidade que você está fornecendo (email, ECID ou AAID) ou insira um namespace de identidade personalizado. Insira os valores de identidade apropriados para os clientes e selecione <b>Criar</b> quando terminar.</li><li>Se estiver carregando um arquivo JSON, selecione a seta ao lado de Criar solicitação. Na lista de opções, selecione <b>Upload de JSON</b> e faça upload do arquivo. Se não tiver um arquivo JSON para fazer upload, selecione <b>Baixar Adobe-GDPR-Request.json</b> para baixar um modelo que pode ser preenchido. Faça upload do JSON e selecione <b>Criar</b> quando terminar.</li><li>Para obter mais ajuda com esse recurso, consulte o <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=pt-BR">Guia do usuário do Serviço de Privacidade</a> na Experience League.</li></ul>"

>[!NOTE]
>
>Para criar uma solicitação de acesso a dados pessoais, você deve fornecer informações de identidade para os clientes específicos cujos dados devem ser acessados ou excluídos. Revise o documento em [dados de identidade para solicitações de privacidade](../identity-data.md) antes de continuar com esta seção.

A interface do usuário do [!DNL Privacy Service] fornece dois métodos para criar novas solicitações de trabalho:

* [Usar o Criador de solicitações](#request-builder)
* [Fazer upload de um arquivo JSON](#json)

As etapas para usar cada um desses métodos são fornecidas nas seções a seguir.

### Usar o Criador de solicitações {#request-builder}

Usando o Construtor de solicitações, você pode criar manualmente uma nova solicitação de trabalho de privacidade na interface do usuário. O Construtor de solicitações é mais adequado para conjuntos de solicitações mais simples e menores, pois o Construtor de solicitações limita as solicitações a terem somente o tipo de ID por usuário. Para solicitações mais complicadas, talvez seja melhor [carregar um arquivo JSON](#json).

Para começar a usar o Construtor de solicitações, selecione **[!UICONTROL Criar solicitação]** abaixo do widget Relatório de status no lado direito da tela.

![Selecionar Criar Solicitação](../images/user-guide/create-request.png)

A caixa de diálogo **[!UICONTROL Criar Solicitação]** é aberta, exibindo as opções disponíveis para enviar uma solicitação de trabalho de privacidade para o tipo de regulamento selecionado atualmente.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Selecione o **[!UICONTROL Tipo de Trabalho]** da solicitação (&quot;Excluir&quot; ou &quot;Acessar&quot;) e um ou mais produtos disponíveis na lista.

O Privacy Service oferece suporte a dois tipos de solicitações de trabalho para dados pessoais: [!UICONTROL Acesso] (leitura) e/ou [!UICONTROL Exclusão]. Você pode enviar uma solicitação para receber todas as informações contidas no produto relacionadas ao assunto da pesquisa ou solicitar a exclusão de todas as informações relacionadas ao assunto da pesquisa.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

Em **[!UICONTROL Tipo de namespace]**, selecione o tipo de namespace apropriado para as IDs do cliente que estão sendo enviadas para [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Ao usar o tipo de namespace padrão, selecione um namespace no menu suspenso (email, ECID ou AAID) e digite os valores de ID na caixa de texto à direita, pressionando **\&lt;enter>** para cada ID adicioná-lo à lista.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Ao usar o tipo de namespace personalizado, você deve digitar manualmente o namespace antes de fornecer os valores de ID abaixo.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Quando terminar, selecione **[!UICONTROL Criar]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

A caixa de diálogo desaparece e a nova tarefa (ou tarefas) é listada no widget Solicitações de tarefa junto com seu status de processamento atual.

### Fazer upload de um arquivo JSON {#json}

Ao criar solicitações mais complicadas, como as que usam vários tipos de ID para cada titular de dados que está sendo processado, é possível criar uma solicitação carregando um arquivo JSON.

Selecione a seta ao lado de **[!UICONTROL Criar solicitação]**, abaixo do widget Relatório de status no lado direito da tela. Na lista de opções exibida, selecione **[!UICONTROL Carregar JSON]**.

![Solicitar opções de criação](../images/user-guide/create-options.png)

A caixa de diálogo **[!UICONTROL Carregar JSON]** é exibida, fornecendo uma janela para que você arraste e solte seu arquivo JSON.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Se você não tiver um arquivo JSON para carregar, selecione **[!UICONTROL Baixar Adobe-GDPR-Request.json]** para baixar um modelo que você pode preencher de acordo com os valores coletados dos titulares de dados.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Localize o arquivo JSON no computador e arraste-o para a janela de diálogo. Se o upload for bem-sucedido, o nome do arquivo aparecerá na caixa de diálogo. Você pode continuar a adicionar mais arquivos JSON, conforme necessário, arrastando-os e soltando-os na caixa de diálogo.

Quando terminar, selecione **[!UICONTROL Criar]**. A caixa de diálogo desaparece e a nova tarefa (ou tarefas) é listada no widget Solicitações de tarefa junto com seu status de processamento atual.

### Próximas etapas

Ao ler este documento, você aprendeu a usar a interface do usuário do [!DNL Privacy Service] para criar um trabalho de privacidade, exibir os detalhes do trabalho e monitorar seu status de processamento, além de baixar os resultados após sua conclusão.

Para obter etapas sobre como executar essas operações de forma programática usando a API [!DNL Privacy Service], consulte o [Guia de API](../api/overview.md).
