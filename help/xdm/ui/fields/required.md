---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados;ui;espaço de trabalho;obrigatório;campo;
title: Definir campos obrigatórios na interface
description: Saiba como definir um campo XDM necessário na interface do usuário do Experience Platform.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Definir campos obrigatórios na interface

No Experience Data Model (XDM), um campo obrigatório indica que ele deve receber um valor válido para que um registro ou evento de série temporal específico seja aceito durante a assimilação de dados. Casos de uso comuns para campos obrigatórios incluem informações de identidade do usuário e carimbos de data e hora.

>[!IMPORTANT]
>
>Independentemente de um campo de esquema ser obrigatório ou não, a Experience Platform não aceita `null` ou valores vazios para qualquer campo assimilado. Se não houver valor para um campo específico em um registro ou evento, a chave desse campo deverá ser excluída da carga de assimilação.

Ao [definir um novo campo](./overview.md#define) na interface do usuário do Adobe Experience Platform, você pode defini-lo como um campo obrigatório marcando a caixa de seleção **[!UICONTROL Obrigatório]** no painel direito. Selecione **[!UICONTROL Aplicar]** para aplicar a alteração ao esquema.

![Caixa de seleção necessária](../../images/ui/fields/required/root.png)

Se o campo for um atributo de nível raiz sob o objeto de ID do locatário, seu caminho aparecerá imediatamente em **[!UICONTROL Campos obrigatórios]** no painel esquerdo.

![Campo obrigatório de nível raiz](../../images/ui/fields/required/applied.png)

No entanto, se um campo obrigatório estiver aninhado em um objeto que não esteja marcado como obrigatório, o campo aninhado não aparecerá em **[!UICONTROL Campos obrigatórios]** no painel esquerdo.

No exemplo abaixo, o campo `internalSKU` está definido como obrigatório, mas seu objeto pai `SKUs` não está. Nesse caso, nenhum erro de validação ocorrerá se `SKUs` for excluído ao assimilar dados, mesmo que o campo filho `internalSKU` esteja marcado como obrigatório. Em outras palavras, embora `SKUs` seja opcional, ele deve conter um campo `internalSKU` caso seja incluído.

![Campo obrigatório aninhado](../../images/ui/fields/required/nested.png)

Se quiser que um campo aninhado seja sempre obrigatório em um esquema, também deverá definir todos os campos pais conforme necessário (com exceção do objeto de ID do locatário).

![Campos obrigatórios pai e filho](../../images/ui/fields/required/parent-and-child.png)

## Próximas etapas

Este guia abordou como definir um campo obrigatório na interface do usuário do. Consulte a visão geral em [definindo campos na interface](./overview.md#special) para saber como definir outros tipos de campos XDM no [!DNL Schema Editor].
