---
keywords: ativar destinos de perfil; ativar destinos; ativar dados; ativar destinos de marketing por email; ativar destinos de armazenamento na nuvem
title: Ativar dados do público-alvo para destinos de exportação de perfil de fluxo
type: Tutorial
seo-title: Activate audience data to streaming profile export destinations
description: Saiba como ativar os dados de público-alvo que você tem no Adobe Experience Platform, enviando segmentos para destinos com base em perfil de transmissão.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by sending segments to streaming profile-based destinations.
source-git-commit: d13920250fafd2ba4ff37dd5d4a45d417ed3ecc7
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Ativar dados do público-alvo para destinos de exportação de perfil de fluxo

## Visão geral {#overview}

Este artigo explica o fluxo de trabalho necessário para ativar dados do público-alvo em destinos baseados em perfil do Adobe Experience Platform streaming, como o Amazon Kinesis.

## Pré-requisitos {#prerequisites}

Para ativar dados em destinos, você deve ter [conectado com êxito a um destino](./connect-destination.md). Se ainda não tiver feito isso, vá para o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar.

## Selecione o destino {#select-destination}

1. Vá para **[!UICONTROL Connections > Destinations]** e selecione a guia **[!UICONTROL Catalog]**.

   ![Guia Catálogo de destino](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Selecione **[!UICONTROL Ativar segmentos]** no cartão correspondente ao destino onde deseja ativar seus segmentos, conforme mostrado na imagem abaixo.

   ![Botão Ativar segmentos](../assets/ui/activate-streaming-profile-destinations/activate-segments-button.png)

1. Selecione a conexão de destino que deseja usar para ativar seus segmentos e selecione **[!UICONTROL Next]**.

   ![Selecionar destino](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Mova para a próxima seção para [selecionar seus segmentos](#select-segments).

## Selecione seus segmentos {#select-segments}

Use as caixas de seleção à esquerda dos nomes de segmentos para selecionar os segmentos que deseja ativar para o destino e selecione **[!UICONTROL Next]**.

![Selecionar segmentos](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## Selecionar atributos de perfil {#select-attributes}

Selecione os atributos de perfil que deseja enviar para o destino.

>[!NOTE]
>
> O Adobe Experience Platform preenche sua seleção com quatro atributos recomendados e comumente usados do esquema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

As exportações de arquivo variam das seguintes maneiras, dependendo se `segmentMembership.status` estiver selecionado:
* Se o campo `segmentMembership.status` for selecionado, os arquivos exportados incluirão **[!UICONTROL membros Ativos]** no instantâneo completo inicial e **[!UICONTROL membros Ativos]** e **[!UICONTROL Expirados]** nas exportações incrementais subsequentes.
* Se o campo `segmentMembership.status` não estiver selecionado, os arquivos exportados incluirão apenas **[!UICONTROL membros Ativos]** no instantâneo completo inicial e nas exportações incrementais subsequentes.

![atributos recomendados](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. Na página **[!UICONTROL Selecionar atributos]**, selecione **[!UICONTROL Adicionar novo campo]**.

   ![Adicionar novo mapeamento](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Selecione a seta à direita da entrada **[!UICONTROL Schema field]**.

   ![Selecionar campo de origem](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. Na página **[!UICONTROL Select field]**, selecione os atributos XDM que deseja enviar para o destino e escolha **[!UICONTROL Select]**.

   ![Página Selecionar campo de origem](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. Para adicionar mais mapeamentos, repita as etapas de 1 a 3 e selecione **[!UICONTROL Next]**.

## Revisão {#review}

Na página **[!UICONTROL Revisar]**, você pode ver um resumo da sua seleção. Selecione **[!UICONTROL Cancelar]** para quebrar o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações ou **[!UICONTROL Concluir]** para confirmar sua seleção e começar a enviar dados para o destino.

>[!IMPORTANT]
>
>Nesta etapa, o Adobe Experience Platform verifica violações da política de uso de dados. Veja abaixo um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho de ativação de segmento até que você tenha resolvido a violação. Para obter informações sobre como resolver violações de política, consulte [Aplicação de política](../../rtcdp/privacy/data-governance-overview.md#enforcement) na seção Documentação de governança de dados.

![violação da política de dados](../assets/common/data-policy-violation.png)

Se nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Finish]** para confirmar a seleção e iniciar o envio de dados para o destino.

![Revisão](../assets/ui/activate-streaming-profile-destinations/review.png)

## Verificar ativação de segmento {#verify}

Os dados [!DNL Experience Platform] exportados chegam ao destino no formato JSON. Por exemplo, o evento abaixo contém o atributo de perfil de endereço de email de um público que se qualificou para um determinado segmento e saiu de outro. As identidades desse prospecto são ECID e email.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
