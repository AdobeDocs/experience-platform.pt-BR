---
keywords: Experience Platform; home; tópicos populares; api; API; XDM; sistema XDM; modelo de dados de experiência; modelo de dados; ui; espaço de trabalho; obrigatório; campo;
title: Definir campos obrigatórios na interface do usuário
description: Saiba como definir um campo XDM necessário na interface do usuário do Experience Platform.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: 1d04bf56c51506f84c5156e6d2ed6c9f58f15235
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Definir campos obrigatórios na interface do usuário

No Experience Data Model (XDM), um campo obrigatório indica que ele deve receber um valor válido para que um registro ou evento de série de tempo específico seja aceito durante a assimilação de dados. Casos de uso comuns para campos obrigatórios incluem informações de identidade do usuário e carimbos de data e hora.

Ao [definir um novo campo](./overview.md#define) na interface do usuário do Adobe Experience Platform, você pode defini-lo como um campo obrigatório marcando a caixa de seleção **[!UICONTROL Required]** no painel direito. Selecione **[!UICONTROL Aplicar]** para aplicar a alteração ao esquema.

![Caixa de seleção necessária](../../images/ui/fields/required/root.png)

Se o campo for um atributo de nível raiz sob o objeto de ID do locatário, seu caminho aparecerá imediatamente em **[!UICONTROL Required fields]** no painel à esquerda.

![Campo obrigatório de nível raiz](../../images/ui/fields/required/applied.png)

No entanto, se um campo obrigatório estiver aninhado dentro de um objeto que não esteja marcado como necessário, o campo aninhado não aparecerá em **[!UICONTROL Campos obrigatórios]** no painel esquerdo.

No exemplo abaixo, o campo `loyaltyId` é definido conforme necessário, mas seu objeto pai `loyalty` não é. Nesse caso, nenhum erro de validação ocorreria se `loyalty` fosse excluído ao assimilar dados, mesmo que o campo filho `loyaltyId` estivesse marcado conforme necessário. Em outras palavras, embora `loyalty` seja opcional, ele deve conter um campo `loyaltyId` no caso de ser incluído.

![Campo obrigatório aninhado](../../images/ui/fields/required/nested.png)

Se quiser que um campo aninhado sempre seja obrigatório em um schema, também deverá definir todos os campos pai, conforme necessário (com exceção do objeto de ID do locatário).

![Campos obrigatórios pai e filho](../../images/ui/fields/required/parent-and-child.png)

## Próximas etapas

Este guia abordou como definir um campo obrigatório na interface do usuário do . Consulte a visão geral em [definindo campos na interface do usuário](./overview.md#special) para saber como definir outros tipos de campos XDM no [!DNL Schema Editor].
