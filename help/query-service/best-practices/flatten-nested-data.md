---
keywords: Experience Platform, serviço de consulta, serviço de consulta, estruturas de dados aninhadas, dados aninhados, achatado, dados aninhados nivelados,
title: Nivelar estruturas de dados aninhadas para uso com ferramentas de BI
description: Este documento explica como nivelar esquemas XDM para todas as tabelas e visualizações durante uma sessão ao usar ferramentas de BI de terceiros com Serviço de Consulta.
source-git-commit: 3c9a1f552760b34bfb2c4246382fcb2d66e563d0
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 1%

---

# Nivelar estruturas de dados aninhadas para uso com ferramentas de BI de terceiros

O Adobe Experience Platform Query Service oferece suporte para `FLATTEN` configuração ao se conectar a um banco de dados por meio de ferramentas de BI de terceiros. Esse recurso nivela estruturas de dados aninhadas em ferramentas de BI de terceiros para melhorar sua usabilidade e reduzir a carga de trabalho necessária para recuperar, analisar, transformar e relatar dados.

Muitas ferramentas de BI como [!DNL Tableau] e [!DNL Power BI] não oferecem suporte nativo a estruturas de dados aninhadas. O `FLATTEN` a configuração remove a necessidade de criar exibições SQL sobre seus dados para fornecer uma versão simples ou usar o Serviço de query `CTAS` ou `INSERT INTO` tarefas para duplicar seus conjuntos de dados em versões simples ao usar esquemas ad hoc.

O `FLATTEN` essa configuração puxa a estrutura de cada campo de folha para a raiz da tabela e nomeia o campo após o namespace original. Isso permite usar a notação de pontos para corresponder um campo ao caminho do Modelo de dados de experiência (XDM), preservando o contexto do campo.

## Pré-requisitos

Usar o `FLATTEN` a configuração do exige uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema XDM](../../xdm/home.md): Uma visão geral de alto nível do XDM e sua implementação no Experience Platform.

   * [Criar um esquema ad hoc](../../xdm/tutorials/ad-hoc.md): Um esquema XDM com campos nomeados para uso somente por um único conjunto de dados é chamado de esquema ad hoc. Esquemas ad hoc são usados em vários workflows de assimilação de dados para o Experience Platform e na criação de determinados tipos de conexões de origem.

* [Sandboxes](../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

* [Estruturas de dados aninhadas](./nested-data-structures.md): Este documento fornece exemplos de como criar, processar ou transformar conjuntos de dados com tipos de dados complexos, incluindo estruturas de dados aninhadas.

## Conectar-se a um banco de dados usando a configuração FLATTEN {#connect-with-flatten}

O `FLATTEN` a configuração nivela estruturas de dados aninhadas em colunas separadas, onde o nome do atributo se torna o nome da coluna que retém os valores da linha. Ao trabalhar com dados em ferramentas de BI que não oferecem suporte a estruturas de dados aninhadas, essa configuração melhora a usabilidade de esquemas ad hoc e reduz a carga de trabalho necessária.

Ao se conectar ao Serviço de query com o cliente de terceiros escolhido, anexe o `FLATTEN` configuração para o nome do banco de dados. Para obter informações sobre como conectar uma ferramenta de BI específica, consulte sua respectiva documentação na [conectar clientes à visão geral do Serviço de query](../clients/overview.md). A cadeia de conexão deve conter:

* O nome da sandbox.
* Dois pontos seguidos de `all` ou um ID de conjunto de dados específico, ID de exibição ou nome de banco de dados.
* Um ponto de interrogação (?) seguido pelo `FLATTEN` palavra-chave.

A entrada deve ter o seguinte formato:

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

Um exemplo de string de conexão pode ser a seguinte:

```terminal
prod:all?FLATTEN
```

## Exemplo {#example}

O schema de exemplo usado neste guia emprega o grupo de campos padrão [!UICONTROL Detalhes de comércio], que utiliza o `commerce` estrutura do objeto e `productListItems` matriz. Consulte a documentação do XDM para [mais informações sobre o [!UICONTROL Detalhes de comércio] grupo de campos](../../xdm/field-groups/event/commerce-details.md). Uma representação da estrutura do schema pode ser vista na imagem abaixo.

![Um diagrama de esquema do grupo de campos Detalhes de Comércio , incluindo o `commerce` e `productListItems` estruturas.](../images/best-practices/final-subscription-schema.png)

Se a ferramenta BI não oferecer suporte a estruturas de dados aninhadas, pode ser difícil fazer referência a campos aninhados caso eles contenham valores serializados (como `commerce` e `productListItems` no schema de exemplo). Esses valores podem aparecer como partes de um único `commerce` e não são realisticamente inutilizáveis.

Os seguintes valores representam `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180) e `commerce.purchases.value`(1.0) em campos aninhados mal formatados.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

Ao usar a variável `FLATTEN` , é possível acessar campos separados no esquema ou seções inteiras da estrutura de dados aninhada usando a notação de pontos e seu nome de caminho original. Um exemplo desse formato usando o `commerce` O grupo de campos é fornecido abaixo.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

O `FLATTEN` A configuração do tem determinadas limitações ao lidar com outras estruturas de dados. Os detalhes completos são fornecidos no [seção limitações](#limitations).

### Usar aspas para campos em queries {#quotation-marks}

Os campos raiz nivelados agora usam a notação de pontos para corresponder aos caminhos XDM. Quando usados em uma query, os campos precisam ser colocados entre aspas (&quot; &quot;).

O exemplo SQL abaixo exibe o estado original da consulta aninhada:

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

Ao usar os campos de dados nivelados, o query é gravado usando a notação de pontos e entre aspas, conforme mostrado abaixo:

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## Limitações {#limitations}

O `FLATTEN` no momento, a configuração não nivela as seguintes estruturas de dados:

| Estrutura de dados | Limitação |
|---|---|
| Matrizes | Use um índice de matriz explícito ou a variável `EXPLODE` para acessar arrays. |
| Mapas | Use a chave da string para acessar um valor em um mapa para acessar mapas. |

Para resolver as limitações de Mapa e Matriz, é necessário usar as ferramentas de BI para a edição SQL bruta, como as Opções avançadas -> Instrução SQL no Power BI.

Ferramentas de BI, como edição SQL bruta, são necessárias para resolver limitações de mapa e matriz. Consulte o guia sobre como [usar opções avançadas do Power BI para inserir uma consulta SQL personalizada](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html#import-tables-using-custom-sql) na seção instrução SQL.

## Próximas etapas

Este documento cobriu como nivelar estruturas de dados aninhadas para uso com ferramentas de BI de terceiros. Se ainda não tiver conectado seu cliente, consulte [visão geral da conexão com o cliente](../clients/overview.md) para obter uma lista de clientes de terceiros suportados.
