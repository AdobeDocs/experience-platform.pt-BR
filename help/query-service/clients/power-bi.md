---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conectar-se ao Power BI
topic: connect
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# Conectar-se com [!DNL Power BI] (PC)

Os usuários do PC podem instalar [!DNL Power BI] em [https://powerbi.microsoft.com/en-us/desktop/](https://powerbi.microsoft.com/en-us/desktop/).

## Configurar [!DNL Power BI]

Depois de [!DNL Power BI] instalar, é necessário configurar os componentes necessários para suportar o conector PostgreSQL. Siga estas etapas:

- Localizar e instalar `npgsql`, um pacote de driver .NET para PostgreSQL que é a maneira oficial para o PowerBI se conectar.

- Selecione v4.0.10 (as versões mais recentes resultam em um erro).

- Em &quot;Npgsql GAC Installation&quot; (Instalação GAC Npgsql) na tela Custom Setup (Configuração personalizada), selecione **[!UICONTROL Will be installed (Será instalado no disco rígido]** local). A não instalação do GAC causará falha de Power BI posteriormente.

- Reinicie o Windows.

- Encontre a versão de avaliação da [!DNL PowerBI] área de trabalho.

## Conectar-se [!DNL Power BI] a [!DNL Query Service]

Depois de executar essas etapas preparatórias, você pode se conectar [!DNL Power BI] a [!DNL Query Service]:

- Abrir [!DNL Power BI].

- Clique em **[!UICONTROL Obter dados]** na faixa superior do menu.

- Escolha o banco de dados **** PostgreSQL e clique em **[!UICONTROL Connect]**.

- Informe os valores para o Servidor e o Banco de Dados. **[!UICONTROL O servidor]** é o host encontrado sob os detalhes da conexão. Para produção, adicione a porta `:80` ao final da string do host. **[!UICONTROL O banco de dados]** pode ser &quot;todos&quot; ou um nome de tabela de conjunto de dados. (Experimente um dos conjuntos de dados derivados do CTAS.)

- Clique em Opções **** avançadas e desmarque **[!UICONTROL incluir colunas]** de relacionamento. Não marque **[!UICONTROL Navegar usando hierarquia]** completa.

- *(Opcional, mas recomendado quando &quot;todos&quot; são declarados para o banco de dados)* Insira uma instrução SQL.

>[!NOTE]
>
>Se uma instrução SQL não for fornecida, então todas as tabelas [!DNL Power BI] serão pré-visualizações no banco de dados. Para dados hierárquicos, uma instrução SQL personalizada deve ser usada. Se o schema de tabela for simples, funcionará com ou sem uma instrução SQL personalizada. Tipos compostos ainda não são suportados por [!DNL Power BI] - para obter tipos primitivos de tipos compostos, será necessário gravar instruções SQL para derivá-los.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=11 AND _ACP_DAY=20 
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- Selecione o modo **[!UICONTROL DirectQuery]** ou **[!UICONTROL Importar]** . No modo **[!UICONTROL Importar]** , os dados serão importados no [!DNL Power BI]. No modo **[!UICONTROL DirectQuery]** , todos os query serão enviados para [!DNL Query Service] execução.

- Clique em **[!UICONTROL OK]**. Agora, [!DNL Power BI] conecta-se ao [!DNL Query Service] e produz uma pré-visualização se não houver erros. Há um problema conhecido com a Pré-visualização que renderiza colunas numéricas. Vá para a próxima etapa.

- Clique em **[!UICONTROL Carregar]** para inserir o conjunto de dados [!DNL Power BI].
