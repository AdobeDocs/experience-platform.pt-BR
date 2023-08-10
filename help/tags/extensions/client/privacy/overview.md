---
title: Visão geral da extensão do Adobe Privacy
description: Saiba mais sobre a extensão de tag do Adobe Privacy na Adobe Experience Platform.
exl-id: 8401861e-93ad-48eb-8796-b26ed8963c32
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 9%

---

# Visão geral da extensão do Adobe Privacy

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleção de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

A extensão de tag da Privacidade de Adobe permite coletar e remover IDs de usuário atribuídas aos usuários finais por soluções de Adobe em dispositivos do lado do cliente. As IDs coletadas podem ser enviadas para [Adobe Experience Platform Privacy Service](../../../../privacy-service/home.md) para acessar ou excluir os dados pessoais do indivíduo relacionado em aplicativos Adobe Experience Cloud compatíveis.

Este guia aborda como instalar e configurar a extensão Adobe Privacy na interface do usuário do Experience Platform ou na interface da coleção de dados.

>[!NOTE]
>
>Se preferir instalar essas funcionalidades sem usar tags, consulte o [Visão geral da biblioteca JavaScript de privacidade](../../../../privacy-service/js-library.md) para obter etapas sobre como implementar o usando código bruto.

## Instalação e configuração da extensão do 

Selecionar **[!UICONTROL Extensões]** na navegação à esquerda, seguido pelo botão **[!UICONTROL Catálogo]** guia. Use a barra de pesquisa para restringir a lista de extensões disponíveis até localizar a Privacidade de Adobe. Selecionar **[!UICONTROL Instalar]** para continuar.

![Instalar a extensão](../../../images/extensions/client/privacy/install.png)

A próxima tela permite configurar de quais fontes e soluções você deseja que a extensão colete IDs. As seguintes soluções são compatíveis com a extensão:

* Adobe Analytics (AA)
* Adobe Audience Manager (AAM)
* Adobe Target
* Serviço de identidade da Adobe Experience Cloud (Visitante ou ECID)
* Adobe Advertising Cloud (AdCloud)

Selecione uma ou mais soluções e, em seguida, **[!UICONTROL Atualizar]**.

![Selecionar soluções](../../../images/extensions/client/privacy/select-solutions.png)

A tela é atualizada para mostrar entradas para os parâmetros de configuração necessários com base nas soluções selecionadas.

![Propriedades obrigatórias](../../../images/extensions/client/privacy/required-properties.png)

Usando o menu suspenso abaixo, você também pode adicionar outros parâmetros específicos da solução à configuração.

![Propriedades opcionais](../../../images/extensions/client/privacy/optional-properties.png)

