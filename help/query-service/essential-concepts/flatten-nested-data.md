---
keywords: Experience Platform;serviço de consulta;serviço de consulta;estruturas de dados aninhadas;dados aninhados;nivelar;nivelar dados aninhados;
title: Nivelar Estruturas de Dados Aninhadas para Uso com Ferramentas de BI
description: Este documento explica como nivelar esquemas XDM para todas as tabelas e exibições durante uma sessão ao usar ferramentas de BI de terceiros com o Serviço de consulta.
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: 1c590350c9d519dba60375b92de7bbbbd77961dc
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 1%

---

# Nivelar estruturas de dados aninhadas para uso com ferramentas de BI de terceiros

O Serviço de consulta do Adobe Experience Platform é compatível com o `FLATTEN` configuração ao conectar-se a um banco de dados por meio de ferramentas de BI de terceiros. Esse recurso nivela as estruturas de dados aninhadas em ferramentas de BI de terceiros para melhorar sua usabilidade e reduzir a carga de trabalho necessária para recuperar, analisar, transformar e relatar dados.

Muitas ferramentas de BI, como [!DNL Tableau] e [!DNL Power BI] não suportam nativamente estruturas de dados aninhadas. A variável `FLATTEN` A configuração remove a necessidade de criar visualizações SQL sobre seus dados para fornecer uma versão simples ou usar o Serviço de consulta `CTAS` ou `INSERT INTO` trabalhos para duplicar seus conjuntos de dados em versões planas ao usar esquemas ad hoc.

A variável `FLATTEN` a configuração puxa a estrutura de cada campo de folha para a raiz da tabela e nomeia o campo após o namespace original. Isso permite usar a notação de pontos para corresponder um campo ao seu caminho do Modelo de dados de experiência (XDM), preservando o contexto do campo.

## Pré-requisitos

Usar o `FLATTEN` A configuração do exige uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema XDM](../../xdm/home.md): uma visão geral de alto nível do XDM e sua implementação no Experience Platform.

   * [Criar um esquema ad hoc](../../xdm/tutorials/ad-hoc.md): um esquema XDM com campos com namespace para uso somente por um único conjunto de dados é chamado de esquema ad hoc. Esquemas ad hoc são usados em vários workflows de assimilação de dados para o Experience Platform e para criar determinados tipos de conexões de origem.

* [Sandboxes](../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

* [Estruturas de dados aninhadas](./nested-data-structures.md): este documento fornece exemplos de como criar, processar ou transformar conjuntos de dados com tipos de dados complexos, incluindo estruturas de dados aninhadas.

## Conectar a um banco de dados usando a configuração NIVELAR {#connect-with-flatten}

A variável `FLATTEN` a configuração nivela estruturas de dados aninhadas em colunas separadas, onde o nome do atributo se torna o nome da coluna que contém os valores de linha. Ao trabalhar com dados em ferramentas de BI que não suportam estruturas de dados aninhadas, essa configuração melhora a usabilidade de esquemas ad hoc e reduz a carga de trabalho necessária.

Ao se conectar ao Serviço de consulta com o cliente de terceiros escolhido, anexe o `FLATTEN` ao nome do banco de dados. Para obter informações sobre como conectar uma ferramenta de BI específica, consulte a respectiva documentação no [conectar clientes à visão geral do Serviço de consulta](../clients/overview.md). A cadeia de conexão deve conter:

* O nome da sandbox.
* Dois pontos seguido por `all` ou uma ID do conjunto de dados, ID da exibição ou nome do banco de dados específico.
* Um ponto de interrogação (?) seguido pelo `FLATTEN` palavra-chave.

A entrada deve ter o seguinte formato:

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

Um exemplo de cadeia de conexão pode ter a seguinte aparência:

```terminal
prod:all?FLATTEN
```

## Exemplo {#example}

O schema de exemplo usado neste guia emprega o grupo de campos padrão [!UICONTROL Detalhes do comércio], que utiliza o `commerce` estrutura do objeto e o `productListItems` matriz. Consulte a documentação do XDM para [mais informações sobre o [!UICONTROL Detalhes do comércio] grupo de campos](../../xdm/field-groups/event/commerce-details.md). Uma representação da estrutura do schema pode ser vista na imagem abaixo.

![Um diagrama de esquema do grupo de campos Commerce Details incluindo o `commerce` e `productListItems` estruturas.](../images/essential-concepts/commerce-details.png)

Se sua ferramenta de BI não suportar estruturas de dados aninhadas, pode ser difícil fazer referência a campos aninhados caso eles contenham valores serializados (como `commerce` e `productListItems` no schema de exemplo). Esses valores podem aparecer como partes de um único código `commerce` e não são realistas.

Os seguintes valores representam `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180), e `commerce.purchases.value`(1.0) em campos aninhados mal formatados.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

Ao usar o `FLATTEN` Ao configurar, é possível acessar campos separados no esquema ou seções inteiras da estrutura de dados aninhada usando a notação de pontos e o nome do caminho original. Um exemplo desse formato usando o `commerce` grupo de campos é fornecido abaixo.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

A variável `FLATTEN` A configuração do tem determinadas limitações ao lidar com outras estruturas de dados. Os detalhes completos são fornecidos no [seção de limitações](#limitations).

### Usar aspas para campos em consultas {#quotation-marks}

Os campos de raiz nivelada agora usam a notação de pontos para corresponder aos caminhos XDM. Quando usados em uma consulta, os campos precisam estar entre aspas (&quot; &quot;).

O exemplo de SQL abaixo exibe o estado original da consulta aninhada:

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

Ao usar os campos de dados nivelados, a consulta é gravada com a notação de pontos e delimitada por aspas, como observado a seguir:

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## Limitações {#limitations}

A variável `FLATTEN` No momento, a configuração não nivela as seguintes estruturas de dados:

| Estrutura de dados | Limitação |
|---|---|
| Matrizes | Use um índice de matriz explícito ou o `EXPLODE` função para acessar matrizes. |
| Mapas | Use a chave de string para acessar um valor em um mapa para acessar mapas. |

Para resolver as limitações de Mapa e Array, é necessário usar a edição bruta de SQL das ferramentas de BI, como Opções avançadas -> Instrução SQL no Power BI.

Ferramentas de BI, como edição de SQL bruto, são necessárias para resolver limitações de mapa e de matriz. Consulte o guia sobre como [usar as opções avançadas do Power BI para inserir uma consulta SQL personalizada](../clients/power-bi.md#import-tables-using-custom-sql) na seção Instrução SQL.

## Próximas etapas

Esse documento abordou como nivelar estruturas de dados aninhadas para uso com ferramentas de BI de terceiros. Se você ainda não tiver conectado seu cliente, consulte [a visão geral da conexão do cliente](../clients/overview.md) para obter uma lista de clientes de terceiros compatíveis.
