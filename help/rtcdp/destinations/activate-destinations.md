---
title: Ativar perfis e segmentos em um destino
seo-title: Ativar perfis e segmentos em um destino
description: Ative os dados que você tem na Adobe Real-time Customer Data Platform mapeando segmentos para destinos. Para fazer isso, siga as etapas abaixo.
seo-description: Ative os dados que você tem na Adobe Real-time Customer Data Platform mapeando segmentos para destinos. Para fazer isso, siga as etapas abaixo.
translation-type: tm+mt
source-git-commit: 098dd31be4d6ee6971cd87bcbfe0f686e34918e1
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 0%

---


# Ativar perfis e segmentos em um destino

Ative os dados que você tem na Adobe Real-time Customer Data Platform mapeando segmentos para destinos. Para fazer isso, siga as etapas abaixo.

## Pré-requisitos {#prerequisites}

Para ativar os dados para destinos, você deve ter [conectado com êxito um destino](/help/rtcdp/destinations/connect-destination.md). Caso ainda não o tenha feito, vá para o catálogo [de](/help/rtcdp/destinations/destinations-catalog.md)destinos, navegue nos destinos suportados e configure um ou mais destinos.

## Ativar dados {#activate-data}

1. Em **[!UICONTROL Destinos > Procurar]**, selecione o destino onde deseja ativar seus segmentos.
2. Clique no nome do destino. Isso leva você ao fluxo Ativar.
   ![ativar-fluxo](/help/rtcdp/destinations/assets/activate-flow.png)Observe que se já existir um fluxo de ativação para um destino, você pode ver os segmentos que estão sendo enviados para o destino. Selecione **[!UICONTROL Editar ativação]** no painel direito e siga as etapas abaixo para modificar os detalhes da ativação.
3. Selecione **[!UICONTROL Ativar]**;
4. No fluxo de trabalho **[!UICONTROL Ativar destino]** , na página **[!UICONTROL Selecionar segmentos]** , selecione quais segmentos enviar para o destino.
   ![segmentos para destino](/help/rtcdp/destinations/assets/email-select-segments.png)
