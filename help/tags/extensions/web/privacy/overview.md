---
title: Visão geral da extensão do Adobe Privacy
description: Saiba mais sobre a extensão de tag Adobe Privacy no Adobe Experience Platform.
source-git-commit: 5b8ef30b1d0e6d682c94453117677c806eba1e02
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 95%

---

# Visão geral da extensão do Adobe Privacy

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

A extensão Adobe Privacy fornece funcionalidades destinadas a coletar e remover IDs de usuário atribuídas a usuários finais por soluções da Adobe.

## Configurar soluções durante a instalação

Ao instalar a extensão Adobe Privacy a partir do catálogo de extensões, será solicitado que você selecione as soluções que deseja atualizar. Atualmente, você pode atualizar as seguintes soluções:

* Analytics (AA)
* Audience Manager (AAM)
* Target
* Visitor Service
* AdCloud
* Selecione uma ou mais soluções e, em seguida, Atualizar.
* Depois de selecionar e configurar as soluções, selecione Salvar. A extensão Adobe Privacy é adicionada à lista de extensões instaladas.

   As opções para cada solução estão descritas abaixo.

### Analytics

![](../../../images/ext-privacy-aa.jpg)

Por padrão, você deve fornecer o conjunto de relatórios inserindo uma string ou selecionando um elemento de dados.

Para configurar outros itens, selecione **[!UICONTROL Escolher um item]**, selecione o item que deseja configurar, selecione **[!UICONTROL Adicionar]** e insira o parâmetro solicitado ou um elemento de dados.

### Audience Manager

![](../../../images/ext-privacy-aam.jpg)

Selecione **[!UICONTROL Escolher um item]**, selecione o item que deseja configurar, selecione **[!UICONTROL Adicionar]** e insira o parâmetro solicitado ou um elemento de dados. Atualmente, você pode configurar apenas o `aamUUIDCookieName`.

### Target

![](../../../images/ext-privacy-target.jpg)

Insira o código de cliente do Target.

### Serviço de visitante

![](../../../images/ext-privacy-visitor.jpg)

Insira seu ID da organização IMS.

### AdCloud

![](../../../images/ext-privacy-adcloud.jpg)

Não há parâmetros específicos a serem configurados para o AdCloud.

## Configurar a extensão Adobe Privacy

Depois de instalar a extensão, você pode desativá-la ou excluí-la. Selecione **[!UICONTROL Configurar]** no cartão de privacidade da Adobe em suas extensões instaladas e, em seguida, selecione **[!UICONTROL Desativar]** ou **[!UICONTROL Desinstalar]**.

## Ações

As seguintes ações estão disponíveis quando você configura uma regra usando a extensão Adobe Privacy.

### Recuperar identidades

Quando o evento e as condições forem atendidas, recupere as informações de identidade armazenadas para o visitante.

Digite o nome de uma função JavaScript para a qual deseja passar os dados. Essa função ou método manipula as identidades recuperadas. Se você as armazenou, exibiu ou enviou para a API do Adobe GDPR, elas estão sob seu controle.

### Remover identidades

Quando o evento e as condições forem atendidas, remova as informações de identidade armazenadas para o visitante.

Digite o nome de uma função JavaScript para a qual deseja passar os dados. Essa função ou método manipula as identidades recuperadas. Se você as armazenou, exibiu ou enviou para a API do Adobe GDPR, elas estão sob seu controle.

### Recuperar e remover as identidades

Quando o evento e as condições forem atendidas, recupere as informações de identidade armazenadas para o visitante e, depois, remova-a.

## Tutorial: Configuração da extensão do Privacy

O documento a seguir mostra um exemplo detalhado de como configurar um elemento de dados e usá-lo com a extensão Privacy.

1. Crie um elemento de dados chamado `privacyFunc`.

   ```JavaScript
   window.privacyFunc = function(a,b){
       console.log(a,b);
   }
   return window.privacyFunc
   ```

1. Crie uma regra para ser executada no Library Load (topo da página) com uma ação da extensão Adobe Privacy. Selecione `privacyFunc` como seu elemento de dados.

   * **Extensão:** Adobe Privacy
   * **Tipo de ação:** Recuperar identidades
Esse tipo de ação exibe identidades que foram criadas, removidas ou que não foram removidas.
   * **Nome:** Recuperar identidades

1. Atualize sua biblioteca de desenvolvimento, publique e teste.
