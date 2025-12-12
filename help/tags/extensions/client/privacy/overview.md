---
title: Visão geral da extensão do Adobe Privacy
description: Saiba mais sobre a extensão de tag do Adobe Privacy na Adobe Experience Platform.
exl-id: 8401861e-93ad-48eb-8796-b26ed8963c32
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 6%

---

# Visão geral da extensão do Adobe Privacy

A extensão de tag do Adobe Privacy permite coletar e remover IDs de usuário atribuídas aos usuários finais por soluções da Adobe em dispositivos do lado do cliente. As IDs coletadas podem então ser enviadas ao [Adobe Experience Platform Privacy Service](../../../../privacy-service/home.md) para acessar ou excluir os dados pessoais dos indivíduos relacionados em aplicativos Adobe Experience Cloud com suporte.

Este guia aborda como instalar e configurar a extensão Adobe Privacy na interface do usuário da Experience Platform ou na interface da coleção de dados.

>[!NOTE]
>
>Se preferir instalar essas funcionalidades sem usar tags, consulte a [Visão geral da Biblioteca de JavaScript de Privacidade](../../../../privacy-service/js-library.md) para obter etapas sobre como implementar o usando código bruto.

## Instalar e configurar a extensão

Selecione **[!UICONTROL Extensions]** na navegação à esquerda, seguido da guia **[!UICONTROL Catalog]**. Use a barra de pesquisa para restringir a lista de extensões disponíveis até localizar a Privacidade de Adobe. Selecione **[!UICONTROL Install]** para continuar.

![Instalar a extensão](../../../images/extensions/client/privacy/install.png)

A próxima tela permite configurar de quais fontes e soluções você deseja que a extensão colete IDs. As seguintes soluções são compatíveis com a extensão:

* Adobe Analytics (AA)
* Adobe Audience Manager (AAM)
* Adobe Target
* Serviço de identidade da Adobe Experience Cloud (Visitante ou ECID)
* Adobe Advertising Cloud (AdCloud)

Selecione uma ou mais soluções e, em seguida, **[!UICONTROL Update]**.

![Selecionar soluções](../../../images/extensions/client/privacy/select-solutions.png)

A tela é atualizada para mostrar entradas para os parâmetros de configuração necessários com base nas soluções selecionadas.

![Propriedades necessárias](../../../images/extensions/client/privacy/required-properties.png)

Usando o menu suspenso abaixo, você também pode adicionar outros parâmetros específicos da solução à configuração.

![Propriedades opcionais](../../../images/extensions/client/privacy/optional-properties.png)

