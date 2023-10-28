---
title: Conecte-se ao Data Distiller a partir de um Jupyter Notebook
description: Saiba como se conectar ao Data Distiller a partir de um Jupyter Notebook.
source-git-commit: 60c5a624bfbe88329ab3e12962f129f03966ce77
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# Conecte-se ao Data Distiller a partir de um Jupyter Notebook

Para enriquecer seus pipelines de aprendizado de máquina com dados de experiência do cliente de alto valor, primeiro você deve se conectar ao Data Distiller em [!DNL Jupyter Notebooks]. Este documento aborda as etapas para se conectar ao Data Distiller a partir de um [!DNL Python] em seu ambiente de aprendizado de máquina.

## Introdução

Este guia pressupõe que você esteja familiarizado com o [!DNL Python] notebooks e ter acesso a um ambiente de notebook. O notebook pode ser hospedado em um ambiente de aprendizado de máquina baseado em nuvem ou localmente com [[!DNL Jupyter Notebook]](https://jupyter.org/).

### Obter credenciais de conexão {#obtain-credentials}

Para se conectar ao Data Distiller e outros serviços da Adobe Experience Platform, você precisa de uma credencial de API de Experience Platform. As credenciais da API podem ser criadas no  [Console do Adobe Developer](https://developer.adobe.com/console/home) por alguém com acesso de desenvolvedor ao Experience Platform. É recomendável criar uma credencial de API Oauth2 especificamente para workflows de ciência de dados e fazer com que um administrador de sistema de Adobe da sua organização atribua a credencial a uma função com permissões apropriadas.

Consulte [Autenticar e acessar APIs de Experience Platform](../../../landing/api-authentication.md) para obter instruções detalhadas sobre como criar uma credencial de API e obter as permissões necessárias.

As permissões recomendadas para ciência de dados incluem:

- Sandboxes que serão usadas para ciência de dados (geralmente `prod`)
- Modelagem de dados: [!UICONTROL Gerenciar esquemas]
- Gestão de dados: [!UICONTROL Gerenciar conjuntos de dados]
- Assimilação de dados: [!UICONTROL Exibir fontes]
- Destinos: [!UICONTROL Gerenciar e ativar destinos do conjunto de dados]
- Serviço de consulta: [!UICONTROL Gerenciar consultas]

Por padrão, uma função (e as credenciais da API atribuídas a essa função) são bloqueadas para acessar quaisquer dados rotulados. Sujeito às políticas de governança de dados da organização, um Administrador do sistema pode conceder à função acesso a determinados dados rotulados que sejam considerados apropriados para o uso da ciência de dados. Os clientes da Platform são responsáveis por gerenciar o acesso a rótulos e políticas adequadamente para cumprir com as normas e políticas organizacionais relevantes.

### Armazenar credenciais em um arquivo de configuração separado {#store-credentials}

Para manter sua credencial segura, é recomendável evitar gravar informações de credencial diretamente em seu código. Em vez disso, mantenha as informações de credencial em um arquivo de configuração separado e leia os valores necessários para se conectar ao Experience Platform e ao Data Distiller.

Como exemplo, você pode criar um arquivo chamado `config.ini` e incluir as seguintes informações (juntamente com quaisquer outras informações, como IDs de conjunto de dados, que seriam úteis para salvar entre sessões):

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

Em seu notebook, você pode ler as informações de credencial na memória usando o `configParser` pacote do padrão [!DNL Python] biblioteca:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)
```

Você pode fazer referência a valores de credencial em seu código da seguinte maneira:

```python
org_id = config.get('Credential', 'ims_org_id')
```

## Instalar biblioteca Python da AEP {#install-python-library}

[aepp](https://github.com/adobe/aepp/tree/main) é um código aberto gerenciado por Adobe [!DNL Python] biblioteca que fornece funções para conectar-se ao Data Distiller e enviar queries, como fazer solicitações a outros serviços Experience Platform. A variável `aepp` A biblioteca, por sua vez, depende do pacote de adaptador de banco de dados PostgreSQL  `psycopg2` para consultas interativas do Data Distiller. É possível se conectar ao Data Distiller e consultar conjuntos de dados de Experience Platform com o `psycopg2` sozinho, mas `aepp` O fornece maior comodidade e funcionalidade adicional para fazer solicitações a todos os serviços de API do Experience Platform.

Para instalar ou atualizar `aepp` e `psycopg2` em seu ambiente, você pode usar o `%pip` comando mágico no seu notebook:

```python
%pip install --upgrade aepp
%pip install --upgrade psycopg2-binary
```

Em seguida, você pode configurar as opções `aepp` com sua credencial usando o seguinte código:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)

# Configure aepp with your credentials
import aepp

aepp.configure(
  org_id=config.get('Credential', 'ims_org_id'),
  sandbox=config.get('Credential', 'sandbox_name'),
  client_id=config.get('Credential', 'client_id'), 
  secret=config.get('Credential', 'client_secret'),
  scopes=config.get('Credential', 'scopes'),
  tech_id=config.get('Credential', 'tech_acct_id')
)
```

## Criar uma conexão com o Data Distiller {#create-connection}

Uma vez `aepp` estiver configurado com suas credenciais, você poderá usar o seguinte código para criar uma conexão com o Data Distiller e iniciar uma sessão interativa da seguinte maneira:

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

Em seguida, você pode consultar os conjuntos de dados na sandbox do Experience Platform. Dada a ID de um conjunto de dados que você deseja consultar, você pode recuperar o nome da tabela correspondente do serviço de catálogo e executar consultas na tabela:

```python
table_name = 'ecommerce_events'
simple_query = f'''SELECT * FROM {table_name} LIMIT 5'''
dd_cursor.query(simple_query)
```

### Conecte-se a um único conjunto de dados para obter um desempenho de consulta mais rápido {#connect-to-single-dataset}

Por padrão, a conexão do Data Distiller se conecta a todos os conjuntos de dados na sandbox. Para consultas mais rápidas e uso reduzido de recursos, você pode se conectar a um conjunto de dados específico de interesse. Você pode fazer isso alterando a variável `dbname` no objeto de conexão do Data Distiller para `{sandbox}:{table_name}`:

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## Próximas etapas

Ao ler este documento, você aprendeu a se conectar ao Data Distiller a partir de uma [!DNL Python] em seu ambiente de aprendizado de máquina. A próxima etapa na criação de pipelines de recursos, do Experience Platform para alimentar modelos personalizados no ambiente de aprendizado de máquina, é criar pipelines de recursos [explorar e analisar seus conjuntos de dados](./exploratory-analysis.md).
