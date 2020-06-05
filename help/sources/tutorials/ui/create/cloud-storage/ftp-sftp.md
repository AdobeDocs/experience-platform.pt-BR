---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem FTP ou SFTP na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 46b57900d9323cffeb59a0a6250bf5a9f4ac64ab
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 1%

---


# Criar um conector de origem FTP ou SFTP na interface do usuário

>[!NOTE]
>Os conectores FTP e SFTP estão em beta. Os recursos e a documentação estão sujeitos a alterações.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para criar um conector de origem FTP ou SFTP usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão FTP ou SFTP válida, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não suportados

A plataforma Experience suporta os seguintes formatos de arquivo para serem assimilados de fontes externas:

* Valores separados por delimitador (DSV): Atualmente, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgula (CSV). O valor dos cabeçalhos de campo nos arquivos formatados em DSV deve consistir apenas em caracteres alfanuméricos e sublinhados. O suporte para DSV geral será fornecido no futuro.
* JSON (JavaScript Object Notation): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
* Parqueta Apache: Os arquivos de dados formatados do parâmetro devem ser compatíveis com XDM.

### Reunir credenciais obrigatórias

Para acessar seu servidor FTP ou SFTP na plataforma, você deve fornecer o nome **do** host do servidor, um nome **de** usuário e uma **senha**.

## Conecte-se ao seu servidor FTP ou SFTP

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conta FTP ou SFTP para se conectar à plataforma.

Faça logon na [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes nas quais você pode criar uma conta de entrada e cada fonte mostra o número de contas e fluxos de dados existentes associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *[!UICONTROL Bancos]* de dados, selecione clique em **[!UICONTROL SFTP]** **no ícone + (+)** para criar um novo conector FTP ou SFTP.

![catálogo](../../../../images/tutorials/create/sftp/catalog.png)

A página *[!UICONTROL Conectar-se ao SFTP]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais FTP ou SFTP. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/sftp/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta FTP ou SFTP com a qual você deseja se conectar e selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/sftp/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta FTP ou SFTP. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para a Plataforma](../../dataflow/batch/cloud-storage.md).