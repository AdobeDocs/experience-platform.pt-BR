---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem Phoenix na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Criar um conector de origem Phoenix na interface do usuário

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem Phoenix usando a interface de usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão Phoenix válida, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md)

### Reunir credenciais obrigatórias

Para acessar sua conta Phoenix na Platform, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou nome do host do servidor Phoenix. |
| `port` | A porta TCP que o servidor Phoenix usa para escutar as conexões do cliente. Se você se conectar ao Azure HDInsights, especifique a porta como 443. |
| `httpPath` | O URL parcial correspondente ao servidor Phoenix. Especifique /hbasephonix0 se estiver a utilizar o cluster Azure HDInsights. |
| `username` | O nome de usuário que você usa para acessar o servidor Phoenix. |
| `password` | A senha que corresponde ao usuário. |
| `enableSsl` | Uma alternância que especifica se as conexões com o servidor são criptografadas usando SSL. |

Para obter mais informações sobre como começar, consulte [este documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html)Phoenix.

## Conecte sua conta Phoenix

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conta Phoenix para se conectar à Platform.

Faça logon na <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **Fontes** na barra de navegação esquerda para acessar a área de trabalho *Fontes* . A tela *Catálogo* exibe várias fontes para as quais você pode criar uma conta de entrada, e cada fonte mostra o número de contas e fluxos de conjunto de dados existentes associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *Bancos* de dados, selecione **Phoenix** para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar à fonte ou à sua documentação de visualização. Para criar uma nova conexão de entrada, selecione Origem **do** Connect.

![catálogo](../../../../images/tutorials/create/phoenix/catalog.png)

A página *Conectar-se a Phoenix* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **Nova conta**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais Phoenix. Quando terminar, selecione **Connect** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/phoenix/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta Phoenix com a qual você deseja se conectar e, em seguida, selecione **Avançar** para continuar.

![existente](../../../../images/tutorials/create/phoenix/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta Phoenix. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Plataforma](../../dataflow/databases.md).