---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conectar-se com o Power BI
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Conecte-se com o Power BI (PC)

Os usuários do PC podem instalar o Power BI em [https://powerbi.microsoft.com/en-us/desktop/](https://powerbi.microsoft.com/en-us/desktop/).

## Configurar o Power Bi

Depois de instalar o Power BI, é necessário configurar os componentes necessários para suportar o conector PostgreSQL. Siga estas etapas:

- Localizar e instalar `npgsql`, um pacote de driver .NET para PostgreSQL que é a maneira oficial para o PowerBI se conectar.

- Selecione v4.0.10 (as versões mais recentes resultam em um erro).

- Em &quot;Npgsql GAC Installation&quot; (Instalação GAC Npgsql) na tela Custom Setup (Configuração personalizada), selecione **Will be installed (Será instalado no disco rígido** local). Se o GAC não for instalado, o Power BI falhará mais tarde.

- Reinicie o Windows.

- Encontre a versão de avaliação do PowerBI Desktop.

## Conectar o Power BI ao serviço de Query

Depois de executar essas etapas preparatórias, você pode conectar o Power BI ao Serviço de Query:

- Abra o Power BI.

- Clique em **Obter dados** na faixa superior do menu.

- Escolha o banco de dados **** PostgreSQL e clique em **Connect**.

- Informe os valores para o Servidor e o Banco de Dados. **O servidor** é o host encontrado sob os detalhes da conexão. Para produção, adicione a porta `:80` ao final da string do host. **O banco de dados** pode ser &quot;todos&quot; ou um nome de tabela de conjunto de dados. (Experimente um dos conjuntos de dados derivados do CTAS.)

- Clique em Opções **** avançadas e desmarque **incluir colunas** de relacionamento. Não marque **Navegar usando hierarquia** completa.

- *(Opcional, mas recomendado quando &quot;todos&quot; são declarados para o banco de dados)* Insira uma instrução SQL.

>[!NOTE]
>
>Se uma instrução SQL não for fornecida, o Power BI pré-visualização todas as tabelas no banco de dados. Para dados hierárquicos, uma instrução SQL personalizada deve ser usada. Se o schema de tabela for simples, funcionará com ou sem uma instrução SQL personalizada. Tipos compostos ainda não são suportados pelo Power BI - para obter tipos primitivos de tipos compostos, será necessário gravar instruções SQL para derivá-los.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=11 AND _ACP_DAY=20 
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- Selecione o modo **DirectQuery** ou **Importar** . No modo **Importar** , os dados serão importados no Power BI. No modo **DirectQuery** , todos os query serão enviados para o Query Service para execução.

- Clique em **OK**. Agora, o Power BI se conecta ao Serviço de Query e produz uma pré-visualização se não houver erros. Há um problema conhecido com a Pré-visualização que renderiza colunas numéricas. Vá para a próxima etapa.

- Clique em **Carregar** para trazer o conjunto de dados para o Power BI.
