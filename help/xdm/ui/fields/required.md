---
keywords: Experience Platform; home; tópicos populares; api; API; XDM; sistema XDM; modelo de dados de experiência; modelo de dados; ui; espaço de trabalho; obrigatório; campo;
title: Definir campos obrigatórios na interface do usuário
description: Saiba como definir um campo XDM necessário na interface do usuário do Experience Platform.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: 11dcb1a824020a5b803621025863e95539ab4d71
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Definir campos obrigatórios na interface do usuário

No Experience Data Model (XDM), um campo obrigatório indica que ele deve receber um valor válido para que um registro ou evento de série de tempo específico seja aceito durante a assimilação de dados. Casos de uso comuns para campos obrigatórios incluem informações de identidade do usuário e carimbos de data e hora.

>[!IMPORTANT]
>
>Independentemente de um campo de esquema ser obrigatório ou não, a Platform não aceita `null` ou valores vazios para qualquer campo assimilado. Se não houver valor para um campo específico em um registro ou evento, a chave desse campo deverá ser excluída do payload de assimilação.

When [definição de um novo campo](./overview.md#define) na interface do usuário do Adobe Experience Platform, é possível defini-lo como um campo obrigatório selecionando o **[!UICONTROL Obrigatório]** caixa de seleção no painel direito. Selecionar **[!UICONTROL Aplicar]** para aplicar a alteração ao schema.

![Caixa de seleção necessária](../../images/ui/fields/required/root.png)

Se o campo for um atributo de nível raiz sob o objeto de ID do locatário, seu caminho aparecerá imediatamente em **[!UICONTROL Campos obrigatórios]** no painel esquerdo.

![Campo obrigatório de nível raiz](../../images/ui/fields/required/applied.png)

Se um campo obrigatório estiver aninhado dentro de um objeto que não esteja marcado como necessário, no entanto, o campo aninhado não aparecerá em **[!UICONTROL Campos obrigatórios]** no painel esquerdo.

No exemplo abaixo, a variável `loyaltyId` for definido conforme necessário, mas seu objeto pai `loyalty` não é. Nesse caso, nenhum erro de validação ocorreria se `loyalty` foi excluído ao assimilar dados, mesmo que o campo filho `loyaltyId` estiver marcada conforme necessário. Em outras palavras, enquanto `loyalty` é opcional, deve conter um `loyaltyId` no caso de inclusão.

![Campo obrigatório aninhado](../../images/ui/fields/required/nested.png)

Se quiser que um campo aninhado sempre seja obrigatório em um schema, também deverá definir todos os campos pai, conforme necessário (com exceção do objeto de ID do locatário).

![Campos obrigatórios pai e filho](../../images/ui/fields/required/parent-and-child.png)

## Próximas etapas

Este guia abordou como definir um campo obrigatório na interface do usuário do . Consulte a visão geral em [definição de campos na interface do usuário](./overview.md#special) para saber como definir outros tipos de campo XDM na variável [!DNL Schema Editor].
