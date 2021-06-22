---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API, perfil unificado, perfil unificado, unificado, perfil, rtcp, gráficos XDM
title: Recursos gerais de acessibilidade na plataforma
topic: guia
type: Documentation
description: Saiba mais sobre os recursos gerais de acessibilidade compatíveis com o Adobe Experience Platform, incluindo navegação por teclado, paletas de cores e contraste, e suporte a tecnologia assistiva.
source-git-commit: 81db01c3e8d332e1fc8127d779c3a584bb498858
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 2%

---


# Recursos de acessibilidade no Experience Platform

A Adobe Experience Platform tem o compromisso de fornecer recursos acessíveis e inclusivos a todos os indivíduos, incluindo usuários que trabalham com dispositivos de assistência, como software de reconhecimento de voz e leitores de tela. Este documento descreve os recursos gerais de acessibilidade compatíveis com a plataforma, incluindo a navegação por teclado, a estrutura semântica, o contraste suficiente entre elementos em primeiro plano e elementos em segundo plano e o suporte para tecnologias assistivas.

## Tecnologias de assistência

Os usuários portadores de deficiências dependem frequentemente de hardware e software, conhecidos como tecnologias de assistência, para acessar conteúdo digital e usar produtos de software. O Adobe Experience Platform oferece suporte a vários tipos de tecnologias de assistência (AT), como leitores de tela, zoom e software de reconhecimento de voz, seguindo as práticas recomendadas de acessibilidade, como o uso de código semântico, equivalentes de texto, rótulos e ARIA, quando necessário. Os elementos interativos na interface do usuário do Experience Platform (UI) usam rótulos correspondentes, nomes acessíveis e funções que identificam sua finalidade e seu estado atual. Isso garante que as tecnologias de assistência, como leitores de tela, possam ler os rótulos e outras informações para os usuários, para que possam interagir facilmente com os controles do aplicativo.

## Acessibilidade do teclado

O Experience Platform se esforça para oferecer suporte à acessibilidade total do teclado.

Os seguintes elementos de navegação facilitam a acessibilidade:
* A tecla Tab se move entre elementos da interface do usuário, seções e grupos de menu.
* As teclas de seta movem-se nos grupos de menus para definir o foco de elementos ativos individuais.
* Shift + Tab move-se para trás pela ordem de tabulação.
* As teclas Retornar (Inserir) e Barra de espaço ativam os itens selecionados.
* A tecla escape (ESC) atua como um botão de cancelamento para fechar uma caixa de diálogo quando presente.
* O Experience Platform exibe uma borda azul em torno de um elemento selecionado para exibir uma indicação clara de qual elemento da interface do usuário tem foco no momento.

![Uma borda azul que aparece em torno de um elemento selecionado para indicar que o foco é aplicado.](images/profile-overview-tab.png)

## Paletas de cores e contraste

O Experience Platform se esforça para obter a conformidade [WCAG 2.1 AA](https://www.w3.org/TR/WCAG/), incluindo os requisitos para contraste de cores. A interface do usuário do Experience Platform fornece contraste suficiente no aplicativo para garantir uma experiência de visualização acessível para usuários com deficiências de visão ou cores baixas.

![A paleta de cores e o contraste presentes na página inicial da interface do usuário do Experience Platform.](images/homepage.png)

## Validação de campo necessária

Ao adicionar dados, criar esquemas ou definir segmentos, os campos obrigatórios são indicados visualmente, usando um asterisco ao lado do rótulo de texto de um campo e programaticamente. Esses campos acionam a validação ao inserir dados inválidos em campos e ao salvar. Se um campo obrigatório não passar na validação, ele será contornado em vermelho com um ícone de erro e também será exibida uma descrição escrita do problema que precisa ser corrigido.

![Um fechamento de um campo obrigatório que não passou na validação. O campo aparece em vermelho e um ícone de erro está presente.](images/field-validation.png)