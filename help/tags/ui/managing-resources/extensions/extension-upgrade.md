---
title: Atualizações de extensão
description: Saiba como as atualizações de extensão são empacotadas e representadas no catálogo de extensões.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 93%

---

# Atualizações de extensão

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Os desenvolvedores de extensão adicionam continuamente novos recursos a suas extensões e corrigem erros com frequência. Essas atualizações são colocadas em novas versões de uma extensão e disponibilizadas no catálogo de extensões como atualizações.

## Catálogo de extensões

Quando um desenvolvedor de extensão tiver fornecido uma nova versão da extensão, essa nova versão ficará disponível no catálogo de extensões. O catálogo mostra apenas a versão mais recente de uma extensão. Não é possível instalar nenhuma versão de extensão diferente de `latest`.

Quando você instala uma extensão na sua propriedade, a versão disponível atualmente é instalada e sua propriedade permanece com essa versão específica a partir desse ponto, mesmo se versões mais recentes forem adicionadas ao catálogo.

## Notificações de atualização

Quando tiver instalado uma extensão na sua propriedade e uma versão mais nova estiver disponível no catálogo, você verá um botão [!UICONTROL Atualizar] no cartão de extensão ao visualizar a página Extensões instaladas.

Você também verá um aviso ao editar os recursos fornecidos por essa extensão.

## As atualizações são permanentes

Se quiser atualizar para uma versão mais nova disponível no catálogo, você deverá instalar a atualização sozinho. Uma atualização é uma &quot;alteração&quot; que deve ser adicionada a uma biblioteca, testada e publicada antes de afetar suas tags implantadas.

A atualização deve ser levada a sério. Você não deve atualizar, a menos que esteja preparado para testar a nova extensão e esteja pronto para implantá-la. Depois que a atualização tiver sido adicionada à propriedade, ela deverá ser incluída em todas as bibliotecas. Qualquer biblioteca que não inclua a extensão atualizada falhará no momento da criação.

No momento, não há nenhum recurso para baixar sua extensão para uma versão anterior. Depois de ter atualizado (quer você publique ou não), a nova versão da extensão estará na propriedade para permanecer.

## Processo de atualização

Instalar uma atualização é o mesmo que instalar a extensão pela primeira vez.

1. Selecione **[!UICONTROL Atualizar]** para ir para a tela [!UICONTROL Configuração de extensão].
1. Faça todas as alterações de configuração que desejar.
1. Selecione **[!UICONTROL Salvar]**.

A atualização não é realizada de fato até que você clique em **[!UICONTROL Salvar]**. A qualquer momento antes disso, você pode selecionar [!UICONTROL Cancelar] e permanecer com a versão instalada atualmente. Clicar em **[!UICONTROL Salvar]** é o ponto sem volta.

Não são permitidas atualizações de extensão se você tiver uma biblioteca no estado `Approved` ou `Submitted`. Isso ocorre porque o próximo build deve conter a nova versão de extensão. Para uma biblioteca que é `Approved` ou `Submitted`, o próximo build é o build de produção. Ocorreria uma falha nesse build, pois ele não contém a versão mais recente, portanto, o fluxo de trabalho é publicar ou rejeitar bibliotecas no estado `Approved` ou `Submitted`, _antes_ de atualizar a extensão.

## Como publicar uma atualização

Depois que a extensão atualizada estiver instalada em sua propriedade, você deverá incluí-la em todas as bibliotecas. Uma mensagem de falha da build será exibida para todas as bibliotecas que não a incluírem.

Além disso, adicionar a extensão atualizada à biblioteca é o mesmo que [adicionar qualquer outra alteração](../../publishing/libraries.md) a uma biblioteca.

Na tela [!UICONTROL Editar biblioteca], você pode usar o botão &quot;[!UICONTROL Adicionar todos os recursos alterados]&quot; ou usar o botão &quot;[!UICONTROL Adicionar um recurso]&quot; e selecionar a extensão atualizada individualmente.

>[!TIP]
>
>Os desenvolvedores de extensão podem adicionar novos itens de configuração a suas exibições de extensão para ativar novas funcionalidades. Se você vir falhas de build depois de ter atualizado para uma nova versão de extensão e tiver isolado para falhas de build dessa extensão, a primeira coisa a fazer é acessar a página Configuração de extensão e certificar-se de salvar (mesmo se não tiver alterado nada). Em seguida, adicione a nova alteração à biblioteca e tente fazer a build novamente.

Depois de ter adicionado a atualização da extensão à biblioteca, siga as etapas descritas em [Fluxo de publicação](../../publishing/publishing-flow.md) para publicar sua biblioteca na produção.
