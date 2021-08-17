---
keywords: SFTP; sftp
title: Conexão SFTP
description: Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 8d1594aeb1d6671eec187643245d940ed3ff74cd
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Conexão SFTP

## Visão geral {#overview}

Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Adobe Experience Platform.

>[!IMPORTANT]
>
> Embora o Adobe seja compatível com exportações de dados para servidores SFTP, os locais de armazenamento em nuvem recomendados para exportar dados são [!DNL Amazon S3] e [!DNL Azure Blob].

## Tipo de exportação {#export-type}

**Baseado em perfil**  - você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos do fluxo de trabalho de ativação de  [destino](../../ui/activate-destinations.md#select-attributes).

![Tipo de exportação com base em perfil SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **Host**: O endereço do local de armazenamento SFTP
* **Nome de usuário**: O nome de usuário para fazer logon no local de armazenamento SFTP
* **Senha**: A senha para fazer logon no local de armazenamento SFTP
* **[!UICONTROL Nome]**: insira um nome que ajudará a identificar esse destino.
* **[!UICONTROL Descrição]**: insira uma descrição deste destino.
* **[!UICONTROL Caminho]** da pasta: insira o caminho para a pasta de destino que hospedará os arquivos exportados.

Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Sua chave pública deve ser gravada como uma sequência de caracteres [!DNL Base64] codificada.

## Dados exportados {#exported-data}

Para destinos [!DNL SFTP], a Platform cria um arquivo `.csv` delimitado por tabulação no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Destinos de marketing por email e destinos de armazenamento na nuvem](../../ui/activate-destinations.md#esp-and-cloud-storage) no tutorial de ativação de segmento.

## LISTA DE PERMISSÕES de endereço IP

Consulte [lista de permissões de endereço IP para destinos de armazenamento em nuvem](ip-address-allow-list.md) se precisar adicionar IPs Adobe a uma lista de permissões.
