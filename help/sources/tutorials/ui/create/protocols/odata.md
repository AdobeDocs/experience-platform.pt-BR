---
keywords: Experience Platform;página inicial;tópicos populares;OData;odata;Generic Open Data Protocol
solution: Experience Platform
title: Criar uma Conexão OData Source Genérica na Interface do Usuário
type: Tutorial
description: Saiba como criar uma conexão de origem de protocolo de dados abertos genérico usando a interface do usuário do Adobe Experience Platform.
exl-id: aad6b6f7-622c-4ab6-bf6d-1221fe1132d1
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 2%

---

# Criar uma conexão de origem [!DNL Generic OData] na interface

Os conectores do Source no Adobe Experience Platform fornecem a capacidade de assimilar dados obtidos externamente de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Generic Open Data Protocol] (a seguir denominado &quot;[!DNL OData]&quot;) usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL OData] válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/protocols.md)

### Coletar credenciais necessárias

Para acessar sua conta do [!DNL OData] em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | A URL raiz do serviço [!DNL OData]. |

Para obter mais informações sobre a introdução, consulte [este [!DNL OData] documento](https://www.odata.org/getting-started/basic-tutorial/).

## Conectar sua conta do [!DNL OData]

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL OData] ao [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Protocolos]**, selecione **[!UICONTROL OData genérico]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector [!DNL OData].

![catálogo](../../../../images/tutorials/create/odata/catalog.png)

A página **[!UICONTROL Conectar-se a OData Genérico]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça à conexão um nome, uma descrição opcional e suas credenciais do [!DNL OData]. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![conectar](../../../../images/tutorials/create/odata/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL OData] com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/odata/existing.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL OData]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados dos protocolos para o [!DNL Platform]](../../dataflow/protocols.md).
