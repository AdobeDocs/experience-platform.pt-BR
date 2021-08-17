---
keywords: ativar destinos de perfil; ativar destinos; ativar dados; ativar destinos de marketing por email; ativar destinos de armazenamento na nuvem
title: Ativar dados do público-alvo para destinos de exportação de perfil de fluxo
type: Tutorial
seo-title: Ativar dados do público-alvo para destinos de exportação de perfil de fluxo
description: Saiba como ativar os dados de público-alvo que você tem no Adobe Experience Platform, enviando segmentos para destinos com base em perfil de transmissão.
seo-description: Saiba como ativar os dados de público-alvo que você tem no Adobe Experience Platform, enviando segmentos para destinos com base em perfil de transmissão.
source-git-commit: 02c22453470d55236d4235c479742997e8407ef3
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# Ativar dados do público-alvo para destinos de exportação de perfil de fluxo

## Visão geral {#overview}

Este artigo explica o fluxo de trabalho necessário para ativar dados do público-alvo em destinos baseados em perfil do Adobe Experience Platform streaming, como o Amazon Kinesis.

## Pré-requisitos {#prerequisites}

Para ativar dados em destinos, você deve ter [conectado com êxito a um destino](./connect-destination.md). Se ainda não tiver feito isso, vá para o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar.

## Selecione o destino {#select-destination}

1. Vá para **[!UICONTROL Connections > Destinations]** e selecione a guia **[!UICONTROL Browse]**.

   ![Guia Navegação de destino](../assets/ui/activate-streaming-profile-destinations/browse-tab.png)

1. Selecione o botão **[!UICONTROL Add segments]** correspondente ao destino onde você deseja ativar seus segmentos, conforme mostrado na imagem abaixo.

   ![Botões Ativar](../assets/ui/activate-streaming-profile-destinations/activate-buttons-browse.png)

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


Para destinos de marketing por email e destinos de armazenamento na nuvem, o Adobe Experience Platform cria um arquivo `.csv` delimitado por tabulação no local de armazenamento fornecido. Espera que um novo arquivo seja criado no seu local de armazenamento todos os dias. O formato de arquivo padrão é:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

Os arquivos que você receberia em três dias consecutivos podem ter a seguinte aparência:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

A presença desses arquivos no local de armazenamento é a confirmação de uma ativação bem-sucedida. Para entender como os arquivos exportados são estruturados, você pode [baixar um arquivo .csv de amostra](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Este arquivo de amostra inclui os atributos de perfil `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear` e `personalEmail.address`.
