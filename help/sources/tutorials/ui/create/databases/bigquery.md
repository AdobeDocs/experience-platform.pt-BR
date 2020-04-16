---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem do Google Big Query na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Criar um conector de origem do Google Big Query na interface do usuário

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem do Google Big Query (a seguir denominado &quot;GBQ&quot;) usando a interface de usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão básica GBQ, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

Para acessar sua conta GBQ na Plataforma, forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `project` | A ID do projeto padrão do projeto BigQuery para o query. |
| `clientID` | O valor da ID usado para gerar o token de atualização. |
| `clientSecret` | O valor secreto usado para gerar o token de atualização. |
| `refreshToken` | O token de atualização obtido do Google usado para autorizar o acesso ao BigQuery. |

Para obter mais informações sobre esses valores, consulte [este documento](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)GBQ.

## Conecte sua conta GBQ

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conexão básica de entrada para vincular sua conta GBQ à Plataforma.

Faça logon na <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **Fontes** na barra de navegação esquerda para acessar a área de trabalho *Fontes* . A tela *Catálogo* exibe várias fontes com as quais você pode criar conexões base de entrada e cada fonte mostra o número de conexões base existentes associadas a elas.

Na categoria *Bancos* de dados, selecione **Google Big Query** para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar à fonte ou à sua documentação de visualização. Para criar uma nova conexão básica de entrada, selecione Origem **do** Connect.

![](../../../../images/tutorials/create/google-big-query/sources-catalog.png)

A página *Conectar-se ao Google Big Query* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **Nova conta**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais de GBQ à conexão básica. Quando terminar, selecione **Connect** e aguarde algum tempo para a nova conexão básica ser estabelecida.

![](../../../../images/tutorials/create/google-big-query/gbq-new-credentials.png)

### Conta existente

Para conectar uma conta existente, selecione a conta GBQ com a qual deseja se conectar e selecione **Avançar** para continuar.

![](../../../../images/tutorials/create/google-big-query/gbq-existing-credentials.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão básica com sua conta GBQ. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Plataforma](../../dataflow/databases.md).