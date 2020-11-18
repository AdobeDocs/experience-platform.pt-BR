---
keywords: activate destination;activate destinations;activate data
title: Ativar perfis e segmentos em um destino
type: Tutorial
seo-title: Ativar perfis e segmentos em um destino
description: 'Ative os dados que você tem na Plataforma de dados do cliente em tempo real mapeando segmentos para destinos. '
seo-description: Ative os dados que você tem na Plataforma de dados do cliente em tempo real mapeando segmentos para destinos. Para fazer isso, siga as etapas abaixo.
translation-type: tm+mt
source-git-commit: bb59d93e016d49a0ebba77af1f90563a8767f072
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 0%

---


# Ativar perfis e segmentos em um destino

Ative os dados que você tem na Plataforma de dados do cliente em tempo real mapeando segmentos para destinos. Para fazer isso, siga as etapas abaixo.

## Pré-requisitos {#prerequisites}

Para ativar os dados para destinos, você deve ter [conectado com êxito um destino](/help/rtcdp/destinations/connect-destination.md). Caso ainda não o tenha feito, vá para o catálogo [de](/help/rtcdp/destinations/destinations-catalog.md)destinos, navegue nos destinos suportados e configure um ou mais destinos.

## Ativar dados {#activate-data}

As etapas no fluxo de trabalho da ativação variam ligeiramente entre os tipos de destino. O fluxo de trabalho completo para todos os tipos de destino está descrito abaixo.

### Selecione para qual destino os dados serão ativados {#select-destination}

Aplica-se a: Todos os destinos

Na interface de usuário CDP em tempo real, navegue até **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]**e selecione o destino onde deseja ativar seus segmentos.
![navegar até o destino](assets/oracle-eloqua-connect.png)

Selecione o nome do destino para navegar até o fluxo de trabalho da ativação.

![ativar fluxo](assets/activate-flow.png)

Observe que se já existir um fluxo de trabalho de ativação para um destino, você poderá ver os segmentos que estão sendo ativados no momento para o destino. Selecione **[!UICONTROL Editar ativação]** no painel direito e siga as etapas abaixo para modificar os detalhes da ativação.

Depois de selecionar um destino, selecione **[!UICONTROL Ativar]**.

### [!UICONTROL Etapa Selecionar segmentos] {#select-segments}

Aplica-se a: Todos os destinos

![Selecionar etapa de segmentos](./assets/select-segments-icon.png)

Na página **[!UICONTROL Ativar fluxo de trabalho de destino]** , na página **[!UICONTROL Selecionar segmentos]** , selecione um ou mais segmentos para ativar no destino. Selecione **[!UICONTROL Avançar]** para prosseguir para a próxima etapa.
![segmentos para destino](assets/email-select-segments.png)

### [!UICONTROL Etapa de mapeamento] de identidade {#identity-mapping}

Aplica-se a: destinos sociais e destino publicitário da Correspondência de clientes do Google

![Etapa de mapeamento de identidade](./assets/identity-mapping-icon.png)

Para destinos sociais, você pode selecionar atributos de origem para mapear como identidades de público alvo no destino. Essa etapa é opcional ou obrigatória, dependendo da identidade primária usada no schema.

Se você estiver usando o endereço de email como identidade primária em seu schema, poderá ignorar a etapa de mapeamento de identidade, como mostrado abaixo:

![Endereço de email como identidade](assets/email-as-identity.gif)

Se estiver usando outra ID, como &quot;ID de recompensa&quot; ou &quot;ID de fidelidade&quot;, como a principal identidade do seu schema, é necessário mapear manualmente o endereço de email do seu schema de identidade como uma identidade de público alvo no destino social, como mostrado abaixo:

![ID de fidelidade como identidade](assets/rewardsid-as-identity.gif)

Selecione `Email_LC_SHA256` como identidade de público alvo se você tiver hash dos endereços de email do cliente na ingestão de dados no Adobe Experience Platform, de acordo com os requisitos [!DNL Facebook] de hash do [](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)email.

