---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API;perfil unificado;Perfil unificado;unificado;Perfil;rtcp;gráficos XDM
title: Recursos gerais de acessibilidade no Experience Platform
type: Documentation
description: Saiba mais sobre os recursos gerais de acessibilidade compatíveis com o Adobe Experience Platform, incluindo navegação pelo teclado, paletas e contraste de cores e suporte à tecnologia assistiva.
exl-id: 4b7e2f2b-af51-4376-8a63-16c921cc7135
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Recursos de acessibilidade no Experience Platform

A Adobe Experience Platform tem o compromisso de fornecer recursos acessíveis e inclusivos para todos os indivíduos, incluindo usuários que trabalham com dispositivos de assistência, como software de reconhecimento de voz e leitores de tela. Este documento descreve os recursos gerais de acessibilidade compatíveis com o Experience Platform, incluindo navegação pelo teclado, estrutura semântica, contraste suficiente entre elementos de primeiro plano e elementos de plano de fundo, e suporte para tecnologias assistivas.

## Tecnologias assistivas

Os usuários portadores de deficiências frequentemente dependem de hardware e software, conhecidos como tecnologias assistivas, para acessar conteúdo digital e usar produtos de software. O Adobe Experience Platform oferece suporte a vários tipos de tecnologias assistivas (AT), como leitores de tela, zoom e software de reconhecimento de voz, seguindo as práticas recomendadas de acessibilidade, como o uso de código semântico, equivalentes de texto, rótulos e ARIA, quando necessário. Os elementos interativos na interface do usuário (UI) do Experience Platform usam rótulos correspondentes, nomes acessíveis e funções que identificam a finalidade e o estado atual. Isso garante que as tecnologias assistivas, como leitores de tela, possam ler os rótulos e outras informações para os usuários para que eles possam interagir facilmente com os controles do aplicativo.

## Acessibilidade do teclado

O Experience Platform se esforça para oferecer suporte à acessibilidade total do teclado.

Os seguintes elementos de navegação facilitam a acessibilidade:

* A tecla Tab se move entre elementos da interface, seções e grupos de menu.
* As teclas de seta se movem dentro de grupos de menus para definir o foco para elementos ativos individuais.
* Shift + Tab move-se para trás pela ordem de tabulação.
* As teclas Return (Enter) e Barra de espaço ativam os itens selecionados.
* A tecla Escape (ESC) atua como um botão Cancelar para fechar uma caixa de diálogo quando presente.
* O Experience Platform exibe uma borda azul ao redor de um elemento selecionado para exibir uma indicação clara de qual elemento da interface do usuário tem foco no momento.

![Uma borda azul que aparece ao redor de um elemento selecionado para indicar que o foco está aplicado.](images/profile-overview-tab.png)

## Paletas de cores e contraste

O Experience Platform se esforça para obter a conformidade [WCAG 2.1 AA](https://www.w3.org/TR/WCAG/), incluindo os requisitos para contraste de cores. A interface do usuário do Experience Platform fornece contraste suficiente no aplicativo para garantir uma experiência de exibição acessível para usuários com limitações visuais ou de percepção de cor.

![A paleta de cores e o contraste presentes na página inicial da interface do usuário do Experience Platform.](images/homepage.png)

## Validação de campo necessária

Ao adicionar dados, criar esquemas ou definir segmentos, os campos obrigatórios são indicados visualmente, usando um asterisco ao lado do rótulo de texto de um campo, e programaticamente. Esses campos acionam a validação quando você insere dados inválidos nos campos e ao salvar. Se um campo obrigatório não passar na validação, ele será contornado em vermelho com um ícone de erro, e uma descrição escrita do problema que precisa ser corrigido também será exibida.

![Um fechamento de um campo obrigatório que não passou na validação. O campo aparece em vermelho e um ícone de erro está presente.](images/field-validation.png)
