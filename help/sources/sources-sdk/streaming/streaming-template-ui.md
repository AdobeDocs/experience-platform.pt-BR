---
title: Modelo de autoatendimento de documentação para interface de usuário do SDK de streaming
description: Saiba como trazer dados de transmissão de uma origem para a Adobe Experience Platform usando a interface do usuário.
hide: true
hidefromtoc: true
exl-id: 82254be0-fa31-4114-a0ec-179a990e0904
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 1%

---

# Criar uma conexão de origem e um fluxo de dados para transmissão *SUA FONTE* dados usando a interface

*À medida que passa por esse modelo, substitua ou exclua todos os parágrafos em itálico (começando por este).*

*Comece atualizando os metadados (título e descrição) na parte superior da página. Ignore todas as instâncias de UICONTROL nesta página. Essa é uma tag que ajuda nossos processos de tradução automática a traduzir corretamente a página para os vários idiomas compatíveis. Adicionaremos tags à sua documentação depois que você enviá-la.*

Este tutorial fornece etapas para a criação de um *SUA FONTE* conector de origem usando a interface do usuário da Platform.

## Visão geral

*Forneça uma breve visão geral da sua empresa, incluindo o valor que ela oferece aos clientes. Inclua um link para a página inicial da documentação do produto, para leitura adicional.*

>[!IMPORTANT]
>
>Esse conector de origem e a página de documentação são criados e mantidos pelo *SUA FONTE* equipe. Para qualquer consulta ou solicitação de atualização, entre em contato diretamente em *Inserir link ou endereço de email no qual você pode ser contatado para obter atualizações*.

## Pré-requisitos

*Adicione informações nesta seção sobre qualquer coisa que os clientes precisem saber antes de começar a configurar o código-fonte na interface do usuário do Adobe Experience Platform. Isso pode se referir a:*

* *que precisam ser adicionados a uma lista de permissões*
* *requisitos para hash de email*
* *quaisquer detalhes específicos da conta da sua parte*
* *como obter as credenciais de autenticação para se conectar à sua plataforma*

### Coletar credenciais necessárias

Para se conectar *SUA FONTE* Para o Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| *credencial um* | *Adicione uma breve descrição à credencial de autenticação da sua origem aqui* | *Adicione um exemplo da credencial de autenticação da sua origem aqui* |
| *credencial dois* | *Adicione uma breve descrição à credencial de autenticação da sua origem aqui* | *Adicione um exemplo da credencial de autenticação da sua origem aqui* |
| *credencial três* | *Adicione uma breve descrição à credencial de autenticação da sua origem aqui* | *Adicione um exemplo da credencial de autenticação da sua origem aqui* |

Para obter mais informações sobre essas credenciais, consulte a *SUA FONTE* documentação de autenticação. *Adicione aqui o link para a documentação de autenticação da sua plataforma*.

### Integrar *SUA FONTE* com seu webhook

*O SDK de transmissão exige que a fonte seja compatível com webhooks para se comunicar com o Experience Platform. Nesta seção, você deve fornecer as etapas que os usuários terão que seguir para integrar YOURSOURCE a um webhook.*

## Conecte seu *SUA FONTE* account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No **Streaming** categoria, selecione *SUA FONTE* e selecione **[!UICONTROL Adicionar dados]**.

>[!TIP]
>
>As capturas de tela usadas abaixo são exemplos. Ao criar sua documentação, substitua as imagens por capturas de tela da origem real. É possível usar o mesmo padrão de marcação e cor, bem como os mesmos nomes de arquivo. Certifique-se de que sua captura de tela capture toda a tela da interface do usuário da Platform. Para obter informações sobre como fazer upload de capturas de tela, consulte o manual sobre [enviar sua documentação para revisão](../documentation/github.md).

![O catálogo de fontes do Experience Platform](../assets/streaming/catalog.png)

## Selecionar dados

