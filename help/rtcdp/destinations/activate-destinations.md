---
title: Ativar perfis e segmentos em um destino
seo-title: Ativar perfis e segmentos em um destino
description: Ative os dados que você tem na Plataforma de dados do cliente em tempo real da Adobe mapeando segmentos para destinos. Para fazer isso, siga as etapas abaixo.
seo-description: Ative os dados que você tem na Plataforma de dados do cliente em tempo real da Adobe mapeando segmentos para destinos. Para fazer isso, siga as etapas abaixo.
translation-type: tm+mt
source-git-commit: 2eddd5bb7b62dcc414ad906647b05ce10c766ac6

---


# Ativar perfis e segmentos em um destino

Ative os dados que você tem na Plataforma de dados do cliente em tempo real da Adobe mapeando segmentos para destinos. Para fazer isso, siga as etapas abaixo.

## Pré-requisitos {#prerequisites}

Para ativar os dados para destinos, você deve ter [conectado com êxito um destino](/help/rtcdp/destinations/assets/connect-destination.png). Caso ainda não o tenha feito, vá para o catálogo [de](/help/rtcdp/destinations/destinations-catalog.md)destinos, navegue nos destinos suportados e configure um ou mais destinos.

## Ativar dados {#activate-data}

1. Em **[!UICONTROL Destinations > Browse]**, selecione o destino onde deseja ativar seus segmentos.
2. Clique no nome do destino. Isso leva você ao fluxo Ativar.
   ![ativar-fluxo](/help/rtcdp/destinations/assets/activate-flow.png)Observe que se já existir um fluxo de ativação para um destino, você pode ver os segmentos que estão sendo enviados para o destino. Selecione **[!UICONTROL Edit activation]** no painel direito e siga as etapas abaixo para modificar os detalhes da ativação.
3. Select **[!UICONTROL Activate]**;
4. No **[!UICONTROL Activate destination]** fluxo de trabalho, na **[!UICONTROL Select Segments]** página, selecione quais segmentos enviar para o destino.
   ![segmentos para destino](/help/rtcdp/destinations/assets/select-segments.png)
5. *Condicional*. Esta etapa se aplica somente aos segmentos mapeados para destinos de marketing de email. <br> Na **[!UICONTROL Destination Attributes]** página, selecione **[!UICONTROL Add new field]** e selecione os atributos que deseja enviar para o destino.
Recomendamos que um dos atributos seja um identificador [](/help/rtcdp/destinations/email-marketing-destinations.md#identity) exclusivo do seu schema de união. Para obter mais informações sobre atributos obrigatórios, consulte Identidade no artigo Destinos [de marketing de](/help/rtcdp/destinations/email-marketing-destinations.md#identity) email.
   ![atributos de destino](/help/rtcdp/destinations/assets/destination-attributes.png)
6. Na **[!UICONTROL Segment schedule]** página, você pode ver a data de start para enviar dados para o destino, bem como a frequência de envio de dados para o destino.

   >[!IMPORTANT]
   >
   >Para destinos sociais, você deve selecionar a origem de sua audiência nesta etapa. Você pode prosseguir para a próxima etapa somente depois de selecionar uma das opções na imagem abaixo.

   ![escolher origem de dados](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. Na **[!UICONTROL Review]** página, você pode ver um resumo de sua seleção. Selecione **[!UICONTROL Cancel]** para dividir o fluxo, **[!UICONTROL Back]** para modificar suas configurações ou **[!UICONTROL Finish]** para confirmar sua seleção e start enviando dados para o destino.

![confirmação de seleção](/help/rtcdp/destinations/assets/confirm-selection.png)

## Editar ativação {#edit-activation}

Siga as etapas abaixo para editar os fluxos de ativação existentes na CDP em tempo real:

1. Selecione **[!UICONTROL Destinations]** na barra de navegação esquerda, clique na **[!UICONTROL Browse]** guia e clique no nome de destino.
2. Selecione **[!UICONTROL Edit activation]** no painel direito para alterar quais segmentos enviar para o destino.

## Verificar se a ativação de segmentos foi bem-sucedida {#verify-activation}

### Destinos de marketing por email e destinos de armazenamentos na nuvem

Para destinos de marketing por email e destinos de armazenamentos na nuvem, o Adobe Real-time CDP cria um arquivo delimitado por tabulação `.txt` ou `.csv` no local do armazenamento fornecido. Espera que um novo arquivo seja criado no local do armazenamento todos os dias. The file format is:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

Os arquivos que você receberia em três dias consecutivos podem ter a seguinte aparência:

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

A presença desses arquivos no local do seu armazenamento é a confirmação da ativação bem-sucedida.

### Destinos de publicidade

Verifique o destino de anúncio respectivo para o qual você está ativando seus dados. Se a ativação tiver sido bem-sucedida, as audiências serão preenchidas em sua plataforma de publicidade.

### Destinos da rede social

Para o Facebook, uma ativação bem-sucedida significa que uma audiência personalizada do Facebook seria criada programaticamente no Gerenciador [de anúncios do](https://www.facebook.com/adsmanager/manage/)Facebook. A associação de segmento na audiência seria adicionada e removida, pois os usuários são qualificados ou desqualificados para os segmentos ativados.

## Desativar ativação {#disable-activation}

Para desativar um fluxo de ativação existente, siga as etapas abaixo:

1. Selecione **[!UICONTROL Destinations]** na barra de navegação esquerda, clique na **[!UICONTROL Browse]** guia e clique no nome de destino.
2. Clique no **[!UICONTROL Enabled]** controle no painel direito para alterar o estado do fluxo da ativação.
3. Na janela **Atualizar estado** do fluxo de dados, selecione **Confirmar** para desativar o fluxo de ativação.

