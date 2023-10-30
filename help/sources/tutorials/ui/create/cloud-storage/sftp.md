---
title: Criar uma conexão de origem SFTP na interface
description: Saiba como criar uma conexão de origem SFTP usando a interface do usuário do Adobe Experience Platform.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: f6d1cc811378f2f37968bf0a42b428249e52efd8
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Criar um [!DNL SFTP] conexão de origem na interface

Este tutorial fornece etapas para criar um [!DNL SFTP] conexão de origem usando a interface do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

>[!IMPORTANT]
>
>É recomendável evitar novas linhas ou retornos de carro ao assimilar objetos JSON com um [!DNL SFTP] conexão de origem. Para contornar a limitação, use um único objeto JSON por linha e use várias linhas para os arquivos subsequentes.

Se você já tiver um [!DNL SFTP] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Coletar credenciais necessárias

Para se conectar a [!DNL SFTP], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado à [!DNL SFTP] servidor. |
| `port` | A variável [!DNL SFTP] porta do servidor à qual você está se conectando. Se não fornecido, o valor padrão será `22`. |
| `username` | O nome de usuário com acesso ao seu [!DNL SFTP] servidor. |
| `password` | A senha do [!DNL SFTP] servidor. |
| `privateKeyContent` | O conteúdo da chave privada SSH codificada na Base64. O tipo de chave OpenSSH deve ser classificado como RSA ou DSA. |
| `passPhrase` | A senha para descriptografar a chave privada se o arquivo de chave ou o conteúdo da chave estiver protegido por uma senha. Se PrivateKeyContent estiver protegida por senha, esse parâmetro precisará ser usado com a senha de PrivateKeyContent como valor. |
| `maxConcurrentConnections` | Esse parâmetro permite especificar um limite máximo para o número de conexões simultâneas que a Platform criará ao se conectar ao servidor SFTP. Você deve definir esse valor como menor que o limite definido pelo SFTP. **Nota**: quando essa configuração estiver ativada para uma conta SFTP existente, ela afetará somente os fluxos de dados futuros, não os existentes. |
| Caminho da pasta | O caminho para a pasta à qual você deseja fornecer acesso. [!DNL SFTP] origem, você pode fornecer o caminho da pasta para especificar o acesso do usuário à subpasta de sua escolha. |

Depois de obter as credenciais necessárias, siga as etapas abaixo para criar uma nova [!DNL SFTP] para se conectar à Platform.

## Conecte-se ao seu [!DNL SFTP] server

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No [!UICONTROL armazenamento na nuvem] categoria, selecione **[!UICONTROL SFTP]** e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de origens de Experience Platform com a origem SFTP selecionada.](../../../../images/tutorials/create/sftp/catalog.png)

A variável **[!UICONTROL Conectar ao SFTP]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta FTP ou SFTP à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![Uma lista de contas SFTP existentes na interface do usuário do Experience Platform.](../../../../images/tutorials/create/sftp/existing.png)

### Nova conta

>[!TIP]
>
>* Depois de criado, não é possível alterar o tipo de autenticação de um [!DNL SFTP] conexão básica. Para alterar o tipo de autenticação, você deve criar uma nova conexão base.
>
>* O SFTP é compatível com uma chave OpenSSH do tipo RSA ou DSA. Verifique se o conteúdo do arquivo principal começa com `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termina com `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se o arquivo de chave privada for um arquivo no formato PPK, use a ferramenta PuTTY para converter do formato PPK para o formato OpenSSH.

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição opcional para o novo [!DNL SFTP] conta.

![A tela de nova conta para SFTP](../../../../images/tutorials/create/sftp/new.png)

A variável [!DNL SFTP] A fonte oferece suporte à autenticação básica e à autenticação por meio da chave pública SSH.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Para usar a autenticação básica, selecione **[!UICONTROL Senha]** e, em seguida, forneça os valores de host e porta para conexão, juntamente com seu nome de usuário e senha. Durante essa etapa, também é possível designar o caminho para a subpasta à qual você deseja fornecer acesso. Quando terminar, selecione **[!UICONTROL Conectar à origem]**.

![A tela de nova conta para a origem SFTP usando autenticação básica](../../../../images/tutorials/create/sftp/password.png)

>[!TAB Autenticação de chave pública SSH]

Para usar credenciais baseadas em chave pública SSH, selecione **[!UICONTROL Chave pública SSH]**  e, em seguida, forneça seus valores de host e porta, bem como sua combinação de conteúdo de chave privada e senha. Durante essa etapa, também é possível designar o caminho para a subpasta à qual você deseja fornecer acesso. Quando terminar, selecione **[!UICONTROL Conectar à origem]**.

![A nova tela de conta para a origem SFTP usando a chave pública SSH.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta SFTP. Agora você pode seguir para o próximo tutorial e [configure um fluxo de dados para trazer dados do armazenamento em nuvem para a Platform](../../dataflow/batch/cloud-storage.md).
