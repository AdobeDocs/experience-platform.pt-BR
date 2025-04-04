---
keywords: Experience Platform;página inicial;tópicos populares;FTP;ftp
solution: Experience Platform
title: Criar uma conexão FTP Source na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem FTP usando a interface do usuário do Adobe Experience Platform.
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---

# Criar uma conexão de origem FTP na interface

>[!NOTE]
>
>O conector FTP está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

Este tutorial fornece etapas para criar uma conexão de origem FTP usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão FTP válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Coletar credenciais necessárias

Para se conectar ao FTP, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado ao servidor FTP. |
| `username` | O nome de usuário com acesso ao servidor FTP. |
| `password` | A senha do servidor FTP. |

## Conectar-se ao servidor FTP

Depois de obter as credenciais necessárias, siga as etapas abaixo para criar uma nova conta FTP para se conectar ao Experience Platform.

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta de entrada.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria [!UICONTROL Armazenamento na nuvem], selecione **[!UICONTROL FTP]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar uma nova conexão FTP.

![catálogo](../../../../images/tutorials/create/ftp/catalog.png)

A página **[!UICONTROL Conectar ao FTP]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/ftp/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta FTP com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/ftp/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta FTP. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para o Experience Platform](../../dataflow/batch/cloud-storage.md).
