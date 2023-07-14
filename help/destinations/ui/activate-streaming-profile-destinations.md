---
keywords: ativar destinos de perfil;ativar destinos;ativar dados; ativar destinos de marketing por email; ativar destinos de armazenamento na nuvem
title: Ativar públicos para destinos de exportação de perfil de transmissão
type: Tutorial
description: Saiba como ativar os dados de público-alvo no Adobe Experience Platform enviando públicos-alvo para destinos com base em perfil de transmissão.
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 37819b5a6480923686d327e30b1111ea29ae71da
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 5%

---


# Ativar públicos para destinos de exportação de perfil de transmissão

>[!IMPORTANT]
> 
> * Para ativar os dados e habilitar a [etapa de mapeamento](#mapping) do fluxo de trabalho, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions).
> * Para ativar os dados sem passar pelo [etapa de mapeamento](#mapping) do fluxo de trabalho, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar segmento sem mapeamento]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions).
> 
> Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

## Visão geral {#overview}

Este artigo explica o fluxo de trabalho necessário para ativar dados de público-alvo em destinos baseados em perfil de transmissão do Adobe Experience Platform, como o Amazon Kinesis.

## Pré-requisitos {#prerequisites}

Para ativar dados para destinos, você deve ter o [conectado a um destino](./connect-destination.md). Se ainda não tiver feito isso, acesse o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar.

## Selecione seu destino {#select-destination}

1. Ir para **[!UICONTROL Conexões > Destinos]** e selecione a variável **[!UICONTROL Catálogo]** guia.

   ![Imagem mostrando a guia do catálogo de destino.](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Selecionar **[!UICONTROL Ativar públicos]** no cartão correspondente ao destino em que deseja ativar os públicos-alvo, conforme mostrado na imagem abaixo.

   ![Imagem destacando o controle ativar públicos-alvo na guia do catálogo de destinos.](../assets/ui/activate-streaming-profile-destinations/activate-audiences-button.png)

1. Selecione a conexão de destino que deseja usar para ativar os públicos-alvo e selecione **[!UICONTROL Próxima]**.

   ![Imagem que mostra uma seleção de dois destinos aos quais você pode se conectar.](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Mover para a próxima seção para [selecionar seus públicos](#select-audiences).

## Selecione seus públicos-alvo {#select-audiences}

Para selecionar os públicos que deseja ativar para o destino, use as caixas de seleção à esquerda dos nomes dos públicos e selecione **[!UICONTROL Próxima]**.

Você pode selecionar entre vários tipos de públicos-alvo, dependendo de sua origem:

* **[!UICONTROL Serviço de segmentação]**: públicos-alvo gerados no Experience Platform pelo serviço de segmentação. Consulte a [documentação de segmentação](../../segmentation/ui/overview.md) para obter mais detalhes.
* **[!UICONTROL Upload personalizado]**: públicos gerados fora do Experience Platform e carregados na Platform como arquivos CSV. Para saber mais sobre públicos-alvo externos, consulte a documentação em [importação de um público](../../segmentation/ui/overview.md#import-audience).
* Outros tipos de públicos-alvo, provenientes de outras soluções de Adobe, como [!DNL Audience Manager].

![Imagem destacando a seleção das caixas de seleção na etapa Selecionar públicos do fluxo de trabalho de ativação.](../assets/ui/activate-streaming-profile-destinations/select-audiences.png)

## Selecionar atributos de perfil {#select-attributes}

No **[!UICONTROL Mapeamento]** selecione os atributos de perfil que deseja enviar ao destino.

1. No **[!UICONTROL Selecionar atributos]** selecione **[!UICONTROL Adicionar novo campo]**.

   ![Imagem destacando o controle Adicionar novo campo na etapa de mapeamento.](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Selecione a seta à direita da **[!UICONTROL Campo de esquema]** entrada.

   ![Imagem que destaca como selecionar um campo de origem na etapa de mapeamento.](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. No **[!UICONTROL Selecionar campo]** selecione os atributos XDM que deseja enviar ao destino e escolha **[!UICONTROL Selecionar]**.

   ![Imagem mostrando uma seleção de campos XDM que você pode selecionar como campos de origem.](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)

1. Para adicionar mais campos, repita as etapas de 1 a 3 e selecione **[!UICONTROL Próxima]**.

## Consulte a seção {#review}

No **[!UICONTROL Revisão]** você poderá ver um resumo da sua seleção. Selecionar **[!UICONTROL Cancelar]** para interromper o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações ou **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

![Resumo da seleção na etapa de revisão.](../assets/ui/activate-streaming-profile-destinations/review.png)

### Avaliação de política de consentimento {#consent-policy-evaluation}

Se sua organização adquiriu o **Adobe Healthcare Shield** ou o **Adobe Privacy &amp; Security Shield**, selecione **[!UICONTROL Exibir políticas de consentimento aplicáveis]** para ver quais políticas de consentimento são aplicadas e quantos perfis são incluídos na ativação como resultado delas. Ler sobre [avaliação da política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para obter mais informações.

### Verificações de política de uso de dados {#data-usage-policy-checks}

No **[!UICONTROL Revisão]** etapa, o Experience Platform também verifica se há violações de política de uso de dados. Veja abaixo um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho de ativação de público-alvo até que a violação seja resolvida. Para obter informações sobre como resolver violações de política, leia sobre [violações de política de uso de dados](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) na seção documentação de governança de dados.

![violação da política de dados](../assets/common/data-policy-violation.png)

### Filtrar públicos {#filter-audiences}

Também nesta etapa é possível usar os filtros disponíveis na página para exibir somente os públicos-alvo cujo agendamento ou mapeamento foi atualizado como parte desse fluxo de trabalho.

![Gravação de tela mostrando os filtros de público-alvo disponíveis na etapa de revisão.](../assets/ui/activate-streaming-profile-destinations/filter-audiences-review-step.gif)

Se estiver satisfeito com a sua seleção e nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

## Verificar ativação de público {#verify}

Seu exportado [!DNL Experience Platform] Os dados do chegam ao destino no formato JSON. Por exemplo, o evento abaixo contém o atributo de endereço de email de um perfil que se qualificou para um determinado público-alvo e saiu de outro. As identidades deste cliente potencial são `ECID` e `email_lc_sha256`.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
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
