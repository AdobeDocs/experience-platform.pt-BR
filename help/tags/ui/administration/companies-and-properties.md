---
title: Propriedades
description: Saiba como suas extensões, ambientes e bibliotecas são organizados e agrupados para sua organização no Adobe Experience Platform.
exl-id: e5b4a853-c23e-498c-9e20-e773ea1de88b
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 90%

---

# Propriedades

## Propriedades da Web

Uma propriedade da Web é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Cada propriedade da Web tem seu próprio conjunto de códigos incorporados e pode ser implantada em qualquer número de sites distintos (domínios diferentes).

## Propriedades para dispositivo móvel

O tipo de propriedade para dispositivo móvel pode conter vários aplicativos. Por exemplo, em uma propriedade para dispositivo móvel, é possível gerenciar o mesmo conjunto de regras e extensões em vários aplicativos de iOS e Android.

## Práticas recomendadas para o planejamento de propriedades {#best-practices-for-planning-properties}

Cada implementação de tag na Adobe Experience Platform pode ser muito diferente. Elas têm diversas necessidades de coleção de dados, uso de variáveis, extensões, tags de terceiros, outros sistemas e tecnologias, pessoas, equipes, áreas geográficas etc. Você deve estruturar suas propriedades de forma que corresponda ao fluxo de trabalho e aos processos de sua organização.

Considere os itens a seguir ao planejar propriedades:

* Estrutura de código
* Dados
* Variáveis
* Extensões, tags e sistemas
* Pessoas

### Estrutura de código

Os sites são em HTML, e os aplicativos para dispositivos móveis se baseiam em códigos. Se os modelos ou as bases de código HTML subjacentes forem os mesmos para vários sites e aplicativos, considere o uso de uma única propriedade de tag para gerenciar vários sites ou aplicativos.

### Dados

Os dados que você coletará de todos seus sites e aplicativos são muito semelhantes, mais ou menos semelhantes ou exclusivos?

Quando os dados que você precisa coletar são semelhantes, pode ser interessante agrupar esses sites ou aplicativos em outra propriedade para evitar regras duplicadas ou a cópia de uma propriedade para outra.

Se a coleção de dados for exclusiva a cada site ou aplicativo, talvez faça sentido separá-las em propriedades próprias. Este método permite controlar a coleção de dados mais especificamente sem usar grandes quantidades de lógica condicional nos scripts personalizados.

### Variáveis

Assim como no caso dos dados, as variáveis que você definirá no seu [!DNL Analytics] e em outras extensões são muito semelhantes, mais ou menos semelhantes ou exclusivas?

Por exemplo, se eVar27 é utilizada para o mesmo valor de origem entre os sites, pode ser interessante agrupar os sites ou aplicativos para poder definir as variáveis comuns usando apenas uma propriedade.

### Extensões, tags e sistemas

As extensões, as tags e os sistemas que você implantará são muito semelhantes, mais ou menos semelhantes ou exclusivos?

Se as extensões, as tags e os sistemas que você implantará são muito semelhantes em seus sites ou aplicativos, convém incluí-los na mesma propriedade.

Se você estiver implantando o [!DNL Adobe Analytics] somente em um site ou aplicativo, e suas outras extensões e tags também forem exclusivas, talvez você queira criar propriedades separadas para ter mais controle.

Por exemplo, se estiver implantando o [!DNL Adobe Analytics], o [!DNL Target] e as mesmas extensões de terceiros em todos os sites ou aplicativos, esse é um motivo para agrupá-los em conjunto.

### Pessoas

As pessoas, as equipes e as organizações que trabalham na Adobe Experience Platform precisarão acessar todos os sites e aplicativos, alguns deles ou apenas um?

Os recursos do Gerenciamento de usuários permitem que você atribua funções diferentes a pessoas diferentes para todas as propriedades da ou de acordo com cada uma. Se alguém tiver as permissões necessárias, essa pessoa poderá executar ações administrativas em todas as propriedades dessa organização da Experience Platform. Todas as demais funções podem ser atribuídas de acordo com propriedades. Você pode ocultar uma propriedade de determinados usuários (que não sejam administradores) não atribuindo a eles nenhuma função na propriedade.

## Página Propriedades