Selecione `Email` como identidade de público alvo se os endereços de email que você está usando não estiverem com hash. A CDP em tempo real hash os endereços de email para atender aos [!DNL Facebook] requisitos.

![mapeamento de identidade após preencher campos](assets/identity-mapping.png)

### **[!UICONTROL Configurar]** etapa {#configure}

Aplica-se a: Destinos de marketing por email e destinos de armazenamentos na nuvem

![Configurar etapa](./assets/configure-icon.png)

Na etapa **[!UICONTROL Configurar]** , é possível configurar o agendamento e os nomes de arquivo para cada segmento que você está exportando. A configuração do agendamento é obrigatória, mas a configuração do nome do arquivo é opcional.

Para adicionar um agendamento para o segmento, selecione **[!UICONTROL Criar agendamento]**.

![](./assets/activate-destinations/configure-destination-schedule.png)

Uma janela pop-up é exibida mostrando opções para criar a programação de segmentos.

- **Exportação** de arquivo: Você tem a opção de exportar arquivos completos ou incrementais. Exportar um arquivo completo publica um instantâneo completo de todos os perfis que se qualificam para esse segmento. Exportar um arquivo incremental publica o delta de perfis que se qualificam para esse segmento desde a última exportação.
- **Frequência**: Se a opção **[!UICONTROL Exportar arquivos]** completos estiver selecionada, você terá a opção de exportar **[!UICONTROL uma vez]** ou **[!UICONTROL diariamente]**. Se a opção **[!UICONTROL Exportar arquivos]** incrementais estiver selecionada, você só terá a opção de exportar **[!UICONTROL diariamente]**. Exportar um arquivo **[!UICONTROL Uma vez]** exporta o arquivo uma vez. Exportar um arquivo **[!UICONTROL Diariamente]** exporta o arquivo todos os dias da data do start para a data final às 12:00 AM UTC (7:00 PM EST) se os arquivos completos estiverem selecionados e 12:00 PM UTC (7:00 AM EST) se os arquivos incrementais estiverem selecionados.
- **Data**: Se **[!UICONTROL Uma vez]** estiver selecionado, você poderá selecionar a data para a exportação única. Se **[!UICONTROL Diariamente]** estiver selecionado, você poderá selecionar as datas de start e término das exportações.

![](./assets/activate-destinations/export-full-file.png)

Os nomes de arquivo padrão consistem em nome de destino, ID de segmento e um indicador de data e hora. Por exemplo, é possível editar os nomes de arquivos exportados para distinguir entre campanhas diferentes ou para anexar o tempo de exportação de dados aos arquivos.

Selecione o ícone de lápis para abrir uma janela modal e editar os nomes dos arquivos. Observe que os nomes de arquivos são limitados a 255 caracteres.

![configurar nome do arquivo](./assets/activate-destinations/configure-name.png)

No editor de nome de arquivo, você pode selecionar componentes diferentes para adicionar ao nome do arquivo. O nome de destino e a ID de segmento não podem ser removidos dos nomes de arquivo. Além disso, você pode adicionar o seguinte:

- **[!UICONTROL Nome]** do segmento: É possível anexar o nome do segmento ao nome do arquivo.
- **[!UICONTROL Data e hora]**: Selecione entre adicionar um `MMDDYYYY_HHMMSS` formato ou um carimbo de data e hora Unix de 10 dígitos do horário em que os arquivos são gerados. Escolha uma dessas opções se desejar que seus arquivos tenham um nome de arquivo dinâmico gerado a cada exportação incremental.
- **[!UICONTROL Texto]** personalizado: Adicione texto personalizado aos nomes dos arquivos.

Selecione **[!UICONTROL Aplicar alterações]** para confirmar sua seleção.

>[!IMPORTANT]
> 
>Se você não selecionar o componente **[!UICONTROL Data e hora]** , os nomes dos arquivos serão estáticos e o novo arquivo exportado substituirá o arquivo anterior no local do armazenamento a cada exportação. Ao executar um trabalho de importação recorrente de um local de armazenamento para uma plataforma de marketing por email, essa é a opção recomendada.

