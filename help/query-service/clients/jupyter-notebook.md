---
title: Conectar o Jupyter Notebook ao Serviço de consulta
description: Saiba como conectar o Jupyter Notebook ao Serviço de consulta da Adobe Experience Platform.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Conectar [!DNL Jupyter Notebook] para o Serviço de consulta

Este documento aborda as etapas necessárias para se conectar [!DNL Jupyter Notebook] com o Adobe Experience Platform Query Service.

## Introdução

Este guia requer que você já tenha acesso ao [!DNL Jupyter Notebook] e estão familiarizados com sua interface. Para baixar [!DNL Jupyter Notebook] ou para obter mais informações, consulte a seção [oficial [!DNL Jupyter Notebook] documentação](https://jupyter.org/).

Para adquirir as credenciais necessárias para conexão [!DNL Jupyter Notebook] para Experience Platform, você deve ter acesso à [!UICONTROL Consultas] espaço de trabalho na interface do usuário da Platform. Entre em contato com o administrador da organização se você não tiver acesso à [!UICONTROL Consultas] espaço de trabalho.

>[!TIP]
>
>[!DNL Anaconda Navigator] O é uma interface gráfica do usuário (GUI) do desktop que oferece uma maneira mais fácil de instalar e iniciar o Common [!DNL Python] programas como [!DNL Jupyter Notebook]. Também ajuda a gerenciar pacotes, ambientes e canais sem usar comandos de linha de comando.
>Siga o processo de instalação guiada em seu site para [instale a versão preferida do aplicativo](https://docs.anaconda.com/anaconda/install/).
>Na tela inicial do Navegador Anaconda, selecione **[!DNL Jupyter Notebook]** na lista de aplicativos compatíveis para iniciar o programa.
>Mais informações podem ser encontradas no [documentação oficial do Anaconda](https://docs.anaconda.com/anaconda/navigator/).

A documentação oficial do Jupyter fornece instruções para [executar o bloco de anotações na interface de linha de comando](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI).

## Launch [!DNL Jupyter Notebook]

Depois de abrir um novo [!DNL Jupyter Notebook] aplicativo web, selecione a variável **[!DNL New]** lista suspensa da interface do usuário, seguida por **[!DNL Python 3]** para criar um novo Notebook. A variável [!DNL Notebook] editor é exibido.

Na primeira linha do [!DNL Notebook] insira o seguinte valor: `pip install psycopg2-binary` e selecione **[!DNL Run]** na barra de comandos. Uma mensagem de sucesso é exibida abaixo da linha de entrada.

>[!IMPORTANT]
>
>Como parte desse processo para formar uma conexão, você deve selecionar **[!DNL Run]** para executar cada linha de código.

Em seguida, importe um [!DNL PostgreSQL] adaptador de banco de dados para [!DNL Python]. Insira o valor: `import psycopg2`e selecione **[!DNL Run]**. Não há mensagem de sucesso para este processo. Se não houver nenhuma mensagem de erro, continue para a próxima etapa.

Agora você deve fornecer suas credenciais do Adobe Experience Platform inserindo o valor: `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. As credenciais de conexão podem ser encontradas no [!UICONTROL Consultas] seção, sob o [!UICONTROL Credenciais] da interface do usuário da Platform. Consulte a documentação sobre como [encontrar as credenciais da organização](../ui/credentials.md) para obter instruções detalhadas.

O uso de credenciais sem expiração é recomendado ao usar clientes de terceiros para economizar o esforço de inserir seus detalhes repetidamente. Consulte a documentação para obter instruções sobre [como gerar e usar credenciais sem expiração](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Ao copiar credenciais da interface do Platform, não há necessidade de formatação adicional das credenciais. Eles podem ser fornecidos em uma linha, com um único espaço entre as propriedades e os valores. As credenciais estão entre aspas e **não** separado por vírgulas.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

Seu [!DNL Jupyter Notebook] A instância do agora está conectada ao Serviço de consulta.

## Exemplo de execução de consulta

Agora que você se conectou [!DNL Jupyter Notebook] para o Serviço de consulta, é possível executar consultas em seus conjuntos de dados usando o [!DNL Notebook] entradas. O exemplo a seguir usa uma consulta simples para demonstrar o processo.

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

Esses comandos não geram uma mensagem de sucesso. Se não houver mensagem de erro, você poderá usar uma função para produzir os resultados da sua consulta SQL em formato de tabela.

Insira e execute o `df.head()` para ver os resultados da consulta tabulada.

## Próximas etapas

Agora que você se conectou ao Serviço de consulta, é possível usar [!DNL Jupyter Notebook] para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
