---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão de Experience Platform 10 de agosto de 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: f881c1365684b1ca9e6bf9a8ce866d234dc54128
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 7%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 10 de junho de 2020**

Novos recursos no Adobe Experience Platform:

- [!DNL Access control](#access-control)
- [!DNL Sandboxes](#sandboxes)

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] aproveita perfis de produtos [do Adobe Admin Console](https://adminconsole.adobe.com) para vincular usuários com permissões e caixas de proteção. As permissões controlam o acesso a uma variedade de recursos do Platform, incluindo modelagem de dados, gerenciamento de perfis e administração de sandbox.

**Principais recursos**

| Recurso | Descrição |
|--- | ---|
| Permissões | Na guia [!DNL Admin Console], dentro de um perfil de [!DNL Platform] produto, você pode personalizar quais [!DNL Platform] recursos estão disponíveis para os usuários conectados a esse perfil. As categorias de permissão disponíveis incluem: [!UICONTROL Modelagem]De Dados, [!UICONTROL Gestão de dados], Gerenciamento [!UICONTROL De]Perfis, [!UICONTROL Identidades], Monitoramento [!UICONTROL De]Dados, Administração Sandbox, Destinos, Fontes. |
| Acesso a caixas de proteção | A guia [!UICONTROL _Permissões _]em um perfil de[!DNL Platform]produto pode conceder aos usuários acesso a caixas de proteção específicas. Consulte a seção sobre[caixas de proteção](#sandboxes)abaixo para obter mais informações. |

Para obter mais informações, consulte a visão geral [do](../../access-control/home.md)controle de acesso.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] foi criada para enriquecer aplicativos de experiência digital em escala global. O Empresa geralmente executa vários aplicativos de experiência digital em paralelo e precisa atender ao desenvolvimento, teste e implantação desses aplicativos, garantindo a conformidade operacional. Para atender a essa necessidade, [!DNL Experience Platform] fornece caixas de proteção que dividem uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

**Principais recursos**

| Recurso | Descrição |
|--- | ---|
| Caixa de proteção de produção | [!DNL Experience Platform] fornece uma única caixa de proteção de produção, que não pode ser excluída ou redefinida. |
| Caixas de proteção de não produção | É possível criar várias caixas de proteção de não produção para uma única [!DNL Platform] instância, permitindo testar recursos, executar experiências e fazer configurações personalizadas sem afetar a caixa de proteção de produção. |
| Comutador Sandbox | Na interface do [!DNL Experience Platform] usuário, o alternador da caixa de proteção no canto superior esquerdo da tela permite alternar entre as caixas de proteção disponíveis por meio de um menu suspenso. |
| `x-sandbox-name` header | Todas as chamadas para [!DNL Experience Platform] APIs agora devem incluir o novo `x-sandbox-name` cabeçalho, cujo valor faz referência ao `name` atributo da caixa de proteção em que a operação ocorrerá. |

Para obter mais informações, consulte a visão geral [das](../../sandboxes/home.md)caixas de proteção.