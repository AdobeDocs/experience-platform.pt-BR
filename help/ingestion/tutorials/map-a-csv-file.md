---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mapear um arquivo CSV para um schema XDM
topic: tutorial
translation-type: tm+mt
source-git-commit: 33282b1c8ab1129344bd4d7054e86fed75e7b899

---


# Mapear um arquivo CSV para um schema XDM

Para assimilar dados CSV na Adobe Experience Platform, os dados devem ser mapeados para um schema do Experience Data Model (XDM). Este tutorial aborda como mapear um arquivo CSV para um schema XDM usando a interface do usuário da plataforma Experience.

Além disso, o apêndice deste tutorial fornece mais informações sobre o uso de funções [de](#mapping-functions)mapeamento.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

- [Modelo de dados de experiência (sistema XDM)](../../xdm/home.md): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
- [Ingestão](../batch-ingestion/overview.md)em lote: O método pelo qual a Plataforma ingere dados de arquivos de dados fornecidos pelo usuário.

Este tutorial também requer que você já tenha criado um conjunto de dados para assimilar seus dados CSV. Para obter etapas sobre como criar um conjunto de dados na interface do usuário, consulte o tutorial [de assimilação de](./ingest-batch-data.md)dados.

## Adicionar dados

Na interface do usuário da plataforma de experiência, clique em **Workflows** no painel de navegação esquerdo e, em seguida, clique em **Mapear o schema** CSV para XDM. No painel direito exibido, clique em **Iniciar**.

![](../images/tutorials/map-a-csv-file/workflow-tab.png)

O fluxo de trabalho _Mapear CSV para schema_ XDM é exibido, começando na etapa _Adicionar dados_ .

![](../images/tutorials/map-a-csv-file/add-data.png)

Arraste e solte o arquivo CSV no espaço fornecido ou clique em **Procurar** para selecionar um arquivo diretamente. Uma seção de dados _de_ amostra é exibida depois que o arquivo é carregado, mostrando as primeiras dez linhas de dados. Depois de confirmar que os dados foram carregados como esperado, clique em **Avançar**.

![](../images/tutorials/map-a-csv-file/csv-added.png)

## Escolher um destino

A etapa _Destino_ é exibida. Na lista fornecida, selecione o conjunto de dados no qual os dados CSV serão assimilados e clique em **Avançar**.

![](../images/tutorials/map-a-csv-file/select-destination.png)

## Mapear campos CSV para campos de schema XDM

A etapa _Mapeamento_ é exibida. As colunas do arquivo CSV são listadas em Campo _de_ origem, com seus campos de schema XDM correspondentes listados em Campo _de_ Público alvo. Os campos de público alvo não selecionados são contornados em vermelho.

Para mapear uma coluna CSV para um campo XDM, clique no ícone de schema ao lado do campo de público alvo correspondente da coluna.

![](../images/tutorials/map-a-csv-file/target-field-mapping.png)

A janela _Selecionar campo_ schema é exibida. Aqui, você pode navegar pela estrutura do schema XDM e localizar o campo para o qual deseja mapear a coluna CSV. Clique em um campo XDM para selecioná-lo e, em seguida, clique em **Selecionar**.

![](../images/tutorials/map-a-csv-file/xdm-field-selection.png)

A tela _Mapeamento_ é exibida novamente, com o campo XDM selecionado aparecendo agora em Campo _de_ Público alvo.

![](../images/tutorials/map-a-csv-file/xdm-field-mapped.png)

Se você não desejar mapear uma coluna CSV específica, é possível remover o mapeamento clicando no ícone **** remover ao lado do campo público alvo. Se desejar adicionar um novo mapeamento, clique em **Adicionar novo mapeamento** na parte inferior da lista.

![](../images/tutorials/map-a-csv-file/remove-or-add-mapping.png)

Ao mapear campos, também é possível incluir funções para calcular valores com base nos campos de origem de entrada. Consulte a seção de funções [de](#mapping-functions) mapeamento no apêndice para obter mais informações.

Repita as etapas acima para continuar mapeando colunas CSV para campos XDM. Quando terminar, clique em **Avançar**.

![](../images/tutorials/map-a-csv-file/mapping-finish.png)

## Dados de assimilação

A etapa _Ingest_ é exibida, permitindo que você analise os detalhes do arquivo de origem e do conjunto de dados do público alvo. Clique em **assimilar** para que o start ingira os dados CSV. Dependendo do tamanho do arquivo CSV, esse processo pode levar vários minutos. A tela é atualizada quando a ingestão é concluída, indicando sucesso ou falha. Click **Finish** to complete the workflow.

![](../images/tutorials/map-a-csv-file/ingest-data.png)

## Próximas etapas

Ao seguir este tutorial, você mapeou com êxito um arquivo CSV simples para um schema XDM e o assimilou na Plataforma. Esses dados agora podem ser usados por serviços de plataforma downstream, como o Perfil do cliente em tempo real. Consulte a visão geral [do Perfil do cliente em tempo](../../profile/home.md) real para obter mais informações.

## Apêndice

A seção a seguir fornece informações adicionais para mapear colunas CSV para campos XDM.

### Funções de mapeamento

Determinadas funções de mapeamento podem ser usadas para calcular e calcular valores com base no que é inserido nos campos de origem. Para usar uma função, digite-a em Campo _de_ origem com a sintaxe e as entradas apropriadas.

Por exemplo, para concatenar campos CSV de **cidade** e **país** e atribuí-los ao campo XDM de **cidade** , defina o campo de origem como `concat(city, ", ", county)`.

![](../images/tutorials/map-a-csv-file/mapping-function.png)

A tabela a seguir lista todas as funções de mapeamento suportadas, incluindo expressões de amostra e suas saídas resultantes.

| Função | Descrição | expressão de amostra | Exemplo de saída |
| -------- | ----------- | ----------------- | ------------- |
| concat | Concatena determinadas cordas. | concat(&quot;Oi, &quot;, &quot;lá&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explosão | Divide a string com base em um regex e retorna uma matriz de partes. | explode(&quot;Oi, aqui!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Retorna o local/índice de uma substring. | instr(&quot;adobe<span>.com&quot;, &quot;com&quot;) | 6 |
| substituta | Substitui a string de pesquisa, se presente na string original. | replace(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Este é um teste de substituição de string&quot; |
| substr | Retorna uma substring de um determinado comprimento. | SAA(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Converte uma string em minúsculas. | lower(&quot;EleLLo&quot;)<br>lcase(&quot;EleLLo&quot;) | &quot;hello&quot; |
| superior /<br>ucase | Converte uma string em maiúsculas. | upper(&quot;HeLLo&quot;)<br>ucase(&quot;EleLLo&quot;) | &quot;OLÁ&quot; |
| split | Divide uma string de entrada em um separador. | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Une uma lista de objetos usando o separador. | `join(" ", ["Hello", "world"]`) | &quot;Olá mundo&quot; |
| coalescência | Retorna o primeiro objeto não nulo em uma determinada lista. | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| decodificação | Considerando uma chave e uma lista de pares de valores chave nivelados como uma matriz, a função retornará o valor se a chave for encontrada ou retornará um valor padrão se estiver presente na matriz. | decode(&quot;k2&quot;, &quot;k1&quot;, &quot;v1&quot;, &quot;k2&quot;, &quot;v2&quot;, &quot;default&quot;) | &quot;v2&quot; |
| iif | Avalia uma determinada expressão booleana e retorna o valor especificado com base no resultado. | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;Verdadeiro&quot; |
| min | Retorna o mínimo dos argumentos fornecidos. Usa ordenação natural. | min(3, 1, 4) | 1 |
| max | Retorna o máximo dos argumentos fornecidos. Usa ordenação natural. | max(3, 1, 4) | 4 |
| first | Recupera o primeiro argumento fornecido. | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Recupera o último argumento fornecido. | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| uid /<br>guid | Gera uma ID pseudo-aleatória. | uuid()<br>guid() | {UNIQUE_ID} |
| now | Recupera a hora atual. | now() | `2019-10-23T10:10:24.556-07:00[America/Los_Angeles]` |
| carimbo de data e hora | Recupera o tempo Unix atual. | carimbo de data e hora() | 1571850624571 |
| format | Formata a data de entrada de acordo com um formato especificado. | format({DATE}, &quot;aaaa-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Converte um carimbo de data e hora em uma string de data de acordo com um formato especificado. | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23-out-2019 11:24&quot; |
| date | Converte uma string de data em um objeto ZondedDateTime (formato ISO 8601). | date(&quot;23-out-2019 11:24&quot;) | &quot;2019-10-23T11:24:00+00:00&quot; |
| date_part | Recupera as partes da data. Os seguintes valores de componente são suportados: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;trimestre&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>&quot;dayofyear&quot;&quot;&quot;&quot;&quot;&quot;dia&quot;&quot;&quot;&quot;semana&quot;&quot;ww&quot;w&quot;&quot;dia da semana&quot;&quot;dw&quot;&quot;horas&quot; hh&quot;&quot;hh24&quot;&quot;hh12&quot;&quot;minuto&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;ms&quot;&quot; | date_part(date(&quot;2019-10-17 11:55:12&quot;), &quot;MM&quot;) | 10 |
| set_date_part | Substitui um componente em uma determinada data. Os seguintes componentes são aceitos: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;dia&quot;<br><br>&quot;dd&quot;<br>&quot;d&quot;<br>&quot;hora&quot;&quot;&quot;hora&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;&quot;s&quot;&quot;s&quot;&quot;&quot;&quot;s&quot;<br><br>&quot;year&quot;yyyy&quot;y&quot;yy&quot;<br>&quot;yy&quot;yy&quot;Money&quot;Money&quot;Money&quot;m&quot;mm&quot;<br><br><br><br><br><br><br><br>&quot;mm&quot;mm&quot;mm&quot;mm&quot;m&quot;mm&quot;&quot;&quot;&quot;&quot;s&quot;&quot;&quot;&quot;&quot;&quot; | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time /<br>make_timestamp | Cria uma data de partes. | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;América/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| current_timestamp | Retorna o carimbo de data e hora atual. | current_timestamp() | 1571850624571 |
| current_date | Retorna a data atual sem um componente de hora. | current_date() | &quot;18-nov-2019&quot; |