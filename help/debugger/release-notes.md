---
title: Notas de versão do Adobe Experience Platform Debugger
description: As notas de versão mais recentes do Adobe Experience Platform Debugger.
keywords: depurador;extensão do Experience Platform Debugger;chrome;extensão;notas de versão
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: 96a092efe5ceefeb7b6c3ddd9845d78b8862ac68
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 2%

---

# Notas de versão do Adobe Experience Platform Debugger

## Versão 1.4.0 - 3 de outubro de 2022

* Adição do suporte à depuração do AEP Assurance para implementações híbridas do SDK da Web.
* Adição do suporte a várias guias na mesma sessão do AEP Assurance.
* Correção de um problema em que os usuários não podiam alternar perfis/organizações após fazer logon.
   * Para algumas contas, é necessário fazer logout e logon novamente para trocar de empresa.
* Adição de uma mensagem de erro ao ativar o Target Trace.
* Dependências atualizadas.

## Versão 1.3.3 - 20 de junho de 2022

* Correção de um problema que impedia a abertura de pop-ups de tabelas de eventos de rede.
* Correção de um problema que impedia o carregamento de informações de liga na página.

## Versão 1.3.2 - 9 de junho de 2022

* Adição de um avatar padrão quando o usuário está conectado.
* Adição do realce de sintaxe aos objetos JSON nos logs.

## Versão 1.3.1 - 24 de maio de 2022

* Dependências atualizadas.
* Correção de um problema do Analytics em que os hits pós-processo não podiam ser ativados.
* Correção de um problema em que o depurador era anexado à janela de logon do Adobe.
* Correção de um problema na AT.js em que as mensagens de log não eram exibidas no Debugger.

## Versão 1.3.0 - 28 de janeiro de 2022

* Adição do link Sobre para mostrar a versão atual e as notas.
* Adição de um botão para exibir ocorrências pós-processadas para solicitações do Analytics. O botão de alternância está disponível na seção Analytics.
* Correção de um problema de sessão de depuração remota quando a sessão era fechada fora do depurador.
* Correção da notificação de erro que estava visível na guia Transações de borda do SDK da Web.
* Corrigidas as tags Adobe no aviso de descontinuação da página quando o depurador acessava o objeto _satellite.
* Correção de alguns casos em que uma instância do AppMeasurement não era encontrada na página.
* Correção de um problema de conexão de página que ocorria ao abrir a janela do depurador pela primeira vez.

## Versão 1.2.0 - 26 de outubro de 2021

* Mostrar eventos de todas as guias do navegador na exibição de rede. Para ver apenas os eventos da guia atual, selecione o ícone de bloqueio no canto inferior direito do depurador.
* Marca atualizada.

## Versão 1.1.0 - 5 de outubro de 2021

* Visualização de depuração remota - Organize os eventos de depuração remota em um fluxograma visual na seção Adobe Experience Platform Web SDK > Transações de borda.
* Exigir que a organização IMS do SDK da Web da Adobe Experience Platform usada na página corresponda à organização conectada ao iniciar uma nova sessão de depuração remota.
* Mostrar somente as transações de borda da guia conectada. Os logs de rastreamento do Target ainda estão disponíveis na seção Logs > Edge.
* Permitir a substituição da configuração da ID de fluxo de dados separada para cada instância do SDK da Web da Adobe Experience Platform na página. Adicionar alternância habilitada para depuração.
* Correção de um problema em que o token de rastreamento do Adobe Target nem sempre era enviado com sessões de depuração remota para o SDK da Web da Adobe Experience Platform.

## Versão 1.0.0 de 5 de maio de 2021

* Primeira versão principal do Experience Platform Debugger. Destina-se a substituir o Experience Cloud Debugger.
