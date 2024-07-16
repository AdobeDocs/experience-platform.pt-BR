---
title: Criar uma conexão SFTP com o Source na interface
description: Saiba como criar uma conexão de origem SFTP usando a interface do usuário do Adobe Experience Platform.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: f6d1cc811378f2f37968bf0a42b428249e52efd8
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL SFTP] na interface

Este tutorial fornece etapas para criar uma conexão de origem do [!DNL SFTP] usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

>[!IMPORTANT]
>
>É recomendável evitar novas linhas ou retornos de carro ao assimilar objetos JSON com uma conexão de origem [!DNL SFTP]. Para contornar a limitação, use um único objeto JSON por linha e use várias linhas para os arquivos subsequentes.

Se você já tiver uma conexão [!DNL SFTP] válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Coletar credenciais necessárias

Para se conectar a [!DNL SFTP], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado ao servidor [!DNL SFTP]. |
| `port` | A porta do servidor [!DNL SFTP] à qual você está se conectando. Se não for fornecido, o valor padrão será `22`. |
| `username` | O nome de usuário com acesso ao servidor [!DNL SFTP]. |
| `password` | A senha do servidor [!DNL SFTP]. |
| `privateKeyContent` | O conteúdo da chave privada SSH codificada na Base64. O tipo de chave OpenSSH deve ser classificado como RSA ou DSA. |
| `passPhrase` | A senha para descriptografar a chave privada se o arquivo de chave ou o conteúdo da chave estiver protegido por uma senha. Se PrivateKeyContent estiver protegida por senha, esse parâmetro precisará ser usado com a senha de PrivateKeyContent como valor. |
| `maxConcurrentConnections` | Esse parâmetro permite especificar um limite máximo para o número de conexões simultâneas que a Platform criará ao se conectar ao servidor SFTP. Você deve definir esse valor como menor que o limite definido pelo SFTP. **Observação**: quando esta configuração é habilitada para uma conta SFTP existente, ela afeta apenas os fluxos de dados futuros, não os existentes. |
| Caminho da pasta | O caminho para a pasta à qual você deseja fornecer acesso. [!DNL SFTP] origem, você pode fornecer o caminho da pasta para especificar o acesso do usuário à subpasta de sua escolha. |

Depois de obter as credenciais necessárias, você poderá seguir as etapas abaixo para criar uma nova conta do [!DNL SFTP] para se conectar à Platform.

## Conectar ao servidor [!DNL SFTP]

Na interface da Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria [!UICONTROL Armazenamento na nuvem], selecione **[!UICONTROL SFTP]** e **[!UICONTROL Adicionar dados]**.

![O catálogo de origens de Experience Platform com a origem SFTP selecionada.](../../../../images/tutorials/create/sftp/catalog.png)

A página **[!UICONTROL Conectar-se ao SFTP]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta FTP ou SFTP com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![Uma lista de contas SFTP existentes na interface do usuário do Experience Platform.](../../../../images/tutorials/create/sftp/existing.png)

### Nova conta

>[!TIP]
>
>* Depois de criada, você não pode alterar o tipo de autenticação de uma conexão de base [!DNL SFTP]. Para alterar o tipo de autenticação, você deve criar uma nova conexão base.
>
>* O SFTP é compatível com uma chave OpenSSH do tipo RSA ou DSA. Verifique se o conteúdo do arquivo de chave começa com `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termina com `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se o arquivo de chave privada for um arquivo no formato PPK, use a ferramenta PuTTY para converter do formato PPK para o formato OpenSSH.

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição opcional para sua nova conta [!DNL SFTP].

![A tela da nova conta para o SFTP](../../../../images/tutorials/create/sftp/new.png)

A origem [!DNL SFTP] dá suporte à autenticação básica e à autenticação via chave pública SSH.

>[!BEGINTABS]

>[!TAB Autenticação básica]

Para usar a autenticação básica, selecione **[!UICONTROL Senha]** e forneça os valores de host e porta aos quais se conectar, junto com seu nome de usuário e senha. Durante essa etapa, também é possível designar o caminho para a subpasta à qual você deseja fornecer acesso. Quando terminar, selecione **[!UICONTROL Conectar à origem]**.

![A tela da nova conta para a origem SFTP usando a autenticação básica](../../../../images/tutorials/create/sftp/password.png)

>[!TAB Autenticação de chave pública SSH]

Para usar credenciais baseadas em chave pública SSH, selecione **[!UICONTROL Chave pública SSH]** e forneça o host e os valores de porta, bem como a combinação de conteúdo de chave privada e senha. Durante essa etapa, também é possível designar o caminho para a subpasta à qual você deseja fornecer acesso. Quando terminar, selecione **[!UICONTROL Conectar à origem]**.

![A tela da nova conta para a origem SFTP usando a chave pública SSH.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta SFTP. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para a Platform](../../dataflow/batch/cloud-storage.md).
