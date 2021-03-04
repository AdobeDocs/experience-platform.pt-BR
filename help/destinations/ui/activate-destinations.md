---
keywords: ativar destino; ativar destinos; ativar dados
title: Ativar perfis e segmentos para um destino
type: Tutorial
seo-title: Ativar perfis e segmentos para um destino
description: Ative os dados que você tem na Adobe Experience Platform, mapeando segmentos para destinos. Para fazer isso, siga as etapas abaixo.
seo-description: Ative os dados que você tem na Adobe Experience Platform, mapeando segmentos para destinos. Para fazer isso, siga as etapas abaixo.
translation-type: tm+mt
source-git-commit: 789534c02746ed24dfa01c7b471cdf3be407711e
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 0%

---


# Ativar perfis e segmentos para um destino

Ative os dados que você tem em [!DNL Adobe Experience Platform] mapeando segmentos para destinos. Para fazer isso, siga as etapas abaixo.

## Pré-requisitos {#prerequisites}

Para ativar dados em destinos, você deve ter [conectado com êxito um destino](./connect-destination.md). Se ainda não tiver feito isso, vá para o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure um ou mais destinos.

## Ativar dados {#activate-data}

As etapas no fluxo de trabalho de ativação variam um pouco entre os tipos de destino. O fluxo de trabalho completo para todos os tipos de destino é descrito abaixo.

### Selecione o destino para ativar os dados em {#select-destination}

Aplica-se a: Todos os destinos

Na interface do usuário da Adobe Experience Platform, navegue até **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** e selecione o destino onde deseja ativar seus segmentos.

![navegar até o destino](../assets/ui/activate-destinations/connect.png)

Selecione o nome do destino para navegar até o workflow de ativação.

![fluxo de ativação](../assets/ui/activate-destinations/activate-flow.png)

>[!NOTE]
>
>Se um workflow de ativação já existir para um destino, você poderá ver os segmentos que estão sendo ativados no momento para o destino. Selecione **[!UICONTROL Editar ativação]** no painel direito e siga as etapas abaixo para modificar os detalhes de ativação.

Depois de selecionar um destino, selecione **[!UICONTROL Ativar]**.

### [!UICONTROL Etapa Selecionar ] segmentos  {#select-segments}

Aplica-se a: Todos os destinos

![Selecionar etapa de segmentos](../assets/ui/activate-destinations/select-segments-icon.png)

No workflow **[!UICONTROL Ativate destination]**, na página **[!UICONTROL Select Segments]**, selecione um ou mais segmentos para ativar no destino. Selecione **[!UICONTROL Next]** para prosseguir para a próxima etapa.

![segmentos para destino](../assets/ui/activate-destinations/email-select-segments.png)

### [!UICONTROL Etapa do ] mapeamento de identidade  {#identity-mapping}

Aplica-se a: destinos sociais e destino de publicidade da Correspondência de clientes do Google

![Etapa de mapeamento de identidade](../assets/ui/activate-destinations/identity-mapping-icon.png)

Para destinos sociais, você deve selecionar atributos de origem ou namespaces de identidade para mapear como identidades de destino no destino.

#### Exemplo: ativação de dados de público-alvo em [!DNL Facebook Custom Audience] {#example-facebook}

Abaixo está um exemplo do mapeamento de identidade correto ao ativar dados de público-alvo em [!DNL Facebook].

Seleção de campos de origem:

