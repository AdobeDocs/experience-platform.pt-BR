---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem do Armazenamento de Tabela do Azure na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 0a2247a9267d4da481b3f3a5dfddf45d49016e61
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# Criar um conector de origem do Armazenamento de Tabela do Azure na interface do usuário

>[!NOTE]
>O conector do Armazenamento de Tabela do Azure está em beta. Os recursos e a documentação estão sujeitos a alterações.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem do Armazenamento de Tabela do Azure (a seguir denominado &quot;ATS&quot;) usando a interface de usuário da Plataforma.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão ATS válida, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

Para acessar sua conta ATS na Plataforma, forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | Uma cadeia de conexão para se conectar à instância do Armazenamento de Tabela do Azure. A cadeia de conexão para conexão com a instância ATS. O padrão da string de conexão para ATS é `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Para obter mais informações sobre a introdução, consulte [este documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction)de Armazenamentos de Tabela do Azure.

## Conectar sua conta do Armazenamento de tabela do Azure

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conta ATS para se conectar à Plataforma.

Faça logon na <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **Fontes** na barra de navegação esquerda para acessar a área de trabalho *Fontes* . A tela *Catálogo* exibe várias fontes para as quais você pode criar uma conta de entrada, e cada fonte mostra o número de contas e fluxos de conjunto de dados existentes associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *Bancos* de Dados, selecione Armazenamento **de Tabela do** Azure para expor uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar à fonte ou à sua documentação de visualização. Para criar uma nova conexão de entrada, selecione Origem **do** Connect.

![catálogo](../../../../images/tutorials/create/ats/catalog.png)

A página *Conectar-se ao Armazenamento* de tabela do Azure é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **Nova conta**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais ATS. Quando terminar, selecione **Connect** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/ats/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta ATS à qual deseja se conectar e, em seguida, selecione **Avançar** para continuar.

![existente](../../../../images/tutorials/create/ats/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta ATS. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Plataforma](../../dataflow/databases.md).