Uma propriedade é uma coleção de regras, elementos de dados, extensões configuradas, ambientes e bibliotecas. Para a Web, há apenas um código incorporado de publicação por propriedade. Para dispositivos móveis, há uma ID de aplicativo para configuração por propriedade.

Uma propriedade pode ser qualquer agrupamento de um ou mais domínios e subdomínios. É possível gerenciar e rastrear esses ativos da mesma maneira. Por exemplo, suponhamos que você tenha vários sites baseados em um só modelo e queira rastrear os mesmos recursos em todos. É possível aplicar uma propriedade a vários domínios.

O lado esquerdo da tela mostra as empresas em sua organização. Isso é particularmente útil se você gerenciar várias contas. Selecione uma empresa para ver as propriedades e logs de auditoria dessa empresa.

Cada propriedade é mostrada na lista Propriedades.

A lista Propriedades mostra as seguintes informações:

* Nome da propriedade
* Plataforma
* Status

Selecione uma propriedade para ter uma visão geral dela. A visão geral mostra qualquer atividade realizada na propriedade. Ela também lista as métricas e extensões da propriedade.

## Criar ou configurar uma propriedade

Esta seção fornece orientação sobre como criar ou configurar uma propriedade de tag na Adobe Experience Platform.

>[!NOTE]
>
>Somente um usuário com as permissões necessárias pode criar uma propriedade. Consulte o [Gerenciamento de usuários](user-permissions.md).

Antes de começar, leia atentamente as [Práticas recomendadas para planejar propriedades](companies-and-properties.md#best-practices-for-planning-properties) dedicada às propriedades.

Navegue até a página da empresa e selecione **[!UICONTROL Add Property]** ou selecione uma propriedade existente na lista e **[!UICONTROL Configure]**.

![](../../images/property-settings.png)

### Para a web

Siga as instruções para criar uma propriedade da Web.

1. Preencha os campos:

   **Nome:** o nome da sua propriedade.

   **Domínios:** o URL básico de qualquer site no qual você planeja implantar essa propriedade

1. (Avançado) **[!UICONTROL Run rule components in sequence]**: marque essa caixa de seleção para fazer com que as condições e ações aguardem a conclusão das anteriores antes de serem executadas
1. (Avançado) **[!UICONTROL Return an empty string for missing data elements:]** Se você fizer referência a um elemento de dados que não existe em uma biblioteca, isso normalmente retornará `undefined`. Marque essa caixa de seleção se desejar que esse cenário retorne uma string vazia.
1. (Avançado) **[!UICONTROL Configure for extension development:]** Ative essa caixa de seleção se você planeja instalar extensões de desenvolvimento que estão sendo desenvolvidas ativamente pela sua empresa
1. Selecione **[!UICONTROL Save]**.

### Para dispositivos móveis

Siga as instruções para criar uma propriedade móvel.

1. Preencha os campos:

   * **Nome:** o nome da sua propriedade.
   * **Privacidade:** por padrão, a configuração de privacidade está definida como Aceitar, o que significa que você gostaria que o SDK coletasse e enviasse dados para soluções. Se você selecionar Recusar, o SDK, por padrão, NÃO enviará dados para soluções. Se você escolher Desconhecido como configuração, o SDK exigirá que o aplicativo primeiro ofereça ao usuário a permissão para compartilhamento e coleção de dados.

     >[!NOTE]
     >
     >Essas configurações podem ser controladas melhor por meio da API no aplicativo móvel.

   * **Usar HTTPS:** escolha essa opção se todas as comunicações de dados devem ser enviadas via HTTP ou HTTPS.

1. Selecione **[!UICONTROL Save]**.

Após a criação da propriedade, o Experience Platform adiciona automaticamente um host padrão, um conjunto de ambientes (desenvolvimento, armazenamento temporário e produção) e as extensões padrão.

## Excluir uma propriedade da

Siga as etapas abaixo para excluir uma propriedade de tag.

>[!NOTE]
>
>A remoção de uma propriedade não pode ser revertida. O solicitante deve ser um usuário de nível administrativo. Esta solicitação não pode ser desfeita.

1. Na lista Propriedades, selecione a propriedade que deseja excluir.

   É possível selecionar várias propriedades para excluir.

1. Selecione **[!UICONTROL Delete]** e confirme a remoção da propriedade.
