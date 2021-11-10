---
title: Visão geral da extensão do Adobe Privacy
description: Saiba mais sobre a extensão de tag do Adobe Privacy na Adobe Experience Platform.
exl-id: 8401861e-93ad-48eb-8796-b26ed8963c32
source-git-commit: 285e7ff1a1cd6c9790c526ca27ffafc60e94218d
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 9%

---

# Visão geral da extensão do Adobe Privacy

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

A extensão de tag Adobe Privacy permite coletar e remover IDs de usuário atribuídas aos usuários finais por soluções do Adobe em dispositivos do lado do cliente. As IDs coletadas podem ser enviadas para [Adobe Experience Platform Privacy Service](../../../../privacy-service/home.md) para acessar ou excluir os dados pessoais do indivíduo relacionado em aplicativos Adobe Experience Cloud compatíveis.

Este guia aborda como instalar e configurar a extensão da Privacidade de Adobe na interface do usuário da coleta de dados.

>[!NOTE]
>
>Se preferir instalar essas funcionalidades sem usar tags, consulte o [Visão geral da biblioteca JavaScript de privacidade](../../../../privacy-service/js-library.md) para obter as etapas sobre como implementar o usando código bruto.

## Instalação e configuração da extensão do 

Na interface do usuário da coleta de dados, selecione **[!UICONTROL Extensões]** no painel de navegação esquerdo, seguido pela variável **[!UICONTROL Catálogo]** guia . Use a barra de pesquisa para restringir a lista de extensões disponíveis até localizar a Privacidade de Adobe. Selecionar **[!UICONTROL Instalar]** para continuar.

![Instalar a extensão](../../../images/extensions/privacy/install.png)

A próxima tela permite configurar de quais fontes e soluções você deseja que a extensão colete IDs. As seguintes soluções são compatíveis com a extensão:

* Adobe Analytics (AA)
* Adobe Audience Manager (AAM)
* Adobe Target
* Serviço de identidade da Adobe Experience Cloud (Visitante ou ECID)
* Adobe Advertising Cloud (AdCloud)

Selecione uma ou mais soluções e, em seguida, selecione **[!UICONTROL Atualizar]**.

![Selecionar soluções](../../../images/extensions/privacy/select-solutions.png)

A tela é atualizada para mostrar entradas para os parâmetros de configuração necessários com base nas soluções selecionadas.

![Propriedades necessárias](../../../images/extensions/privacy/required-properties.png)

Usando o menu suspenso abaixo, também é possível adicionar mais parâmetros específicos da solução à configuração.

![Propriedades opcionais](../../../images/extensions/privacy/optional-properties.png)

