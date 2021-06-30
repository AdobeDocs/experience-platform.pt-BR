---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API, perfil unificado, perfil unificado, unificado, perfil, rtcp, gráficos XDM
title: Soluções de acessibilidade personalizadas para o Experience Platform
topic-legacy: guide
type: Documentation
description: Saiba mais sobre as soluções de acessibilidade personalizadas na interface do usuário do Adobe Experience Platform.
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 0%

---


# Soluções de acessibilidade personalizadas para o Experience Platform

O Adobe Experience Platform é aprimorado continuamente para atender às necessidades de todos os tipos de usuários e seguir os padrões mundiais que incluem indivíduos com deficiências visuais, auditivas, de mobilidade ou outras. Este documento descreve as soluções de acessibilidade personalizadas na interface do usuário do Experience Platform.

## Visão geral da página inicial e da interface do usuário

A interface do usuário do Experience Platform atende às taxas de contraste necessárias para componentes normais de texto, gráficos e interface do usuário. As cores da interface do usuário também foram escolhidas para oferecer suporte à acessibilidade para todos os usuários, incluindo aqueles com deficiências visuais.

Na Plataforma, os elementos da interface do usuário que são clicáveis ou acionáveis com um ponteiro também podem ser envolvidos usando um teclado. Isso inclui a navegação à esquerda, reprodutores de vídeo, tabelas e muito mais.

O Experience Platform se esforça para atender aos padrões internacionais de acessibilidade, incluindo as diretrizes de acessibilidade de conteúdo da Web 2.1, Nível A e Nível AA e os padrões da Web Web Accessibility Initiative - Accessible Rich Internet Applications (WAI-ARIA).

![A página inicial da interface do usuário do Adobe Experience Platform.](images/homepage.png)

## Navegação à esquerda

A navegação à esquerda na interface do usuário do Experience Platform é acessível por teclado e fornece contraste de cores em estados normais, de flutuação e de seleção que atendam aos padrões de acessibilidade.

Na tela inicial, os usuários podem acessar a navegação à esquerda. Selecionar **Shift + Tab** retorna o usuário à tela inicial.

![A navegação Experience Platform à esquerda.](images/left-navigation-select.png)

Com a navegação à esquerda em foco, **Tab** leva os usuários para a interação expandir e recolher. A capacidade de expandir ou recolher a navegação à esquerda é ativada com **Enter (Return)**.

![A navegação Experience Platform à esquerda foi reduzida.](images/left-navigation-collapse.png)

Com a navegação à esquerda em foco, as teclas de seta para cima e para baixo navegam para cada item na navegação e ciclo continuamente (em outras palavras, o foco não se afasta até que o usuário se afaste da navegação à esquerda). O foco é mostrado para itens de navegação quando selecionado. A seleção atual é mostrada com um realce e um texto em negrito. Ao selecionar um item de navegação à esquerda, **Enter (Return)** abre o item de interface de usuário selecionado no painel direito, no entanto, o foco permanece na navegação à esquerda até que o usuário saia.

![A Experience Platform da navegação à esquerda com Fontes selecionadas.](images/left-navigation-sources.png)

Alguns recursos no Platform não estão habilitados para todos os usuários. Esses itens aparecem na navegação, mas não podem ser selecionados. Ao navegar com um teclado, esses itens são ignorados durante a navegação da seta e não podem ser selecionados usando **Enter (Return)**.

![Seções da navegação Experience Platform à esquerda que não estão habilitadas para o usuário não podem ser selecionadas.](images/left-navigation-sections-disabled.png)

## Caixa de diálogo de vídeo incorporado

Os vídeos podem ser exibidos no Experience Platform usando a navegação pelo teclado para realçar e selecionar um link de vídeo disponível. Isso abre uma caixa de diálogo de vídeo integrado na interface do usuário da plataforma.

![Uma borda azul que aparece em torno de um elemento selecionado para indicar que o foco é aplicado.](images/profile-overview-tab.png)

## Acessibilidade do teclado da caixa de diálogo de vídeo

A caixa de diálogo de vídeo incorporado também pode ser navegada usando o teclado. A tabela a seguir descreve a navegação completa do teclado disponível para a caixa de diálogo de vídeo incorporado.

