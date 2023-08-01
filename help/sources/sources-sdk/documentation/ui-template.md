---
keywords: Experience Platform;página inicial;tópicos populares;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK
title: Modelo de documentação de autoatendimento para a interface do
description: Saiba como criar uma conexão de origem YOURSOURCE usando a interface do usuário do Adobe Experience Platform.
exl-id: 6471c0a2-22e8-4133-a76f-ee3c5c669ef8
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 1%

---

# Criar um *SUA FONTE* conexão de origem na interface

*À medida que passa por esse modelo, substitua ou exclua todos os parágrafos em itálico (começando por este).*

*Comece atualizando os metadados (título e descrição) na parte superior da página. Ignore todas as instâncias de UICONTROL nesta página. Essa é uma tag que ajuda nossos processos de tradução automática a traduzir corretamente a página para os vários idiomas compatíveis. Adicionaremos tags à sua documentação depois que você enviá-la.*

Este tutorial fornece etapas para a criação de um *SUA FONTE* conector de origem usando a interface do usuário da Platform.

## Visão geral

*Forneça uma breve visão geral da sua empresa, incluindo o valor que ela oferece aos clientes. Inclua um link para a página inicial da documentação do produto, para leitura adicional.*

>[!IMPORTANT]
>
>Esse conector de origem e a página de documentação são criados e mantidos pelo *SuaOrigem* equipe. Para qualquer consulta ou solicitação de atualização, entre em contato diretamente em *Inserir link ou endereço de email no qual você pode ser contatado para obter atualizações*.

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

## Conecte seu *SUA FONTE* account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No *CATEGORIA DE SUA FONTE* categoria, selecione *SUA FONTE* e selecione **[!UICONTROL Adicionar dados]**.

>[!TIP]
>
>As capturas de tela usadas abaixo são exemplos. Ao criar sua documentação, substitua as imagens por capturas de tela da origem real. É possível usar o mesmo padrão de marcação e cor, bem como os mesmos nomes de arquivo. Certifique-se de que sua captura de tela capture toda a tela da interface do usuário da Platform. Para obter informações sobre como fazer upload de capturas de tela, consulte o manual sobre [enviar sua documentação para revisão](./github.md).

![catálogo](../assets/ui/catalog.png)

A variável **[!UICONTROL Conecte sua conta de ORIGEM]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a variável *SUA FONTE* conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../assets/ui/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![novo](../assets/ui/new.png)

## Próximas etapas

*Os workflows para as etapas restantes de criação de um fluxo de dados são modularizados. Se houver chamadas específicas que você queira fazer em relação à sua origem, consulte a seção de recursos adicionais abaixo.*

Ao seguir este tutorial, você estabeleceu uma conexão com o seu *SUA FONTE* conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Recursos adicionais

*Esta é uma seção opcional na qual você pode fornecer links adicionais para a documentação do seu produto ou quaisquer outras etapas, capturas de tela e nuances que considere importantes para o cliente ser bem-sucedido. Você pode usar esta seção para adicionar informações ou dicas sobre todo o fluxo de trabalho da sua fonte, especialmente se houver &quot;armadilhas&quot; específicas que um usuário final possa encontrar.*
