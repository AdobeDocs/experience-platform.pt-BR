---
title: Republicar uma biblioteca
description: Saiba como republicar uma biblioteca de tag anterior na Adobe Experience Platform.
exl-id: 026b01f2-a93d-4e8a-9ed2-47c4f011e70f
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 93%

---

# Republicar uma biblioteca

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

As cinco bibliotecas mais recentes que foram publicadas no seu ambiente de produção em uma propriedade da Web estão disponíveis para posterior recuperação. Esse recurso é útil quando você encontra um bug na biblioteca de produção e precisa revertê-la para um estado em boas condições imediatamente.

O processo de recuperação depende das configurações do ambiente no momento em que a biblioteca foi originalmente publicada. Isso é importante porque a recuperação de uma biblioteca arquivada não altera nada no site que está ativo, enquanto uma recuperação de uma biblioteca comum alteraria.

As opções disponíveis são as seguintes:

* **Host: Gerenciado pela Adobe, Arquivamento: desativado:** Se você estiver usando o host gerenciado pela Adobe e não estiver arquivando a biblioteca, será possível republicar essas bibliotecas mais antigas.

* **Host: gerenciado pela Adobe, Arquivamento: ativado:** se você estiver usando o host gerenciado pela Adobe e estiver arquivando a biblioteca, será possível baixar essas bibliotecas mais antigas.

* **Host: SFTP, Arquivamento: Ligado ou desligado:** se estiver usando o host SFTP, presume-se que você tenha estratégias de arquivamento próprias em funcionamento e que nenhuma opção de recuperação está disponível.

As opções de recuperação para propriedades em dispositivos móveis ainda não estão disponíveis.

## Republicação

Cada ambiente de tag fornece um link de um arquivo de biblioteca. Qualquer biblioteca que você criar nesse ambiente será referenciável por meio desse link.

Quando é gerada uma build de um ambiente de desenvolvimento ou de preparo, a antiga é removida e a nova build é implantada. Para seu ambiente de produção, esse link é atualizado para apontar para a build mais recente, mas as cinco builds mais recentes são mantidas antes de serem limpas.

Essas cinco builds mais recentes em seu ambiente de produção são aquelas que estão disponíveis para recuperação.

Quando você republica uma biblioteca mais antiga, a Platform atualiza o link do ambiente para apontar para um dos builds mais antigos que ainda não foram removidos.  Além disso, a Platform emite uma solicitação de limpeza para os nós de borda da CDN a fim de indicar que a biblioteca foi atualizada e que uma cópia nova deve ser recuperada da origem.

Isso significa que, ao publicar novamente uma biblioteca mais antiga:

* Não são feitas alterações em nenhum dos recursos (ou revisões históricas) na propriedade da tag

* A forma como os ambientes de desenvolvimento e de preparo calculam o que está em contrafluxo não muda

Leve em consideração a situação ao reverter a versão por causa de um problema com uma regra específica. A revisão de regra que está em produção pode, por exemplo, ter sido implementada há três versões atrás. Quando você exibe essa regra na interface do usuário para corrigi-la, ela ainda reflete as alterações mais salvas recentes, em vez das que estão em produção.

Por essa razão, a Platform notifica você de que uma propriedade consta como republicada, para lembrá-lo de que o que está vendo na interface da Coleção de dados está um pouco mais distante da produção do que o normal. Essa notificação é dispensável e aparece uma vez por sessão do navegador na primeira vez que você exibe a propriedade.

### Como republicar uma biblioteca mais antiga

![Como republicar uma biblioteca](images/retrieve_republish.png)

Na tela Publicação:

1. Localize na coluna Publicado a biblioteca que você deseja republicar.
1. Selecione as reticências (`...`) no canto superior direito do cartão Biblioteca.
1. Selecione **[!UICONTROL Republicar]**.

## Baixar

Baixar uma biblioteca arquivada é mais simples. Você não está fazendo referência direta a esses arquivos .zip em lugar nenhum, portanto, basta baixar a biblioteca mais antiga no seu computador e executar o processo normal.

### Como baixar uma biblioteca mais antiga

![Como baixar uma biblioteca](images/retrieve_download.png)

Na tela Publicação:

1. Localize na coluna Publicado a biblioteca que você deseja baixar.
1. Selecione as reticências (`...`) no canto superior direito do cartão Biblioteca.
1. Selecione **[!UICONTROL Download]**.