![editar opções de nome de arquivo](./assets/activate-workflow-configure-step-2.png)

Após terminar de configurar todos os seus segmentos, selecione **[!UICONTROL Avançar]** para continuar.

### **[!UICONTROL Etapa do agendamento]** do segmento {#segment-schedule}

Aplica-se a: destinos publicitários, destinos sociais

![etapa de programação de segmento](./assets/segment-schedule-icon.png)

Na página Agendamento **[!UICONTROL do]** segmento, é possível definir a data do start para enviar dados para o destino, bem como a frequência do envio de dados para o destino.

>[!IMPORTANT]
>
>Para destinos sociais, você deve selecionar a origem de sua audiência nesta etapa. Você pode prosseguir para a próxima etapa somente depois de selecionar uma das opções na imagem abaixo.

![escolher origem de dados](./assets/choose-data-origin.png)

### **[!UICONTROL Etapa de agendamento]** {#scheduling}

Aplica-se a: destinos de marketing por email e destinos de armazenamentos na nuvem

![etapa de programação de segmento](./assets/scheduling-icon.png)

Na página **[!UICONTROL Agendamento]** , você pode ver a data de start para enviar dados para o destino, bem como a frequência de envio de dados para o destino. Esses valores não podem ser editados.

### **[!UICONTROL Etapa Selecionar atributos]** {#select-attributes}

Aplica-se a: destinos de marketing por email e destinos de armazenamentos na nuvem

![etapa selecionar atributos](./assets/select-attributes-icon.png)

Na página **[!UICONTROL Selecionar atributos]** , selecione **[!UICONTROL Adicionar novo campo]** e escolha os atributos que deseja enviar para o destino.

>[!NOTE]
>
> A CDP em tempo real preenche sua seleção com quatro atributos recomendados e comumente usados do seu schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

As exportações de arquivos variam das seguintes maneiras, dependendo se `segmentMembership.status` estiver selecionado:
- Se o `segmentMembership.status` campo for selecionado, os arquivos exportados incluirão membros **[!UICONTROL ativos]** no instantâneo completo inicial e membros **[!UICONTROL ativos]** e **[!UICONTROL expirados]** em exportações incrementais subsequentes.
- Se o `segmentMembership.status` campo não estiver selecionado, os arquivos exportados incluirão apenas membros **[!UICONTROL ativos]** no instantâneo completo inicial e em exportações incrementais subsequentes.

![atributos recomendados](./assets/activate-destinations/mark-mandatory.png)

Além disso, é possível marcar atributos diferentes como obrigatórios. Marcar um atributo como obrigatório faz com que o segmento exportado contenha esse atributo. Como resultado, ele pode ser usado como uma forma adicional de filtragem. Marcar um atributo como obrigatório **não** é necessário.

