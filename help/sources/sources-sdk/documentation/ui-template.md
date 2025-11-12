---
keywords: Experience Platform;página inicial;tópicos populares;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK
title: Modelo de documentação de autoatendimento para a interface do
description: Saiba como criar uma conexão de origem YOURSOURCE usando a interface do usuário do Adobe Experience Platform.
exl-id: 6471c0a2-22e8-4133-a76f-ee3c5c669ef8
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 1%

---

# Criar uma conexão de origem *YOURSOURCE* na interface

*Conforme você passar por este modelo, substitua ou exclua todos os parágrafos em itálico (começando por este).*

*Comece atualizando os metadados (título e descrição) na parte superior da página. Ignore todas as instâncias de UICONTROL nesta página. Essa é uma tag que ajuda nossos processos de tradução automática a traduzir corretamente a página para os vários idiomas compatíveis. Adicionaremos marcas à sua documentação após você enviá-la.*

Este tutorial fornece etapas para a criação de um conector de origem *YOURSOURCE* usando a interface do usuário do Experience Platform.

## Visão geral

*Forneça uma breve visão geral da sua empresa, incluindo o valor que ela oferece aos clientes. Inclua um link para a página inicial da documentação do produto para leitura adicional.*

>[!IMPORTANT]
>
>Este conector de origem e página de documentação são criados e mantidos pela equipe *YourSource*. Para qualquer consulta ou solicitação de atualização, contate-os diretamente em *Inserir link ou endereço de email onde você pode ser contatado para atualizações*.

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

## Conecte sua conta *YOURSOURCE*

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Sources]. A tela [!UICONTROL Catalog] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *CATEGORIA* de YOURSOURCE, selecione *YOURSOURCE* e **[!UICONTROL Add data]**.

>[!TIP]
>
>As capturas de tela usadas abaixo são exemplos. Ao criar sua documentação, substitua as imagens por capturas de tela da origem real. É possível usar o mesmo padrão de marcação e cor, bem como os mesmos nomes de arquivo. Certifique-se de que sua captura de tela capture toda a tela da interface do usuário do Experience Platform. Para obter informações sobre como carregar capturas de tela, consulte o manual em [enviando sua documentação para revisão](./github.md).

![catálogo](../assets/ui/catalog.png)

A página **[!UICONTROL Connect YOURSOURCE account]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta *YOURSOURCE* com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Next]** para continuar.

![existente](../assets/ui/existing.png)

### Nova conta

Se você estiver criando uma nova conta, selecione **[!UICONTROL New account]** e forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Connect to source]** e aguarde algum tempo para a nova conexão ser estabelecida.

![novo](../assets/ui/new.png)

## Próximas etapas

*Os fluxos de trabalho para as etapas restantes da criação de um fluxo de dados são modularizados. Se houver chamadas específicas que você queira fazer em relação à sua origem, consulte a seção de recursos adicionais abaixo.*

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta *YOURSOURCE*. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html?lang=pt-BR).

## Recursos adicionais

*Esta é uma seção opcional na qual você pode fornecer mais links para a documentação do produto ou quaisquer outras etapas, capturas de tela e nuances que considere importantes para o sucesso do cliente. Você pode usar esta seção para adicionar informações ou dicas sobre todo o fluxo de trabalho de sua origem, especialmente se houver &quot;armadilhas&quot; específicas que um usuário final possa encontrar.*
