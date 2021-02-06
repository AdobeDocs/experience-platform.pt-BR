---
keywords: email;email;email;email;destinos de email;oracle responsys destino
title: Destino da Conexão oracle Responsys
description: A Responsys é uma ferramenta de marketing por email empresarial para campanhas de marketing entre canais oferecida pela Oracle para personalizar interações entre email, dispositivos móveis, vídeos e redes sociais.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# [!DNL Oracle Responsys] conexão

[A ](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) Responsysis é uma ferramenta de marketing por email empresarial para campanhas de marketing entre canais, oferecida  [!DNL Oracle] para personalizar interações entre email, dispositivos móveis, vídeos e redes sociais.

Para enviar dados de segmento para [!DNL Oracle Responsys], primeiro [conecte-se ao destino](#connect-destination) no Adobe Experience Platform e, em seguida, [configure uma importação de dados](#import-data-into-responsys) do local do armazenamento para [!DNL Oracle Responsys].

## Tipo de exportação {#export-type}

**Baseado**  em perfis - você está exportando todos os membros de um segmento, juntamente com os campos de schema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela de atributos selecionados do fluxo de trabalho [ da ativação de ](../../ui/activate-destinations.md#select-attributes)destino.

## Destino do Connect {#connect-destination}

Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione [!DNL Oracle Responsys] e **[!UICONTROL Ligar destino]**.

![Conectar-se ao Responsys](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

Na etapa **[!UICONTROL Autenticação]**, se você tiver configurado anteriormente uma conexão com o destino do armazenamento na nuvem, selecione **[!UICONTROL Conta existente]** e selecione uma de suas conexões existentes. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão. Preencha as credenciais de autenticação da sua conta e selecione **[!UICONTROL Ligar ao destino]**. Para [!DNL Oracle Responsys], você pode selecionar entre **[!UICONTROL SFTP com Password]** e **[!UICONTROL SFTP com chave SSH]**. Preencha as informações abaixo, dependendo do tipo de conexão, e selecione **[!UICONTROL Conecte-se ao destino]**.

Para conexões **[!UICONTROL SFTP com Password]**, você deve fornecer Domínio, Porta, Nome de usuário e Senha.

Para conexões **[!UICONTROL SFTP com chave SSH]**, você deve fornecer Domínio, Porta, Nome de usuário e Chave SSH.

![Preencha as informações do Responsys](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

Na etapa **[!UICONTROL Setup]**, preencha as informações relevantes para seu destino, conforme mostrado abaixo:
- **[!UICONTROL Nome]**: Escolha um nome relevante para o seu destino.
- **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino.
- **[!UICONTROL Caminho]** da pasta: Forneça o caminho no local do armazenamento onde a Plataforma depositará seus dados de exportação como CSV ou arquivos delimitados por tabulação.
- **[!UICONTROL Formato]** de arquivo:  **** CSV ou  **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local do armazenamento.

![Informações básicas sobre a resposta](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

Clique em **[!UICONTROL Criar destino]** depois de preencher os campos acima. Seu destino agora está conectado e você pode [ativar segmentos](../../ui/activate-destinations.md) no destino.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](../../ui/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

## Atributos de destino {#destination-attributes}

Quando [ativar segmentos](../../ui/activate-destinations.md) no destino [!DNL Oracle Responsys], recomendamos que você selecione um identificador exclusivo do seu [schema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [Selecione quais campos de schema usar como atributos de destino em seus arquivos exportados](./overview.md#destination-attributes) em Destinos de marketing de email.

## Dados exportados {#exported-data}

Para destinos [!DNL Oracle Responsys], a plataforma cria um arquivo `.txt` ou `.csv` delimitado por tabulação no local do armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Destinos de e-mail Marketing e destinos do armazenamento Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) no tutorial de ativação de segmentos.

## Configurar importação de dados para [!DNL Oracle Responsys] {#import-data-into-responsys}

Depois de conectar a Plataforma ao seu [!DNL Amazon S3] ou armazenamento SFTP, você deve configurar a importação de dados do local do armazenamento para [!DNL Oracle Responsys]. Para saber como fazer isso, consulte [Importando contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) no [!DNL Oracle Responsys Help Center].