É recomendável que um dos atributos seja um identificador [](/help/rtcdp/destinations/email-marketing-destinations.md#identity) exclusivo do seu schema. Para obter mais informações sobre atributos obrigatórios, consulte a seção de identidade na documentação de destinos [de marketing de](/help/rtcdp/destinations/email-marketing-destinations.md#identity) email.

>[!NOTE]
> 
>Se algum rótulo de uso de dados tiver sido aplicado a determinados campos em um conjunto de dados (em vez de todo o conjunto de dados), a imposição desses rótulos de nível de campo na ativação ocorrerá sob as seguintes condições:
>- Os campos são usados na definição do segmento.
>- Os campos são configurados como atributos projetados para o destino do público alvo.

>
> 
Por exemplo, se o campo `person.name.firstName` tiver determinados rótulos de uso de dados que entram em conflito com o caso de uso de marketing do destino, você verá uma violação da política de uso de dados na etapa de revisão. Para obter mais informações, consulte Controle de [dados em CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations)em tempo real.

### **[!UICONTROL Etapa de revisão]** {#review}

Aplica-se a: todos os destinos

![etapa de revisão](./assets/review-icon.png)

Na página **[!UICONTROL Revisar]** , você pode ver um resumo de sua seleção. Selecione **[!UICONTROL Cancelar]** para quebrar o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações ou **[!UICONTROL Concluir]** para confirmar sua seleção e start enviando dados para o destino.

>[!IMPORTANT]
>
>Nesta etapa, a CDP em tempo real verifica se há violações da política de uso de dados. Abaixo está um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho da ativação de segmentos até que você tenha resolvido a violação. Para obter informações sobre como resolver violações de política, consulte Aplicação de [política](/help/rtcdp/privacy/data-governance-overview.md#enforcement) na seção de documentação de controle de dados.

![violação da política de dados](assets/data-policy-violation.png)

Se nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Concluir]** para confirmar sua seleção e start enviando dados para o destino.

![confirmação de seleção](assets/confirm-selection.png)

## Editar ativação {#edit-activation}

Siga as etapas abaixo para editar os fluxos de ativação existentes na CDP em tempo real:

1. Selecione **[!UICONTROL Destinos]** na barra de navegação esquerda, clique na guia **[!UICONTROL Procurar]** e clique no nome de destino.
2. Selecione **[!UICONTROL Editar ativação]** no painel direito para alterar quais segmentos enviar para o destino.

## Verificar se a ativação de segmentos foi bem-sucedida {#verify-activation}

### Destinos de marketing por email e destinos de armazenamentos na nuvem {#esp-and-cloud-storage}

Para destinos de marketing por email e destinos de armazenamentos na nuvem, o CDP em tempo real cria um arquivo delimitado por tabulação `.csv` ou `.txt` no local do armazenamento fornecido. Espera que um novo arquivo seja criado no local do armazenamento todos os dias. The default file format is:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv|txt`

Observe que você pode editar o formato de arquivo. Para obter mais informações, vá para a etapa [Configurar](/help/rtcdp/destinations/activate-destinations.md#configure) destinos de armazenamentos na nuvem e destinos de marketing por email.

Com o formato de arquivo padrão, os arquivos que você receberia em três dias consecutivos podem ter a seguinte aparência:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

A presença desses arquivos no local do seu armazenamento é a confirmação da ativação bem-sucedida. Para entender como os arquivos exportados são estruturados, é possível [baixar um arquivo](assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv).csv de amostra. Esse arquivo de amostra inclui os atributos do perfil `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`e `personalEmail.address`.

### Destinos de publicidade

Verifique sua conta no respectivo destino de anúncio para o qual você está ativando seus dados. Se a ativação tiver sido bem-sucedida, as audiências serão preenchidas em sua plataforma de publicidade.

### Destinos da rede social

Por exemplo, [!DNL Facebook]uma ativação bem-sucedida significa que uma audiência [!DNL Facebook] personalizada seria criada programaticamente no Gerenciador [[!UICONTROL de anúncios do]](https://www.facebook.com/adsmanager/manage/)Facebook. A associação de segmento na audiência seria adicionada e removida, pois os usuários são qualificados ou desqualificados para os segmentos ativados.

>[!TIP]
>
>A integração entre a CDP em tempo real e [!DNL Facebook] suporta preenchimentos retroativos históricos de audiência. Todas as qualificações de segmento histórico são enviadas para [!DNL Facebook] quando você ativa os segmentos para o destino.

## Desativar ativação {#disable-activation}

Para desativar um fluxo de ativação existente, siga as etapas abaixo:

1. Selecione **[!UICONTROL Destinos]** na barra de navegação esquerda, clique na guia **[!UICONTROL Procurar]** e clique no nome de destino.
2. Clique no controle **[!UICONTROL Ativado]** no painel direito para alterar o estado do fluxo de ativação.
3. Na janela **Atualizar estado** do fluxo de dados, selecione **Confirmar** para desativar o fluxo de ativação.
