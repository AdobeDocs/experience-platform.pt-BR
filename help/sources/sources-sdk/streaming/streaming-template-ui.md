---
title: Modelo de autoatendimento de documentação para interface de usuário de streaming do SDK
description: Saiba como trazer dados de transmissão de uma origem para a Adobe Experience Platform usando a interface do usuário.
exl-id: 82254be0-fa31-4114-a0ec-179a990e0904
badge: Beta
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 1%

---

# Crie uma conexão de origem e um fluxo de dados para transmitir dados de *YOURSOURCE* usando a interface

*Conforme você passar por este modelo, substitua ou exclua todos os parágrafos em itálico (começando por este).*

*Comece atualizando os metadados (título e descrição) na parte superior da página. Ignore todas as instâncias de UICONTROL nesta página. Essa é uma tag que ajuda nossos processos de tradução automática a traduzir corretamente a página para os vários idiomas compatíveis. Adicionaremos marcas à sua documentação após você enviá-la.*

Este tutorial fornece etapas para a criação de um conector de origem *YOURSOURCE* usando a interface do usuário do Experience Platform.

## Visão geral

*Forneça uma breve visão geral da sua empresa, incluindo o valor que ela oferece aos clientes. Inclua um link para a página inicial da documentação do produto para leitura adicional.*

>[!IMPORTANT]
>
>Este conector de origem e página de documentação são criados e mantidos pela equipe *YOURSOURCE*. Para qualquer consulta ou solicitação de atualização, contate-os diretamente em *Inserir link ou endereço de email onde você pode ser contatado para atualizações*.

## Pré-requisitos

*Adicione nesta seção informações sobre qualquer item que os clientes precisem saber antes de começar a configurar a origem na interface do usuário do Adobe Experience Platform. Isso pode ser sobre:*

* *que precisa ser adicionado a um incluo na lista de permissões*
* *requisitos para hash de email*
* *qualquer especificação de conta da sua parte*
* *como obter as credenciais de autenticação para se conectar à sua plataforma*

### Coletar credenciais necessárias

Para conectar *YOURSOURCE* à Experience Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| *credencial um* | *Adicione aqui uma breve descrição à credencial de autenticação da sua origem* | *Adicione aqui um exemplo da credencial de autenticação da sua origem* |
| *credencial dois* | *Adicione aqui uma breve descrição à credencial de autenticação da sua origem* | *Adicione aqui um exemplo da credencial de autenticação da sua origem* |
| *credencial três* | *Adicione aqui uma breve descrição à credencial de autenticação da sua origem* | *Adicione aqui um exemplo da credencial de autenticação da sua origem* |

Para obter mais informações sobre essas credenciais, consulte a documentação de autenticação de *SUA ORIGEM*. *Adicione aqui o link para a documentação de autenticação da sua plataforma*.

### Integrar *YOURSOURCE* ao seu webhook

*O Streaming SDK requer que sua fonte seja capaz de oferecer suporte a webhooks para se comunicar com o Experience Platform. Nesta seção, você deve fornecer as etapas que seus usuários terão que seguir para integrar YOURSOURCE a um webhook.*

## Conecte sua conta *YOURSOURCE*

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Sources]. A tela [!UICONTROL Catalog] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **Streaming**, selecione *YOURSOURCE* e **[!UICONTROL Add data]**.

>[!TIP]
>
>As capturas de tela usadas abaixo são exemplos. Ao criar sua documentação, substitua as imagens por capturas de tela da origem real. É possível usar o mesmo padrão de marcação e cor, bem como os mesmos nomes de arquivo. Certifique-se de que sua captura de tela capture toda a tela da interface do usuário do Experience Platform. Para obter informações sobre como carregar capturas de tela, consulte o manual em [enviando sua documentação para revisão](../documentation/github.md).

![O catálogo de fontes do Experience Platform](../assets/streaming/catalog.png)

## Selecionar dados

