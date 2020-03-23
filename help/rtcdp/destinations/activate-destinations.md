---
title: Ativar perfis e segmentos em um destino
seo-title: Ativar perfis e segmentos em um destino
description: Ative os dados que você tem na Plataforma de dados do cliente em tempo real da Adobe mapeando segmentos para destinos. Para fazer isso, siga as etapas abaixo.
seo-description: Ative os dados que você tem na Plataforma de dados do cliente em tempo real da Adobe mapeando segmentos para destinos. Para fazer isso, siga as etapas abaixo.
translation-type: tm+mt
source-git-commit: 73925aa59f9981d8945fb0be6c4924e1831cf902

---


# Ativar perfis e segmentos em um destino

Ative os dados que você tem na Plataforma de dados do cliente em tempo real da Adobe mapeando segmentos para destinos. Para fazer isso, siga as etapas abaixo.

## Pré-requisitos {#prerequisites}

Para ativar os dados para destinos, você deve ter [conectado com êxito um destino](/help/rtcdp/destinations/assets/connect-destination.png). Caso ainda não o tenha feito, vá para o catálogo [de](/help/rtcdp/destinations/destinations-catalog.md)destinos, navegue nos destinos suportados e configure um ou mais destinos.

## Ativar dados {#activate-data}

1. Em **Destinos > Procurar**, selecione o destino onde deseja ativar seus segmentos.
2. Clique no nome do destino. Isso leva você ao fluxo Ativar.
   ![ativar-fluxo](/help/rtcdp/destinations/assets/activate-flow.png)Observe que se já existir um fluxo de ativação para um destino, você poderá ver os segmentos que estão sendo enviados para o destino. Selecione **Editar ativação** no painel direito e siga as etapas abaixo para modificar os detalhes de ativação.
3. Selecione **Ativar**;
4. Em **Ativar o assistente de destino** , na página **Selecionar segmentos** , selecione quais segmentos enviar para o destino.
   ![segmentos para destino](/help/rtcdp/destinations/assets/select-segments.png)
5. *Condicional*. Esta etapa se aplica somente aos segmentos mapeados para destinos de marketing de email. <br> Na página Atributos **de** destino, selecione **Adicionar novo campo** e selecione os atributos que deseja enviar para o destino.
Recomendamos que um dos atributos seja um identificador [](/help/rtcdp/destinations/email-marketing-destinations.md#identity) exclusivo do esquema de união. Para obter mais informações sobre atributos obrigatórios, consulte Identidade no artigo Destinos [de marketing de](/help/rtcdp/destinations/email-marketing-destinations.md#identity) email.
   ![atributos de destino](/help/rtcdp/destinations/assets/destination-attributes.png)
6. Na página **Agendar** , é possível visualizar a data de início para o envio de dados para o destino, bem como a frequência do envio de dados para o destino.
7. Na página **Revisar** , você pode ver um resumo de sua seleção. Selecione **Cancelar** para quebrar o fluxo, **Voltar** para modificar suas configurações ou **Concluir** para confirmar sua seleção e começar a enviar dados para o destino.

![confirmação de seleção](/help/rtcdp/destinations/assets/confirm-selection.png)

## Editar ativação {#edit-activation}

Siga as etapas abaixo para editar os fluxos de ativação existentes no CDP em tempo real:

1. Selecione **Destinos** na barra de navegação esquerda, clique na guia **Procurar** e clique no nome de destino.
2. Selecione **[!UICONTROL Edit activation]** no painel direito para alterar quais segmentos enviar para o destino.

## Verificar se a ativação do segmento foi bem-sucedida {#verify-activation}

### Destinos de marketing por email e destinos de armazenamento em nuvem

Para destinos de marketing por email e destinos de armazenamento em nuvem, o Adobe Real-time CDP cria um arquivo delimitado por tabulação `.txt` ou `.csv` no local de armazenamento fornecido. Espera que um novo arquivo seja criado em seu local de armazenamento todos os dias. The file format is:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

Os arquivos que você receberia em três dias consecutivos podem ter a seguinte aparência:

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

A presença desses arquivos no local de armazenamento é a confirmação da ativação bem-sucedida.

### Destinos de publicidade

Verifique o destino de anúncio respectivo para o qual você está ativando seus dados. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos na plataforma de publicidade.

## Desativar ativação {#disable-activation}

Para desativar um fluxo de ativação existente, siga as etapas abaixo:

1. Selecione **Destinos** na barra de navegação esquerda, clique na guia **Procurar** e clique no nome de destino.
2. Clique no **[!UICONTROL Enabled]** controle no painel direito para alterar o estado do fluxo de ativação.
3. Na janela **Atualizar estado** do fluxo de dados, selecione **Confirmar** para desativar o fluxo de ativação.

