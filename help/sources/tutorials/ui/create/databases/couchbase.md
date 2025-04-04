---
keywords: Experience Platform;página inicial;tópicos populares;Couchbase;couchbase
solution: Experience Platform
title: Criar uma conexão Couchbase Source na interface
type: Tutorial
description: Saiba como criar uma conexão de origem Couchbase usando a interface do Adobe Experience Platform.
exl-id: 4270a48a-843c-4f1e-b280-35b620581d68
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Couchbase] na interface

>[!WARNING]
>
>A origem [!DNL Couchbase] será substituída no final de junho de 2025.

Os conectores do Source em [!DNL Adobe Experience Platform] fornecem a capacidade de assimilar dados obtidos externamente de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Couchbase] usando a interface do usuário [!DNL Experience Platform].

## Introdução

Este tutorial requer entendimento prático dos seguintes componentes do [!DNL Experience Platform]:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL Couchbase] válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

Para autenticar seu conector de origem [!DNL Couchbase], você deve fornecer valores para a seguinte propriedade de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão usada para se conectar à sua instância do [!DNL Couchbase]. O padrão da cadeia de conexão para [!DNL Couchbase] é `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Para obter mais informações sobre como adquirir uma cadeia de conexão, consulte a documentação em [[!DNL Couchbase] conexão](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |

## Conectar sua conta do [!DNL Couchbase]

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL Couchbase] ao [!DNL Experience Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Databases]**, selecione **[!UICONTROL Couchbase]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector [!DNL Couchbase].

![catálogo](../../../../images/tutorials/create/couchbase/catalog.png)

A página **[!UICONTROL Conectar-se à Couchbase]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e suas credenciais do [!DNL Couchbase]. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![conectar](../../../../images/tutorials/create/couchbase/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Couchbase] com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** no canto superior direito para continuar.

![existente](../../../../images/tutorials/create/couchbase/existing.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Couchbase]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o  [!DNL Experience Platform]](../../dataflow/databases.md).
