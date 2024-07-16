---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API;perfil unificado;Perfil unificado;perfil;gráficos XDM
title: Soluções personalizadas de acessibilidade para o Experience Platform
type: Documentation
description: Saiba mais sobre as soluções de acessibilidade personalizadas na interface do usuário do Adobe Experience Platform.
exl-id: cb5ad99e-8a95-4c9e-aae6-1d0036ecf052
source-git-commit: 2cf28acb5b0ddb4965b2d5120333659e0ac460bf
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 0%

---

# Soluções de acessibilidade personalizadas para o Experience Platform

O Adobe Experience Platform é aprimorado continuamente para atender às necessidades de todos os tipos de usuários e aderir aos padrões mundiais que incluem indivíduos com deficiências visuais, auditivas, de mobilidade ou outras. Este documento descreve soluções de acessibilidade personalizadas na interface do usuário do Experience Platform.

## Visão geral da página inicial e da interface do usuário

A interface de usuário do Experience Platform atende às taxas de contraste necessárias para texto normal, gráficos e componentes de interface do usuário. As cores da interface do usuário também foram escolhidas para oferecer suporte à acessibilidade para todos os usuários, incluindo aqueles com deficiências visuais.

Na Platform, os elementos da interface do usuário clicáveis ou acionáveis com um ponteiro também podem ser engajados usando um teclado. Isso inclui a navegação à esquerda, players de vídeo, tabelas e muito mais.

O Experience Platform se esforça para atender aos padrões internacionais de acessibilidade, incluindo as Web Content Accessibility Guidelines 2.1 Nível A e Nível AA e os padrões Web Web Web Accessibility Initiative - Accessible Rich Internet Applications (WAI-ARIA).

![A página inicial da interface do usuário do Adobe Experience Platform.](images/homepage.png)

## Navegação à esquerda

A navegação à esquerda na interface do usuário do Experience Platform é acessível pelo teclado e fornece contraste de cores em estados normais, de passar o mouse e de seleção que atendem aos padrões de acessibilidade.

Na tela inicial, os usuários podem ir para a navegação à esquerda. Selecionar **Shift + Tab** retornará o usuário à tela inicial.

![A navegação à esquerda do Experience Platform.](images/left-navigation-select.png)

Com a navegação à esquerda em foco, a **Guia** leva os usuários para a interação de expansão e recolhimento. A capacidade de expandir ou recolher a navegação à esquerda é ativada com **Enter (Return)**.

![A navegação à esquerda do Experience Platform foi recolhida.](images/left-navigation-collapse.png)

Com a navegação à esquerda em foco, as teclas de seta para cima e para baixo navegam até cada item na navegação e alternam continuamente (em outras palavras, o foco não é deslocado até que o usuário saia da navegação à esquerda). O foco é mostrado para itens de navegação quando selecionado. A seleção atual é mostrada com um realce e um texto em negrito. Ao selecionar um item de navegação à esquerda, **Inserir (Retornar)** abre o item de interface do usuário selecionado no painel à direita. No entanto, o foco permanece na navegação à esquerda até que o usuário se afaste.

![A navegação à esquerda do Experience Platform com Fontes selecionadas.](images/left-navigation-sources.png)

Alguns recursos na Platform não estão habilitados para todos os usuários. Esses itens aparecem na navegação, mas não podem ser selecionados. Ao navegar com um teclado, esses itens são ignorados durante a navegação de seta e não podem ser selecionados usando **Enter (Return)**.

![As seções de navegação à esquerda do Experience Platform que não estão habilitadas para o usuário não podem ser selecionadas.](images/left-navigation-sections-disabled.png)

## Caixa de diálogo Vídeo incorporado

Os vídeos podem ser exibidos no Experience Platform usando a navegação pelo teclado para realçar e selecionar um link de vídeo disponível. Isso abre uma caixa de diálogo de vídeo incorporada na interface do usuário da Platform.

![Uma borda azul que aparece ao redor de um elemento selecionado para indicar que o foco está aplicado.](images/profile-overview-tab.png)

## Acessibilidade do teclado da caixa de diálogo de vídeo

A caixa de diálogo de vídeo incorporado também pode ser navegada usando o teclado. A tabela a seguir descreve a navegação completa pelo teclado disponível para a caixa de diálogo de vídeo incorporado.

