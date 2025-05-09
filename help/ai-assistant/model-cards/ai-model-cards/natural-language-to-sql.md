---
title: Linguagem natural do assistente de IA para o cartão de modelo SQL
description: Saiba mais sobre a Linguagem natural do assistente de IA para o modelo de IA do SQL.
hide: true
hidefromtoc: true
source-git-commit: 70b705a7c6df24ad9549c46832ff4898253670ac
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Pasta de linguagem natural para modelo SQL do AI Assistant Operational Insights

## Visão geral do modelo {#model-overview}

* O nome oficial do modelo é Linguagem natural para modelo SQL do AI Assistant Operational Insights ([!DNL NL2SQL]) e foi lançado em sua versão mais recente disponível em fevereiro de 2025.
* O modelo foi projetado para traduzir para consultas SQL as consultas em linguagem natural dos clientes sobre insights operacionais. Essas consultas SQL são executadas no gráfico de conhecimento do Adobe Experience Platform, que contém metadados sobre as entidades Experience Platform dos clientes — como esquemas, conjuntos de dados, públicos, destinos e jornadas. Os resultados dos queries SQL são usados para gerar respostas às perguntas da linguagem natural original dos clientes.
* Os principais usuários desse modelo são profissionais de marketing, analistas de dados ou gerentes de jornadas de clientes, que buscam entender e agir com base em insights operacionais no Experience Platform usando linguagem natural. Eles podem não ser especialistas em SQL ou engenharia de dados, mas precisam de respostas rápidas e precisas sobre suas entidades da Experience Platform para tomar decisões informadas e otimizar as experiências do cliente.
* Esse modelo faz parte do Assistente de IA para Insights operacionais, onde ajuda os usuários a acessar metadados sobre suas entidades do Experience Platform, como públicos, jornadas, esquemas, atributos, conjuntos de dados e destinos. Os usuários podem fazer perguntas em linguagem natural — como quais públicos-alvo são ativados ou quais públicos-alvo estão usando um esquema específico — e o modelo os traduz em consultas SQL no gráfico de conhecimento do Experience Platform. Isso permite que os usuários ganhem visibilidade operacional rapidamente e tomem decisões informadas sem precisar explorar ou consultar manualmente o sistema.
* Esse modelo aborda os principais pontos problemáticos enfrentados pelos usuários e analistas de negócios que trabalham com o Experience Platform, como a complexidade de navegar em grandes volumes de metadados interconectados, a necessidade de gravar consultas SQL manualmente para recuperar insights operacionais e a falta de visibilidade sobre como entidades do Experience Platform, como públicos, conjuntos de dados e jornadas, estão conectadas ou estão em desempenho. Ao permitir o acesso a metadados em linguagem natural e automatizar a geração de SQL, o modelo reduz a dependência de recursos técnicos, diminui o tempo de detecção da insight e permite que os usuários tomem decisões mais rápidas orientadas por dados.
* O modelo não deve ser usado para acessar ou inferir informações pessoais identificáveis (PII), como nomes de clientes, endereços de email ou números de telefone, mesmo se esses dados existirem na plataforma.
* Além disso, ela não deve ser usada para verificações de conformidade ou governança, como validação de políticas de retenção de dados, regras de controle de acesso ou status de consentimento. Essas tarefas exigem sistemas e estratégias especializados.

## Detalhes do modelo {#model-details}

* O tipo de modelo é Prompt do LLM com Aprendizado dinâmico em contexto.
* A entrada do modelo são consultas de linguagem natural do usuário.
* O modelo gera consultas SQL na sintaxe [!DNL Snowflake], que são executadas pelo Gráfico de conhecimento Experience Platform.

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

## Treinamento de modelo {#model-training}

* [!DNL NL2SQL] usou [!DNL OpenAI] modelos baseados em GPT para aprendizado em contexto.
* O banco de perguntas [!DNL NL2SQL] contém 428 consultas da equipe [!DNL Operational Insights] e 524 de equipes externas para casos de uso alfa.

## Avaliação do modelo {#model-evaluation}

* O modelo é avaliado usando a precisão. Por exemplo, de todas as [!DNL NL2SQL] solicitações, quantas produzem os resultados SQL corretos.
* O processo de avaliação é uma combinação de correspondência baseada em regras (padronização de SQL e, em seguida, correspondência direta de sequência de SQL), solucionador de SQL baseado em LLM e avaliação humana
* Os conjuntos abertos são usados para testes de regressão e os projetos de anotação semanal monitoram o desempenho do modelo por meio de amostragem de tráfego real do cliente.
* Em termos de avaliação contraditória, há um modelo separado dentro e fora do escopo que funciona como uma garantia para [!DNL NL2SQL].

## Implantação do modelo {#model-deployment}

* O modelo LLM é um modelo baseado em GPT hospedado por [!DNL Azure OpenAI] APIs.
* O modelo base está hospedado por [!DNL Azure].
* O modelo é atualizado regularmente, em uma base semanal, através da expansão do banco de perguntas. A lista de modos também é atualizada por meio de novas estratégias de solicitação e instruções, quando necessário.

## Explicabilidade {#explainability}

O modelo usa um modelo de explicação separado para SQL.

## Equidade e viés {#fairness-and-bias}

* Para garantir que o modelo interprete e gere consultas de maneira consistente em diferentes intenções de usuários e variações linguísticas sem introduzir preconceitos ou reforçar estereótipos, o Adobe usa auditoria imediata, explicabilidade e salvaguardas contra geração de resultados tendenciosos ou não éticos.
* A saída do modelo é afetada pelos exemplos de aprendizagem em contexto e pelo que o recuperador seleciona no prompt. Os exemplos de bancos de perguntas contêm exemplos considerados representativos da perspectiva do PM, e também estamos expandindo os bancos de perguntas com base no tráfego real de clientes.

## Robustez {#robustness}

Como a maioria das consultas que recebe não é coberta pelo banco de perguntas, a precisão do tráfego de produção reflete a robustez do modelo.

## Considerações de privacidade e segurança {#privacy-and-security-considerations}

O modelo não processa nem retém informações de identificação pessoal (PII), e essas informações são mascaradas para a geração de SQL. Para a verificação de permissão de controle de acesso baseado em atributos, o SQL gerado será processado ainda mais pela equipe do Gráfico de conhecimento Experience Platform para garantir a qualidade da governança.

## Considerações éticas {#ethical-considerations}

Para evitar a exposição de PII ou atributos confidenciais, o modelo foi projetado para oferecer suporte à privacidade, evitar o reforço de vieses de dados existentes e respeitar os limites de controle de acesso. Isso inclui filtragem, marcação e auditoria de campos de esquema para uso responsável.

