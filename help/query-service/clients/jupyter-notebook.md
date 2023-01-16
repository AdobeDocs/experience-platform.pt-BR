---
title: Conectar o notebook do Júpiter ao serviço de query
description: Saiba como conectar o Notebook Jupyter com o Serviço de query da Adobe Experience Platform.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '575'
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
>Siga o processo de instalação guiada em seu site para [instale sua versão preferencial do aplicativo](https://docs.anaconda.com/anaconda/install/).
>Na tela inicial do Navegador Anaconda, selecione **[!DNL Jupyter Notebook]** da lista de aplicativos compatíveis para iniciar o programa.
>Mais informações podem ser encontradas no [documentação oficial do Anaconda](https://docs.anaconda.com/anaconda/navigator/).

A documentação oficial do Júpiter fornece instruções para [executar o bloco de anotações a partir da interface da linha de comando](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI).

## Launch [!DNL Jupyter Notebook]

Após ter aberto um novo [!DNL Jupyter Notebook] aplicação web, selecione o **[!DNL New]** lista suspensa da interface do usuário, seguida por **[!DNL Python 3]** para criar um novo Bloco de Notas. O [!DNL Notebook] é exibido.

Na primeira linha do [!DNL Notebook] , insira o seguinte valor: `pip install psycopg2-binary` e selecione **[!DNL Run]** na barra de comandos. Uma mensagem de sucesso é exibida abaixo da linha de entrada.

>[!IMPORTANT]
>
>Como parte desse processo para formar uma conexão, você deve selecionar **[!DNL Run]** para executar cada linha de código.

Em seguida, importe um [!DNL PostgreSQL] adaptador de banco de dados para [!DNL Python]. Insira o valor: `import psycopg2`e selecione **[!DNL Run]**. Não há mensagem de sucesso para esse processo. Se não houver uma mensagem de erro, continue para a próxima etapa.

Agora, você deve fornecer suas credenciais do Adobe Experience Platform inserindo o valor : `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Suas credenciais de conexão podem ser encontradas no [!UICONTROL Queries] na seção [!UICONTROL Credenciais] da interface do usuário da plataforma. Consulte a documentação sobre como [encontre suas credenciais da organização](../ui/credentials.md) para obter instruções detalhadas.

O uso de credenciais que não expiram é recomendado ao usar clientes de terceiros para salvar o esforço de inserir seus detalhes repetidamente. Consulte a documentação para obter instruções sobre [como gerar e usar credenciais que não estão expirando](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Ao copiar credenciais da interface do usuário da plataforma, não há necessidade de formatação adicional das credenciais. Eles podem ser fornecidos em uma linha, com um único espaço entre as propriedades e os valores. As credenciais são entre aspas e **not** separado por vírgulas.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

Seu [!DNL Jupyter Notebook] A instância agora está conectada ao Serviço de query.

## Exemplo de execução de query

Agora que você se conectou [!DNL Jupyter Notebook] para o Serviço de query, você pode realizar consultas em seus conjuntos de dados usando seu [!DNL Notebook] entradas. O exemplo a seguir usa um query simples para demonstrar o processo.

Insira os seguintes valores:

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

Em seguida, chame o parâmetro (`data` no exemplo acima) para exibir os resultados da consulta em uma resposta não formatada.

Para formatar os resultados de uma maneira mais legível, use os seguintes comandos:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

Esses comandos não geram uma mensagem de sucesso. Se não houver mensagem de erro, você poderá usar uma função para exibir os resultados da consulta SQL em um formato de tabela.

Digite e execute o `df.head()` para ver os resultados da consulta tabularizada.

## Próximas etapas

Agora que você se conectou ao Serviço de query, é possível usar [!DNL Jupyter Notebook] para gravar queries. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