A variável **[!UICONTROL Selecionar dados]** será exibida, fornecendo uma interface para você selecionar os dados que trará para a Platform.

* A parte esquerda da interface é um navegador que permite visualizar os fluxos de dados disponíveis em sua conta;
* A parte direita da interface permite visualizar até 100 linhas de dados de um arquivo JSON.

Selecionar **[!UICONTROL Fazer upload de arquivos]** para carregar um arquivo JSON do seu sistema local. Como alternativa, você pode arrastar e soltar o arquivo JSON que deseja fazer upload na [!UICONTROL Arrastar e soltar arquivos] painel.

![A etapa adicionar dados do fluxo de trabalho de fontes.](../assets/streaming/add-data.png)

Depois que o arquivo for carregado, a interface de visualização será atualizada para exibir uma visualização do esquema carregado. A interface de visualização permite inspecionar o conteúdo e a estrutura de um arquivo. Você também pode usar a variável [!UICONTROL Campo de pesquisa] para acessar itens específicos no esquema.

Quando terminar, selecione **[!UICONTROL Próxima]**.

![A etapa de visualização do fluxo de trabalho de origens.](../assets/streaming/preview.png)

## Detalhes do fluxo de dados

A variável **Detalhes do fluxo de dados** A etapa é exibida, fornecendo opções para usar um conjunto de dados existente ou estabelecer um novo para o fluxo de dados, bem como uma oportunidade de fornecer um nome e uma descrição para o fluxo de dados. Durante essa etapa, você também pode definir configurações para Assimilação de perfil, diagnóstico de erro, assimilação parcial e alertas.

Quando terminar, selecione **[!UICONTROL Próxima]**.

![A etapa detalhada do fluxo de dados do fluxo de trabalho de origens.](../assets/streaming/dataflow-detail.png)

## Mapeamento

A variável [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

A Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso. Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre como usar a interface do mapeador e campos calculados, consulte [Guia da interface de preparação de dados](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Depois que os dados de origem forem mapeados com sucesso, selecione **[!UICONTROL Próxima]**.

![A etapa de mapeamento do fluxo de trabalho de origens.](../assets/streaming/mapping.png)

## Consulte a seção

A variável **[!UICONTROL Revisão]** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas nesse arquivo de origem.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

Depois de revisar o fluxo de dados, clique em **[!UICONTROL Concluir]** e aguarde algum tempo para criar o fluxo de dados.

![A etapa de revisão do fluxo de trabalho de origens.](../assets/streaming/review.png)

## Obter o URL do ponto de extremidade de streaming

Com o fluxo de dados de transmissão criado, agora é possível recuperar o URL do ponto de extremidade de transmissão. Esse endpoint será usado para assinar seu webhook, permitindo que a fonte de streaming se comunique com o Experience Platform.

Para recuperar o ponto de extremidade de transmissão, acesse o [!UICONTROL Atividade de fluxo de dados] página do fluxo de dados que você acabou de criar e copie o ponto de extremidade da parte inferior do [!UICONTROL Propriedades] painel.

![O ponto final de transmissão na atividade de fluxo de dados.](../assets/testing/endpoint-test.png)

## Próximas etapas

*Os workflows para as etapas restantes de criação de um fluxo de dados são modularizados. Se houver chamadas específicas que você queira fazer em relação à sua origem, consulte a seção de recursos adicionais abaixo.*

Ao seguir este tutorial, você estabeleceu uma conexão com o seu *SUA FONTE* conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Recursos adicionais

*Esta é uma seção opcional na qual você pode fornecer links adicionais para a documentação do seu produto ou quaisquer outras etapas, capturas de tela e nuances que considere importantes para o cliente ser bem-sucedido. Você pode usar esta seção para adicionar informações ou dicas sobre todo o fluxo de trabalho da sua fonte, especialmente se houver &quot;armadilhas&quot; específicas que um usuário final possa encontrar.*
