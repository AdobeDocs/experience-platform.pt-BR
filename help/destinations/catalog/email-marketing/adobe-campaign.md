---
keywords: email;Email;e-mail;destinos de e-mail;adobe campaign;campanha
title: Conexão com o Adobe Campaign
description: O Adobe Campaign é um conjunto de soluções que ajudam você a personalizar e entregar campanhas em todos os seus canais online e offline.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 2%

---

# Conexão com o Adobe Campaign

## Visão geral {#overview}

O Adobe Campaign é um conjunto de soluções que ajudam você a personalizar e entregar campanhas em todos os seus canais online e offline. Consulte [Introdução ao Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=pt-BR) para obter mais informações.

Para enviar dados do público-alvo para o Adobe Campaign, primeiro você deve [conectar o destino](#connect-destination) no Adobe Experience Platform e [configurar uma importação de dados](#import-data-into-campaign) do local de armazenamento para o Adobe Campaign.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | ✓ | Públicos-alvo [importado](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil da [workflow de ativação de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Lote]** | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos baseados em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## INCLUIR NA LISTA DE PERMISSÕES endereço IP {#allow-list}

Ao configurar destinos de marketing por email com armazenamento SFTP, a Adobe recomenda adicionar determinados intervalos IP ao incluo na lista de permissões.

Consulte [Endereço IP relacionado à inclui na lista de permissões para destinos SFTP](../cloud-storage/ip-address-allow-list.md) se você precisar adicionar IPs do Adobe ao seu incluo na lista de permissões.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

O Adobe Campaign é compatível com os seguintes tipos de conexão:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP com senha]**
* **[!UICONTROL SFTP com chave SSH]**
* **[!UICONTROL Azure Blob]**

O método preferido para enviar dados para o Adobe Campaign é por meio de [!DNL Amazon S3] ou [!DNL Azure Blob].

### Parâmetros de conexão {#parameters}

Enquanto [configuração](../../ui/connect-destination.md) Para esse destino, você deve fornecer as seguintes informações:

* Para **[!UICONTROL Amazon S3]** conexões, você deve fornecer seus [!UICONTROL ID da chave de acesso] e [!UICONTROL Chave de Acesso Secreta].
* Para **[!UICONTROL SFTP com senha]** conexões, você deve fornecer [!UICONTROL Domínio], [!UICONTROL Porta], [!UICONTROL Nome de usuário], e [!UICONTROL Senha].
* Para **[!UICONTROL SFTP com chave SSH]** conexões, você deve fornecer [!UICONTROL Domínio], [!UICONTROL Porta], [!UICONTROL Nome de usuário], e [!UICONTROL Chave SSH].
* Para **[!UICONTROL Azure Blob]** conexões, você deve fornecer uma cadeia de conexão.
* Como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia com PGP/GPG aos arquivos exportados no **[!UICONTROL Chave]** seção. Sua chave pública deve ser gravada como [!DNL Base64] string codificada.
* **[!UICONTROL Nome]**: escolha um nome relevante para o seu destino.
* **[!UICONTROL Descrição]**: digite uma descrição para o destino.
* **[!UICONTROL Nome do bloco]**: *Para conexões S3*. Informe o local do seu período S3 em que [!DNL Platform] O depositará os dados de exportação como arquivos CSV.
* **[!UICONTROL Caminho da pasta]**: forneça o caminho no local de armazenamento onde [!DNL Platform] O depositará os dados de exportação como arquivos CSV.
* **[!UICONTROL Container]**: *Para conexões Blob*. O container que contém o Blob em que o caminho da pasta está.
* **[!UICONTROL Formato de arquivo]**: Selecionar **CSV** para exportar arquivos CSV para o local de armazenamento.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}


Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Atributos de destino {#destination-attributes}

Ao ativar públicos para esse destino, o Adobe recomenda selecionar um identificador exclusivo dentre os [esquema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte [práticas recomendadas ao ativar públicos para destinos de marketing por email](overview.md#best-practices).

## Dados exportados {#exported-data}

Para [!DNL Adobe Campaign] destinos, [!DNL Platform] cria um `.csv` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [verificar ativação de público](../../ui/activate-batch-profile-destinations.md#verify) no tutorial de ativação de público-alvo.

## Configurar importação de dados para o Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Lembre-se [!DNL SFTP] limites de armazenamento, limites de armazenamento do banco de dados e limites do perfil ativo conforme o contrato do Adobe Campaign ao realizar essa integração.
>* Você precisa agendar, importar e mapear os segmentos exportados no Adobe Campaign usando [!DNL Campaign] fluxos de trabalho. Consulte [Configuração de uma importação recorrente](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) na documentação do Adobe Campaign Classic e [Sobre as atividades de gestão de dados](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) na documentação do Adobe Campaign Standard.
>* O método preferido para enviar dados para o Adobe Campaign é por meio de [!DNL Amazon S3] ou [!DNL Azure Blob].

Depois de se conectar [!DNL Platform] ao seu [!DNL Amazon S3] ou [!DNL Azure Blob] armazenamento, você deve configurar a importação de dados do local de armazenamento para o Adobe Campaign. Para saber como fazer isso, consulte as seguintes páginas de documentação do Adobe Campaign:
* [Introdução à importação e exportação de dados](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=pt-BR) e [Carregamento de dados (arquivo)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) na documentação do Adobe Campaign Classic.
* [Introdução a processos e gerenciamento de dados](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) e [Carregar arquivo](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) na documentação do Adobe Campaign Standard.
