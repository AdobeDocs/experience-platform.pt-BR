---
title: Classe de perfil de cliente potencial individual XDM
description: Saiba mais sobre a classe Perfil de cliente potencial individual XDM no Experience Data Model (XDM).
exl-id: 10fd9d16-4123-4ad4-971f-b715231ee6a9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 3%

---

# [!UICONTROL Perfil de cliente potencial individual XDM] classe

No Experience Data Model (XDM), a variável [!UICONTROL Perfil de cliente potencial individual XDM] a classe captura perfis de prospecto geralmente obtidos de parceiros de dados para casos de uso de aquisição de clientes topo de funil.

![O diagrama do esquema da classe XDM Prospect.](../images/classes/individual-prospect-profile.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_repo` | Objeto | Essa classe permite que você forneça perfis de prospecto provenientes de fornecedores de dados para direcionar casos de uso de aquisição de clientes. |
| `_repo.createDate` | [!UICONTROL DateTime] | A data e hora do servidor em que o recurso foi criado no repositório. O horário de criação pode ser quando um arquivo de ativo é carregado pela primeira vez ou um diretório é criado pelo servidor como o pai de um novo ativo. A propriedade datetime deve estar em conformidade com o padrão ISO 8601. Um exemplo desse formato é &quot;2004-10-23T12:00:00-06:00&quot; |
| `_repo.modifyDate` | [!UICONTROL DateTime] | A data e hora do servidor quando o recurso foi modificado pela última vez no repositório, como quando uma nova versão de um ativo é carregada ou um recurso filho do diretório é adicionado ou removido. A propriedade datetime deve estar em conformidade com o padrão ISO 8601. Um exemplo de formulário é &quot;2004-10-23T12:00:00-06:00&quot; |
| `_id` | [!UICONTROL String] | Um identificador de sequência de caracteres exclusivo gerado pelo sistema para o registro. Este campo é usado para rastrear a exclusividade de um registro individual, impedir a duplicação de dados e pesquisar esse registro nos serviços downstream.<br><br>Como esse campo é gerado pelo sistema, ele não fornece um valor explícito durante a assimilação de dados. No entanto, você pode optar por fornecer seus próprios valores de ID exclusivos, se desejar. |
| `createdByBatchID` | [!UICONTROL String] | A ID do lote assimilado que causou a criação do registro. |
| `modifiedByBatchID` | [!UICONTROL String] | A ID do último lote assimilado que causou a atualização do registro. |
| `partnerID` | [!UICONTROL String] | Normalmente, um identificador exclusivo de pseudônimo que identifica um prospecto individual. Consulte a documentação em [tipos de identidade](../../identity-service/namespaces.md#identity-type) para saber mais sobre a ID do parceiro e outros tipos de identidade disponíveis no Adobe Experience Platform. |
| `repositoryCreatedBy` | [!UICONTROL String] | A ID do usuário que criou o registro. |
| `repositoryLastModifiedBy` | [!UICONTROL String] | A ID do usuário que modificou o registro pela última vez. Quando o registro é criado, a variável `modifiedByUser` é definido como o `createdByUser` valor. |

{style="table-layout:auto"}
