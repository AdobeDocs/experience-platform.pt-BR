---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
title: Modelo de documentação de autoatendimento para a interface do usuário
description: Saiba como criar uma conexão de origem YOURSOURCE usando a interface do usuário do Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 39accd28edc388c6444910f9a2ea6d2f01acfdaf
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---

# Crie um *SUA FONTE* conexão de origem na interface do usuário

*Conforme você passa por esse modelo, substitua ou exclua todos os parágrafos em itálico (começando por este).*

*Comece atualizando os metadados (título e descrição) na parte superior da página. Ignore todas as instâncias do UICONTROL nesta página. Esta é uma tag que ajuda nossos processos de tradução automática a traduzir a página corretamente para os vários idiomas suportados. Adicionaremos tags à sua documentação após enviá-la.*

Este tutorial fornece etapas para criar um *SUA FONTE* conector de origem usando a interface do usuário da plataforma.

## Visão geral

*Forneça uma breve visão geral da empresa, incluindo o valor que ela oferece aos clientes. Inclua um link para a página inicial da documentação do produto para mais leitura.*

>[!IMPORTANT]
>
>Esta página de documentação foi criada pela *SUA FONTE* equipe. Para quaisquer consultas ou pedidos de atualização, contacte-os diretamente em *Inserir link ou endereço de email onde você pode acessar para obter atualizações*.

## Pré-requisitos

*Adicione informações nesta seção sobre qualquer coisa que os clientes precisam saber antes de começar a configurar a origem na interface do usuário do Adobe Experience Platform. Isso pode ser sobre:*

* *precisar ser adicionado a uma lista de permissões*
* *requisitos para hash de email*
* *qualquer conta específica do seu lado*
* *como obter as credenciais de autenticação para se conectar à plataforma*

### Obter credenciais necessárias

Para se conectar *SUA FONTE* para Plataforma, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| *credencial um* | *Adicione uma breve descrição à credencial de autenticação da sua origem aqui* | *Adicione aqui um exemplo da credencial de autenticação da sua origem* |
| *credencial dois* | *Adicione uma breve descrição à credencial de autenticação da sua origem aqui* | *Adicione aqui um exemplo da credencial de autenticação da sua origem* |
| *credencial três* | *Adicione uma breve descrição à credencial de autenticação da sua origem aqui* | *Adicione aqui um exemplo da credencial de autenticação da sua origem* |

Para obter mais informações sobre essas credenciais, consulte o *SUA FONTE* documentação de autenticação. *Adicione um link à documentação de autenticação da plataforma aqui*.

## Conecte seu *SUA FONTE* account

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em *CATEGORIA DA SUA FONTE* categoria , selecione *SUA FONTE* e selecione **[!UICONTROL Adicionar dados]**.

>[!TIP]
>
>As capturas de tela usadas abaixo são exemplos. Ao criar sua documentação, substitua as imagens por capturas de tela de sua fonte real. Você pode usar o mesmo padrão e a mesma cor de marcação, bem como os mesmos nomes de arquivo. Certifique-se de que a captura de tela capture a tela inteira da interface do usuário da plataforma. Para obter informações sobre como fazer upload de suas capturas de tela, consulte o guia em [enviar sua documentação para revisão](./github.md).

![catálogo](../assets/ui/catalog.png)

O **[!UICONTROL Conectar sua conta de ORIGEM]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para usar uma conta existente, selecione a *SUA FONTE* conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../assets/ui/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e, em seguida, forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e, em seguida, permitir que a nova conexão seja estabelecida.

![novo](../assets/ui/new.png)

## Próximas etapas

*Os workflows para as etapas restantes da criação de um fluxo de dados são modularizados. Se houver chamadas de retorno específicas que você queira fazer em relação à sua fonte, consulte a seção recursos adicionais abaixo.*

Ao seguir este tutorial, você estabeleceu uma conexão com seu *SUA FONTE* conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a plataforma](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Recursos adicionais

*Esta é uma seção opcional na qual você pode fornecer mais links para a documentação do seu produto ou quaisquer outras etapas, capturas de tela, nuances que você considere importantes para o sucesso do cliente. Você pode usar esta seção para adicionar informações ou dicas sobre todo o fluxo de trabalho da sua origem, especialmente se houver &quot;gotchas&quot; específicas que um usuário final poderá encontrar.*
