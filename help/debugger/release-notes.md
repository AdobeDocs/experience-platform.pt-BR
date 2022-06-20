---
title: Notas de versão do Adobe Experience Platform Debugger
description: As notas de versão mais recentes do Adobe Experience Platform Debugger.
keywords: depurador, extensão do Experience Platform Debugger, chrome, extensão, notas de versão
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: b4e3b40942390ef183ccb01f65702ae400a5e22f
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 2%

---

# Notas de versão do Adobe Experience Platform Debugger

## Versão 1.3.3 - 20 de junho de 2022

* Correção de um problema que impedia a abertura de pop-ups a partir de tabelas de eventos de rede.
* Correção de um problema que impedia o carregamento de informações de Alloy na página.

## Versão 1.3.2 - 9 de junho de 2022

* Adição de um avatar padrão quando o usuário está conectado.
* Adicionado o realce da sintaxe aos objetos JSON em logs.

## Versão 1.3.1 - 24 de maio de 2022

* Dependências atualizadas.
* Correção de um problema do Analytics em que as ocorrências pós-processo não podiam ser ativadas.
* Correção de um problema em que o depurador era anexado à janela de logon do Adobe.
* Correção de um problema da AT.js em que as mensagens de log não eram exibidas no Debugger.

## Versão 1.3.0 - 28 de janeiro de 2022

* Adição do link Sobre para mostrar a versão e as notas atuais.
* Adição de alternância para exibir ocorrências pós-processadas em solicitações do Analytics. A alternância está disponível na seção Analytics .
* Correção de um problema de sessão de depuração remota quando a sessão era fechada fora do depurador.
* Correção de uma notificação de erro que estava visível na guia Transações de borda do SDK da Web.
* Correção de Tags de Adobe no aviso de desativação da página quando o depurador acessava o objeto _satellite.
* Correção de alguns casos em que uma instância do AppMeasurement não era encontrada na página.
* Correção de um problema de conexão de página que ocorria ao abrir a janela do depurador pela primeira vez.

## Versão 1.2.0 - 26 de outubro de 2021

* Mostrar eventos de todas as guias do navegador na exibição de rede. Para visualizar apenas os eventos da guia atual, selecione o ícone de bloqueio no canto inferior direito do depurador.
* Marca atualizada.

## Versão 1.1.0 - 5 de outubro de 2021

* Visualização de depuração remota - organize os eventos de depuração remota em um gráfico de fluxo visual na seção Adobe Experience Platform Web SDK > Edge Transactions .
* Exigir que a organização IMS do SDK da Web da Adobe Experience Platform usada na página corresponda à organização conectada ao iniciar uma nova sessão de depuração remota.
* Mostrar somente as transações de borda da guia conectada. Os logs de rastreamento do Target ainda estão disponíveis na seção Logs > Edge .
* Permitir substituições separadas da configuração da ID de fluxo de dados para cada instância do SDK da Web do Adobe Experience Platform na página. Adicione a alternância de depuração ativada.
* Correção de um problema em que o token de rastreamento do Adobe Target nem sempre era enviado com sessões de depuração remota para o SDK da Web do Adobe Experience Platform.

## Versão 1.0.0 de 5 de maio de 2021

* Primeira versão principal do Experience Platform Debugger. Destinado a substituir o Experience Cloud Debugger.
