---
title: Gerenciar dados da plataforma usando Python e SQLAlchemy
description: Saiba como usar o SQLAlchemy para gerenciar dados da Platform usando o Python em vez do SQL.
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: 8644b78c947fd015f6a169c9440b8d1df71e5e17
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# Gerenciar dados da Plataforma usando [!DNL Python] e [!DNL SQLAlchemy]

Saiba como usar o SQLAlchemy para maior flexibilidade no gerenciamento de dados do Adobe Experience Platform. Para aqueles que não estão tão familiarizados com o SQL, o SQLAlchemy pode melhorar muito o tempo de desenvolvimento ao trabalhar com bancos de dados relacionais. Este documento fornece instruções e exemplos para conectar o [!DNL SQLAlchemy] ao Serviço de Consulta e começar a usar o Python para interagir com seus bancos de dados.

[!DNL SQLAlchemy] é um ORM (Object Relational Mapper) e uma biblioteca de códigos [!DNL Python] que pode transferir dados armazenados em um banco de dados SQL para objetos [!DNL Python]. Você pode executar operações CRUD em dados mantidos no data lake da Platform usando o código [!DNL Python]. Isso elimina a necessidade de gerenciar dados usando apenas o PSQL.

## Introdução

Para adquirir as credenciais necessárias para conectar [!DNL SQLAlchemy] ao Experience Platform, você deve ter acesso ao espaço de trabalho de Consultas na interface do usuário da Platform. Entre em contato com o administrador da organização se não tiver acesso ao espaço de trabalho de Consultas.

## [!DNL Query Service] credenciais {#credentials}

Para encontrar suas credenciais, faça logon na interface do usuário da Platform e selecione **[!UICONTROL Consultas]** na navegação à esquerda, seguido de **[!UICONTROL Credenciais]**. Para obter instruções completas sobre como encontrar suas credenciais de logon, leia o [guia de credenciais](../ui/credentials.md).

![A guia Credencial com credenciais expirando para o Serviço de Consulta foi realçada.](../images/use-cases/credentials.png)

Embora a porta 80 seja a porta recomendada para uma conexão com o Serviço de consulta, você também pode usar a porta 5432.

>[!IMPORTANT]
>
>Se você usar credenciais com expiração (como visto na imagem acima) para se conectar ao Serviço de consulta, a vida da sessão para sua conexão expirará após o período definido nas configurações de sua organização. Por padrão, esse período é de 24 horas. Consulte a documentação para saber como [conectar um cliente com credenciais sem expiração](../ui/credentials.md#non-expiring-credentials) ou como [alterar a vida da sessão para suas credenciais com expiração](../ui/credentials.md#expiring-credentials).

Depois de ter acesso às suas credenciais de QS, abra o editor [!DNL Python] de sua escolha.

### Armazenar credenciais em [!DNL Python] {#store-credentials}

No editor [!DNL Python], importe a biblioteca `urllib.parse.quote` e salve cada variável de credencial como um parâmetro. O módulo `urllib.parse` fornece uma interface padrão para dividir cadeias de caracteres de URL em componentes. A função de aspas substitui caracteres especiais na string do URL para tornar os dados seguros para uso como componentes do URL. Um exemplo do código necessário é visto abaixo:

>[!TIP]
>
>Use as aspas triplas de [!DNL Python] para inserir sua cadeia de caracteres de senha de várias linhas.

```python
from urllib.parse import quote

host = "<YOUR_HOST>"

port = "<YOUR_PORT>"

dbname = "<YOUR_DATABASE>"

user = "<YOUR_USERNAME>"

password = quote('''
<YOUR_PASSWORD>
''')
```

>[!NOTE]
>
>A senha fornecida para conectar [!DNL SQLAlchemy] ao Experience Platform irá expirar se você usar credenciais que estão expirando. Consulte a [seção de credenciais](#credentials) para obter mais informações.

### Criar uma instância de mecanismo [#create-engine]

Depois que as variáveis forem criadas, importe a função `create_engine` e crie uma cadeia de caracteres para compilar e formatar suas credenciais do Serviço de Consulta em SQLAlchemy. A função `create_engine` é então usada para construir uma instância de mecanismo.

>[!NOTE]
>
>`create_engine`retorna uma instância de um mecanismo. No entanto, ela não abre a conexão com o Serviço de consulta até que uma consulta seja chamada e exija uma conexão.

O SSL deve ser ativado ao acessar a Platform usando clientes de terceiros. Como parte do mecanismo, use o `connect_args` para inserir argumentos de palavra-chave adicionais. É recomendável definir o modo SSL como `require`. Consulte a [documentação sobre modos SSL](../clients/ssl-modes.md) para obter mais informações sobre valores aceitos.

O exemplo abaixo exibe o código [!DNL Python] necessário para inicializar um mecanismo e uma cadeia de conexão.

```python
from sqlalchemy import create_engine

db_string = "postgresql://{user}:{password}@{host}:{port}/{dbname}".format(
    user=user,
    password=password,
    host=host,
    port = port,
    dbname = dbname
)

engine = create_engine(db_string, connect_args={'sslmode':'require'})
```

>[!NOTE]
>
>A senha fornecida para conectar [!DNL SQLAlchemy] ao Experience Platform irá expirar se você usar credenciais que estão expirando. Consulte a [seção de credenciais](#credentials) para obter mais informações.

Agora você está pronto para consultar dados da Platform usando [!DNL Python]. O exemplo mostrado abaixo retorna uma matriz de nomes de tabela do Serviço de consulta.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