| Elemento da caixa de diálogo | Acessibilidade do teclado | Descrição |
|---|---|---|
| Reproduzir e pausar | Guia<br/>Barra de espaço | Use **Tab** para definir o foco no botão Reproduzir. A **Barra de Espaços** inicia a reprodução de vídeo e pausa a reprodução. |
| Depurador | Guia<br/>Seta para a esquerda<br/>Seta para a direita | Quando o vídeo estiver sendo reproduzido, use **Tab** para focalizar o depurador. Com o depurador em foco, **as teclas de seta para a esquerda e para a direita** ignoram a reprodução de vídeo 5 segundos, respectivamente. |
| Silenciar | Guia<br/>Barra de espaço | Use **Tab** para focalizar o elemento de volume mudo. Use a **barra de espaços** para ativar ou desativar o som da reprodução de vídeo. |
| Volume | Guia<br/>Seta para a esquerda<br/>Seta para a direita | Use **Tab** para focalizar o elemento de volume. **Teclas de seta para a esquerda e para a direita** movem o volume para cima e para baixo, respectivamente. |
| [!UICONTROL Legendas ocultas] (&quot;cc&quot;) | Guia<br/>Inserir<br/>Seta para cima<br/>Seta para baixo | **Guia** para [!UICONTROL Elemento de Legendas ocultas] (&quot;cc&quot;). Use **Enter** para abrir o menu e **teclas de seta para cima e para baixo** para selecionar um idioma para as legendas. **Inserir** confirma sua seleção. |
| [!UICONTROL Qualidade] | Guia<br/>Inserir<br/>Seta para cima<br/>Seta para baixo | Use **Tab** para focalizar o elemento [!UICONTROL Quality]. Use **Enter** para abrir o menu e as **teclas de seta para cima e para baixo** para selecionar a qualidade do vídeo. **Inserir** confirma sua seleção. |
| Tela cheia | Tab<br/>Barra de Espaços ou Enter<br/>Escape | Use **Tab** para focalizar o elemento de tela inteira. Use a **barra de espaço ou Enter** para ativar o modo de exibição de tela inteira. **Escape** (&quot;esc&quot;) sai do modo de tela cheia. |
| Fechar | Tab<br/>Barra de Espaços ou Enter | Use **Tab** para focalizar o botão Fechar. Use a **barra de espaços ou a tecla Enter** para sair da caixa de diálogo de vídeo. |

>[!NOTE]
>
>A qualquer momento durante a reprodução, a tecla escape (&quot;esc&quot;) pode ser usada para fechar a caixa de diálogo de vídeo incorporada.

![A caixa de diálogo de vídeo inserido com números que identificam elementos de navegação do teclado.](images/video-dialog.png)

## Arrastar e soltar arquivo

No Experience Platform, todas as zonas de arrastar e soltar para seleção de arquivos são acessíveis pelo teclado. Usar **Tab** para realçar **[!UICONTROL Escolher arquivos]** e usar **Enter ou a barra de espaços** para selecioná-la invoca a interface de seleção de arquivos do sistema operacional.

Depois que um arquivo é carregado, um ícone de exclusão se torna navegável pelo teclado para remover o arquivo selecionado e carregar um novo. Os usuários podem usar a **Guia** para se concentrarem no ícone de exclusão e a **Enter ou a barra de espaços** para selecioná-lo. Após a remoção do arquivo, **[!UICONTROL Escolher arquivos]** ficará automaticamente em foco e poderá ser selecionado.

Como alternativa, se o arquivo carregado não estiver no formato correto, um ícone de erro será exibido junto com uma mensagem de erro e o botão **[!UICONTROL Escolher arquivos]** estará em foco e poderá ser selecionado.

![Uma zona de arrastar e soltar arquivos com uma mensagem de erro e o botão Escolher arquivos em foco.](images/drag-and-drop.png)

Usar um mouse para selecionar a zona de arrastar e soltar também chama a interface de seleção de arquivos, ou um usuário de mouse pode selecionar um arquivo e arrastar até a zona para começar o upload.

![Uma zona de arrastar e soltar arquivos em foco quando um usuário de mouse arrasta um arquivo para a zona.](images/drag-and-drop-mouse-over.png)

## Procurar tabela

Todas as tabelas na interface do usuário do Experience Platform podem ser acessadas pelo teclado. Procurar e interagir com linhas e colunas da tabela é possível por meio de uma série de atalhos de teclado:

* No cabeçalho da tabela, use a **seta para baixo** para navegar na tabela. Os cabeçalhos da tabela podem ser selecionados ao navegar pela **Guia**, e você pode alterar a ordem de classificação usando a **barra de espaço**.
* **Teclas de seta para cima e para baixo** movem-se para cima e para baixo nas linhas da tabela.
* Quando uma linha é selecionada ou está em foco, usar **Enter** na linha fornece detalhes no painel direito.
* Quando uma linha for selecionada ou estiver em foco, use as **teclas de seta** para percorrer cada item na linha.
* Use **Enter** para selecionar um item na linha. Os usuários com leitores de tela são avisados se uma nova janela precisar ser aberta.
* Ao ampliar para 200% ou mais, você pode ver o ícone do **inspetor do painel** à medida que o painel direito é recolhido para fornecer mais espaço de visualização para a tabela.

