---
title: Notas de versão do Adobe Experience Platform Debugger
description: As notas de versão mais recentes do Adobe Experience Platform Debugger.
keywords: debugger;extensão do experience platform debugger;chrome;extensão;notas de versão
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: c4048b83c916f4b3b4b5acb3cccb957b65ee25c8
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 92%

---

# Notas de versão do Adobe Experience Platform Debugger

## Versão 1.6.4 - quarta-feira, 6 de maio de 2025

### Correções e melhorias

* Correção de um problema em que o logon não estava disponível.

## Versão 1.6.3 - 30 de abril de 2025

### Correções e melhorias

* Correção de um problema em que o Depurador impedia que as funções do DTM e das Tags funcionassem.
* Correção de um problema em que as ocorrências pós-processadas do Analytics não eram exibidas nos logs.
* Correção de um problema em que os dados em idiomas não ASCII, como japonês, não eram exibidos corretamente nos logs.

## Versão 1.6.2 - quarta-feira, 1 de outubro de 2024

### Correções e melhorias

* Correção de um problema em que o Depurador era muito sensível a todos os erros da CSP

## Versão 1.6.1 - 25 de julho de 2024

### Correções e melhorias

* Correção de um problema que impedia usuários de adicionarem novos códigos incorporados de tags em páginas sem tags.

## Versão 1.6.0 - 11 de julho de 2024

### Novos recursos

* Permitir que usuários aceitem ou recusem a coleta de dados técnicos e pessoais.

### Correções e melhorias

* Correção do link da política de privacidade e injeção de script do Firefox.
* Captura de solicitações ausentes do Analytics.
* Correção de falhas em páginas com várias mensagens de console complexas.
* Atualize o Adobe Experience Platform Debugger para uma extensão Manifest v3.

## Versão 1.5.4 - 19 de dezembro de 2023

### Correções e melhorias

* Correção de um problema em que as configurações não eram mantidas.
* Correção de um problema que causava falha no Debugger ao visualizar ocorrências pós-processadas do Analytics.

## Versão 1.5.3 - 6 de dezembro de 2023

### Novos recursos

* Adição de uma configuração para “bloquear a guia ativa ao abrir o Debugger”.

### Correções e melhorias

* Correção de um problema em que as solicitações do Analytics estavam ausentes em domínios privados.
* Correção de um problema com dados do Activity Map ausentes na tabela de solicitações do Analytics.
* Correção de uma falha na exibição do Target Trace.
* Adição de um aviso quando o Debugger falha ao configurar a infraestrutura da página do Firefox.

## Versão 1.5.2 - 10 de novembro de 2023

(Somente Firefox)

### Correções e melhorias

* Atualização da organização dos arquivos.

## Versão 1.5.1 - 2 de novembro de 2023

### Correções e melhorias

* Correção de problemas em que os eventos do Analytics eram ignorados ou duplicados.
* Correção de um problema em que o tamanho máximo do armazenamento de estado era excedido.
* Correção de um problema em que a pesquisa de logs do Edge não filtrava eventos.

## Versão 1.5.0 - 19 de outubro de 2023

### Novos recursos

* Exibição de links para a propriedade, o ambiente e as regras no resumo e nos logs das tags.

### Correções e melhorias

* Correção de um problema em que os dados de resumo de tags não eram enviados.
* Correção de um erro CORS nas sessões do Assurance
* Correção de um problema que impedia a exibição do Target Trace.
* Correção do botão “Enviar feedback”.
* Correção da “ID de sequência de dados” ausente no Resumo do SDK da Web na versão ≥2.18.0.
* Correção de um problema em que não era possível pesquisar os logs do Edge.
* Adição de uma observação sobre perfis adicionais para determinados tipos de conta.

## Versão 1.4.1 - 1º de novembro de 2022

* Desempenho aprimorado em páginas com vários eventos do Adobe Experience Platform Assurance.

## Versão 1.4.0 - 3 de outubro de 2022

* Adição de suporte para depuração do AEP Assurance em implementações híbridas do SDK da Web.
* Adição de suporte a várias guias na mesma sessão do AEP Assurance.
* Correção de um problema em que usuários não podiam alternar entre perfis ou organizações após fazer logon.
   * Em algumas contas, é necessário sair e fazer logon novamente para trocar de organização.
* Adição de uma mensagem de erro para a falha ao habilitar o Target Trace.
* Dependências atualizadas.

## Versão 1.3.3 - 20 de junho de 2022

* Correção de um problema que impedia a abertura de pop-ups a partir de tabelas de eventos de rede.
* Correção de um problema que impedia o carregamento de informações do Alloy na página.

## Versão 1.3.2 - 9 de junho de 2022

* Adição de um avatar padrão para o usuário conectado.
* Adição de realce de sintaxe aos objetos JSON em logs.

## Versão 1.3.1 - 24 de maio de 2022

* Dependências atualizadas.
* Correção de um problema em que não era possível habilitar ocorrências de pós-processamento do Analytics.
* Correção de um problema em que o Debugger era fixado na janela de logon da Adobe.
* Correção de um problema em que as mensagens de log da AT.js não eram exibidas no Debugger.

## Versão 1.3.0 - 28 de janeiro de 2022

* Adição do link Sobre para mostrar a versão atual e as notas da versão.
* Adição de um botão de alternância para exibir ocorrências pós-processadas de solicitações do Analytics. O botão de alternância está disponível na seção Analytics.
* Correção de um problema que ocorria ao fechar a sessão de depuração remota fora do Debugger.
* Correção de uma notificação de erro visível na guia Transações do Edge do SDK da Web.
* Correção de tags da Adobe que apareceiam no aviso de descontinuação da página quando o Debugger acessava o objeto _satellite.
* Correção de alguns casos em que uma instância do AppMeasurement não era encontrada na página.
* Correção de um problema de conexão de página que ocorria ao abrir a janela do Debugger pela primeira vez.

## Versão 1.2.0 - 26 de outubro de 2021

* Mostra eventos de todas as guias do navegador na exibição de rede. Para ver apenas os eventos da guia atual, selecione o ícone de cadeado no canto inferior direito do Debugger.
* Atualização da marca.

## Versão 1.1.0 - 5 de outubro de 2021

* Visualização de depuração remota: organize os eventos de depuração remota em um fluxograma visual na seção SDK da Web da Adobe Experience Platform > Transações do Edge.
* Exigir que a organização do SDK da Web da Adobe Experience Platform usada na página corresponda à organização conectada ao iniciar uma nova sessão de depuração remota.
* Mostrar somente as transações do Edge da guia conectada. Os logs do Target Trace ainda estão disponíveis na seção Logs > Edge.
* Permitir a substituição de configurações de ID de sequência de dados separadas para cada instância do SDK da Web da Adobe Experience Platform na página. Adição do botão de alternância para habilitar a depuração.
* Correção de um problema em que o token TRACE do Adobe Target nem sempre era enviado com as sessões de depuração remota para o SDK da Web da Adobe Experience Platform.

## Versão 1.0.0 - 5 de maio de 2021

* Primeira versão principal do Experience Platform Debugger. Criada para substituir o Experience Cloud Debugger.
