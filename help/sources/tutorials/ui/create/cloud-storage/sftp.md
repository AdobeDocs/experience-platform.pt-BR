---
keywords: Experience Platform;home;popular topics;SFTP;sftp
solution: Experience Platform
title: Criar uma conexão de origem SFTP na interface do usuário
topic: overview
type: Tutorial
description: Saiba como criar uma conexão de origem SFTP usando a interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---


# Criar uma conexão de origem SFTP na interface do usuário

>[!NOTE]
>
>O conector SFTP está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores marcados com beta.

Este tutorial fornece etapas para criar uma conexão de origem SFTP usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

>[!IMPORTANT]
>
>É recomendável evitar novas linhas ou retornos de carro ao assimilar objetos JSON com uma conexão de origem SFTP. Para contornar a limitação, use um único objeto JSON por linha e use várias linhas para arquivos subsequentes.

Se você já tiver uma conexão SFTP válida, poderá ignorar o restante desse documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Reunir credenciais obrigatórias

Para se conectar ao SFTP, é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado ao servidor SFTP. |
| `username` | O nome de usuário com acesso ao seu servidor SFTP. |
| `password` | A senha do servidor SFTP. |
| `privateKeyContent` | O conteúdo de chave privada SSH codificado em Base64. O formato SSH private key OpenSSH (RSA/DSA). |
| `passPhrase` | A senha ou senha para descriptografar a chave privada se o arquivo de chave ou o conteúdo de chave estiver protegido por uma senha. Se PrivateKeyContent for protegido por senha, esse parâmetro deverá ser usado com a senha de PrivateKeyContent como valor. |

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conta SFTP para se conectar à Plataforma.

## Conecte-se ao seu servidor SFTP

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catalog] exibe várias fontes com as quais você pode criar uma conta de entrada.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria [!UICONTROL armazenamento de nuvem], selecione **[!UICONTROL SFTP]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar uma nova conexão SFTP.

![catálogo](../../../../images/tutorials/create/sftp/catalog.png)

A página **[!UICONTROL Conectar-se ao SFTP]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

O conector SFTP fornece tipos de autenticação diferentes para acesso. Em **[!UICONTROL Autenticação de conta]** selecione **[!UICONTROL Senha]** para utilizar uma credencial baseada em senha.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

Como alternativa, você pode selecionar **[chave pública SSH]** e conectar sua conta SFTP usando uma combinação de [!UICONTROL conteúdo de chave privada] e [!UICONTROL Senha].

>[!IMPORTANT]
>
>O conector SFTP suporta uma chave RSA/DSA OpenSSH. Certifique-se de que seu conteúdo de arquivo principal seja start com `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`. Se o arquivo de chave privada for um arquivo no formato PPK, use a ferramenta PuTTY para converter do formato PPK para OpenSSH.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| Credencial | Descrição |
| ---------- | ----------- |
| Conteúdo da chave privada | Um conteúdo de chave privada SSH codificado em Base64. A chave privada SSH deve estar no formato OpenSSH. |
| Senha | Especifica a senha ou senha para descriptografar a chave privada se o arquivo de chave ou o conteúdo de chave estiver protegido por uma senha. Se PrivateKeyContent for protegido por senha, esse parâmetro deverá ser usado com a senha de PrivateKeyContent como valor. |

### Conta existente

Para conectar uma conta existente, selecione a conta FTP ou SFTP com a qual deseja se conectar e, em seguida, selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/sftp/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta FTP ou SFTP. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para a Plataforma](../../dataflow/batch/cloud-storage.md).