>[!NOTE]
>
>Consulte a seção sobre [parâmetros de configuração](../../../../privacy-service/js-library.md#config-params) na visão geral da Biblioteca de JavaScript de privacidade para obter detalhes sobre os valores de configuração aceitos para cada solução suportada.

Quando terminar de adicionar os parâmetros das soluções selecionadas, selecione **[!UICONTROL Save]** para salvar a configuração.

![Propriedades opcionais](../../../images/extensions/client/privacy/save-config.png)

## Uso da extensão {#using}

A extensão Adobe Privacy fornece três tipos de ação que podem ser usados em uma [regra](../../../ui/managing-resources/rules.md) quando ocorre um determinado evento e as condições são atendidas:

* **[!UICONTROL Retrieve Identities]**: as informações de identidade armazenadas do usuário são recuperadas.
* **[!UICONTROL Remove Identities]**: as informações de identidade armazenadas do usuário são removidas.
* **[!UICONTROL Retrieve Then Remove Identities]**: as informações de identidade armazenadas do usuário são recuperadas e removidas.

Para cada uma das ações acima, você deve fornecer uma função JavaScript de retorno de chamada que aceite e manipule os dados de identidade recuperados como um parâmetro de objeto. Aqui, você pode armazenar essas identidades, exibi-las ou enviá-las para a [API do Privacy Service](../../../../privacy-service/api/overview.md), conforme necessário.

Ao usar a extensão de tag do Adobe Privacy, você deve fornecer a função de retorno de chamada necessária na forma de um elemento de dados. Consulte a próxima seção para obter etapas sobre como configurar esse elemento de dados.

### Definir um elemento de dados para lidar com identidades

Inicie o processo de criação de um novo elemento de dados selecionando **[!UICONTROL Data Elements]** na navegação à esquerda, seguido de **[!UICONTROL Add Data Element]**. Quando você estiver na tela de configuração, selecione **[!UICONTROL Core]** para a extensão e **[!UICONTROL Custom Code]** para o tipo de elemento de dados. Aqui, selecione **[!UICONTROL Open Editor]** no painel direito.

![Selecionar tipo de elemento de dados](../../../images/extensions/client/privacy/data-element-type.png)

Na caixa de diálogo exibida, defina uma função JavaScript que manipulará as identidades recuperadas. O retorno de chamada deve aceitar um único argumento de tipo de objeto (`ids` no exemplo abaixo). A função pode manipular as IDs da maneira que você desejar e também pode chamar quaisquer variáveis e funções que estejam disponíveis globalmente no site para processamento adicional.

>[!NOTE]
>
>Para obter mais informações sobre a estrutura do objeto `ids` que a função de retorno de chamada deve manipular, consulte as [amostras de código](../../../../privacy-service/js-library.md#samples) fornecidas na visão geral da Biblioteca JavaScript de Privacidade.

Quando terminar, selecione **[!UICONTROL Save]**.

![Definir função de retorno de chamada](../../../images/extensions/client/privacy/define-custom-code.png)

Você pode continuar criando outros elementos de dados de código personalizado se precisar de retornos de chamada diferentes para eventos diferentes.

### Criar uma regra com uma ação de privacidade

Depois de configurar um elemento de dados de retorno de chamada para lidar com as IDs recuperadas, você pode criar uma regra que chame a extensão Adobe Privacy sempre que um determinado evento ocorrer em seu site, juntamente com quaisquer outras condições necessárias.

Ao configurar a ação para a regra, selecione **[!UICONTROL Adobe Privacy]** para a extensão. Para o tipo de ação, selecione uma das [três funções](#using) fornecidas pela extensão.

![Selecionar tipo de ação](../../../images/extensions/client/privacy/action-type.png)

O painel direito solicita selecionar um elemento de dados que servirá como retorno de chamada da ação. Selecione o ícone de banco de dados (![Ícone de Banco de Dados](/help/images/icons/database.png)) e escolha na lista o elemento de dados criado anteriormente. Selecione **[!UICONTROL Keep Changes]** para continuar.

![Selecionar elemento de dados](../../../images/extensions/client/privacy/add-data-element.png)

A partir daqui, você pode continuar configurando a regra para que a ação Privacidade da Adobe seja acionada nos eventos e condições necessários. Quando estiver satisfeito, selecione **[!UICONTROL Save]**.

![Salvar a regra](../../../images/extensions/client/privacy/save-rule.png)

Agora é possível adicionar a regra a uma biblioteca para implantar como um build em seu site para teste. Consulte a visão geral no [fluxo de publicação de tags](../../../ui/publishing/overview.md) para obter mais informações.

## Desabilitar ou desinstalar a extensão

Depois de instalar a extensão, você pode desabilitá-la ou excluí-la. Selecione **[!UICONTROL Configure]** no cartão de privacidade da Adobe em suas extensões instaladas e, em seguida, selecione **[!UICONTROL Disable]** ou **[!UICONTROL Uninstall]**.

## Próximas etapas

Este guia abordou o uso da extensão de tag do Adobe Privacy na interface. Para obter mais informações sobre as funcionalidades fornecidas pela extensão, incluindo exemplos de como empregá-la usando código bruto, consulte a [Visão geral da Biblioteca de JavaScript de Privacidade](../../../../privacy-service/js-library.md) na documentação da Privacy Service.
