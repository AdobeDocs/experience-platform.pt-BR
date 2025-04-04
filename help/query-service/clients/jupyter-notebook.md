---
title: Conectar o Jupyter Notebook ao Serviço de consulta
description: Saiba como conectar o Jupyter Notebook ao Serviço de consulta da Adobe Experience Platform.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# Conectar [!DNL Jupyter Notebook] ao Serviço de consulta

Este documento aborda as etapas necessárias para conectar o [!DNL Jupyter Notebook] ao Serviço de Consulta da Adobe Experience Platform.

## Introdução

Este guia requer que você já tenha acesso a [!DNL Jupyter Notebook] e esteja familiarizado com sua interface. Para baixar [!DNL Jupyter Notebook] ou obter mais informações, consulte a [documentação [!DNL Jupyter Notebook] oficial](https://jupyter.org/).

Para adquirir as credenciais necessárias para conectar [!DNL Jupyter Notebook] ao Experience Platform, você deve ter acesso ao espaço de trabalho [!UICONTROL Consultas] na interface do usuário do Experience Platform. Entre em contato com o administrador da organização se você não tiver acesso ao espaço de trabalho [!UICONTROL Consultas].

>[!TIP]
>
>O [!DNL Anaconda Navigator] é uma interface gráfica de usuário (GUI) de desktop que fornece uma maneira mais fácil de instalar e iniciar programas comuns do [!DNL Python], como o [!DNL Jupyter Notebook]. Também ajuda a gerenciar pacotes, ambientes e canais sem usar comandos de linha de comando.
>Siga o processo de instalação guiada no site para [instalar a versão preferencial do aplicativo](https://docs.anaconda.com/anaconda/install/).
>Na tela inicial do Navegador Anaconda, selecione **[!DNL Jupyter Notebook]** na lista de aplicativos compatíveis para iniciar o programa.
>Encontre mais informações na [documentação oficial do Anaconda](https://docs.anaconda.com/anaconda/navigator/).

A documentação oficial do Jupyter fornece instruções para [executar o bloco de anotações a partir da interface de linha de comando](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI).

## Launch [!DNL Jupyter Notebook]

Após abrir um novo aplicativo Web [!DNL Jupyter Notebook], selecione a lista suspensa **[!DNL New]** na interface, seguida por **[!DNL Python 3]** para criar um novo Bloco de Anotações. O editor [!DNL Notebook] é exibido.

Na primeira linha do editor [!DNL Notebook], digite o seguinte valor: `pip install psycopg2-binary` e selecione **[!DNL Run]** na barra de comandos. Uma mensagem de sucesso é exibida abaixo da linha de entrada.

>[!IMPORTANT]
>
>Como parte desse processo para formar uma conexão, você deve selecionar **[!DNL Run]** para executar cada linha de código.

Em seguida, importe um adaptador de banco de dados [!DNL PostgreSQL] para [!DNL Python]. Insira o valor: `import psycopg2` e selecione **[!DNL Run]**. Não há mensagem de sucesso para este processo. Se não houver nenhuma mensagem de erro, continue para a próxima etapa.

Agora você deve fornecer suas credenciais do Adobe Experience Platform inserindo o valor: `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. As credenciais de conexão podem ser encontradas na seção [!UICONTROL Consultas], na guia [!UICONTROL Credenciais] da interface do usuário do Experience Platform. Consulte a documentação sobre como [encontrar as credenciais da organização](../ui/credentials.md) para obter instruções detalhadas.

O uso de credenciais sem expiração é recomendado ao usar clientes de terceiros para economizar o esforço de inserir seus detalhes repetidamente. Consulte a documentação para obter instruções sobre [como gerar e usar credenciais sem expiração](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Ao copiar credenciais da interface do usuário do Experience Platform, não há necessidade de formatação adicional das credenciais. Eles podem ser fornecidos em uma linha, com um único espaço entre as propriedades e os valores. As credenciais estão entre aspas e **não** separadas por vírgulas.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

Sua instância [!DNL Jupyter Notebook] agora está conectada ao Serviço de consulta.

## Exemplo de execução de consulta

Agora que você conectou o [!DNL Jupyter Notebook] ao Serviço de Consulta, é possível executar consultas em seus conjuntos de dados usando suas entradas [!DNL Notebook]. O exemplo a seguir usa uma consulta simples para demonstrar o processo.

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

Insira e execute a função `df.head()` para ver os resultados da consulta tabulada.

## Próximas etapas

Agora que você se conectou ao Serviço de Consulta, pode usar [!DNL Jupyter Notebook] para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o [guia de execução de consultas](../best-practices/writing-queries.md).
