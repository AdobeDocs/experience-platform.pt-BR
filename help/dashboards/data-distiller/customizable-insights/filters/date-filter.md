---
title: Criar um filtro de datas
description: Saiba como filtrar seus insights personalizados por data.
exl-id: fa05d651-ea43-41f0-9b7d-f19c4a9ac256
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Criar um filtro de datas {#create-date-filter}

Para filtrar seus insights por data, você deve adicionar parâmetros às suas consultas SQL que podem aceitar restrições de data. Isso é feito como parte do fluxo de trabalho de criação de insight do modo pro de consulta. Consulte a [documentação do modo pro de consulta](#query-pro-mode) para saber como inserir SQL para seus insights.

Parâmetros de consulta permitem trabalhar com dados dinâmicos como eles atuam como espaços reservados para os valores adicionados no tempo de execução. Esses valores de espaços reservados podem ser atualizados por meio da interface do usuário e permitem que usuários menos técnicos atualizem os insights com base em intervalos de datas.

Se você não estiver familiarizado com parâmetros de consulta, consulte a documentação de [orientação sobre como implementar consultas parametrizadas](../../../../query-service/ui/parameterized-queries.md).

## Aplicar um filtro de datas ao painel {#apply-date-filter}

Para aplicar um filtro de datas, selecione **[!UICONTROL Adicionar filtro]** e **[!UICONTROL Filtro de Datas]** no menu suspenso do modo de exibição de painel.

![Um painel personalizado com Adicionar filtro e seu menu suspenso realçado.](../../../images/customizable-insights/add-filter.png)

## Edite seu SQL para incluir parâmetros de consulta de data {#include-date-parameters}

Em seguida, verifique se o SQL inclui parâmetros de consulta para permitir um intervalo de datas. Se você ainda não tiver incorporado parâmetros de consulta ao seu SQL, edite seus insights para incluir esses parâmetros. Consulte a documentação para obter instruções sobre como [editar um insight](../query-pro-mode.md#edit).

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

![A caixa de diálogo [!UICONTROL Inserir SQL] com os parâmetros de data realçados no SQL.](../../../images/customizable-insights/sql-date-parameters.png)

## Ativar parâmetros de data em cada insight {#enable-date-parameters}

Depois de incorporar os parâmetros apropriados ao SQL dos seus insights, as variáveis `Start_date` e `End_date` agora estão disponíveis como alternadores no widget composer. Consulte a [seção de população do widget do modo pro de consulta](#populate-widget) para obter informações sobre como editar um insight.

No widget composer, selecione alternar para habilitar os parâmetros `Start_date` e `End_date`.

![O widget composer com as opções Start_date e End_date está realçado.](../../../images/customizable-insights/widget-composer-date-filter-toggles.png)

Em seguida, selecione os parâmetros de consulta apropriados nos menus suspensos.

![O widget composer com o menu suspenso Start_date realçado.](../../../images/customizable-insights/widget-composer-date-filter-dropdown.png)

Finalmente, selecione **[!UICONTROL Salvar e fechar]** para retornar ao seu painel. Agora, os filtros de data estão ativados para todos os insights que têm parâmetros de data de início e término.

## Usar o filtro de datas

Para usar um filtro de data personalizado, selecione o ícone de calendário e escolha um início e fim na exibição de calendário.

>[!IMPORTANT]
>
>Simplesmente adicionar um filtro de data não fará com que os gráficos sejam alterados. Você deve editar cada um dos insights para incluir as datas de início e término escolhidas.

![Um painel personalizado com o calendário de filtro de data realçado.](../../../images/customizable-insights/date-filter.png)

Depois de selecionar um intervalo de datas no painel, os insights que têm parâmetros de data em seu SQL verão as opções de filtro de data no widget composer.

>[!NOTE]
>
>Selecionar um intervalo de datas no painel exibe os botões para filtros de data como parte do fluxo de trabalho de criação de insight.

## Excluir um filtro de datas {#delete-date-filter}

Para remover o filtro de datas, selecione o ícone de exclusão de filtro (![O ícone de exclusão de filtro.](/help/images/icons/filter-delete.png)).

![Um painel personalizado com o ícone de exclusão de filtro realçado.](../../../images/customizable-insights/delete-date-filter.png)
