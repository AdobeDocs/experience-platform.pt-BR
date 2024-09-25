---
title: Criar um filtro de datas
description: Saiba como filtrar seus insights personalizados por data.
exl-id: fa05d651-ea43-41f0-9b7d-f19c4a9ac256
source-git-commit: 77cedd351b5628d15c279fceabde735f4f93f392
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 1%

---

# Criar um filtro de datas {#create-date-filter}

Para filtrar seus insights por data, você deve adicionar parâmetros às suas consultas SQL que podem aceitar restrições de data. Isso é feito como parte do fluxo de trabalho de criação de insight do modo pro de consulta. Consulte a [documentação do modo pro de consulta](#query-pro-mode) para saber como inserir SQL para seus insights.

Parâmetros de consulta permitem trabalhar com dados dinâmicos como eles atuam como espaços reservados para os valores adicionados no tempo de execução. Esses valores de espaços reservados podem ser atualizados por meio da interface do usuário e permitem que usuários menos técnicos atualizem os insights com base em intervalos de datas.

Se você não estiver familiarizado com parâmetros de consulta, consulte a documentação de [orientação sobre como implementar consultas parametrizadas](../../../../query-service/ui/parameterized-queries.md).

## Aplicar um filtro de datas ao painel {#apply-date-filter}

Para aplicar um filtro de datas, selecione **[!UICONTROL Adicionar filtro]** e **[!UICONTROL Filtro de Datas]** no menu suspenso do modo de exibição de painel.

![Um painel personalizado com Adicionar filtro e seu menu suspenso realçado.](../../../images/query-pro-mode/add-filter.png)

As seguintes opções de filtragem de data são apresentadas a você.

| Filtro | Descrição |
| --- | --- |
| Nenhuma data personalizada | Selecione uma ou mais datas personalizadas a partir de vários valores predefinidos. |
| Intervalo de datas personalizado | Selecione uma ou mais datas personalizadas de vários valores predefinidos ou especifique um intervalo de datas personalizado. |
| Data personalizada | Selecione nos valores atuais ou especifique a data de início do seu painel. |

![A caixa de diálogo Criar filtro de data com as três opções personalizadas de seletor de data está realçada.](../../../images/query-pro-mode/create-date-filter.png)

### Criar um filtro sem data personalizada

Para aplicar um filtro de data predefinido, selecione **[!UICONTROL Sem data personalizada]** e selecione as opções de data predefinidas que deseja incluir. Por fim, use a lista suspensa para selecionar o intervalo de datas padrão, em seguida, selecione **[!UICONTROL Salvar]**.

![A caixa de diálogo Criar filtro de data sem filtro de data personalizado e salvar realçada.](../../../images/query-pro-mode/no-custom-date-filter.png)

Você retornará ao painel, que mostra o intervalo de datas padrão selecionado anteriormente. Use o menu suspenso para selecionar outro intervalo de datas predefinido.

![Um painel personalizado mostrando o intervalo de datas padrão com a lista suspensa realçada.](../../../images/query-pro-mode/no-custom-date-filter-results.png)

### Criar um filtro de intervalo de datas personalizado

Para aplicar um filtro de intervalo de datas personalizado, selecione **[!UICONTROL Intervalo de datas personalizado]** e selecione as opções de data predefinidas que deseja incluir. Finalmente, selecione **[!UICONTROL Personalizado]** para definir o intervalo de datas padrão. Use o calendário para especificar um intervalo de datas, depois selecione **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Não é necessário selecionar opções de data predefinidas.

![A caixa de diálogo Criar filtro de data com o filtro de intervalo de datas personalizado, personalizado e salvar realçado.](../../../images/query-pro-mode/custom-date-range-filter.png)

Você retornará ao painel, que mostra o intervalo de dados personalizado especificado anteriormente. Use o menu suspenso para selecionar outro intervalo de datas predefinido.

![Um painel personalizado mostrando o intervalo de datas padrão com a data personalizada realçada.](../../../images/query-pro-mode/custom-date-range-filter-results.png)

### Criar um filtro de data personalizado

Para aplicar um filtro de data personalizado, selecione **[!UICONTROL Data personalizada]** e selecione as opções de data predefinidas que deseja incluir. Finalmente, selecione **[!UICONTROL Personalizado]** e use o calendário para selecionar uma data de início. Finalmente, selecione **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Não é necessário selecionar opções de data predefinidas.

![A caixa de diálogo Criar filtro de data com o filtro de data personalizado, personalizado e salvar realçado.](../../../images/query-pro-mode/custom-date-filter.png)

Você retornará ao painel, que mostra os dados personalizados especificados anteriormente. Use o menu suspenso para selecionar outra data.

![Um painel personalizado mostrando o intervalo de datas padrão com a data personalizada realçada.](../../../images/query-pro-mode/custom-date-filter-results.png)

## Excluir um filtro de datas {#delete-date-filter}

Para remover o filtro de datas, selecione o ícone de exclusão de filtro (![O ícone de exclusão de filtro.](/help/images/icons/filter-delete.png)).

![Um painel personalizado com o ícone de exclusão de filtro realçado.](../../../images/query-pro-mode/delete-date-filter.png)

## Edite seu SQL para incluir parâmetros de consulta de data {#include-date-parameters}

Em seguida, verifique se o SQL inclui parâmetros de consulta para permitir um intervalo de datas. Se você ainda não tiver incorporado parâmetros de consulta ao SQL, edite seus insights para incluir esses parâmetros. Consulte a documentação para obter instruções sobre como [editar um insight](../overview.md#edit).

>[!TIP]
>
>É recomendável adicionar `$START_DATE` e `$END_DATE` parâmetros à instrução SQL em cada um dos gráficos para os quais você deseja habilitar filtros de data.

>[!NOTE]
>
>Os filtros de data não suportam restrições de tempo. O filtro se aplica somente a intervalos de datas. Isso significa que se você tiver vários relatórios em um período de 24 horas, não será possível distinguir entre horas diferentes no mesmo dia. Por esse motivo, é recomendável converter o componente de tempo como uma data.

Se o modelo de dados ou as tabelas que você está analisando tiverem um componente de tempo, você poderá agrupar seus dados por data e aplicar esses filtros de data.

A instrução SQL de exemplo abaixo demonstra como incorporar os parâmetros `$START_DATE` e `$END_DATE` e usa `cast` para enquadrar o componente de tempo como uma data.

```sql
SELECT Sum(personalization_consent_count) AS Personalization,
       Sum(datacollection_consent_count)  AS Datacollection,
       Sum(datasharing_consent_count)     AS Datasharing
FROM   fact_daily_consent_aggregates f
       INNER JOIN dim_consent_valued
               ON f.consent_value_id = d.consent_value_id
WHERE  f.date BETWEEN Upper(Coalesce(Cast('$START_DATE' AS date), '')) AND Upper
                      (
                             Coalesce(Cast('$END_DATE' AS date), ''))
       AND ( ( Upper(Coalesce($consent_value_filter, '')) IN ( '', 'NULL' ) )
              OR ( f.consent_value_id IN ( $consent_value_filter ) ) )
LIMIT  0; 
```

A captura de tela abaixo destaca as restrições de data incorporadas na instrução SQL e nos pares de valores-chave do parâmetro de consulta.

>[!NOTE]
>
>Ao compor sua instrução no modo query pro, você deve fornecer valores de amostra para cada parâmetro para executar a instrução SQL e criar o gráfico. Os valores de amostra fornecidos ao compor a instrução são substituídos pelos valores reais selecionados para o filtro de data (ou global) no tempo de execução.

![A caixa de diálogo [!UICONTROL Inserir SQL] com os parâmetros de data realçados no SQL.](../../../images/sql-insights/sql-date-parameters.png)

## Ativar parâmetros de data em cada insight {#enable-date-parameters}

Depois de incorporar os parâmetros apropriados ao SQL dos seus insights, as variáveis `Start_date` e `End_date` agora estão disponíveis como alternadores no widget composer. Consulte a [seção de população do widget do modo pro de consulta](#populate-widget) para obter informações sobre como editar um insight.

No widget composer, selecione alternar para habilitar os parâmetros `Start_date` e `End_date`.

![O widget composer com as opções Start_date e End_date está realçado.](../../../images/sql-insights/widget-composer-date-filter-toggles.png)

Em seguida, selecione os parâmetros de consulta apropriados nos menus suspensos.

![O widget composer com o menu suspenso Start_date realçado.](../../../images/sql-insights/widget-composer-date-filter-dropdown.png)

Finalmente, selecione **[!UICONTROL Salvar e fechar]** para retornar ao seu painel. Agora, os filtros de data estão ativados para todos os insights que têm parâmetros de data de início e término.
