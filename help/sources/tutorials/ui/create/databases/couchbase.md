---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem Couchbase na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: adb9c46e7337897e2336971e58ebc90b0e497ea0
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# Criar um conector de origem Couchbase na interface do usuário

> [!NOTE]
> O conector Couchbase está em beta. Os recursos e a documentação estão sujeitos a alterações.

Os conectores de origem fornecem [!DNL Adobe Experience Platform] a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem Couchbase usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do [!DNL Platform]:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida com o Couchbase, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

Para autenticar seu conector de origem Couchbase, é necessário fornecer valores para a seguinte propriedade de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A string de conexão usada para conectar-se à sua instância Couchbase. O padrão da string de conexão para Couchbase é `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Para obter mais informações sobre como adquirir uma string de conexão, consulte a documentação sobre a conexão com a [base de dados](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |

## Ligar a sua conta Couchbase

Depois de coletar as credenciais necessárias, siga as etapas abaixo para criar uma nova conta Couchbase para conexão [!DNL Platform].

Faça logon na [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes nas quais você pode criar uma conta de entrada e cada fonte mostra o número de contas e fluxos de conjunto de dados associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *[!UICONTROL Bancos]* de dados, selecione **[!UICONTROL Couchbase]** clique **no ícone + (+)** para criar um novo conector Couchbase.

![catálogo](../../../../images/tutorials/create/couchbase/catalog.png)

A página *[!UICONTROL Conectar-se ao Couchbase]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que é exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais de Couchbase. Quando terminar, selecione **[!UICONTROL Conectar-se à fonte]** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/couchbase/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta Couchbase à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Próximo]** no canto superior direito para prosseguir.

![existente](../../../../images/tutorials/create/couchbase/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta Couchbase. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Plataforma](../../dataflow/databases.md).