---
title: Criar uma conexão SFTP com o Source na interface
description: Saiba como criar uma conexão de origem SFTP usando a interface do usuário do Adobe Experience Platform.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: 4816a6b627dc6551e351bfe3cdc4bc8c8ea8b17e
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL SFTP] na interface

Este tutorial fornece etapas para criar uma conexão de origem do [!DNL SFTP] usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

>[!IMPORTANT]
>
>É recomendável evitar novas linhas ou retornos de carro ao assimilar objetos JSON com uma conexão de origem [!DNL SFTP]. Para contornar a limitação, use um único objeto JSON por linha e use várias linhas para os arquivos subsequentes.

Se você já tiver uma conexão [!DNL SFTP] válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Coletar credenciais necessárias

Leia o [[!DNL SFTP] guia de autenticação](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials) para obter etapas detalhadas sobre como recuperar suas credenciais de autenticação.

## Conectar ao servidor [!DNL SFTP]

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria [!UICONTROL Armazenamento na nuvem], selecione **[!UICONTROL SFTP]** e **[!UICONTROL Adicionar dados]**.

![O catálogo de origens da Experience Platform com a origem SFTP selecionada.](../../../../images/tutorials/create/sftp/catalog.png)

A página **[!UICONTROL Conectar-se ao SFTP]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta FTP ou SFTP com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![Uma lista de contas SFTP existentes na interface do usuário do Experience Platform.](../../../../images/tutorials/create/sftp/existing.png)

### Nova conta

>[!TIP]
>
>* Depois de criada, você não pode alterar o tipo de autenticação de uma conexão de base [!DNL SFTP]. Para alterar o tipo de autenticação, você deve criar uma nova conexão base.
>
>* O SFTP dá suporte para a chave OpenSSH do tipo `ed25519`, `RSA` ou `DSA`. Verifique se o conteúdo do arquivo de chave começa com `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termina com `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se o arquivo de chave privada for um arquivo no formato PPK, use a ferramenta PuTTY para converter do formato PPK para o formato OpenSSH.

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição opcional para sua nova conta [!DNL SFTP].

![A tela da nova conta para o SFTP](../../../../images/tutorials/create/sftp/new.png)

A origem [!DNL SFTP] dá suporte à autenticação básica e à autenticação via chave pública SSH.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Para usar a autenticação básica, selecione **[!UICONTROL Senha]** e forneça os valores apropriados para as seguintes credenciais:

* host
* porta
* nome de usuário
* senha

Durante esta etapa, você também pode configurar o máximo de conexões simultâneas, definir o caminho da pasta e habilitar ou desabilitar a divisão para o servidor [!DNL SFTP]. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde alguns momentos para estabelecer a conexão.

Para obter mais informações sobre autenticação, leia o manual sobre [coleta das credenciais necessárias para [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![A tela da nova conta para a origem SFTP usando a autenticação básica](../../../../images/tutorials/create/sftp/password.png)

>[!TAB Autenticação de chave pública SSH]

Para usar credenciais baseadas em chave pública SSH, selecione **[!UICONTROL Chave pública SSH]** e forneça os valores apropriados para as seguintes credenciais:

* host
* porta
* nome de usuário
* conteúdo da chave privada
* senha

Durante esta etapa, você também pode configurar o máximo de conexões simultâneas, definir o caminho da pasta e habilitar ou desabilitar a divisão para o servidor [!DNL SFTP]. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde alguns momentos para estabelecer a conexão.

Para obter mais informações sobre autenticação, leia o manual sobre [coleta das credenciais necessárias para [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![A tela da nova conta para a origem SFTP usando a chave pública SSH.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta SFTP. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para o Experience Platform](../../dataflow/batch/cloud-storage.md).
