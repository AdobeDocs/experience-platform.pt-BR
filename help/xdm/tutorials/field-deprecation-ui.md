---
title: Descontinuar um campo XDM na interface do usuário
description: Saiba como descontinuar os campos do Experience Data Model (XDM) usando o Editor de esquema no Experience Platform.
source-git-commit: f791d32ae38dffe82723800aa9fb5b44bb4f0109
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Descontinuar um campo XDM na interface do usuário

O Experience Data Model (XDM) oferece a flexibilidade para gerenciar o modelo de dados conforme as necessidades da empresa mudam, descontinuando os campos do esquema depois que os dados são assimilados. Campos indesejados podem ser descontinuados para removê-los da exibição da interface do usuário e também ocultá-los das interfaces do usuário downstream. Por conveniência, uma caixa de seleção no Editor de esquemas permite exibir campos obsoletos e, se necessário, também é possível descontinuá-los.

Como os campos obsoletos estão ocultos da interface do usuário por padrão, isso simplifica o esquema no Editor de esquemas e impede que campos indesejados sejam adicionados às dependências downstream, como o construtor de segmentos, o designer do jornada e assim por diante. A desativação do campo também é compatível com versões anteriores. Outros sistemas que usam campos obsoletos, como segmentos e consultas, continuarão a avaliá-los conforme esperado. Se um campo obsoleto for usado em um segmento existente, ele será tratado normalmente, o que significa que o campo será exibido como esperado na tela do construtor de segmentos ou será avaliado com base em quaisquer dados disponíveis nos campos obsoletos. Essa é uma alteração sem quebra que não afeta negativamente nenhum fluxo de dados existente.

>[!NOTE]
>
>Antes de os dados serem assimilados em um schema, é possível remover grupos de campos desnecessários. Consulte a documentação em [como remover um grupo de campos de um schema](../ui/resources/schemas.md#remove-fields) para obter mais informações.

Depois que os dados forem assimilados no esquema, não será mais possível remover os campos do esquema sem fazer alterações. Nesse caso, é possível descontinuar um campo indesejado em um esquema ou recurso personalizado usando o [Editor de esquema](./create-schema-ui.md) ou [API do Registro de Schema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Este documento aborda como descontinuar campos para diferentes recursos do XDM usando o Editor de esquemas na interface do usuário do Experience Platform. Para obter etapas sobre como descontinuar um campo XDM usando a API, consulte o tutorial em [descontinuar um campo XDM usando a API do Registro de Schema](./field-deprecation-api.md).

## Descontinuar um campo {#deprecate}

Para descontinuar um campo personalizado, navegue até o Editor de esquema do esquema que deseja editar. Selecione o campo que deseja descontinuar do [!UICONTROL Estrutura] seção da tela, seguida de **[!UICONTROL Substituir]** do [!UICONTROL Propriedades do campo].

![O editor de Esquema com um campo selecionado e Substituir destacado.](../images/tutorials/field-deprecation/deprecate-single-field.png)

Uma caixa de diálogo é exibida para confirmar suas opções e notificar que o campo será removido da visualização da interface do usuário do esquema de união e oculto das interfaces do usuário downstream. Para concluir a ação, selecione **[!UICONTROL Confirmar]**.

![A caixa de diálogo Descontinuar campo com Confirmar destacado.](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

O campo agora é removido da exibição da interface do usuário.

>[!NOTE]
>
>Depois de obsoletas, as interfaces do usuário downstream, como painéis de Segmentação, Customer Journey Analytics e Adobe Journey Optimizer, não exibem mais campos obsoletos como parte de seu fluxo de trabalho. No entanto, as interfaces de usuário downstream têm a opção de mostrar campos obsoletos, se necessário, e continuar a tratar o campo obsoleto como normal. Consulte a respectiva documentação para obter mais informações. As consultas e segmentos que usam o campo obsoleto continuarão a ser executadas conforme esperado.

## Mostrar campos obsoletos {#show-deprecated}

Para exibir campos anteriormente obsoletos, navegue até o schema relevante no Editor de esquemas. Selecione o **[!UICONTROL Mostrar campos obsoletos]** na caixa de seleção [!UICONTROL Composição] da tela.

O campo obsoleto agora aparece na exibição da interface do usuário. Selecionar **[!UICONTROL Salvar]** para confirmar as configurações.

![O Editor de esquemas com um campo selecionado, Mostrar campos obsoletos e Salvar realçado.](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## Descontinuar campos {#undeprecate-fields}

Para desfazer um campo obsoleto, primeiro [exibir o campo obsoleto](#show-deprecated) como descrito acima, selecione o campo obsoleto no editor [!UICONTROL Estrutura] seção. Em seguida, selecione **[!UICONTROL Descontinuar]** do [!UICONTROL Propriedades do campo] barra lateral seguida de **[!UICONTROL Salvar]**.

![O Editor de esquemas com o campo obsoleto, Substituir e Salvar são realçados.](../images/tutorials/field-deprecation/undeprecate-single-field.png)

O [!UICONTROL Descontinuar campo] será exibida. Para confirmar as alterações, selecione **[!UICONTROL Confirmar]**.

![O [!UICONTROL Descontinuar campo] com Confirmar destacado.](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

O campo agora é exibido como padrão na exibição da interface do usuário e também nas interfaces do usuário downstream. Novamente, agora há a opção de descontinuar o campo.

## Próximas etapas

Este documento cobriu como descontinuar campos XDM usando a interface do Editor de esquemas. Para obter mais informações sobre como configurar campos para recursos personalizados, consulte o guia sobre [definição de campos XDM na API](./custom-fields-api.md). Para obter mais informações sobre o gerenciamento de descritores, consulte o [guia do endpoint de descritores](../api/descriptors.md).