5. *Condicional*. Essa etapa difere dependendo do tipo de destino em que você está ativando seus segmentos. <br> Para destinos *de marketing de* email e destinos *de armazenamentos de* nuvem, na página **[!UICONTROL Selecionar atributos]** , selecione **[!UICONTROL Adicionar novo campo]** e selecione os atributos que deseja enviar para o destino.
Recomendamos que um dos atributos seja um identificador [](/help/rtcdp/destinations/email-marketing-destinations.md#identity) exclusivo do seu schema de união. Para obter mais informações sobre atributos obrigatórios, consulte Identidade no artigo Destinos [de marketing de](/help/rtcdp/destinations/email-marketing-destinations.md#identity) email.

   >[!NOTE]
   > 
   >Se algum rótulo de uso de dados tiver sido aplicado a determinados campos em um conjunto de dados (em vez de todo o conjunto de dados), a imposição desses rótulos de nível de campo na ativação ocorrerá sob as seguintes condições:
   >* Os campos são usados na definição do segmento.
   >* Os campos são configurados como atributos projetados para o destino do público alvo.

   >
   > Considere a captura de tela abaixo. Por exemplo, se o campo `person.name.first.Name` tivesse determinados rótulos de uso de dados que entrassem em conflito com o caso de uso de marketing do destino, você veria uma violação da política de uso de dados na etapa de revisão (etapa 7). Para obter mais informações, consulte Controle de [dados em CDP em tempo real](/help/rtcdp/privacy/data-governance-overview.md#destinations)

   ![atributos de destino](/help/rtcdp/destinations/assets/select-attributes-step.png)

   <br> 

   Para destinos ** sociais, na etapa de mapeamento **** Identidade, você pode selecionar atributos de origem para mapear como identidades de público alvo no destino. Essa etapa é opcional ou obrigatória, dependendo da identidade primária usada no schema. <br> 

   *Endereço de email como identidade* principal: Se você estiver usando o endereço de email como identidade primária em seu schema, poderá ignorar a etapa de mapeamento de identidade, como mostrado abaixo:

   ![Endereço de email como identidade](/help/rtcdp/destinations/assets/email-as-identity.gif)

   <br> 

   *Outra ID como identidade* primária: Se estiver usando outra ID, como ID *de* recompensa ou ID *de* fidelidade, como a principal identidade do seu schema, é necessário mapear manualmente o endereço de email do seu schema de identidade como uma identidade de público alvo no destino social, como mostrado abaixo:

   ![ID de fidelidade como identidade](/help/rtcdp/destinations/assets/rewardsid-as-identity.gif)


   Selecione `Email_LC_SHA256` como identidade do público alvo se você tiver hash de endereços de email do cliente na ingestão de dados no Adobe Experience Platform, de acordo com os requisitos [!DNL Facebook] de hash do [](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)email. <br> Selecione `Email` como identidade de público alvo se os endereços de email que você está usando não estiverem com hash. A CDP em tempo real do Adobe hash os endereços de email para atender aos [!DNL Facebook] requisitos.

   ![mapeamento de identidade após preencher campos](/help/rtcdp/destinations/assets/identity-mapping.png)

6. Na página Agendamento **[!UICONTROL do]** segmento, é possível visualizar a data do start para enviar dados para o destino, bem como a frequência do envio de dados para o destino.

   >[!IMPORTANT]
   >
   >Para destinos sociais, você deve selecionar a origem de sua audiência nesta etapa. Você pode prosseguir para a próxima etapa somente depois de selecionar uma das opções na imagem abaixo.

   ![escolher origem de dados](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. Na página **[!UICONTROL Revisar]** , você pode ver um resumo de sua seleção. Selecione **[!UICONTROL Cancelar]** para quebrar o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações ou **[!UICONTROL Concluir]** para confirmar sua seleção e start enviando dados para o destino.

   >[!IMPORTANT]
   >
   >Nesta etapa, a CDP em tempo real verifica se há violações da política de uso de dados. Abaixo está um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho da ativação de segmentos até que você tenha resolvido a violação. Para obter informações sobre como resolver violações de política, consulte Aplicação de [política](/help/rtcdp/privacy/data-governance-overview.md#enforcement) na seção de documentação de controle de dados.

![confirmação de seleção](/help/rtcdp/destinations/assets/data-policy-violation.png)

Se nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Concluir]** para confirmar sua seleção e start enviando dados para o destino.

![confirmação de seleção](/help/rtcdp/destinations/assets/confirm-selection.png)



## Editar ativação {#edit-activation}

Siga as etapas abaixo para editar os fluxos de ativação existentes na CDP em tempo real:

1. Selecione **[!UICONTROL Destinos]** na barra de navegação esquerda, clique na guia **[!UICONTROL Procurar]** e clique no nome de destino.
2. Selecione **[!UICONTROL Editar ativação]** no painel direito para alterar quais segmentos enviar para o destino.

## Verificar se a ativação de segmentos foi bem-sucedida {#verify-activation}

### Destinos de marketing por email e destinos de armazenamentos na nuvem {#esp-and-cloud-storage}

Para destinos de marketing por email e destinos de armazenamento na nuvem, o Adobe Real-time CDP cria um arquivo delimitado por tabulação `.txt` ou `.csv` no local do armazenamento fornecido. Espera que um novo arquivo seja criado no local do armazenamento todos os dias. The file format is:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

Os arquivos que você receberia em três dias consecutivos podem ter a seguinte aparência:

```
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

A presença desses arquivos no local do seu armazenamento é a confirmação da ativação bem-sucedida. Para entender como os arquivos exportados são estruturados, é possível [baixar um arquivo](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv).csv de amostra. Esse arquivo de amostra inclui os atributos do perfil `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`e `personalEmail.address`.

### Destinos de publicidade

Verifique o destino de anúncio respectivo para o qual você está ativando seus dados. Se a ativação tiver sido bem-sucedida, as audiências serão preenchidas em sua plataforma de publicidade.

### Destinos da rede social

Por exemplo, [!DNL Facebook]uma ativação bem-sucedida significa que uma audiência [!DNL Facebook] personalizada seria criada programaticamente no Gerenciador [de anúncios do](https://www.facebook.com/adsmanager/manage/)Facebook. A associação de segmento na audiência seria adicionada e removida, pois os usuários são qualificados ou desqualificados para os segmentos ativados.

>[!TIP]
>
>A integração entre a CDP em tempo real do Adobe e [!DNL Facebook] suporta preenchimentos retroativos históricos de audiência. Todas as qualificações de segmento histórico são enviadas para [!DNL Facebook] quando você ativa os segmentos para o destino.

## Desativar ativação {#disable-activation}

Para desativar um fluxo de ativação existente, siga as etapas abaixo:

1. Selecione **[!UICONTROL Destinos]** na barra de navegação esquerda, clique na guia **[!UICONTROL Procurar]** e clique no nome de destino.
2. Clique no controle **[!UICONTROL Ativado]** no painel direito para alterar o estado do fluxo de ativação.
3. Na janela **Atualizar estado** do fluxo de dados, selecione **Confirmar** para desativar o fluxo de ativação.