![O ícone do inspetor do painel em foco quando um usuário aumenta para 200%.](images/rail-inspector.png)

### Procurar acessibilidade do teclado da tabela

| Acessibilidade do teclado | Descrição |
|---|---|
| HOME (Função + seta para a esquerda) | Quando a linha é focalizada, leva os usuários para o primeiro item na linha |
| END (Função + seta para a direita) | Quando a linha é focalizada, leva os usuários para o último item da linha |
| Página para cima | Atravessa 10 linhas para cima na tabela (por página) |
| Página para baixo | Atravessa 10 linhas para baixo na tabela (por página) |
| Control + HOME | Vai para a primeira linha da tabela |
| Control+END | Vai para o primeiro trabalho na tabela por página |

## Interface do Editor de esquemas

A interface do Editor de esquemas é acessível pela seguinte funcionalidade:

* O Editor de Esquemas oferece suporte à navegação pelo teclado, incluindo o uso de **Tab** para navegação pelos elementos da interface.
* **Guia** entra no campo de pesquisa e, em seguida, na árvore de esquema.
* A árvore de esquema suporta o uso de teclas de seta para navegar pela interface da árvore de esquema
   * **As setas para cima e para baixo** podem ser usadas para percorrer a árvore.
   * **As setas para a esquerda e para a direita** podem ser usadas para expandir e recolher nós ou se mover entre ações embutidas na árvore de esquema.
* **Inserir (Retornar)** ativa os detalhes de nós individuais no painel de detalhes à direita.
* A tecla **Home** retorna à parte superior da árvore.
* A chave **End** navega até a parte inferior da árvore.
* A árvore de esquema também inclui rótulos ARIA para leitores de tela.

## Interface do construtor de segmentos

Ao usar a interface do Construtor de segmentos para criar, editar e interagir com segmentos no Experience Platform, os seguintes recursos melhoram a acessibilidade:

* A interface do usuário do Construtor de segmentos pode ser acessada pela navegação pelo teclado.
* Os leitores de tela devem reconhecer as tags de marcação para cabeçalhos e podem anunciar o cabeçalho junto com seu nível.
* Outras tecnologias de assistência podem alterar a exibição visual de uma página, usando cabeçalhos codificados corretamente para exibir um outline ou uma exibição alternativa.

Agora é possível recolher ou expandir os painéis esquerdo e direito da tela do construtor de segmentos para obter mais espaço na tela. Esse recurso é particularmente útil, pois oferece capacidade de função completa com 200% de zoom.

![A tela do construtor de segmentos com os widgets de divulgação do painel esquerdo e direito realçados.](images/left-right-rail-expandables.png)

## Editor do serviço de consulta

Os seguintes recursos de acessibilidade estão disponíveis no editor do Serviço de consulta:

* O contraste de cores na interface do editor do Serviço de consulta atende à conformidade de acessibilidade.
* A navegação pelo teclado é suportada fora da interface do editor. A interface do usuário do editor é um Espelho de código incorporado.

>[!NOTE]
>
>O Editor de consultas não lida com a chave **Tab** por padrão. Para invocar a funcionalidade **Tab** enquanto estiver no editor, você deve pressionar a tecla **Escape** e pressionar **Tab** diretamente após ela. Pressione **Tab** novamente para mover o foco para além do editor.

## Guia Exibição de sistema em Origens e Destinos

Ao navegar pela **[!UICONTROL Exibição do Sistema]** em Fontes e Destinos, a seguinte funcionalidade melhora a acessibilidade:

* **Tab** define o foco na primeira placa de conexão de origem
   * **Pressione Tab** novamente para focalizar no botão dentro do cartão
   * Selecione **Inserir** para ativar o botão de chamada para ação dentro do cartão
* Selecionar **Enter** no cartão de conexão também ativa mais detalhes no painel direito
   * Quando o painel direito é ativado, o foco é definido para essa área. **Guia** focaliza em **Fechar** para o painel direito. Selecionar **Tab** novamente move o foco pelo painel direito
   * Se houver mais de uma placa de conexão de origem, **Tab** percorrerá as conexões
   * Use **teclas de seta (para cima, para baixo, para a esquerda e para a direita)** para percorrer a lista de fontes
   * Selecione **Guia** para definir o foco no painel direito
