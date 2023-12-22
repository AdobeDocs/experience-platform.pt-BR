---
title: Empacotamento do serviço de consulta
description: O documento a seguir descreve o pacote de recursos e produtos disponíveis para o Serviço de consulta e destaca as diferenças entre consultas ad hoc e em lote.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: 47f02f6d1d4017dfe0fccddcd137487e064b3039
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 2%

---

# Empacotamento do Serviço de consulta

Este documento descreve os diferentes tipos de recursos de empacotamento e execução de consulta disponíveis no Serviço de consulta.

O Serviço de consulta do Adobe Experience Platform pode ser dividido em dois recursos com base nos padrões de consulta que podem ser executados:

- **Consultas ad hoc** são consultas SQL usadas para explorar conjuntos de dados assimilados para verificação, validação, experimentação e assim por diante. Essas consultas não gravam dados de volta no data lake da Platform.
- **Consultas em lote** são consultas SQL usadas para executar o processamento de pós-assimilação de conjuntos de dados assimilados. Essas consultas limpam, moldam, manipulam e enriquecem dados, cujos resultados são gravados no data lake da Platform. Essas consultas podem ser agendadas, gerenciadas e monitoradas como trabalhos em lote.

Os recursos do Serviço de consulta são fornecidos com os seguintes produtos e complementos:

- **Aplicativos baseados em plataforma** (Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics e Adobe Journey Optimizer): o acesso ao Serviço de consulta para executar consultas ad hoc é fornecido desde o início com cada variação e camada de aplicativos baseados na plataforma.
- **[!DNL Data Distiller]** (pacote complementar que pode ser adquirido com o Adobe Real-Time CDP, Customer Journey Analytics e Adobe Journey Optimizer): o acesso ao Serviço de consulta para executar consultas em lote é fornecido com o [!DNL Data Distiller].

## Direitos {#entitlements}

A tabela a seguir descreve os principais direitos do Serviço de consulta com base em como eles são empacotados:

| Qualificação do Serviço de Consulta | Fornecido com aplicativos baseados em plataforma | Empacotado com [!DNL Data Distiller] |
|---|---|---|
| Padrão de consulta compatível | Somente consultas ad hoc | Consulta em lote |
| Caso de uso suportado | <ul><li>Exploração&#x200B;</li><li>Descoberta de dados&#x200B;</li><li>Validação de dados</li><li>Experimentação</li></ul> | <ul><li>Limpando</li><li>Modelagem</li><li>Manipular</li><li>Enriquecimento</li></ul> |
| Semântica Compatível | <ul><li>Consultas SELECT</li></ul> | <ul><li>Queries CTAS e ITAS</li></ul> |
| Tempo Máximo de Execução | 10 minutos | 24 horas |
| Licenciar métrica | **Consultar Simultaneidade de Usuário**: <ul><li>1 usuário simultâneo (Real-Time CDP, Adobe Journey Optimizer)&#x200B;</li><li>5 usuários simultâneos (Customer Journey Analytics)&#x200B;</li></ul> **Simultaneidade da consulta**: <ul><li>1 consulta em execução simultânea (todas as aplicações)&#x200B;</li></ul> **Complemento de pacote de usuários de consulta ad hoc adicional** pode ser adquirido para aumentar os direitos de consulta ad hoc autorizados dos clientes. <ul><li>+5 usuários simultâneos adicionais por pacote</li><li>+1 consulta de execução simultânea adicional por pacote</li></ul> | **Computar horas**: <ul><li>Variável (com base nos direitos do aplicativo do cliente)</li></ul> **Computar horas** é uma medida do tempo gasto pelo mecanismo do Serviço de consulta para ler, processar e gravar dados de volta no data lake quando uma consulta em lote é executada. |
| Uso acelerado de consultas e relatórios | Não | Sim - Consultas aceleradas simultâneas permitem ler dados do armazenamento acelerado e exibi-los em seus painéis. Também é fornecido um direito dedicado para armazenar modelos de relatórios e conjuntos de dados no armazenamento acelerado. |
| Capacidade de armazenamento do data lake | Seu direito total de armazenamento depende das licenças dos aplicativos baseados em plataforma. Por exemplo, Real-Time CDP, AJO, CJA e assim por diante. | Sim — um direito de armazenamento adicional é fornecido para manter seus conjuntos de dados brutos e derivados para casos de uso do Data Distiller além de uma data de expiração de dados de sete dias.<br>A capacidade de armazenamento do data lake é medida em terabytes (TB) e depende da quantidade de horas de Computação que você comprou. Verifique a descrição do produto para obter mais detalhes. |
| Bonificação de exportação de dados | Seu direito total de exportação depende das licenças dos aplicativos baseados na plataforma. Por exemplo, Real-Time CDP, AJO, CJA e assim por diante. | Sim - direitos de exportação adicionais são fornecidos para permitir a exportação de conjuntos de dados derivados criados usando o Data Distiller.<br>Sua permissão anual de exportação de dados é medida em terabytes (TB) e depende da quantidade de horas de Computação que você adquiriu. Verifique a descrição do produto para obter mais detalhes. |
| Interface de execução de consulta | <ul><li>Interface do usuário do serviço de consulta</li><li>Interface do usuário do cliente de terceiros</li><li>[!DNL PostgresSQL] interface do cliente</li></ul> | <ul><li>Interface do usuário do serviço de consulta </li><li>Interface do usuário do cliente de terceiros</li><li>[!DNL PostgresSQL] interface do cliente</li><li>REST APIs</li></ul> |
| Resultados da Consulta Retornados via | Interface do cliente | Conjunto de dados derivado armazenado no data lake |
| Limite do resultado | <ul><li>Interface do usuário do serviço de consulta - 100 linhas</li><li>Clientes de terceiros - 50.000</li><li>[!DNL PostgresSQL] cliente - 50.000</li></ul> | <ul><li>Interface do usuário do serviço de consulta - O número de linhas de saída pode ser [configurado com uma configuração de interface](./ui/user-guide.md#result-count) entre 50 e 500 linhas.</li><li>Clientes de terceiros (sem limite superior para linhas)</li><li>[!DNL PostgresSQL] cliente (sem limite superior para linhas)</li><li>REST APIs (sem limite superior para linhas)</li></ul> |
| Capacidade do conjunto de dados de leitura | Sim | Sim |
| Capacidade do conjunto de dados de gravação | Não | Sim |
| Capacidade de programação | Não | Sim |
| Monitorando a capacidade | Sim | Sim |
| Capacidade de Configuração de Alerta de Consulta | Não | Sim |

{style="table-layout:auto"}

## Controle de acesso {#access-control}

O controle de acesso para o Experience Platform é administrado através do [Adobe Admin Console](https://adminconsole.adobe.com/) em que os perfis de produto vinculam usuários com permissões e sandboxes. Consulte a [visão geral do controle de acesso](../access-control/home.md) para obter mais informações.

Para usar o Serviço de consulta, a variável [!DNL Manage Queries] a permissão deve ser ativada no Admin Console. Essa permissão permite que os usuários executem consultas ad hoc e em lote. Instruções detalhadas para solicitar acesso ao perfil do produto [!DNL Manage Queries] foram descritos na seção [gerenciar permissões para um perfil de produto](../access-control/ui/permissions.md) e [gerenciar usuários para um perfil de produto](../access-control/ui/users.md) documentos.

Após a compra do [!DNL Data Distiller] complemento, a variável [!DNL Write Dataset] a permissão deve ser concedida. Essa permissão permite [!DNL Data Distiller] usuários para executar consultas em lote.

O quadro seguinte descreve os efeitos da [!DNL Manage Queries] permissão:

| Permissão | Função |
|---|---|
| [!DNL Manage Queries] (sem permissão para gravar dados) | Fornece acesso para executar consultas ad hoc |
| [!DNL Manage Queries] (com permissão para gravar dados) | Fornece acesso para executar consultas em lote |

{style="table-layout:auto"}

## Suporte à sandbox {#sandbox-support}

As sandboxes são partições virtuais dentro de uma única instância do Experience Platform. Cada instância da Platform é compatível com várias sandboxes de produção e não produção, cada uma mantendo sua própria biblioteca de recursos da Platform. As sandboxes de não produção permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar suas sandboxes de produção. Para obter mais informações sobre sandboxes, consulte a [visão geral das sandboxes](../sandboxes/home.md). Todos os direitos do Serviço de consulta são compartilhados em todas as sandboxes.

## Próximas etapas

Ao ler este documento, você deve ter uma melhor compreensão dos diferentes tipos de empacotamento e recursos de execução de consulta disponíveis no Serviço de consulta. Para saber mais sobre o Serviço de consulta, como casos de uso conhecidos do setor, leia o [documentação do caso de uso](./use-cases/abandoned-browse.md). Para obter informações mais gerais, visite o [Visão geral do Serviço de consulta](./home.md).