| Elemento de diálogo | Acessibilidade do teclado | Descrição |
|---|---|---|
| Reproduzir e pausar | Tabulação<br/>Barra de espaço | Use **Tab** para definir o foco no botão Reproduzir. **** A barra de espaço inicia a reprodução do vídeo e pausa a reprodução. |
| Esmagador | Tabulação<br/>Seta para a esquerda<br/>Seta para a direita | Quando o vídeo estiver sendo reproduzido, use **Tab** para focalizar o depurador. Com o depurador em foco, **as teclas de seta para a esquerda e para a direita** ignoram a reprodução do vídeo com antecedência e volta em 5 segundos, respectivamente. |
| Mudo | Tabulação<br/>Barra de espaço | Use **Tab** para focalizar o elemento de volume mudo. Use a **barra de espaço** para silenciar ou ativar o som da reprodução do vídeo. |
| Volume | Tabulação<br/>Seta para a esquerda<br/>Seta para a direita | Use **Tab** para se concentrar no elemento de volume. **As** teclas de seta para a esquerda e para a direita movem o volume para cima e para baixo, respectivamente. |
| [!UICONTROL Legendas ocultas]  (&quot;cc&quot;) | Tabulação<br/>Enter<br/>Seta para cima<br/>Seta para baixo | **Elemento** Tabto  [!UICONTROL Closed Captions]  (&quot;cc&quot;). Use **Enter** para abrir o menu e **teclas de seta para cima e para baixo** para selecionar um idioma para legendas. **** Enterconfirm sua seleção. |
| [!UICONTROL Qualidade] | Tabulação<br/>Enter<br/>Seta para cima<br/>Seta para baixo | Use **Tab** para focalizar o elemento [!UICONTROL Qualidade]. Use **Enter** para abrir o menu e as **teclas de seta para cima e para baixo** para selecionar a qualidade do vídeo. **** Enterconfirm sua seleção. |
| Tela cheia | Tabulação<br/>Barra de espaço ou Enter<br/>Evitar | Use **Tab** para focalizar o elemento de tela cheia. Use **barra de espaço ou Enter** para ativar a visualização em tela cheia. **Escape** (&quot;esc&quot;) sai do modo de tela cheia. |
| Fechar | Tabulação<br/>Barra de espaço ou Enter | Use **Tab** para focalizar o botão fechar. Use a **barra de espaço ou a tecla Enter** para sair da caixa de diálogo do vídeo. |

>[!NOTE]
>
>A qualquer momento durante a reprodução, a tecla escape (&quot;esc&quot;) pode ser usada para fechar a caixa de diálogo do vídeo incorporado.

![A caixa de diálogo de vídeo incorporada com números que identificam elementos de navegação do teclado.](images/video-dialog.png)

## Arrastar e soltar arquivo

No Experience Platform, todas as zonas de arrastar e soltar da seleção de arquivos são acessíveis ao teclado. Usar **Tab** para realçar **[!UICONTROL Escolher arquivos]** e usar **Enter ou spacebar** para selecioná-lo chama a interface de seleção de arquivo do sistema operacional.

Após o upload de um arquivo, um ícone de exclusão se torna navegável pelo teclado para remover o arquivo selecionado e fazer upload de um novo. Os usuários podem usar **Tab** para se concentrar no ícone de exclusão e **Enter ou spacebar** para selecioná-lo. Depois que o arquivo for removido, **[!UICONTROL Choose files]** estará automaticamente em foco e poderá ser selecionado.

Como alternativa, se o arquivo carregado não estiver no formato correto, um ícone de erro será exibido junto com uma mensagem de erro e o botão **[!UICONTROL Choose files]** estará em foco e selecionável.

![Uma zona de arrastar e soltar arquivo com uma mensagem de erro e o botão Escolher arquivos em foco.](images/drag-and-drop.png)

Usar um mouse para selecionar a zona de arrastar e soltar também chama a interface de seleção de arquivo ou um usuário do mouse pode selecionar um arquivo e arrastar até a zona para começar a fazer o upload.

![Uma zona de arrastar e soltar arquivos em foco enquanto um usuário de mouse arrasta um arquivo para a zona.](images/drag-and-drop-mouse-over.png)

## Navegação em tabela

Todas as tabelas da interface do usuário do Experience Platform são acessíveis por teclado. A navegação e interação com linhas e colunas da tabela é possível por meio de uma série de atalhos do teclado:

