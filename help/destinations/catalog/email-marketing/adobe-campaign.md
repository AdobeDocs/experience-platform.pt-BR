---
keywords: email; Email; email; destinos de email; adobe campaign; campanha
title: Conexão Adobe Campaign
description: O Adobe Campaign é um conjunto de soluções que ajudam você a personalizar e entregar campanhas em todos os seus canais online e offline.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 70be44e919070df910d618af4507b600ad51123c
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 0%

---

# Conexão Adobe Campaign

## Visão geral {#overview}

O Adobe Campaign é um conjunto de soluções que ajudam você a personalizar e entregar campanhas em todos os seus canais online e offline. Consulte [Introdução ao Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) para obter mais informações.

Para enviar dados de segmento ao Adobe Campaign, primeiro [conecte o destino](#connect-destination) no Adobe Experience Platform e, em seguida, [configure uma importação de dados](#import-data-into-campaign) do seu local de armazenamento para o Adobe Campaign.

## Tipo de exportação {#export-type}

**Baseado em perfil**  - você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na etapa  **[!UICONTROL Selecionar]** atributos do fluxo de trabalho de ativação de  [destino](../../ui/activate-destinations.md#select-attributes).

## LISTA DE PERMISSÕES do endereço IP {#allow-list}

Ao configurar destinos de marketing por email com o armazenamento SFTP, o Adobe recomenda adicionar determinados intervalos IP à lista de permissões.

Consulte [lista de permissões de endereço IP para destinos de armazenamento em nuvem](../cloud-storage/ip-address-allow-list.md) se precisar adicionar IPs Adobe à lista de permissões.

## Conectar destino {#connect-destination}

Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione Adobe Campaign e selecione **[!UICONTROL Configurar]**.

>[!NOTE]
>
>Se uma conexão com esse destino já existir, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre [!UICONTROL Ativate] e [!UICONTROL Configure], consulte a seção [Catalog](../../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino.

![Conexão com o Adobe Campaign](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

Na etapa **[!UICONTROL Account]** do fluxo de trabalho Connect destination , selecione o **[!UICONTROL Connection type]** para seu local de armazenamento. Para o Adobe Campaign, você pode selecionar entre **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP com senha]**, **[!UICONTROL SFTP com chave SSH]** e **[!UICONTROL Azure Blob]**. O método preferido para enviar dados para o Adobe Campaign é por meio de [!DNL Amazon S3] ou [!DNL Azure Blob]. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect]**.


![Configurar o assistente do Campaign](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- Para conexões **[!UICONTROL Amazon S3]**, você deve fornecer seu [!UICONTROL Access Key ID] e [!UICONTROL Secret Access Key].
- Para **[!UICONTROL SFTP com conexões de senha]**, você deve fornecer [!UICONTROL Domínio], [!UICONTROL Porta], [!UICONTROL Nome de usuário] e [!UICONTROL Senha].
- Para **[!UICONTROL SFTP com conexões de chave SSH]**, você deve fornecer [!UICONTROL Domínio], [!UICONTROL Porta], [!UICONTROL Nome de usuário] e [!UICONTROL Chave SSH].
- Para conexões **[!UICONTROL Azure Blob]**, você deve fornecer uma string de conexão.

Como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia com PGP/GPG aos arquivos exportados na seção **[!UICONTROL Key]**. Sua chave pública deve ser gravada como uma sequência de caracteres [!DNL Base64] codificada.

![Preencha as informações da campanha](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

Em **[!UICONTROL Autenticação da conta]**, preencha as informações relevantes para o seu destino, conforme mostrado abaixo:
- **[!UICONTROL Nome]**: Escolha um nome relevante para o seu destino.
- **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino.
- **[!UICONTROL Nome]** do bucket:  *Para conexões* S3. Insira o local do seu bucket S3, onde [!DNL Platform] depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
- **[!UICONTROL Caminho]** da pasta: Forneça o caminho no local de armazenamento, onde  [!DNL Platform] depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
- **[!UICONTROL Contêiner]**:  *Para conexões* Blob. O contêiner que contém o Blob em que seu caminho de pasta está.
- **[!UICONTROL Formato]** de arquivo:  **** CSVou  **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local de armazenamento.
- **[!UICONTROL Ações]** de marketing: As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a página [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md) .

![Informações básicas do Campaign](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

Selecione **[!UICONTROL Criar destino]** após preencher os campos acima. Seu destino agora está conectado e você pode [ativar segmentos](../../ui/activate-destinations.md) no destino.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos para um destino](../../ui/activate-destinations.md) para obter informações sobre o fluxo de trabalho de ativação de segmentos.

## Atributos de destino {#destination-attributes}

Quando [ativar segmentos](../../ui/activate-destinations.md) para o destino Adobe Campaign, o Adobe recomenda selecionar um identificador exclusivo no [esquema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que deseja exportar para o destino. Para obter mais informações, consulte [Selecionar quais campos de esquema usar como atributos de destino em seus arquivos exportados](./overview.md#destination-attributes).

## Dados exportados {#exported-data}

Para destinos [!DNL Adobe Campaign] , [!DNL Platform] cria um arquivo `.csv` delimitado por tabulação no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Destinos de marketing por email e destinos de armazenamento na nuvem](../../ui/activate-destinations.md#esp-and-cloud-storage) no tutorial de ativação de segmento.

## Configurar importação de dados no Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>- Lembre-se dos limites de armazenamento [!DNL SFTP], limites de armazenamento de banco de dados e limites de perfil ativos de acordo com seu contrato do Adobe Campaign ao executar essa integração.
>- Você precisa agendar, importar e mapear os segmentos exportados no Adobe Campaign usando [!DNL Campaign] workflows. Consulte [Configuração de uma importação recorrente](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) na documentação do Adobe Campaign Classic e [Sobre as atividades de gestão de dados](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) na documentação do Adobe Campaign Standard.
>- O método preferido para enviar dados para o Adobe Campaign é por meio de [!DNL Amazon S3] ou [!DNL Azure Blob].



Depois de conectar [!DNL Platform] ao armazenamento [!DNL Amazon S3] ou [!DNL Azure Blob], você deve configurar a importação de dados do local de armazenamento para o Adobe Campaign. Para saber como fazer isso, consulte as seguintes páginas de documentação do Adobe Campaign:
- [Introdução à importação e ](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html) exportação de dados e ao carregamento  [de dados (arquivo)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) na documentação do Adobe Campaign Classic.
- [Comece a usar processos e ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) gerenciamento de dados e  [carregue ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) arquivos na documentação do Adobe Campaign Standard.
