---
keywords: SFTP; sftp
title: Conexão SFTP
description: Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: cb0b80f79a849d81216c5500c54b62ac5d85e2f6
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# Conexão SFTP

## Log de alterações de destino {#changelog}

>[!IMPORTANT]
>
>Com a versão beta da funcionalidade de exportação de conjuntos de dados e a funcionalidade aprimorada de exportação de arquivos, agora é possível ver dois [!DNL SFTP] cartões no catálogo de destinos.
>* Se você já estiver exportando arquivos para o **[!UICONTROL SFTP]** destino: Crie novos fluxos de dados para o novo **[!UICONTROL beta SFTP]** destino.
>* Se você ainda não tiver criado nenhum fluxo de dados para a **[!UICONTROL SFTP]** destino, use o novo **[!UICONTROL beta SFTP]** cartão para exportar arquivos para **[!UICONTROL SFTP]**.


![Imagem dos dois cartões de destino SFTP em uma exibição lado a lado.](../../assets/catalog/cloud-storage/sftp/two-sftp-destination-cards.png)

Melhorias nas novas [!DNL SFTP] o cartão de destino inclui:

* [Suporte à exportação de conjuntos de dados](/help/destinations/ui/export-datasets.md).
* Adicional [opções de nomenclatura de arquivo](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Capacidade de definir cabeçalhos de arquivo personalizados em seus arquivos exportados por meio do [etapa de mapeamento aprimorada](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Capacidade de personalizar a formatação de arquivos de dados CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Visão geral {#overview}

Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Adobe Experience Platform.

>[!IMPORTANT]
>
> Embora o Experience Platform seja compatível com exportações de dados para servidores SFTP, os locais de armazenamento em nuvem recomendados para exportar dados são [!DNL Amazon S3] e [!DNL SFTP].

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Em lote]** | Destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Tipo de exportação com base em perfil SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

### Informações de autenticação {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Chave pública RSA"
>abstract="Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Veja um exemplo de uma chave corretamente formatada no link da documentação abaixo."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Chave SSH privada"
>abstract="A chave SSH privada deve ser formatada como uma cadeia de caracteres codificada em Base64 e não deve ser protegida por senha."

Se você selecionar a variável **[!UICONTROL Autenticação básica]** digite para se conectar ao local do SFTP:

![Autenticação básica de destino SFTP](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Host]**: O endereço do local de armazenamento SFTP;
* **[!UICONTROL Nome do usuário]**: O nome de usuário para fazer logon no local de armazenamento SFTP;
* **[!UICONTROL Senha]**: A senha para fazer logon no local de armazenamento SFTP.
* **[!UICONTROL Chave de criptografia]**: Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Exiba um exemplo de uma chave de criptografia corretamente formatada na imagem abaixo.

   ![Imagem que mostra um exemplo de uma chave PGP formatada corretamente na interface do usuário](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Se você selecionar a variável **[!UICONTROL SFTP com chave SSH]** tipo de autenticação para se conectar ao local SFTP:

![Autenticação de chave SSH de destino SFTP](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domínio]**: Preencha o endereço IP ou o nome de domínio de sua conta SFTP
* **[!UICONTROL Port]**: A porta usada pelo local de armazenamento SFTP;
* **[!UICONTROL Nome do usuário]**: O nome de usuário para fazer logon no local de armazenamento SFTP;
* **[!UICONTROL Chave SSH]**: A chave SSH privada usada para fazer logon no local de armazenamento SFTP. A chave privada deve ser formatada como uma cadeia de caracteres codificada em Base64 e não deve ser protegida por senha.
* **[!UICONTROL Chave de criptografia]**: Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Exiba um exemplo de uma chave de criptografia corretamente formatada na imagem abaixo.

   ![Imagem que mostra um exemplo de uma chave PGP formatada corretamente na interface do usuário](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Detalhes do destino {#destination-details}

Depois de estabelecer a conexão de autenticação com o local SFTP, forneça as seguintes informações para o destino:

![Detalhes de destino disponíveis para destino SFTP](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Nome]**: insira um nome que o ajudará a identificar esse destino na interface do usuário do Experience Platform;
* **[!UICONTROL Descrição]**: indicar uma descrição para este destino;
* **[!UICONTROL Caminho da pasta]**: insira o caminho para a pasta no local SFTP onde os arquivos serão exportados.
* **[!UICONTROL Tipo de arquivo]**: selecione o Experience Platform format que deve ser usado para os arquivos exportados. Essa opção só está disponível para a variável **[!UICONTROL beta SFTP]** destino. Ao selecionar o [!UICONTROL CSV] , você também pode [configurar as opções de formatação de arquivo](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato de compactação]**: selecione o tipo de compactação que o Experience Platform deve usar para os arquivos exportados. Essa opção só está disponível para a variável **[!UICONTROL beta SFTP]** destino.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## (Beta) Exportar conjuntos de dados {#export-datasets}

Esse destino é compatível com exportações de conjunto de dados. Para obter informações completas sobre como configurar exportações de conjunto de dados, leia a [tutorial exportar conjuntos de dados](/help/destinations/ui/export-datasets.md).

## Dados exportados {#exported-data}

Para [!DNL SFTP] destinos, a Platform cria uma `.csv` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) no tutorial de ativação de segmento.

## LISTA DE PERMISSÕES de endereço IP

Consulte [LISTA DE PERMISSÕES de endereço IP para destinos de armazenamento em nuvem](ip-address-allow-list.md) se você precisar adicionar IPs Adobe a uma lista de permissões.
