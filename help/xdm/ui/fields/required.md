---
keywords: Experience Platform; home; tópicos populares; api; API; XDM; sistema XDM; modelo de dados de experiência; modelo de dados; ui; espaço de trabalho; obrigatório; campo;
solution: Experience Platform
title: Definir campos obrigatórios na interface do usuário
description: Saiba como definir um campo XDM necessário na interface do usuário do Experience Platform.
topic-legacy: user guide
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# Definir campos obrigatórios na interface do usuário

No Experience Data Model (XDM), um campo obrigatório indica que ele deve receber um valor válido para que um registro ou evento de série de tempo específico seja aceito durante a assimilação de dados. Casos de uso comuns para campos obrigatórios incluem informações de identidade do usuário e carimbos de data e hora.

Ao [definir um novo campo](./overview.md#define) na interface do usuário do Adobe Experience Platform, você pode defini-lo como um campo obrigatório marcando a caixa de seleção **[!UICONTROL Required]** no painel direito. Selecione **[!UICONTROL Apply]** para aplicar a alteração ao schema.

![](../../images/ui/fields/special/required.png)

Depois que o campo é aplicado, seu caminho aparece em **[!UICONTROL Required fields]** no painel esquerdo. Se o campo estiver aninhado, quaisquer campos pai também aparecerão conforme necessário.

![](../../images/ui/fields/special/required-applied.png)

## Próximas etapas

Este guia abordou como definir um campo obrigatório na interface do usuário do . Consulte a visão geral em [definindo campos na interface do usuário](./overview.md#special) para saber como definir outros tipos de campos XDM no [!DNL Schema Editor].
