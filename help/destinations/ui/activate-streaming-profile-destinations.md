---
keywords: ativar destinos de perfil;ativar destinos;ativar dados; ativar destinos de marketing por email; ativar destinos de armazenamento na nuvem
title: Ativar dados do público-alvo para destinos de exportação de perfil de transmissão
type: Tutorial
description: Saiba como ativar os dados de público-alvo no Adobe Experience Platform enviando segmentos para destinos com base em perfil de transmissão.
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 9bde403338187409892d76de68805535de03d59f
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# Ativar dados do público-alvo para destinos de exportação de perfil de transmissão

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

## Visão geral {#overview}

Este artigo explica o fluxo de trabalho necessário para ativar dados de público-alvo em destinos baseados em perfil de transmissão do Adobe Experience Platform, como o Amazon Kinesis.

## Pré-requisitos {#prerequisites}

Para ativar dados para destinos, você deve ter o [conectado a um destino](./connect-destination.md). Se ainda não tiver feito isso, acesse o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar.

## Selecione seu destino {#select-destination}

1. Ir para **[!UICONTROL Conexões > Destinos]** e selecione a variável **[!UICONTROL Catálogo]** guia.

   ![Imagem mostrando a guia do catálogo de destino.](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Selecionar **[!UICONTROL Ativar segmentos]** no cartão correspondente ao destino em que deseja ativar os segmentos, conforme mostrado na imagem abaixo.

   ![Imagem destacando o controle ativar segmentos na guia do catálogo de destinos.](../assets/ui/activate-streaming-profile-destinations/activate-segments-button.png)

1. Selecione a conexão de destino que deseja usar para ativar seus segmentos e selecione **[!UICONTROL Próxima]**.

   ![Imagem que mostra uma seleção de dois destinos aos quais você pode se conectar.](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Mover para a próxima seção para [selecionar os segmentos](#select-segments).

## Selecionar seus segmentos {#select-segments}

Use as caixas de seleção à esquerda dos nomes de segmento para selecionar os segmentos que você deseja ativar para o destino e, em seguida, selecione **[!UICONTROL Próxima]**.

![Imagem destacando a seleção das caixas de seleção na etapa Selecionar segmentos do fluxo de trabalho de ativação.](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## Selecionar atributos de perfil {#select-attributes}

No **[!UICONTROL Mapeamento]** selecione os atributos de perfil que deseja enviar ao destino.

>[!NOTE]
>
> O Adobe Experience Platform preenche sua seleção com quatro atributos recomendados, usados com frequência a partir do esquema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

As exportações de arquivos variam das seguintes maneiras, dependendo se `segmentMembership.status` está selecionado:
* Se a variável `segmentMembership.status` for selecionado, os arquivos exportados incluirão **[!UICONTROL Ativo]** membros no instantâneo completo inicial e **[!UICONTROL Ativo]** e **[!UICONTROL Expirado]** membros em exportações incrementais subsequentes.
* Se a variável `segmentMembership.status` não estiver selecionado, os arquivos exportados incluirão apenas **[!UICONTROL Ativo]** membros no instantâneo completo inicial e em exportações incrementais subsequentes.

![Imagem mostrando os atributos pré-preenchidos e recomendados na etapa de mapeamento.](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. No **[!UICONTROL Selecionar atributos]** selecione **[!UICONTROL Adicionar novo campo]**.

   ![Imagem destacando o controle Adicionar novo campo na etapa de mapeamento.](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Selecione a seta à direita da **[!UICONTROL Campo de esquema]** entrada.

   ![Imagem que destaca como selecionar um campo de origem na etapa de mapeamento.](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. No **[!UICONTROL Selecionar campo]** selecione os atributos XDM que deseja enviar ao destino e escolha **[!UICONTROL Selecionar]**.

   ![Imagem mostrando uma seleção de campos XDM que você pode selecionar como campos de origem.](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. Para adicionar mais mapeamentos, repita as etapas de 1 a 3 e selecione **[!UICONTROL Próxima]**.

## Consulte a seção {#review}

No **[!UICONTROL Revisão]** você poderá ver um resumo da sua seleção. Selecionar **[!UICONTROL Cancelar]** para interromper o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações ou **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

![Resumo da seleção na etapa de revisão.](/help/destinations/assets/ui/activate-streaming-profile-destinations/review.png)

### Avaliação de política de consentimento {#consent-policy-evaluation}

Se sua organização comprou **Adobe Healthcare Shield** ou **Proteção de segurança e privacidade do Adobe**, selecione **[!UICONTROL Exibir políticas de consentimento aplicáveis]** para ver quais políticas de consentimento são aplicadas e quantos perfis são incluídos na ativação como resultado delas. Ler sobre [avaliação da política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para obter mais informações.

### Verificações de política de uso de dados {#data-usage-policy-checks}

No **[!UICONTROL Revisão]** etapa, o Experience Platform também verifica se há violações de política de uso de dados. Veja abaixo um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho de ativação de segmento até que a violação seja resolvida. Para obter informações sobre como resolver violações de política, leia sobre [violações de política de uso de dados](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) na seção documentação de governança de dados.

![violação da política de dados](../assets/common/data-policy-violation.png)

### Filtrar segmentos {#filter-segments}

Também nesta etapa é possível usar os filtros disponíveis na página para exibir apenas os segmentos cujo agendamento ou mapeamento foi atualizado como parte desse fluxo de trabalho.

![Gravação de tela mostrando os filtros de segmento disponíveis na etapa de revisão.](/help/destinations/assets/ui/activate-streaming-profile-destinations/filter-segments-review-step.gif)

Se estiver satisfeito com a sua seleção e nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

## Verificar ativação de segmento {#verify}

Seu exportado [!DNL Experience Platform] Os dados do chegam ao destino no formato JSON. Por exemplo, o evento abaixo contém o atributo de perfil de endereço de email de um público-alvo que se qualificou para um determinado segmento e saiu de outro. As identidades desse cliente potencial são ECID e email.

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
