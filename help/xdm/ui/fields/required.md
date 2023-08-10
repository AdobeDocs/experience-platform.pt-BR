---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados;iu;espaço de trabalho;obrigatório;campo;
title: Definir campos obrigatórios na interface
description: Saiba como definir um campo XDM necessário na interface do usuário do Experience Platform.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Definir campos obrigatórios na interface

No Experience Data Model (XDM), um campo obrigatório indica que ele deve receber um valor válido para que um registro ou evento de série temporal específico seja aceito durante a assimilação de dados. Casos de uso comuns para campos obrigatórios incluem informações de identidade do usuário e carimbos de data e hora.

>[!IMPORTANT]
>
>Independentemente de um campo de esquema ser obrigatório ou não, a Platform não aceita `null` ou valores vazios para qualquer campo assimilado. Se não houver valor para um campo específico em um registro ou evento, a chave desse campo deverá ser excluída da carga de assimilação.

Quando [definição de um novo campo](./overview.md#define) na interface do usuário do Adobe Experience Platform, é possível defini-lo como um campo obrigatório selecionando o **[!UICONTROL Obrigatório]** no painel direito. Selecionar **[!UICONTROL Aplicar]** para aplicar a alteração ao esquema.

![Caixa de seleção Obrigatória](../../images/ui/fields/required/root.png)

Se o campo for um atributo de nível raiz sob o objeto de ID do locatário, seu caminho aparecerá imediatamente em **[!UICONTROL Campos obrigatórios]** no painel esquerdo.

![Campo obrigatório de nível raiz](../../images/ui/fields/required/applied.png)

No entanto, se um campo obrigatório estiver aninhado em um objeto que não esteja marcado como obrigatório, o campo aninhado não aparecerá em **[!UICONTROL Campos obrigatórios]** no painel esquerdo.

No exemplo abaixo, a variável `internalSKU` o campo é definido como obrigatório, mas seu objeto principal `SKUs` não é. Nesse caso, não ocorreriam erros de validação se `SKUs` é excluído ao assimilar dados, mesmo que o campo filho `internalSKU` está marcado como obrigatório. Por outras palavras, `SKUs` é opcional e deve conter um `internalSKU` caso seja incluído.

![Campo obrigatório aninhado](../../images/ui/fields/required/nested.png)

Se quiser que um campo aninhado seja sempre obrigatório em um esquema, também deverá definir todos os campos pais conforme necessário (com exceção do objeto de ID do locatário).

![Campos obrigatórios pai e filho](../../images/ui/fields/required/parent-and-child.png)

## Próximas etapas

Este guia abordou como definir um campo obrigatório na interface do usuário do. Consulte a visão geral em [definição de campos na interface](./overview.md#special) para saber como definir outros tipos de campo XDM na variável [!DNL Schema Editor].
