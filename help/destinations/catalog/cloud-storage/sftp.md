---
keywords: SFTP; sftp
title: Conexão SFTP
description: Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: fa393b2bd8085a17653962b5a8b112a5db10df83
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 1%

---

# Conexão SFTP

## Visão geral {#overview}

Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Adobe Experience Platform.

>[!IMPORTANT]
>
> Embora o Adobe seja compatível com exportações de dados para servidores SFTP, os locais de armazenamento em nuvem recomendados para exportar dados são [!DNL Amazon S3] e [!DNL Azure Blob].

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Em lote]** | Destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Tipo de exportação com base em perfil SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Chave pública RSA"
>abstract="Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Sua chave pública deve ser escrita como uma sequência de caracteres codificada em Base64."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Chave SSH"
>abstract="A chave SSH requer uma string Base64."

When [conexão](../../ui/connect-destination.md) para esse destino, você deve fornecer as seguintes informações:

#### Informações de autenticação {#authentication-information}

Se você selecionar a variável **[!UICONTROL Autenticação básica]** digite para se conectar ao local do SFTP:

![Autenticação básica de destino SFTP](/help/destinations/assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Host]**: O endereço do local de armazenamento SFTP;
* **[!UICONTROL Nome do usuário]**: O nome de usuário para fazer logon no local de armazenamento SFTP;
* **[!UICONTROL Senha]**: A senha para fazer logon no local de armazenamento SFTP.
* **[!UICONTROL Chave de criptografia]**: Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Sua chave pública deve ser escrita como uma [!DNL Base64] sequência de caracteres codificada.


Se você selecionar a variável **[!UICONTROL SFTP com chave SSH]** tipo de autenticação para se conectar ao local SFTP:

![Autenticação de chave SSH de destino SFTP](/help/destinations/assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domínio]**: Preencha o endereço IP ou o nome de domínio de sua conta SFTP
* **[!UICONTROL Port]**: A porta usada pelo local de armazenamento SFTP;
* **[!UICONTROL Nome do usuário]**: O nome de usuário para fazer logon no local de armazenamento SFTP;
* **[!UICONTROL Chave SSH]**: A chave SSH para fazer logon no local de armazenamento SFTP.
* **[!UICONTROL Chave de criptografia]**: Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Sua chave pública deve ser escrita como uma [!DNL Base64] sequência de caracteres codificada.

#### Detalhes do destino {#destination-details}

Depois de estabelecer a conexão de autenticação com o local SFTP, forneça as seguintes informações para o destino:

![Detalhes de destino disponíveis para destino SFTP](/help/destinations/assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Nome]**: insira um nome que o ajudará a identificar esse destino na interface do usuário do Experience Platform;
* **[!UICONTROL Descrição]**: indicar uma descrição para este destino;
* **[!UICONTROL Caminho da pasta]**: insira o caminho para a pasta no local SFTP onde os arquivos serão exportados.

## Dados exportados {#exported-data}

Para [!DNL SFTP] destinos, a Platform cria uma `.csv` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) no tutorial de ativação de segmento.

## LISTA DE PERMISSÕES de endereço IP

Consulte [LISTA DE PERMISSÕES de endereço IP para destinos de armazenamento em nuvem](ip-address-allow-list.md) se você precisar adicionar IPs Adobe a uma lista de permissões.
