---
keywords: Experience Platform;página inicial;tópicos populares;
title: Guia de solução de problemas de preparação de dados
description: Este documento fornece respostas a perguntas frequentes sobre o Preparo de dados da Adobe Experience Platform.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: ff8f660c2b3a04d8b4b9d4f19891816a44069088
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# Guia de solução de problemas do [!DNL Data Prep]

Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform [!DNL Data Prep], bem como um guia de solução de problemas para erros comuns. Para obter perguntas e informações sobre a solução de problemas das APIs da Platform em geral, consulte o [guia de solução de problemas da API do Adobe Experience Platform](../landing/troubleshooting.md).

## Perguntas frequentes

Veja a seguir uma lista de perguntas frequentes sobre [!DNL Data Prep] e suas respostas.

### Como os erros de transformação são resolvidos?

[!DNL Data Prep] localiza todos os erros de transformação na coluna em que ocorreram. Como resultado, essa coluna é anulada e o restante da linha continuará a ser processado. Esses problemas de transformação são registrados como **Avisos**. É recomendável que você revise os avisos periodicamente e ajuste a lógica de transformação para levar em conta os problemas de transformação. Isso aumentará a qualidade dos dados assimilados no Experience Platform.

Se as colunas marcadas como **Obrigatório** forem anuladas devido a problemas de transformação, a linha não será assimilada. Quando a assimilação parcial de dados está ativada, é possível definir o limite dessas rejeições antes que todo o fluxo falhe. Se o atributo nulo não tiver afetado nenhuma validação de nível de esquema, a linha continuará sendo assimilada.

Quaisquer linhas inválidas, mesmo sem erros de transformação, também serão rejeitadas. Por exemplo, um fluxo de assimilação de dados pode ter um mapeamento de passagem (sem lógica de transformação) para um campo obrigatório e não há valor de entrada para esse atributo. Esta linha será rejeitada.

### Como posso escapar caracteres especiais em um campo?

