---
title: Consultas com parâmetros
description: Saiba como usar consultas com parâmetros na interface do usuário do Adobe Experience Platform.
source-git-commit: 4fc94fc39fa09756a440b5e532330cd310dd96d2
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# Consultas parametrizadas (versão limitada) {#parameterized-queries}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_parameterizedQueries"
>title="Consultas com parâmetros"
>abstract="Use consultas parametrizadas para adicionar valores de parâmetros no momento da execução. Isso permite trabalhar com dados dinâmicos e reutilizar consultas para casos de uso diferentes. Use o `'$'` prefácio para inserir um parâmetro de consulta na sua consulta no editor de texto. Em seguida, adicione um valor para a chave na seção Parâmetros de consulta abaixo do editor."

>[!IMPORTANT]
>
>O recurso de interface de consulta parametrizada está disponível em uma **somente versão limitada** e não está disponível para todos os clientes.

O Serviço de consulta suporta o uso de consultas parametrizadas no Editor de consultas. Com consultas parametrizadas, agora é possível usar espaços reservados para parâmetros e adicionar os valores de parâmetro no tempo de execução. Os espaços reservados permitem trabalhar com dados dinâmicos em que você não sabe quais serão os valores até que a instrução seja executada. Você também pode preparar suas consultas antecipadamente e reutilizá-las para fins semelhantes. A reutilização de consultas economiza um esforço considerável, pois você evita criar consultas SQL distintas para cada caso de uso.

## Pré-requisitos

Antes de continuar com este guia, leia o [Guia da interface do Editor de consultas](./user-guide.md). O guia do Editor de consultas fornece informações detalhadas sobre como gravar, validar e executar consultas para dados de experiência do cliente na interface do usuário do Experience Platform.

>[!NOTE]
>
>Na interface do usuário do Adobe Experience Platform, as consultas parametrizadas só são suportadas no nível principal dos modelos em linha. Isso significa que as consultas parametrizadas só funcionam quando usadas no template original. Os modelos filho devem ser um modelo estático e não podem ter parâmetros dinâmicos. Consulte a [documentação de modelos em linha](../essential-concepts/inline-templates.md) para saber mais.

## Sintaxe de consulta com parâmetros {#syntax}

Consultas parametrizadas usam o formato `'$YOUR_PARAMETER_NAME'` e podem ser concatenadas usando a notação de pontos. Um exemplo de instrução SQL que usa consultas parametrizadas pode ser visto abaixo.

```sql
INSERT INTO
   $Database_Name.Schema_Name.adwh_lkup_process_delta_log
   (process_name, merge_policy_id, process_status, process_date, create_ts, change_ts)
SELECT
   '$Table_Process_Name' process_name,
   hash('$Merge_PolicyID') merge_policy_id,
   '$process_status' process_status,
   to_date('$date_key') process_date,
   CURRENT_TIMESTAMP create_ts,
   CURRENT_TIMESTAMP change_ts;
```

## Criar uma consulta com parâmetros {#create}

Para criar sua consulta parametrizada na interface do usuário do, navegue até o Editor de consultas. Consulte a seção sobre [acesso ao Editor de consultas](./user-guide.md#accessing-query-editor) para obter mais instruções.

Use o `'$'` prefácio para inserir um parâmetro de consulta na sua consulta no editor de texto. Em seguida, adicione o valor ausente para a chave no [!UICONTROL Parâmetros de consulta] seção abaixo do editor. A consulta não pode ser executada se você não adicionar um valor a qualquer uma das chaves necessárias. Um ícone de alerta (![Um ícone de alerta.](../images/ui/parameterized-queries/alert-icon.png)) aparece na seção Parâmetros de consulta ao lado de qualquer [!UICONTROL Valor] campos de entrada.

![O Editor de consultas com uma consulta parametrizada e a seção Parâmetros de consulta destacados.](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>Alterar guias de [!UICONTROL Parâmetros de consulta] para [!UICONTROL Console] para exibir a saída do console do query.

Se você remover um parâmetro e tentar executar a consulta novamente após ela já ter sido executada, uma mensagem de erro será exibida na [!UICONTROL Parâmetros de consulta] seção para alertá-lo.

>[!NOTE]
>
>Se a consulta não usar parâmetros, você ainda poderá inserir parâmetros desnecessários no Editor de consultas. O Editor de consultas ignora todos os pares de valores chave desnecessários e não têm efeito na execução ou nos resultados da consulta.

![O Editor de consultas com um campo de valor vazio e o erro nos parâmetros de consulta foi realçado.](../images/ui/parameterized-queries/query-parameter-error.png)

## Usar detalhes de logs de consulta para verificar valores de parâmetros {#check-parameter-values}

Não é possível salvar parâmetros nos modelos, pois os valores usados não são persistentes. No entanto, você pode verificar o [!UICONTROL Detalhes do log de consulta] página para localizar os valores de parâmetro usados em uma execução de consulta. Nesse caso, os logs não indicam que a consulta era uma consulta com parâmetros. Consulte a [documentação dos logs de consulta](./query-logs.md) para obter instruções sobre como encontrar os valores usados.

![A visualização dos logs de consulta com o SQL de uma consulta com parâmetros destacada na seção de detalhes.](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## Agendar uma consulta com parâmetros {#schedule}

Os valores de parâmetro são salvos quando você agenda uma consulta com parâmetros. Para programar uma consulta parametrizada, siga o processo normal para criar uma consulta programada, conforme descrito no guia para [criar um agendamento de consulta](./query-schedules.md#create-schedule), em seguida, insira os valores de parâmetro a serem usados na execução da consulta. Esta seção da interface só é exibida para consultas parametrizadas. Consulte a seção sobre [definindo parâmetros para uma consulta parametrizada programada](./query-schedules.md#set-parameters) para obter instruções específicas.

>[!TIP]
>
>O Serviço de consulta oferece suporte a instruções preparadas por meio do uso de consultas parametrizadas. Consulte a [guia de sintaxe de instruções preparadas](../sql/prepared-statements.md) para obter mais informações sobre a sintaxe SQL envolvida.

## Próximas etapas

Ao ler este documento, você aprendeu a parametrizar consultas na interface do usuário do Adobe Experience Platform e usá-las em execuções de consultas programadas. O documento também destacou como verificar os logs para os valores de parâmetro usados nas execuções de consulta.

Em seguida, é recomendável ler o guia em [monitoramento de consultas programadas](./monitor-queries.md) para obter uma melhor compreensão do status de todos os trabalhos de consulta por meio da interface do usuário da Platform.
