---
keywords: Experience Platform, home, tópicos populares, SFTP, sftp
solution: Experience Platform
title: Criar uma conexão de fonte SFTP na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem SFTP usando a interface do usuário do Adobe Experience Platform.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# Crie um [!DNL SFTP] conexão de origem na interface do usuário

Este tutorial fornece etapas para criar um [!DNL SFTP] conexão de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

>[!IMPORTANT]
>
>Recomenda-se evitar quebras de linha ou retornos de carro ao assimilar objetos JSON com um [!DNL SFTP] conexão de origem. Para contornar a limitação, use um único objeto JSON por linha e use várias linhas para os arquivos subsequentes.

Se você já tiver um [!DNL SFTP] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Obter credenciais necessárias

Para se conectar ao [!DNL SFTP], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O nome ou endereço IP associado à [!DNL SFTP] servidor. |
| `port` | O [!DNL SFTP] porta de servidor à qual você está se conectando. Se não for fornecido, o valor assumirá como padrão `22`. |
| `username` | O nome de usuário com acesso ao [!DNL SFTP] servidor. |
| `password` | A senha de seu [!DNL SFTP] servidor. |
| `privateKeyContent` | O conteúdo da chave privada SSH codificada em Base64. O tipo de chave OpenSSH deve ser classificado como RSA ou DSA. |
| `passPhrase` | A senha ou senha para descriptografar a chave privada se o arquivo da chave ou o conteúdo da chave estiver protegido por uma senha. Se PrivateKeyContent estiver protegido por senha, esse parâmetro precisará ser usado com a senha de PrivateKeyContent como valor. |
| `maxConcurrentConnections` | Esse parâmetro permite especificar um limite máximo para o número de conexões simultâneas que a Platform criará ao se conectar ao servidor SFTP. É necessário definir esse valor como sendo inferior ao limite definido pelo SFTP. **Observação**: Quando essa configuração é ativada para uma conta SFTP existente, ela só afeta os fluxos de dados futuros e não os fluxos de dados existentes. |

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para criar um novo [!DNL SFTP] para se conectar à Platform.

## Conecte-se ao seu [!DNL SFTP] server

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta de entrada.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em [!UICONTROL armazenamento na nuvem] categoria , selecione **[!UICONTROL SFTP]** e depois selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes de Experience Platform com a fonte SFTP selecionada.](../../../../images/tutorials/create/sftp/catalog.png)

O **[!UICONTROL Conectar-se ao SFTP]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para conectar uma conta existente, selecione a conta FTP ou SFTP com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![Uma lista de contas SFTP existentes na interface do usuário do Experience Platform.](../../../../images/tutorials/create/sftp/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição opcional para o novo [!DNL SFTP] conta.

![A nova tela de conta do SFTP](../../../../images/tutorials/create/sftp/new.png)

#### Autenticar usando senha

[!DNL SFTP] O suporta tipos de autenticação diferentes para acesso. Em **[!UICONTROL Autenticação da conta]** select **[!UICONTROL Senha]** e, em seguida, forneça os valores de host e porta para conexão, junto com seu nome de usuário e senha.

![A nova tela de conta da fonte SFTP usando autenticação básica](../../../../images/tutorials/create/sftp/password.png)

#### Autenticar usando chave pública SSH

Para usar credenciais baseadas em chave pública SSH, selecione **[!UICONTROL Chave pública SSH]**  e, em seguida, forneça seus valores de host e porta, bem como sua combinação de conteúdo de chave privada e senha.

>[!IMPORTANT]
>
>O SFTP suporta uma chave OpenSSH tipo RSA ou DSA. Certifique-se de que o conteúdo do arquivo principal comece com `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termina com `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se o arquivo de chave privada for um arquivo no formato PPK, use a ferramenta PuTTY para converter do formato PPK para OpenSSH.

![A nova tela de conta da fonte SFTP usando a chave pública SSH.](../../../../images/tutorials/create/sftp/ssh.png)

| Credencial | Descrição |
| ---------- | ----------- |
| Conteúdo da chave privada | O conteúdo da chave privada SSH codificada em Base64. O tipo de chave OpenSSH deve ser classificado como RSA ou DSA. |
| Senha | Especifica a senha ou senha para descriptografar a chave privada se o arquivo de chave ou o conteúdo de chave estiver protegido por uma senha. Se PrivateKeyContent estiver protegido por senha, esse parâmetro precisará ser usado com a senha de PrivateKeyContent como seu valor. |


## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta SFTP. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do armazenamento em nuvem para a Platform](../../dataflow/batch/cloud-storage.md).