>[!NOTE]
>
>Consulte a seção sobre [parâmetros de configuração](../../../../privacy-service/js-library.md#config-params) na Visão geral da Biblioteca JavaScript de privacidade para obter detalhes sobre os valores de configuração aceitos para cada solução compatível.

Quando terminar de adicionar os parâmetros das soluções selecionadas, selecione **[!UICONTROL Salvar]** para salvar a configuração.

![Propriedades opcionais](../../../images/extensions/client/privacy/save-config.png)

## Uso da extensão {#using}

A extensão Privacidade de Adobe fornece três tipos de ação que podem ser usados em uma [regra](../../../ui/managing-resources/rules.md) quando um determinado evento ocorre e as condições são atendidas:

* **[!UICONTROL Recuperar identidades]**: as informações de identidade armazenadas do usuário são recuperadas.
* **[!UICONTROL Remover identidades]**: as informações de identidade armazenadas do usuário são removidas.
* **[!UICONTROL Recuperar E Remover Identidades]**: as informações de identidade armazenadas do usuário são recuperadas e removidas.

Para cada uma das ações acima, você deve fornecer uma função JavaScript de retorno de chamada que aceite e manipule os dados de identidade recuperados como um parâmetro de objeto. Aqui, você pode armazenar essas identidades, exibi-las ou enviá-las para a [API PRIVACY SERVICE](../../../../privacy-service/api/overview.md) conforme necessário.

Ao usar a extensão de tag da Privacidade de Adobe, você deve fornecer a função de retorno de chamada necessária na forma de um elemento de dados. Consulte a próxima seção para obter etapas sobre como configurar esse elemento de dados.

### Definir um elemento de dados para lidar com identidades

Inicie o processo de criação de um novo elemento de dados selecionando **[!UICONTROL Elementos de dados]** na navegação à esquerda, seguido por **[!UICONTROL Adicionar elemento de dados]**. Quando estiver na tela de configuração, selecione **[!UICONTROL Núcleo]** para a extensão e **[!UICONTROL Custom Code]** para o tipo de elemento de dados. Aqui, selecione **[!UICONTROL Abrir editor]** no painel direito.

![Selecionar tipo de elemento de dados](../../../images/extensions/client/privacy/data-element-type.png)

Na caixa de diálogo exibida, defina uma função JavaScript que manipulará as identidades recuperadas. O retorno de chamada deve aceitar um único argumento de tipo de objeto (`ids` no exemplo abaixo). A função pode manipular as IDs da maneira que você desejar e também pode chamar quaisquer variáveis e funções que estejam disponíveis globalmente no site para processamento adicional.

>[!NOTE]
>
>Para obter mais informações sobre a estrutura do `ids` objeto que a função de retorno de chamada deve manipular, consulte o [amostras de código](../../../../privacy-service/js-library.md#samples) fornecido na visão geral da Biblioteca JavaScript de privacidade.

Quando terminar, selecione **[!UICONTROL Salvar]**.

![Definir função de retorno de chamada](../../../images/extensions/client/privacy/define-custom-code.png)

Você pode continuar criando outros elementos de dados de código personalizado se precisar de retornos de chamada diferentes para eventos diferentes.

### Criar uma regra com uma ação de privacidade

Depois de configurar um elemento de dados de retorno de chamada para lidar com as IDs recuperadas, você pode criar uma regra que chame a extensão de Privacidade de Adobe sempre que um determinado evento ocorrer em seu site, juntamente com quaisquer outras condições necessárias.

Ao configurar a ação para a regra, selecione **[!UICONTROL Privacidade Adobe]** para a extensão. Para o tipo de ação, selecione uma das opções [três funções](#using) fornecido pela extensão.

![Selecionar tipo de ação](../../../images/extensions/client/privacy/action-type.png)

O painel direito solicita selecionar um elemento de dados que servirá como retorno de chamada da ação. Selecione o ícone do banco de dados (![Ícone do banco de dados](../../../images/extensions/client/privacy/database.png)) e escolha na lista o elemento de dados criado anteriormente. Selecionar **[!UICONTROL Manter alterações]** para continuar.

![Selecionar elemento de dados](../../../images/extensions/client/privacy/add-data-element.png)

Aqui, você pode continuar configurando a regra para que a ação Privacidade de Adobe seja acionada nos eventos e condições necessários. Quando estiver satisfeito, selecione **[!UICONTROL Salvar]**.

![Salvar a regra](../../../images/extensions/client/privacy/save-rule.png)

Agora é possível adicionar a regra a uma biblioteca para implantar como um build em seu site para teste. Consulte a visão geral no [fluxo de publicação de tags](../../../ui/publishing/overview.md) para obter mais informações.

## Desabilitar ou desinstalar a extensão

Depois de instalar a extensão, você pode desativá-la ou excluí-la. Selecione **[!UICONTROL Configurar]** no cartão de privacidade da Adobe em suas extensões instaladas e, em seguida, selecione **[!UICONTROL Desativar]** ou **[!UICONTROL Desinstalar]**.

## Próximas etapas

Este guia abordou o uso da extensão de tag da Privacidade de Adobe na interface do usuário do. Para obter mais informações sobre as funcionalidades fornecidas pela extensão, incluindo exemplos de como empregá-la usando código bruto, consulte o [Visão geral da biblioteca JavaScript de privacidade](../../../../privacy-service/js-library.md) na documentação do Privacy Service.
