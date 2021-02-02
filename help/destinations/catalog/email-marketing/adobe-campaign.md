---
keywords: email;Email;email;email;email destinos;adobe campanha;campanha
title: Adobe Campaign
seo-title: Adobe Campaign
description: A Adobe Campaign é um conjunto de soluções que ajudam a personalizar e fornecer campanhas em todos os seus canais online e offline.
seo-description: A Adobe Campaign é um conjunto de soluções que ajudam a personalizar e fornecer campanhas em todos os seus canais online e offline.
translation-type: tm+mt
source-git-commit: cf2d76799c03a2ea0414aedd83b35f3ce2ca3cb5
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 1%

---


# Adobe Campaign

## Visão geral

A Adobe Campaign é um conjunto de soluções que ajudam a personalizar e fornecer campanhas em todos os seus canais online e offline. Consulte [Sobre o Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) para obter mais informações.

Para enviar dados de segmento para a Adobe Campaign, primeiro [conecte o destino](#connect-destination) no Adobe Experience Platform e, em seguida, [configure uma importação de dados](#import-data-into-campaign) do local do armazenamento para o Adobe Campaign.

## Tipo de exportação {#export-type}

**Baseado**  em perfis - você está exportando todos os membros de um segmento, juntamente com os campos de schema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela de atributos selecionados do fluxo de trabalho [ da ativação de ](../../ui/activate-destinations.md#select-attributes)destino.

## Destino do Connect {#connect-destination}

Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione Adobe Campaign e, em seguida, **[!UICONTROL Ligar destino]**.

![Conectar-se à adobe campanha](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

No fluxo de trabalho de destino do Connect, selecione **[!UICONTROL Tipo de conexão]** para o local do seu armazenamento. Para Adobe Campaign, você pode selecionar entre **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP com Senha]**, **[!UICONTROL SFTP com Chave SSH]** e **[!UICONTROL Blob do Azure]**. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Connect]**.

![Configurar o assistente de Campanhas](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- Para conexões **[!UICONTROL Amazon S3]**, você deve fornecer sua ID da chave de acesso e sua chave de acesso secreta.
- Para conexões **[!UICONTROL SFTP com Password]**, você deve fornecer Domínio, Porta, Nome de usuário e Senha.
- Para conexões **[!UICONTROL SFTP com chave SSH]**, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.
- Para conexões **[!UICONTROL Blob do Azure]**, você deve fornecer uma cadeia de conexão.

Opcionalmente, você pode anexar sua chave pública formatada pelo RSA para adicionar criptografia com PGP/GPG aos arquivos exportados na seção **[!UICONTROL Key]**. Observe que essa chave pública **deve** ser gravada como uma string codificada em Base64.

![Preencher informações de Campanha](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

Em **[!UICONTROL Informações básicas]**, preencha as informações relevantes para seu destino, como mostrado abaixo:
- **[!UICONTROL Nome]**: Escolha um nome relevante para o seu destino.
- **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino.
- **[!UICONTROL Nome]** do grupo:  *Para conexões* S3. Insira o local do bucket S3 no qual a Plataforma depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
- **[!UICONTROL Caminho]** da pasta: Forneça o caminho no local do armazenamento onde a Plataforma depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
- **[!UICONTROL Container]**:  *Para conexões* Blob. O container que armazena o Blob no caminho da sua pasta.
- **[!UICONTROL Formato]** de arquivo:  **** CSV ou  **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local do armazenamento.

![Informações básicas sobre campanhas](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

Clique em **[!UICONTROL Criar]** depois de preencher os campos acima. Seu destino agora está conectado e você pode [ativar segmentos](../../ui/activate-destinations.md) no destino.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](../../ui/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

## Atributos de destino {#destination-attributes}

Quando [ativar segmentos](../../ui/activate-destinations.md) no destino Adobe Campaign, recomendamos que você selecione um identificador exclusivo do seu [schema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecione quais campos de schema usar como atributos de destino em seus arquivos exportados](./overview.md#destination-attributes) na documentação de destinos de marketing de email.

## Dados exportados {#exported-data}

Para destinos [!DNL Adobe Campaign], a plataforma cria um arquivo `.txt` ou `.csv` delimitado por tabulação no local do armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Destinos de e-mail Marketing e destinos do armazenamento Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) no tutorial de ativação de segmentos.

## Configurar importação de dados para o Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>- Lembre-se dos limites do armazenamento SFTP, dos limites do armazenamento do banco de dados e dos limites ativos do perfil conforme o contrato da Adobe Campaign ao executar essa integração.
>- Você precisa agendar, importar e mapear seus segmentos exportados no Adobe Campaign usando workflows [!DNL Campaign]. Consulte [Configurar uma importação recorrente](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#automating-with-workflows) na documentação do Adobe Campaign.



Depois de conectar a Plataforma ao seu [!DNL Amazon S3] ou armazenamento SFTP, você deve configurar a importação de dados do local do armazenamento para o Adobe Campaign. Para saber como fazer isso, consulte [Importando dados](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) na documentação da Adobe Campaign.