Você pode escapar caracteres especiais em um campo usando `${...}`. No entanto, arquivos JSON que contêm campos com um ponto (`.`) não são suportados por esse mecanismo. Ao interagir com hierarquias, se um atributo filho tiver um ponto (`.`), você deverá usar uma barra invertida (`\`) para usar escape em caracteres especiais. Por exemplo, `address` é um objeto que contém o atributo `street.name`, ele pode ser chamado de `address.street\.name` em vez de `address.street.name`.

### Qual é o comprimento máximo dos campos calculados?

Os campos calculados têm um comprimento máximo de 4096 caracteres.

### Minha assimilação falhou devido à validação em um atributo, mas eu tenho esse atributo corretamente no arquivo. O que exatamente está errado?

Verifique se o tipo de dados de cada campo corresponde ao tipo definido no esquema. Além disso, restrições como &quot;Obrigatório&quot;, &quot;enum&quot; e &quot;format&quot; devem ser seguidas.

Os dados assimilados devem estar em conformidade com o esquema do Experience Data Model (XDM) definido no Experience Platform. Se o atributo não corresponder ao tipo ou formato especificado no esquema, a assimilação falhará.

Se as funções de Preparo de dados estiverem sendo usadas, verifique se a transformação resulta nos atributos corretos. Você pode revisar os atributos durante o processo de configuração do workflow de origens. Durante a etapa de mapeamento, selecione **[!UICONTROL Novo tipo de campo]** e **[!UICONTROL Adicionar campo calculado]**. Em seguida, use a interface de campo calculado para visualizar cada função.

### Como posso remover valores de dados incorretos de registros de streaming ou assimilação em lote?

Você pode usar a interface de mapeamento Preparação de dados para executar a filtragem em nível de coluna, mapeando apenas as colunas que têm dados necessários. Também é possível usar campos calculados para transformar os dados usando as funções de suporte.

No momento, a filtragem em nível de linha está disponível somente para o [conector de origem do Adobe Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md#row-level-filtering).

Após a assimilação, você pode usar o destilador de dados para limpar, moldar e manipular os dados usando SQL. No entanto, esse processo exigirá a exclusão do lote com os registros inválidos e a assimilação novamente de um novo lote criado a partir do resultado do SQL.

>[!IMPORTANT]
>
>* Data lake: somente é possível remover registros que já foram assimilados excluindo e assimilando novamente o lote em que o registro está.
>
>* Perfil de cliente em tempo real: você pode substituir registros baseados em atributos assimilando novos registros, mas os registros de evento de experiência não podem ser removidos.
>
>* Serviço de identidade: não é possível remover registros diretamente no Serviço de identidade. Será necessário excluir o perfil inteiro e fazer upload novamente do perfil com os registros corretos usando a API de exclusão de perfil.

### Quais são as práticas recomendadas para usar campos calculados em dados de GIF?

Você pode usar as funções de mapeamento Preparação de dados durante a etapa de mapeamento dos dados de origem para o esquema XDM para criar um novo campo calculado.

### Ao trazer os dados do Adobe Analytics como uma fonte, o esquema criado automaticamente é habilitado para o perfil?

Os dados do Analytics não são configurados automaticamente para o Perfil. Depois de configurar o conector de origem, você deve acessar o conjunto de dados e o esquema e ativá-los para assimilação do Perfil.

Ao criar um fluxo de dados de origem do Analytics em uma sandbox de produção, dois fluxos de dados são criados:

* Um fluxo de dados que faz um preenchimento retroativo de 13 meses de dados históricos do conjunto de relatórios no data lake. Esse fluxo de dados termina quando o preenchimento retroativo é concluído.
* Um fluxo de dados que envia dados em tempo real para o data lake e o Perfil. Esse fluxo de dados é executado continuamente.

### Como posso colocar um valor em minúsculas dentro de um objeto de mapa usando funções de Preparo de dados?

Você pode recuperar o valor usando a função `map_get_values` e deixá-lo em minúsculas usando a função lower:

```shell
lower(map_get_values(mapObject, 'keyName'))
```

Você pode usar a mesma função para colocar um objeto de mapa em minúsculas. No entanto, não é possível percorrer um mapa inteiro e colocar cada item em letras minúsculas.

### Posso usar as funções de Preparo de dados de maneira aninhada?

Sim, você pode usar uma função Preparo de dados em outra função para solucionar recursos complexos de preparação de dados durante a assimilação de dados.

Por exemplo, se você quiser definir um campo como nulo com base em uma condição específica, poderá usar a função &quot;iif&quot; para verificar esse campo. Se a função retornar `true`, você poderá usar &quot;nullify()&quot; e, se retornar `false`, poderá usar o respectivo campo.

Se marketing_type era o campo, você pode usar &quot;.equals&quot; para verificar o valor no campo marketing_type e isso pode ser aninhado em uma função &quot;iif&quot;. Se retornar `true`, você poderá usar a função &quot;nullify()&quot; como mostrado abaixo:

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

A seguir são descritos exemplos de como é possível aninhar funções de Preparo de dados usando if, equals e nullify:

| Função | Descrição | Parâmetros | Sintaxe | Expressão | Saída de exemplo |
| --- | --- | --- | --- | --- | --- |
| iif | Avalia uma determinada expressão booleana e retorna o valor especificado com base no resultado. | <ul><li>EXPRESSION: **Required** A expressão booleana que está sendo avaliada.</li><li>TRUE_VALUE: **Obrigatório** O valor retornado se a expressão for avaliada como verdadeira.</li><li>FALSE_VALUE: **Obrigatório** O valor retornado se a expressão for avaliada como falsa.</li></ul> | iif(EXPRESSÃO, VALOR_VERDADEIRO, VALOR_FALSO) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |
| igual a | Compara duas strings para confirmar se são iguais. Esta função diferencia maiúsculas de minúsculas. | <ul><li>STRING1: **Obrigatório** A primeira cadeia de caracteres que você deseja comparar.</li><li>CADEIA DE CARACTERES2: **Obrigatório** A segunda cadeia de caracteres que você deseja comparar. | STRING1.&#x200B;equals(&#x200B;STRING2) | &quot;string1&quot;.&#x200B;equals&#x200B;(&quot;STRING1&quot;) | false |
| nullify | Define o valor do atributo como nulo. Isso deve ser usado quando você não deseja copiar o campo para o schema de destino. | | nullify() | nullify() | nulo |

{style="table-layout:auto"}

Este é um exemplo de como as funções podem ser aninhadas, supondo que o campo que está sendo avaliado seja &quot;marketing_type&quot;.

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

Em seguida, considerando que você tem os três campos a seguir:

* marketing_type: (email, phyMail, push, sms, telefone)
* total_consents: intervalo numérico de 4000 a 5500
* data: de fevereiro a março de 2024

Você pode usar e aninhar as três funções listadas acima para manipular os três campos:

* iif(marketing_type.equals(&quot;email&quot;), nullify(), iif(marketing_type.equals(&quot;push&quot;), &quot;push-notification&quot;, marketing_type))
* iif(marketing_type.equals(&quot;phyMail&quot;), nullify(), iif(marketing_type.equals(&quot;sms&quot;), &quot;text-message&quot;, marketing_type))
* iif(total_consentimentos > 5000, iif(marketing_type.equals(&quot;phone&quot;), nullify(), marketing_type), &quot;consentimentos insuficientes&quot;)
* iif(date.equals(&quot;3/21/24&quot;), iif(marketing_type.equals(&quot;push&quot;), nullify(), marketing_type), &quot;not-March&quot;)
* iif(total_consents &lt; 4500, iif(marketing_type.equals(&quot;sms&quot;), &quot;low-consent-sms&quot;, marketing_type), &quot;high-consents&quot;)
* iif(marketing_type.equals(&quot;email&quot;), iif(total_consents > 5000, nullify(), &quot;email-low-consents&quot;), marketing_type)
* iif(marketing_type.equals(&quot;push&quot;), iif(total_consents &lt; 4500, &quot;low-consent-push&quot;, nullify()), marketing_type)
* iif(total_consentimentos >= 5500, iif(marketing_type.equals(&quot;phyMail&quot;), nullify(), &quot;alto-consentimento&quot;), marketing_type)