---
title: Conectar o notebook do Júpiter ao serviço de query
description: Saiba como conectar o Notebook Jupyter com o Serviço de query da Adobe Experience Platform.
source-git-commit: f910deca43ac49d3a3452b8dbafda20ffdf3bf48
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Connect [!DNL Jupyter Notebook] para Serviço de Consulta

Este documento aborda as etapas necessárias para se conectar [!DNL Jupyter Notebook] com o Adobe Experience Platform Query Service.

## Introdução

Este guia requer que você já tenha acesso ao [!DNL Jupyter Notebook] e estão familiarizados com a sua interface. Para baixar [!DNL Jupyter Notebook] ou para obter mais informações, consulte a [funcionário [!DNL Jupyter Notebook] documentação](https://jupyter.org/).

Para adquirir as credenciais necessárias para conexão [!DNL Jupyter Notebook] para o Experience Platform, você deve ter acesso ao [!UICONTROL Queries] na interface do usuário da plataforma. Entre em contato com o administrador da organização caso não tenha acesso ao [!UICONTROL Queries] espaço de trabalho.

>[!TIP]
>
>[!DNL Anaconda Navigator] é uma interface gráfica do usuário (GUI) do desktop que fornece uma maneira mais fácil de instalar e iniciar o [!DNL Python] programas como [!DNL Jupyter Notebook]. Também ajuda a gerenciar pacotes, ambientes e canais sem usar comandos de linha de comando.
>Você pode [instale sua versão preferencial do aplicativo](https://docs.anaconda.com/anaconda/install/) do seu site.
>Siga o processo de instalação guiada. Na tela inicial do Navegador Anaconda, selecione **[!DNL Jupyter Notebook]** da lista de aplicativos compatíveis para iniciar o programa.
>![O [!DNL Anaconda Navigator] tela inicial com [!DNL Jupyter Notebook] destacado.](../images/clients/jupyter-notebook/anaconda-navigator-home.png)
>Mais informações podem ser encontradas em [documentação oficial](https://docs.anaconda.com/anaconda/navigator/).

## Launch [!DNL Jupyter Notebook]

Após ter aberto um novo [!DNL Jupyter Notebook] aplicação web, selecione o **[!DNL New]** lista suspensa seguida de **[!DNL Python 3]** para criar um novo Bloco de Notas. O [!DNL Notebook] é exibido.

![O [!DNL Jupiter Notebook] Guia Arquivo com o [!DNL New dropdown] e [!DNL Python] 3 destacado.](../images/clients/jupyter-notebook/new-notebook.png)

Na primeira linha do [!DNL Notebook] , insira o seguinte valor: `pip install psycopg2-binary` e selecione **[!DNL Run]** na barra de comandos. Uma mensagem de sucesso é exibida abaixo da linha de entrada.

>[!IMPORTANT]
>
>Como parte desse processo para formar uma conexão, você deve selecionar **[!DNL Run]** para executar cada linha de código.

![O [!DNL Notebook] Interface do usuário com o comando instalar bibliotecas realçado.](../images/clients/jupyter-notebook/install-library.png)

Em seguida, importe um [!DNL PostgreSQL] adaptador de banco de dados para [!DNL Python]. Insira o valor: `import psycopg2`e selecione **[!DNL Run]**. Não há mensagem de sucesso para esse processo. Se não houver uma mensagem de erro, continue para a próxima etapa.

![O [!DNL Notebook] Interface do usuário com o código do driver do banco de dados de importação realçado.](../images/clients/jupyter-notebook/import-dbdriver.png)

Agora, você deve fornecer suas credenciais do Adobe Experience Platform inserindo o valor : `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Suas credenciais de conexão podem ser encontradas no [!UICONTROL Queries] na seção [!UICONTROL Credenciais] da interface do usuário da plataforma. Consulte a documentação sobre como [encontre suas credenciais da organização](../ui/credentials.md) para obter instruções detalhadas.

O uso de credenciais que não expiram é recomendado ao usar clientes de terceiros para salvar o esforço de inserir seus detalhes repetidamente. Consulte a documentação para obter instruções sobre [como gerar e usar credenciais que não estão expirando](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Ao copiar credenciais da interface do usuário da plataforma, verifique se não há formatação adicional das credenciais. Todos devem estar em uma linha, com um espaço único entre as propriedades e os valores. As credenciais são entre aspas e **not** separado por vírgulas.

![O [!DNL Notebook] Interface do usuário com as credenciais de conexão destacadas.](../images/clients/jupyter-notebook/provide-credentials.png)

Seu [!DNL Jupyter Notebook] A instância agora está conectada ao Serviço de query.

## Exemplo de execução de query

Agora que você se conectou [!DNL Jupyter Notebook] para o Serviço de query, você pode realizar consultas em seus conjuntos de dados usando seu [!DNL Notebook] entradas. O exemplo a seguir usa um query simples para demonstrar o processo.

Insira os seguintes valores:

```console
cur = conn.cursor()
cur.execute('''{YOUR_QUERY_HERE}''')
data = [r for r in cur]
```

Em seguida, chame o parâmetro (`data` no exemplo acima) para exibir os resultados da consulta em uma resposta não formatada.

![O [!DNL Notebook] Interface do usuário com comandos para retornar e exibir resultados SQL no Bloco de Notas.](../images/clients/jupyter-notebook/example-query.png)

Para formatar os resultados de uma maneira mais legível, use os seguintes comandos:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`

Esses comandos não geram uma mensagem de sucesso. Se não houver mensagem de erro, você poderá usar uma função para exibir os resultados da consulta SQL em um formato de tabela.

![Os comandos necessários para formatar os resultados SQL.](../images/clients/jupyter-notebook/format-results-commands.png)

Digite e execute o `df.head()` para ver os resultados da consulta tabularizada.

![Resultados tabularizados da consulta SQL no [!DNL Jupyter Notebook].](../images/clients/jupyter-notebook/format-results-output.png)

## Próximas etapas

Agora que você se conectou ao Serviço de query, é possível usar [!DNL Jupyter Notebook] para gravar queries. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