>[!NOTE]
>
>Consulte a seção sobre [parâmetros de configuração](../../../../privacy-service/js-library.md#config-params) na visão geral da Biblioteca JavaScript de privacidade para obter detalhes sobre os valores de configuração aceitos para cada solução suportada.

Depois de concluir a adição de parâmetros para as soluções selecionadas, selecione **[!UICONTROL Salvar]** para salvar a configuração.

![Propriedades opcionais](../../../images/extensions/privacy/save-config.png)

## Uso da extensão {#using}

A extensão Adobe Privacy fornece três tipos de ação que podem ser usados em um [regra](../../../ui/managing-resources/rules.md) quando um determinado evento ocorre e as condições são atendidas:

* **[!UICONTROL Recuperar identidades]**: As informações de identidade armazenadas do usuário são recuperadas.
* **[!UICONTROL Remover identidades]**: As informações de identidade armazenadas do usuário são removidas.
* **[!UICONTROL Recuperar E Remover Identidades]**: As informações de identidade armazenadas do usuário são recuperadas e depois removidas.

Para cada uma das ações acima, você deve fornecer uma função de retorno de chamada JavaScript que aceite e manipule os dados de identidade recuperados como um parâmetro de objeto. A partir daqui, você pode armazenar essas identidades, exibi-las ou enviá-las para o [API Privacy Service](../../../../privacy-service/api/overview.md) conforme você precisar.

Ao usar a extensão de tag Adobe Privacy, você deve fornecer a função de retorno de chamada necessária no formato de um elemento de dados. Consulte a próxima seção para obter etapas sobre como configurar esse elemento de dados.

### Definir um elemento de dados para manipular identidades

Na interface do usuário da coleta de dados, inicie o processo de criação de um novo elemento de dados selecionando **[!UICONTROL Elementos de dados]** no painel de navegação esquerdo, seguido de **[!UICONTROL Adicionar elemento de dados]**. Quando estiver na tela de configuração, selecione **[!UICONTROL Núcleo]** para a extensão e **[!UICONTROL Código personalizado]** para o tipo de elemento de dados. Aqui, selecione **[!UICONTROL Abrir editor]** no painel direito.

![Selecionar tipo de elemento de dados](../../../images/extensions/privacy/data-element-type.png)

Na caixa de diálogo exibida, defina uma função JavaScript que lidará com as identidades recuperadas. O retorno de chamada deve aceitar um único argumento do tipo de objeto (`ids` no exemplo abaixo). A função pode lidar com as IDs da maneira que você desejar e também pode invocar variáveis e funções que estão globalmente disponíveis no site para processamento adicional.

>[!NOTE]
>
>Para obter mais informações sobre a estrutura do `ids` objeto que deve ser manipulado pela função de retorno de chamada, consulte [amostras de código](../../../../privacy-service/js-library.md#samples) fornecida na visão geral da Biblioteca JavaScript de privacidade.

Quando terminar, selecione **[!UICONTROL Salvar]**.

![Definir função de retorno de chamada](../../../images/extensions/privacy/define-custom-code.png)

Você pode continuar criando outros elementos de dados de código personalizado se precisar de retornos de chamada diferentes para eventos diferentes.

### Criar uma regra com uma ação de privacidade

Após configurar um elemento de dados de retorno de chamada para lidar com IDs recuperadas, você pode criar uma regra que chame a extensão Adobe Privacy sempre que um determinado evento ocorrer em seu site, juntamente com quaisquer outras condições necessárias.

Ao configurar a ação para a regra, selecione **[!UICONTROL Privacidade de Adobe]** para a extensão do . Para o tipo de ação , selecione uma das opções [três funções](#using) fornecido pela extensão.

![Selecionar tipo de ação](../../../images/extensions/privacy/action-type.png)

O painel direito solicita que você selecione um elemento de dados que servirá como o retorno de chamada da ação. Selecione o ícone do banco de dados (![Ícone do banco de dados](../../../images/extensions/privacy/database.png)) e escolha o elemento de dados criado anteriormente na lista. Selecionar **[!UICONTROL Manter alterações]** para continuar.

![Selecionar elemento de dados](../../../images/extensions/privacy/add-data-element.png)

A partir daqui, você pode continuar configurando a regra para que a ação Privacidade de Adobe seja acionada nos eventos e condições necessários. Quando estiver satisfeito, selecione **[!UICONTROL Salvar]**.

![Salvar a regra](../../../images/extensions/privacy/save-rule.png)

Agora é possível adicionar a regra a uma biblioteca para implantar como uma build no seu site para testes. Consulte a visão geral no [fluxo de publicação de tags](../../../ui/publishing/overview.md) para obter mais informações.

## Desativar ou desinstalar a extensão

Depois de instalar a extensão, você pode desativá-la ou excluí-la. Selecione **[!UICONTROL Configurar]** no cartão de privacidade da Adobe em suas extensões instaladas e, em seguida, selecione **[!UICONTROL Desativar]** ou **[!UICONTROL Desinstalar]**.

## Próximas etapas

Este guia cobriu o uso da extensão de tag da Privacidade de Adobe na interface do usuário da coleta de dados. Para obter mais informações sobre as funcionalidades fornecidas pela extensão, incluindo exemplos de como empregá-la usando o código bruto, consulte o [Visão geral da biblioteca JavaScript de privacidade](../../../../privacy-service/js-library.md) na documentação do Privacy Service.
