---
title: Gerenciar dados da plataforma usando Python e SQLAlchemy
description: Saiba como usar o SQLAlchemy para gerenciar dados da Platform usando o Python em vez do SQL.
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: 8644b78c947fd015f6a169c9440b8d1df71e5e17
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Gerenciar dados da plataforma usando o [!DNL Python] e [!DNL SQLAlchemy]

Saiba como usar o SQLAlchemy para maior flexibilidade no gerenciamento de dados do Adobe Experience Platform. Para aqueles que não estão tão familiarizados com o SQL, o SQLAlchemy pode melhorar muito o tempo de desenvolvimento ao trabalhar com bancos de dados relacionais. Este documento fornece instruções e exemplos para conectar [!DNL SQLAlchemy] para o Serviço de consulta e começar a usar o Python para interagir com seus bancos de dados.

[!DNL SQLAlchemy] é um Mapeador Relacional de Objeto (ORM) e um [!DNL Python] que pode transferir dados armazenados em um banco de dados SQL para [!DNL Python] objetos. Em seguida, você pode executar operações CRUD em dados mantidos no data lake da Platform usando [!DNL Python] código. Isso elimina a necessidade de gerenciar dados usando apenas o PSQL.

## Introdução

Para adquirir as credenciais necessárias para conexão [!DNL SQLAlchemy] Para o Experience Platform, você deve ter acesso ao espaço de trabalho Consultas na interface do usuário da Platform. Entre em contato com o administrador da organização se não tiver acesso ao espaço de trabalho de Consultas.

## [!DNL Query Service] credenciais {#credentials}

Para encontrar suas credenciais, faça logon na interface do usuário da Platform e selecione **[!UICONTROL Consultas]** na navegação à esquerda, seguido por **[!UICONTROL Credenciais]**. Para obter instruções completas sobre como encontrar suas credenciais de logon, leia o [guia de credenciais](../ui/credentials.md).

![A guia Credencial com credenciais de expiração para o Serviço de consulta foi realçada.](../images/use-cases/credentials.png)

Embora a porta 80 seja a porta recomendada para uma conexão com o Serviço de consulta, você também pode usar a porta 5432.

>[!IMPORTANT]
>
>Se você usar credenciais com expiração (como visto na imagem acima) para se conectar ao Serviço de consulta, a vida da sessão para sua conexão expirará após o período definido nas configurações de sua organização. Por padrão, esse período é de 24 horas. Consulte a documentação para saber como [conectar um cliente com credenciais sem expiração](../ui/credentials.md#non-expiring-credentials)ou como [alterar a vida da sessão para suas credenciais que estão expirando](../ui/credentials.md#expiring-credentials).

Depois de ter acesso às credenciais de QS, abra o [!DNL Python] editor de escolha.

### Armazenar credenciais em [!DNL Python] {#store-credentials}

No seu [!DNL Python] editor, importe o `urllib.parse.quote` e salve cada variável de credencial como um parâmetro. A variável `urllib.parse` O módulo fornece uma interface padrão para dividir cadeias de caracteres de URL em componentes. A função de aspas substitui caracteres especiais na string do URL para tornar os dados seguros para uso como componentes do URL. Um exemplo do código necessário é visto abaixo:

>[!TIP]
>
>Uso [!DNL Python]aspas triplas para digitar sua cadeia de caracteres de senha de várias linhas.

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
>A senha fornecida para conexão [!DNL SQLAlchemy] para o Experience Platform expirará se você usar credenciais de expiração. Consulte a [seção credenciais](#credentials) para obter mais informações.

### Criar uma instância de mecanismo [#create-engine]

Depois que as variáveis forem criadas, importe o `create_engine` e criar uma string para compilar e formatar suas credenciais do Serviço de Consulta no SQLAlchemy. A variável `create_engine` é então usada para construir uma instância de mecanismo.

>[!NOTE]
>
>`create_engine`retorna uma instância de um mecanismo. No entanto, ela não abre a conexão com o Serviço de consulta até que uma consulta seja chamada e exija uma conexão.

O SSL deve ser ativado ao acessar a Platform usando clientes de terceiros. Como parte do mecanismo, use o `connect_args` para inserir argumentos adicionais de palavras-chave. É recomendável definir o modo SSL como `require`. Consulte a [Documentação de modos SSL](../clients/ssl-modes.md) para obter mais informações sobre valores aceitos.

O exemplo abaixo exibe a variável [!DNL Python] código necessário para inicializar um mecanismo e uma cadeia de conexão.

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
>A senha fornecida para conexão [!DNL SQLAlchemy] para o Experience Platform expirará se você usar credenciais de expiração. Consulte a [seção credenciais](#credentials) para obter mais informações.

Agora você está pronto para consultar dados da Platform usando [!DNL Python]. O exemplo mostrado abaixo retorna uma matriz de nomes de tabela do Serviço de consulta.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