* No cabeçalho da tabela, use a seta **para baixo** para navegar na tabela. Os cabeçalhos da tabela são selecionáveis ao navegar por **Tab**, e você pode alterar a ordem de classificação usando **spacebar**.
* **As** teclas de seta para cima e para baixo são movidas para cima e para baixo pelas linhas da tabela.
* Quando uma linha é selecionada ou está em foco, usar **Enter** na linha fornece detalhes no painel direito.
* Quando uma linha estiver selecionada ou em foco, use **as teclas de seta** para percorrer cada item na linha.
* Use **Enter** para selecionar um item na linha. Os usuários com leitores de tela são alertados se uma nova janela precisar ser aberta.

### Navegar pela acessibilidade do teclado da tabela

| Acessibilidade do teclado | Descrição |
|---|---|
| HOME (Função + seta para a esquerda) | Quando a linha é focada, os usuários são direcionados para o primeiro item na linha |
| END (Função + seta para a direita) | Quando a linha é focada, os usuários são direcionados para o último item na linha |
| Page up | Atravessa 10 linhas para cima na tabela (por página) |
| Page down | Atravessa 10 linhas para baixo na tabela (por página) |
| Controle + HOME | Vai para a primeira linha da tabela |
| Control + END | Vai para o primeiro trabalho na tabela por página |

## Interface do usuário do Editor de esquemas

A interface do Editor de esquemas é disponibilizada pela seguinte funcionalidade:

* O Editor de esquema suporta a navegação pelo teclado, incluindo o uso de **Tab** para navegar pelos elementos da interface do usuário.
* **** Tabelas insere o campo de pesquisa e, em seguida, a árvore de esquema.
* A árvore de esquema oferece suporte ao uso de teclas de seta para navegar pela interface da árvore de esquema
   * **As** setas para cima e para baixo devem ser usadas para atravessar a árvore.
   * **As** setas para a esquerda e para a direita podem ser usadas para expandir e recolher nós ou mover entre ações em linha na árvore de esquema.
* **Enter (Return)** ativa detalhes individuais do nó no painel de detalhes à direita.
* A tecla **Home** retorna ao topo da árvore.
* A tecla **End** navega até a parte inferior da árvore.
* A árvore de esquema também inclui rótulos ARIA para leitores de tela.

## Interface do usuário do Construtor de segmentos

Ao usar a interface do usuário do Construtor de segmentos para criar, editar e interagir com segmentos no Experience Platform, os seguintes recursos melhoram a acessibilidade:

* A interface do usuário do Construtor de segmentos pode ser acessada por meio da navegação pelo teclado.
* Os leitores de tela devem reconhecer tags de marcação para cabeçalhos e podem anunciar o cabeçalho junto com seu nível.
* Outras tecnologias de assistência podem alterar a exibição visual de uma página, usando cabeçalhos corretamente codificados para exibir um outline ou uma exibição alternativa.

## Editor do Serviço de Consulta

Os seguintes recursos de acessibilidade estão disponíveis no Editor do Serviço de query:

* O contraste de cores na interface do usuário do Editor do Serviço de query atende à conformidade de acessibilidade.
* A navegação por teclado é compatível fora da interface do editor. A interface do editor é um Espelho de código incorporado.

## Guia Exibição do sistema em Origens e Destinos

Ao navegar pela **[!UICONTROL Exibição do sistema]** em Fontes e Destinos, a seguinte funcionalidade melhora a acessibilidade:

* **** Os tabulações se concentram na primeira placa de conexão de origem
   * **** Tabulação novamente para focalizar o botão dentro do cartão
   * Selecione **Enter** para ativar o botão de ação da chamada para dentro do cartão
* Selecionar **Enter** no cartão de conexão também ativa mais detalhes no painel direito
   * Quando o painel direito for ativado, o foco é definido para essa área. **** As guias se concentram em  **** Fechar para o painel direito. Selecionar **Tab** novamente move o foco através do painel direito do painel
   * Se houver mais de uma placa de conexão de origem, **Tab** se move pelas conexões
   * Use **as teclas de seta (para cima, para baixo, para a esquerda e para a direita)** para percorrer a lista de origens
   * Selecione **Tab** para definir o foco no painel direito do painel