A etapa **[!UICONTROL Select data]** é exibida, fornecendo uma interface para que você selecione os dados que trará para a Experience Platform.

* A parte esquerda da interface é um navegador que permite visualizar os fluxos de dados disponíveis em sua conta;
* A parte direita da interface permite visualizar até 100 linhas de dados de um arquivo JSON.

Selecione **[!UICONTROL Upload files]** para carregar um arquivo JSON do sistema local. Como alternativa, você pode arrastar e soltar o arquivo JSON que deseja carregar no painel [!UICONTROL Drag and drop files].

![A etapa para adicionar dados do fluxo de trabalho de fontes.](../assets/streaming/add-data.png)

Depois que o arquivo for carregado, a interface de visualização será atualizada para exibir uma visualização do esquema carregado. A interface de visualização permite inspecionar o conteúdo e a estrutura de um arquivo. Você também pode usar o utilitário [!UICONTROL Search field] para acessar itens específicos no esquema.

Quando terminar, selecione **[!UICONTROL Next]**.

![A etapa de visualização do fluxo de trabalho de fontes.](../assets/streaming/preview.png)

## Detalhes do fluxo de dados

A etapa **Detalhes do fluxo de dados** é exibida, fornecendo opções para usar um conjunto de dados existente ou estabelecer um novo para o fluxo de dados, bem como uma oportunidade de fornecer um nome e uma descrição para o fluxo de dados. Durante essa etapa, você também pode definir configurações para Assimilação de perfil, diagnóstico de erro, assimilação parcial e alertas.

Quando terminar, selecione **[!UICONTROL Next]**.

![A etapa de detalhes do fluxo de dados do fluxo de trabalho de fontes.](../assets/streaming/dataflow-detail.png)

## Mapeamento

A etapa [!UICONTROL Mapping] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

O Experience Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso. Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre como usar a interface do mapeador e campos calculados, consulte o [Guia da Interface do Preparo de Dados](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html?lang=pt-BR).

Após mapear os dados de origem com êxito, selecione **[!UICONTROL Next]**.

![A etapa de mapeamento do fluxo de trabalho de origens.](../assets/streaming/mapping.png)

## Revisar

A etapa **[!UICONTROL Review]** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Connection]**: Mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas nesse arquivo de origem.
* **[!UICONTROL Assign dataset & map fields]**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

Depois de revisar seu fluxo de dados, clique em **[!UICONTROL Finish]** e aguarde algum tempo para que o fluxo de dados seja criado.

![A etapa de revisão do fluxo de trabalho de fontes.](../assets/streaming/review.png)

## Obter o URL do ponto de extremidade de streaming

Com o fluxo de dados de transmissão criado, agora é possível recuperar o URL do ponto de extremidade de transmissão. Esse endpoint será usado para assinar seu webhook, permitindo que a fonte de streaming se comunique com o Experience Platform.

Para recuperar o ponto de extremidade de streaming, vá para a página [!UICONTROL Dataflow activity] do fluxo de dados que você acabou de criar e copie o ponto de extremidade da parte inferior do painel [!UICONTROL Properties].

![A extremidade de streaming na atividade de fluxo de dados.](../assets/testing/endpoint-test.png)

## Próximas etapas

*Os fluxos de trabalho para as etapas restantes da criação de um fluxo de dados são modularizados. Se houver chamadas específicas que você queira fazer em relação à sua origem, consulte a seção de recursos adicionais abaixo.*

Seguindo este tutorial, você estabeleceu uma conexão com sua conta *YOURSOURCE*. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html?lang=pt-BR).

## Recursos adicionais

*Esta é uma seção opcional na qual você pode fornecer mais links para a documentação do produto ou quaisquer outras etapas, capturas de tela e nuances que considere importantes para o sucesso do cliente. Você pode usar esta seção para adicionar informações ou dicas sobre todo o fluxo de trabalho de sua origem, especialmente se houver &quot;armadilhas&quot; específicas que um usuário final possa encontrar.*
