---
keywords: Experience Platform;home;popular topics;SFTP;FTP;ftp;sftp
solution: Experience Platform
title: Criar um conector de origem FTP ou SFTP na interface do usuário
topic: overview
type: Tutorial
description: Este tutorial fornece etapas para criar um conector de origem FTP ou SFTP usando a interface do usuário da plataforma.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---


# Criar um conector de origem FTP ou SFTP na interface do usuário

>[!NOTE]
>
>Os conectores FTP e SFTP estão em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para criar um conector de origem FTP ou SFTP usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão FTP ou SFTP válida, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não suportados

[!DNL Experience Platform] oferece suporte aos seguintes formatos de arquivo para serem assimilados de fontes externas:

* Valores separados por delimitador (DSV): Atualmente, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgula (CSV). O valor dos cabeçalhos de campo nos arquivos formatados em DSV deve consistir apenas em caracteres alfanuméricos e sublinhados. O suporte para DSV geral será fornecido no futuro.
* JSON (JavaScript Object Notation): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
* Parqueta Apache: Os arquivos de dados formatados do parâmetro devem ser compatíveis com XDM.

### Reunir credenciais obrigatórias

Para acessar seu servidor FTP ou SFTP em [!DNL Platform], você deve fornecer o nome do host do servidor, um nome de usuário e uma senha.

## Conecte-se ao seu servidor FTP ou SFTP

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conta FTP ou SFTP para se conectar [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta de entrada.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Bancos]** de dados, selecione **[!UICONTROL SFTP]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector FTP ou SFTP.

![catálogo](../../../../images/tutorials/create/sftp/catalog.png)

A página **[!UICONTROL Conectar-se ao SFTP]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

O conector SFTP fornece tipos de autenticação diferentes para acesso. Em Autenticação **[!UICONTROL de]** conta, selecione **[!UICONTROL Senha]** para usar uma credencial baseada em senha.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

Como alternativa, você pode selecionar chave **[pública SSH e conectar sua conta SFTP usando uma combinação de conteúdo]** de chave **[!UICONTROL privada e]** Senha ****.

>[!IMPORTANT]
>
>O conector SFTP suporta uma chave RSA/DSA OpenSSH. Certifique-se de que seu conteúdo de arquivo principal seja start com `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`. Se o arquivo de chave privada for um arquivo no formato PPK, use a ferramenta PuTTY para converter do formato PPK para OpenSSH.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| Credencial | Descrição |
| ---------- | ----------- |
| Conteúdo da chave privada | Um conteúdo de chave privada SSH codificado em Base64. A chave privada SSH deve estar no formato OpenSSH. |
| Senha | Especifica a senha ou senha para descriptografar a chave privada se o arquivo de chave ou o conteúdo de chave estiver protegido por uma senha. Se PrivateKeyContent for protegido por senha, esse parâmetro deverá ser usado com a senha de PrivateKeyContent como valor. |

### Conta existente

Para conectar uma conta existente, selecione a conta FTP ou SFTP com a qual você deseja se conectar e selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/sftp/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta FTP ou SFTP. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para [!DNL Platform]](../../dataflow/batch/cloud-storage.md)dentro.