---
title: Linguagem natural do assistente de IA para detalhes do modelo SQL
description: Saiba mais sobre a Linguagem natural do assistente de IA para o modelo de IA do SQL.
exl-id: ca157945-5f74-45d0-9d40-c65d09a8e80d
source-git-commit: 3d870c367317d73bba8b75b38f7b2a93ab6b5bbd
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# Detalhes do modelo de Linguagem natural para SQL dos Insights operacionais do assistente de IA

>[!IMPORTANT]
>
>A Adobe está publicando ativamente mais detalhes do modelo; uma documentação adicional será adicionada ao Experience League assim que estiver disponível.

## Visão geral do modelo {#model-overview}

* **Nome e versão do modelo**: linguagem natural para modelo SQL dos Insights Operacionais do assistente do Adobe Experience Platform AI ([!DNL NL2SQL]).
* **Data de lançamento do modelo**: fevereiro de 2025
* **Finalidade do modelo**: o modelo foi criado para traduzir para consultas SQL as linguagens naturais dos clientes sobre insights operacionais. Essas consultas SQL são executadas no gráfico de conhecimento do Adobe Experience Platform, que contém metadados sobre as entidades Experience Platform dos clientes — como esquemas, conjuntos de dados, públicos, destinos e jornadas. Os resultados dos queries SQL são usados para gerar respostas às perguntas da linguagem natural original dos clientes.
* **Usuários pretendidos**: os principais usuários deste modelo são profissionais de marketing, analistas de dados ou gerentes de jornadas de clientes, que buscam entender e agir com base em insights operacionais no Experience Platform usando linguagem natural. Eles podem não ser especialistas em SQL ou engenharia de dados, mas precisam de respostas rápidas e precisas sobre suas entidades da Experience Platform para tomar decisões informadas e otimizar as experiências do cliente.
* **Casos de uso**: esse modelo ajuda os usuários a acessar metadados sobre suas entidades do Experience Platform, como públicos, jornadas, esquemas, atributos, conjuntos de dados e destinos. Os usuários podem fazer perguntas em linguagem natural — como quais públicos-alvo são ativados ou quais públicos-alvo estão usando um esquema específico — e o modelo os traduz em consultas SQL no gráfico de conhecimento do Experience Platform. Isso permite que os usuários ganhem visibilidade operacional rapidamente e tomem decisões informadas sem precisar explorar ou consultar manualmente o sistema.
* **Pontos problemáticos**: esse modelo aborda os principais pontos problemáticos enfrentados pelos usuários e analistas empresariais que trabalham com a Experience Platform, como a complexidade de navegar em grandes volumes de metadados interconectados, a necessidade de gravar consultas SQL manualmente para recuperar insights operacionais e a falta de visibilidade sobre como entidades da Experience Platform, como públicos, conjuntos de dados e jornadas, estão conectadas ou estão se apresentando. Ao permitir o acesso a metadados em linguagem natural e automatizar a geração de SQL, o modelo reduz a dependência de recursos técnicos, diminui o tempo de detecção da insight e permite que os usuários tomem decisões mais rápidas orientadas por dados.

## Detalhes do modelo {#model-details}

* **Tipo de modelo**: prompt do LLM com Aprendizado em Contexto Dinâmico
* **Entrada**: consultas de linguagem natural do usuário.
* **Saída**: o modelo gera consultas SQL na sintaxe [!DNL Snowflake], que serão executadas no gráfico de conhecimento do Experience Platform.

**Exemplo de entrada**

```console
How many datasets were created within the last 10 days?
```

**Exemplo de saída**

```SQL
SELECT
    COUNT(*) AS datasetCount 
FROM hkg_dim_dataset 
WHERE
    createdTime >= DATEADD(day, -10, CURRENT_DATE);
```

## Avaliação do modelo {#model-evaluation}

* **Métricas e procedimentos de avaliação**: o modelo é avaliado observando as [!DNL NL2SQL] solicitações e avaliando quantas delas produzem os resultados SQL corretos. O processo de avaliação é uma combinação de correspondência baseada em regras (padronização de SQL e, em seguida, correspondência direta de sequência de SQL), solucionador de SQL baseado em LLM e avaliação humana.
* **Dados de avaliação e pré-processamento**: usamos conjuntos abertos para testes de regressão e também temos projetos de anotação semanais para monitorar o desempenho do modelo por meio do tráfego real do cliente amostrado.

## Implantação do modelo {#model-deployment}

* **Monitoramento de modelo**: o modelo base está hospedado por [!DNL Azure].
* **Atualização do modelo**: a Linguagem natural para o modelo SQL dos Insights Operacionais do Assistente de IA do Adobe Experience Platform é atualizada regularmente (semanalmente) por meio da expansão do banco de perguntas. O modelo também é atualizado por meio de novas estratégias de solicitação e instruções quando necessário.

## Equidade e viés {#fairness-and-bias}

* **Integridade do modelo**: para garantir que o modelo interprete e gere consultas consistentemente em diferentes intenções de usuário e variações linguísticas sem introduzir viés ou reforçar estereótipos, o Adobe usa auditoria imediata, explicabilidade e proteções contra geração de saída enviesada ou não ética.
* **Vieses de dados**: a saída do modelo é afetada pelos exemplos de Aprendizado em contexto interno e o que o recuperador seleciona no prompt. Os exemplos de banco de perguntas contêm exemplos considerados representativos da perspectiva do Gerenciamento de produtos. Dependendo do caso de uso, os clientes devem considerar como possíveis distorções nas saídas do modelo podem se alinhar ou afetar a aplicação desejada.

## Considerações éticas {#ethical-considerations}

**Considerações éticas associadas ao modelo**: para evitar a exposição de PII ou atributos confidenciais, o modelo foi projetado para evitar o reforço de distorções de dados existentes e respeitar limites de controle de acesso. Isso inclui filtragem, marcação e auditoria de campos de esquema para uso responsável.
