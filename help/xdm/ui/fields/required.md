---
keywords: Experience Platform;home;popular topics;api;API;XDM;sistema XDM;experimentar modelo de dados;modelo de dados;ui;espaço de trabalho;obrigatório;campo;
solution: Experience Platform
title: Definir um campo obrigatório na interface do usuário
description: Saiba como definir um campo XDM obrigatório na interface do usuário do Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 48025fc11558bf6773ce5c48054483758c7e993f
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 1%

---


# Definir um campo obrigatório na interface do usuário

No Modelo de Dados de Experiência (XDM), um campo obrigatório indica que ele deve receber um valor válido para que um registro ou evento de série cronológica específico seja aceito durante a ingestão de dados. Casos de uso comuns para campos obrigatórios incluem informações de identidade do usuário e carimbos de data e hora.

Quando [definir um novo campo](./overview.md#define) na interface do usuário do Adobe Experience Platform, você pode defini-lo como um campo obrigatório selecionando a caixa de seleção **[!UICONTROL Required]** no painel direito. Selecione **[!UICONTROL Aplicar]** para aplicar a alteração ao schema.

![](../../images/ui/fields/special/required.png)

Depois que o campo é aplicado, seu caminho aparece em **[!UICONTROL Campos obrigatórios]** no painel esquerdo. Se o campo estiver aninhado, quaisquer campos pais também aparecerão conforme necessário.

![](../../images/ui/fields/special/required-applied.png)

## Próximas etapas

Este guia aborda como definir um campo obrigatório na interface do usuário. Consulte a visão geral em [definindo campos na interface do usuário](./overview.md#special) para saber como definir outros tipos de campos XDM no [!DNL Schema Editor].