* Selecione o namespace `Email` como identidade de origem se os endereços de email que você está usando não estiverem com hash.
* Selecione o namespace `Email_LC_SHA256` como identidade de origem se tiver colocado hash em endereços de email de clientes na assimilação de dados em [!DNL Platform], de acordo com [!DNL Facebook] [requisitos de hash de email](../catalog/social/facebook.md#email-hashing-requirements).
* Selecione o namespace `PHONE_E.164` como identidade de origem se seus dados consistirem em números de telefone não com hash. [!DNL Platform] O hash os números de telefone estão em conformidade com  [!DNL Facebook] os requisitos.
* Selecione o namespace `Phone_SHA256` como identidade de origem se você tiver hash de números de telefone na assimilação de dados em [!DNL Platform], de acordo com [!DNL Facebook] [requisitos de hash de número de telefone](../catalog/social/facebook.md#phone-number-hashing-requirements).
* Selecione o namespace `IDFA` como identidade de origem se os dados consistem em [!DNL Apple] IDs de dispositivo.
* Selecione o namespace `GAID` como identidade de origem se os dados consistem em [!DNL Android] IDs de dispositivo.
* Selecione o namespace `Custom` como identidade de origem se os dados consistirem de outro tipo de identificadores.

Seleção de campos de destino:

* Selecione o namespace `Email_LC_SHA256` como identidade de destino quando os namespaces de origem forem `Email` ou `Email_LC_SHA256`.
* Selecione o namespace `Phone_SHA256` como identidade de destino quando os namespaces de origem forem `PHONE_E.164` ou `Phone_SHA256`.
* Selecione os namespaces `IDFA` ou `GAID` como identidade de destino quando os namespaces de origem forem `IDFA` ou `GAID`.
* Selecione o namespace `Extern_ID` como identidade de destino quando o namespace de origem for personalizado.

![Mapeamento de identidade](../assets/ui/activate-destinations/identity-mapping.png)

Os dados de namespaces sem hash são automaticamente atribuídos a hash por [!DNL Platform] após a ativação.

Os dados da fonte de atributo não são automaticamente transformados em hash. Quando o campo de origem contém atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para ter [!DNL Platform] hash automaticamente os dados na ativação.
![Transformação de mapeamento de identidade](../assets/ui/activate-destinations/identity-mapping-transformation.png)

 

#### Exemplo: ativação de dados de público-alvo em [!DNL Google Customer Match] {#example-gcm}

Este é um exemplo do mapeamento de identidade correto ao ativar dados de público-alvo em [!DNL Google Customer Match].

Seleção de campos de origem:

* Selecione o namespace `Email` como identidade de origem se os endereços de email que você está usando não estiverem com hash.
* Selecione o namespace `Email_LC_SHA256` como identidade de origem se tiver colocado hash em endereços de email de clientes na assimilação de dados em [!DNL Platform], de acordo com [!DNL Google Customer Match] [requisitos de hash de email](../catalog/social/../advertising/google-customer-match.md).
* Selecione o namespace `PHONE_E.164` como identidade de origem se seus dados consistirem em números de telefone não com hash. [!DNL Platform] O hash os números de telefone estão em conformidade com  [!DNL Google Customer Match] os requisitos.
* Selecione o namespace `Phone_SHA256_E.164` como identidade de origem se você tiver hash de números de telefone na assimilação de dados em [!DNL Platform], de acordo com [!DNL Facebook] [requisitos de hash de número de telefone](../catalog/social/../advertising/google-customer-match.md).
* Selecione o namespace `IDFA` como identidade de origem se os dados consistem em [!DNL Apple] IDs de dispositivo.
* Selecione o namespace `GAID` como identidade de origem se os dados consistem em [!DNL Android] IDs de dispositivo.
* Selecione o namespace `Custom` como identidade de origem se os dados consistirem de outro tipo de identificadores.

Seleção de campos de destino:

* Selecione o namespace `Email_LC_SHA256` como identidade de destino quando os namespaces de origem forem `Email` ou `Email_LC_SHA256`.
* Selecione o namespace `Phone_SHA256_E.164` como identidade de destino quando os namespaces de origem forem `PHONE_E.164` ou `Phone_SHA256_E.164`.
* Selecione os namespaces `IDFA` ou `GAID` como identidade de destino quando os namespaces de origem forem `IDFA` ou `GAID`.
* Selecione o namespace `User_ID` como identidade de destino quando o namespace de origem for personalizado.

![Mapeamento de identidade](../assets/ui/activate-destinations/identity-mapping-gcm.png)

Os dados de namespaces sem hash são automaticamente atribuídos a hash por [!DNL Platform] após a ativação.

Os dados da fonte de atributo não são automaticamente transformados em hash. Quando o campo de origem contém atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para ter [!DNL Platform] hash automaticamente os dados na ativação.
![Transformação de mapeamento de identidade](../assets/ui/activate-destinations/identity-mapping-gcm-transformation.png)

<!-- 
`IDFA` IDs will be mapped to:

* [MADID](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences#hash) if you are activating audiences in [[!DNL Facebook]](../../destinations/catalog/social/facebook.md).
* [mobileId](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.Member#mobileid) if you are activating audiences in [[!DNL Google Customer Match]](../../destinations/catalog/advertising/google-customer-match.md).

Select `GAID` as target identity if your data consists of Android device IDs. `GAID` IDs will be mapped to:

* [MADID](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences#hash) if you are activating audiences in [[!DNL Facebook]](../../destinations/catalog/social/facebook.md).
* [mobileId](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.Member#mobileid) if you are activating audiences in [[!DNL Google Customer Match]](../../destinations/catalog/advertising/google-customer-match.md).

If you are using another ID, such as "Rewards ID" or "Loyalty ID", as primary identity in your schema, you need to map it to the following target identities:

* [EXTERN_ID](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences#external_identifiers) if you are activating audiences in [[!DNL Facebook]](../../destinations/catalog/social/facebook.md).
* [USER_ID](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.Member#userid) if you are activating audiences in [[!DNL Google Customer Match]](../../destinations/catalog/advertising/google-customer-match.md). -->

### **** Configurestep  {#configure}

Aplica-se a: Destinos de marketing por email e destinos de armazenamento em nuvem

![Etapa de configuração](../assets/ui/activate-destinations/configure-icon.png)

[!DNL Adobe Experience Platform] exporta dados para marketing por email e destinos de armazenamento na nuvem na forma de  [!DNL CSV] arquivos. Na etapa **[!UICONTROL Configurar]**, é possível configurar o agendamento e os nomes de arquivo para cada segmento que você está exportando. A configuração do agendamento é obrigatória, mas a configuração do nome do arquivo é opcional.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] divide automaticamente os arquivos de exportação em 5 milhões de registros (linhas) por arquivo. Cada linha representa um perfil.
>
>Nomes de arquivos divididos são anexados com um número que indica que o arquivo faz parte de uma exportação maior, desta forma: `filename.csv`, `filename_2.csv`, `filename_3.csv`.


Para adicionar um agendamento ao segmento, selecione **[!UICONTROL Criar agendamento]**.

![](../assets/ui/activate-destinations/configure-destination-schedule.png)

Uma caixa de diálogo é exibida mostrando opções para criar a programação do segmento.

* **Exportação** de arquivo: Você tem a opção de exportar arquivos completos ou arquivos incrementais. Exportar um arquivo completo publica um instantâneo completo de todos os perfis qualificados para esse segmento. A exportação de um arquivo incremental publica o delta de perfis qualificados para esse segmento desde a última exportação.
* **Frequência**: Se  **[!UICONTROL Exportar arquivo completo estiver selecionado, você terá a opção de exportar]** uma vez  **** por dia ****. Se **[!UICONTROL Exportar arquivos incrementais]** estiver selecionado, você só terá a opção de exportar **[!UICONTROL Diariamente]**. Exportar um arquivo **[!UICONTROL Uma vez]** exporta o arquivo uma vez. Exportar um arquivo **[!UICONTROL Diariamente]** exporta o arquivo todos os dias da data de início para a data de término às 12:00 AM UTC (7:00 PM EST) se os arquivos completos estiverem selecionados e 12:00 PM UTC (7:00 AM EST) se os arquivos incrementais estiverem selecionados.
* **Data**: Se a opção  **** Ondas estiver selecionada, você poderá selecionar a data para a exportação única. Se **[!UICONTROL Diariamente]** estiver selecionado, você poderá selecionar as datas de início e término das exportações.

![](../assets/ui/activate-destinations/export-full-file.png)

Os nomes de arquivo padrão consistem em nome de destino, ID de segmento e um indicador de data e hora. Por exemplo, você pode editar os nomes de arquivo exportados para distinguir entre campanhas diferentes ou para ter o tempo de exportação de dados anexado aos arquivos.

Selecione o ícone de lápis para abrir uma janela modal e editar os nomes dos arquivos. Observe que os nomes de arquivo são limitados a 255 caracteres.

![configurar nome do arquivo](../assets/ui/activate-destinations/configure-name.png)

No editor de nome de arquivo, é possível selecionar componentes diferentes para adicionar ao nome do arquivo. O nome de destino e a ID de segmento não podem ser removidos dos nomes de arquivo. Além disso, você pode adicionar o seguinte:

* **[!UICONTROL Nome]** do segmento: Você pode anexar o nome do segmento ao nome do arquivo.
* **[!UICONTROL Data e hora]**: Selecione entre adicionar um  `MMDDYYYY_HHMMSS` formato ou um carimbo de data e hora de 10 dígitos do Unix da hora em que os arquivos são gerados. Escolha uma dessas opções se desejar que seus arquivos tenham um nome de arquivo dinâmico gerado com cada exportação incremental.
* **[!UICONTROL Texto]** personalizado: Adicione texto personalizado aos nomes dos arquivos.

Selecione **[!UICONTROL Aplicar alterações]** para confirmar a seleção.

>[!IMPORTANT]
> 
>Se você não selecionar o componente **[!UICONTROL Date and Time]**, os nomes de arquivo serão estáticos e o novo arquivo exportado substituirá o arquivo anterior no local de armazenamento com cada exportação. Ao executar um trabalho de importação recorrente de um local de armazenamento em uma plataforma de marketing por email, essa é a opção recomendada.

![editar opções de nome de arquivo](../assets/ui/activate-destinations/activate-workflow-configure-step-2.png)

Depois de concluir a configuração de todos os seus segmentos, selecione **[!UICONTROL Next]** para continuar.

### **[!UICONTROL Etapa de]** agendamento do segmento  {#segment-schedule}

Aplica-se a: destinos de publicidade, destinos sociais

![etapa de agendamento de segmento](../assets/ui/activate-destinations/segment-schedule-icon.png)

Na página **[!UICONTROL Segment schedule]**, você pode definir a data de início do envio de dados para o destino e a frequência do envio de dados para o destino.

>[!IMPORTANT]
>
>Para destinos sociais, você deve selecionar a origem do público nesta etapa. Você pode prosseguir para a próxima etapa somente após selecionar uma das opções na imagem abaixo.

![Origem do público-alvo do Facebook](../assets/catalog/social/facebook/facebook-origin-audience.png)

>[!IMPORTANT]
>
>Para Correspondência de clientes do Google, você deve fornecer a [!UICONTROL ID do aplicativo] nesta etapa, ao ativar os segmentos [!DNL IDFA] ou [!DNL GAID].

![inserir id do aplicativo](../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

### **** Etapa de agendamento  {#scheduling}

Aplica-se a: destinos de marketing por email e destinos de armazenamento em nuvem

![etapa de agendamento de segmento](../assets/ui/activate-destinations/scheduling-icon.png)

Na página **[!UICONTROL Scheduling]**, você pode ver a data de início para enviar dados para o destino, bem como a frequência do envio de dados para o destino. Esses valores não podem ser editados.

### **[!UICONTROL Selecionar etapa de]** atribuição  {#select-attributes}

Aplica-se a: destinos de marketing por email e destinos de armazenamento em nuvem

![etapa selecionar atributos](../assets/ui/activate-destinations/select-attributes-icon.png)

Na página **[!UICONTROL Select attributes]**, selecione **[!UICONTROL Add new field]** e escolha os atributos que deseja enviar para o destino.

>[!NOTE]
>
> A Adobe Experience Platform preenche sua seleção com quatro atributos recomendados e comumente usados do esquema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

As exportações de arquivo variam das seguintes maneiras, dependendo se `segmentMembership.status` estiver selecionado:
* Se o campo `segmentMembership.status` for selecionado, os arquivos exportados incluirão **[!UICONTROL membros Ativos]** no instantâneo completo inicial e **[!UICONTROL membros Ativos]** e **[!UICONTROL Expirados]** nas exportações incrementais subsequentes.
* Se o campo `segmentMembership.status` não estiver selecionado, os arquivos exportados incluirão apenas **[!UICONTROL membros Ativos]** no instantâneo completo inicial e nas exportações incrementais subsequentes.

![atributos recomendados](../assets/ui/activate-destinations/mark-mandatory.png)

Além disso, é possível marcar atributos diferentes como obrigatórios. Marcar um atributo como obrigatório o torna obrigatório, portanto, o segmento exportado deve conter esse atributo. Como resultado, ele pode ser usado como uma forma adicional de filtragem. Marcar um atributo como obrigatório é **não** necessário.

Recomenda-se que um dos atributos seja um [identificador exclusivo](../../destinations/catalog/email-marketing/overview.md#identity) do esquema. Para obter mais informações sobre atributos obrigatórios, consulte a seção de identidade na documentação [Destinos de marketing de email](../../destinations/catalog/email-marketing/overview.md#identity) .

>[!NOTE]
> 
>Se algum rótulo de uso de dados tiver sido aplicado a determinados campos em um conjunto de dados (em vez do conjunto de dados inteiro), a imposição desses rótulos em nível de campo na ativação ocorrerá sob as seguintes condições:
>* Os campos são usados na definição do segmento.
>* Os campos são configurados como atributos projetados para o destino.

>
> 
Por exemplo, se o campo `person.name.firstName` tiver determinados rótulos de uso de dados que entrem em conflito com a ação de marketing do destino, você verá uma violação da política de uso de dados na etapa de revisão. Para obter mais informações, consulte [Governança de dados na Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

### **** Etapa de revisão  {#review}

Aplica-se a: todos os destinos

![etapa de revisão](../assets/ui/activate-destinations/review-icon.png)

Na página **[!UICONTROL Revisar]**, você pode ver um resumo da sua seleção. Selecione **[!UICONTROL Cancelar]** para quebrar o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações ou **[!UICONTROL Concluir]** para confirmar sua seleção e começar a enviar dados para o destino.

>[!IMPORTANT]
>
>Nesta etapa, a Adobe Experience Platform verifica violações da política de uso de dados. Veja abaixo um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho de ativação de segmento até que você tenha resolvido a violação. Para obter informações sobre como resolver violações de política, consulte [Aplicação de política](../../rtcdp/privacy/data-governance-overview.md#enforcement) na seção Documentação de governança de dados.

![violação da política de dados](../assets/common/data-policy-violation.png)

Se nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Finish]** para confirmar a seleção e iniciar o envio de dados para o destino.

![confirmar seleção](../assets/ui/activate-destinations/confirm-selection.png)

## Editar ativação {#edit-activation}

Siga as etapas abaixo para editar os fluxos de ativação existentes na Adobe Experience Platform:

1. Selecione **[!UICONTROL Destinations]** na barra de navegação esquerda, clique na guia **[!UICONTROL Browse]** e clique no nome do destino.
2. Selecione **[!UICONTROL Edit ativation]** no painel direito para alterar quais segmentos enviar para o destino.

## Verifique se a ativação do segmento foi bem-sucedida {#verify-activation}

### Destinos de marketing por email e destinos de armazenamento em nuvem {#esp-and-cloud-storage}

Para destinos de marketing por email e destinos de armazenamento em nuvem, a Adobe Experience Platform cria um arquivo `.csv` ou `.txt` delimitado por tabulação no local de armazenamento fornecido. Espera que um novo arquivo seja criado no seu local de armazenamento todos os dias. O formato de arquivo padrão é:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv|txt`

Observe que é possível editar o formato de arquivo. Para obter mais informações, vá para a etapa [Configure](#configure) para destinos de armazenamento em nuvem e destinos de marketing de email.

Com o formato de arquivo padrão, os arquivos que você receberia em três dias consecutivos podem ter a seguinte aparência:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

A presença desses arquivos no local de armazenamento é a confirmação de uma ativação bem-sucedida. Para entender como os arquivos exportados são estruturados, você pode [baixar um arquivo .csv de amostra](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Este arquivo de amostra inclui os atributos de perfil `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear` e `personalEmail.address`.

### Destinos de publicidade

Verifique sua conta no respectivo destino de publicidade para o qual você está ativando seus dados. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos em sua plataforma de publicidade.

### Destinos da rede social

Para [!DNL Facebook], uma ativação bem-sucedida significa que um público-alvo personalizado [!DNL Facebook] seria criado programaticamente no [[!UICONTROL Gerenciador de Anúncios do Facebook]](https://www.facebook.com/adsmanager/manage/). A associação de segmento no público-alvo seria adicionada e removida, pois os usuários eram qualificados ou desqualificados para os segmentos ativados.

>[!TIP]
>
>A integração entre a Adobe Experience Platform e [!DNL Facebook] oferece suporte a preenchimentos retroativos de público-alvo histórico. Todas as qualificações de segmento histórico são enviadas para [!DNL Facebook] quando você ativa os segmentos para o destino.

## Desativar ativação {#disable-activation}

Para desativar um fluxo de ativação existente, siga as etapas abaixo:

1. Selecione **[!UICONTROL Destinations]** na barra de navegação esquerda, clique na guia **[!UICONTROL Browse]** e clique no nome do destino.
2. Clique no controle **[!UICONTROL Enabled]** no painel direito para alterar o estado do fluxo de ativação.
3. Na janela **Update data flow state**, selecione **Confirm** para desativar o fluxo de ativação.
