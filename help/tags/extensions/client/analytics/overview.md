---
title: Visão geral da extensão do Adobe Analytics
description: Saiba mais sobre a extensão de tags do Adobe Analytics na Adobe Experience Platform.
exl-id: 33ebdcb6-9bf0-44e6-b016-e93fe78af578
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '2263'
ht-degree: 82%

---

# Visão geral da extensão do Adobe Analytics

Use essa referência para obter informações sobre como configurar a extensão do Adobe Analytics e as opções disponíveis ao usar esta extensão para criar uma regra.

## Configurar a extensão do Adobe Analytics

Esta seção fornece uma referência para as opções disponíveis ao configurar a extensão do Adobe Analytics.

Se a extensão do Adobe Analytics ainda não tiver sido instalada, abra a propriedade e selecione **[!UICONTROL Extensions > Catalog]**, passe o mouse sobre a extensão do Adobe Analytics e selecione **[!UICONTROL Install]**.

Para configurar a extensão, abra a guia Extensões, passe o mouse sobre a extensão e selecione **[!UICONTROL Configure]**.

![](../../../images/ext-analytics-config.png)

## Gerenciamento de biblioteca

Selecione uma opção na seção Gerenciamento de biblioteca da página de configuração. As opções de configuração disponíveis são as seguintes:

### Gerenciar a biblioteca para mim

#### Conjuntos de relatórios

Especifique um ou mais conjuntos de relatórios para cada um dos seguintes ambientes:

* Desenvolvimento
* Armazenamento temporário
* Produção

### Usar a biblioteca já instalada na página

#### Definir os seguintes conjuntos de relatórios no rastreador

Se você selecionar essa opção, especifique um ou mais conjuntos de relatórios para cada um dos seguintes ambientes:

* Desenvolvimento
* Armazenamento temporário
* Produção

#### Uso do módulo do Activity Map

O Activity Map é carregado como um módulo separado (como o módulo AAM). Por padrão, o Activity Map está ativado, mas se você preferir desativá-lo, desmarque a caixa na configuração.

#### O rastreador pode ser acessado na variável global chamada

Marcar essa caixa permite que o objeto do rastreador seja usado globalmente. Por exemplo, você pode definir a variável `window.s.pageName` em qualquer lugar do site.

### Carregue a biblioteca de um URL personalizado

#### URL HTTP

Especifique o URL onde a biblioteca está localizada.

#### URL HTTPS

Especifique o URL onde a biblioteca está localizada.

#### Definir os seguintes conjuntos de relatórios no rastreador

Se você selecionar essa opção, especifique um ou mais conjuntos de relatórios para cada um dos seguintes ambientes:

* Desenvolvimento
* Armazenamento temporário
* Produção

#### O rastreador pode ser acessado na variável global chamada

Especifique o objeto do rastreador a ser usado globalmente.

### Deixe-me fornecer o código de biblioteca personalizado

#### Abrir editor

Permite inserir o código principal [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=pt-BR). Este código é preenchido automaticamente ao utilizar o método de configuração automático.

>[!NOTE]
>
>O validador usado no editor de código de tags foi projetado para identificar problemas em código escrito pelo desenvolvedor. O código que passou por um processo de minificação, como o código AppMeasurement.js baixado do Gerenciador de código, pode ser falsamente sinalizado como tendo problemas pelo validador de tags, que geralmente pode ser ignorado.

#### Definir os seguintes conjuntos de relatórios no rastreador

Se você selecionar essa opção, especifique um ou mais conjuntos de relatórios para cada um dos seguintes ambientes:

* Desenvolvimento
* Armazenamento temporário
* Produção

#### O rastreador pode ser acessado na variável global chamada

Especifique o objeto do rastreador a ser usado globalmente.

## Geral

Selecione uma opção na seção Geral da página de configuração. As opções de configuração disponíveis são as seguintes:

### Habilitar a conformidade UE para o Adobe Analytics

Habilita ou desabilita o rastreamento com base no cookie de privacidade UE.

Ao habilitar a caixa de seleção Conformidade com a UE, o campo [!UICONTROL Tracking Cookie Name] é exibido. O cookie de rastreamento substitui o nome do cookie de rastreamento padrão. Você pode personalizar o nome que as tags usam a fim de rastrear o status de recusa para o recebimento de outros cookies.

Quando uma página é carregada, o sistema verifica se um cookie chamado sat\_track está definido (ou o nome do cookie personalizado especificado na página Editar propriedade). Considere as seguintes informações:

* Se o cookie não existe ou existe e está definido como qualquer item exceto true, o carregamento da ferramenta é ignorado quando esta configuração é habilitada. Ou seja, toda parte de uma regra que usa a ferramenta não será aplicada. Se uma regra tiver o Analytics com conformidade UE ativada e o código de terceiros, e o cookie estiver definido como false, o código de terceiros ainda será executado. Contudo, as variáveis de análise não serão definidas.
* Se o cookie existir, mas estiver definido como true, a ferramenta será carregada normalmente.

Você é responsável por definir o cookie sat\_track (ou com nome personalizado) como false se um visitante rejeitar. Você pode fazer isso usando o código personalizado:

```javascript
_satellite.cookie.set("sat_track", "false");
```

Você também deve ter um mecanismo para definir esse cookie como true, se quiser que um visitante possa aceitar a participação posteriormente:

```javascript
_satellite.cookie.set("sat_track", "true");
```

### Conjunto de caracteres

Determina como a solicitação de imagem é codificada. Se sua implementação ou site usar caracteres não ASCII, é importante definir o conjunto de caracteres aqui. É possível selecionar um conjunto de caracteres predefinido ou especificar um conjunto de caracteres personalizado. A Adobe recomenda usar a mesma codificação de caracteres do site. Normalmente esse valor é UTF -8.

O conjunto de caracteres pode ser definido no código personalizado do Analytics usando a variável `s.charSet`.
Para obter mais informações sobre conjuntos de caracteres, consulte a documentação [charSet](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/charset.html?lang=pt-BR).

### Código de moeda

Determina a taxa de conversão a ser aplicada aos eventos de receita e moeda. Se o site permite que os visitantes comprem em várias moedas, definir o código monetário garante que o valor monetário seja convertido e armazenado corretamente.

Para obter mais informações sobre os códigos de moeda aceitos, consulte [currencyCode](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/currencycode.html?lang=pt-BR).

### Servidor de rastreamento

Usado para implementações de cookies primários para determinar onde o cookie primário é armazenado. Se você usar o serviço da Experience Cloud ID, a Adobe recomenda não preencher esse campo.

O servidor de rastreamento pode ser definido no código personalizado do Analytics usando a variável `s.trackingServer`.

Consulte [trackingServer](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackingserver.html?lang=pt-BR) no guia de implementação do Adobe Analytics.

### Servidor de rastreamento de SSL

Usado para implementações de cookies primários SSL para determinar onde o cookie primário é armazenado. Se você usar o serviço da Experience Cloud ID, a Adobe recomenda não preencher esse campo. Se não estiver definido, os dados do SSL usarão o Servidor de rastreamento.

O Servidor de rastreamento do SSL pode ser definido no código personalizado do Analytics usando a variável `s.trackingServerSecure`.

Consulte [trackingServerSecure](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackingserversecure.html?lang=pt-BR).

## Variáveis globais

Use esta seção para configurar [eVars e Props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=pt-BR) e para criar hierarquias.

As variáveis globais são variáveis definidas no objeto de rastreamento do Analytics quando esse objeto é inicializado na página. Todas as variáveis configuradas aqui serão definidas quando o objeto de rastreamento for criado em cada página. Uma vez que essas variáveis são configuradas, elas são como qualquer outra variável definida. Especificamente, isso significa que uma regra pode modificar, alterar ou apagar essas variáveis.

Se o aplicativo da Web normalmente envia um beacon por página, esta seção pode ajudar a definir suas variáveis em um local. Se o aplicativo enviar mais de um beacon por página (como em um aplicativo de página única) e você precisar apagar suas variáveis e redefiní-las usando o mesmo objeto de rastreamento, é mais simples confiar em regras para definir e limpar as variáveis.

## Rastreamento de links

Selecione uma opção na seção Rastreamento de link da página de configuração. As opções de configuração disponíveis são as seguintes:

### Habilitar o ClickMap

O [ClickMap](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html?lang=pt-BR) é um plug-in para Internet Explorer e Firefox e um módulo do Reports &amp; Analytics.

### Rastrear os links de download

Rastreie links para arquivos do site que podem ser baixados.

Consulte [s.trackDownLoadLinks](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackdownloadlinks.html?lang=pt-BR).

### Baixar de extensões

Se a opção Rastrear os links de download estiver habilitada, é possível selecionar as extensões dos links de arquivo incluídos no Relatório de downloads se o site contiver links para arquivos com qualquer uma das extensões listadas, os URLs desses links aparecerão nos relatórios.

Consulte [s.linkDownloadFileTypes](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/linkdownloadfiletypes.html?lang=pt-BR).

### Rastrear links externos

Determina se algum link clicado é um link de saída.

Consulte [s.trackExternalLinks](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackexternallinks.html?lang=pt-BR).

**Considerações sobre aplicativos de página única:** devido ao modo de codificação dos sites de SPAs, um link interno para uma página no site de SPA pode parecer externo.

Use um dos métodos a seguir para rastrear links externos de sites de SPA:

* Se não quiser rastrear nenhum link externo do SPA, insira uma entrada na seção Nunca rastrear. Por exemplo, `http://testsite.com/spa/\#`. Todos os links \# para esse host são ignorados. Todos os links externos para outros hosts são rastreados, como [https://www.google.com](https://www.google.com).
* Se houver links que você queira rastrear no seu SPA, use a seção Rastrear sempre.

Por exemplo, em uma página spa/\#/about, você pode colocar &quot;about&quot; na seção Rastrear sempre.

A página &quot;about&quot; (sobre) será o único link externo rastreado. Nenhum outro link da página (por exemplo, [https://www.google.com](https://www.google.com)) será rastreado.

>[!NOTE]
>
>Essas duas opções se excluem mutuamente.

### Manter parâmetros de URL

Preserva as cadeias de caracteres de consulta.

Consulte [s.linkLeaveQueryString](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/linkleavequerystring.html?lang=pt-BR).

## Cookies

Configurar descrições de campo para as configurações globais de cookies usadas para implantar a extensão do Adobe Analytics. As opções de configuração disponíveis são as seguintes:

### ID de visitante

Valor único que representa um cliente tanto no sistema online como no offline.

Consulte [visitorID](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html?lang=pt-BR).

### Namespace do visitante

Variável para identificar o domínio com o qual os cookies são definidos.

Consulte [visitorNamespace](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitornamespace.html?lang=pt-BR).

### Períodos de domínio

O domínio no qual os cookies `s_cc` e `s_sq` do Analytics são definidos ao determinar o número de períodos no domínio do URL da página. Essa variável também é usada por alguns plug-ins na determinação do domínio correto para definir o cookie do plug-in.

Consulte [s.cookieDomainPeriods](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/cookiedomainperiods.html?lang=pt-BR).

### Períodos de domínio primário

A variável `fpCookieDomainPeriods` é para cookies definidos pelo JavaScript (`s_sq`, `s_cc` plug-ins) que são inerentemente cookies primários, mesmo se a implementação do usar os domínios 2o7.net ou omtrdc.net de terceiros.

Consulte [s.fpCookieDomainPeriods](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/fpcookiedomainperiods.html?lang=pt-BR).

### Duração do cookie

Determina a duração de um cookie.

Consulte [s.cookieLifetime](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/cookielifetime.html?lang=pt-BR).

### Cookies seguros

Essa variável permite que o AppMeasurement grave cookies protegidos.

Consulte [writeSecureCookies](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/writesecurecookies.html?lang=pt-BR)


## Personalizar código de página

Use o editor para personalizar o código de página.

## Adobe Audience Manager

Use esta seção da configuração de extensão para especificar o Audience Manager funciona com o Analytics.

Habilite a opção **Automatically share Analytics data with Audience Manager**.

As seguintes opções aparecem:

![](../../../images/an-ext-aam.png)

O subdomínio do Audience Manager é atribuído pelo Adobe Audience Manager. Às vezes, ele é chamado de &quot;Nome do parceiro&quot; ou &quot;Subdomínio do parceiro&quot;. Entre em contato com o consultor da Adobe ou com o Atendimento ao cliente se você não souber o Nome do parceiro.

Você pode definir as configurações avançadas selecionando **Mostrar configurações avançadas** e inserindo suas preferências.

![](../../../images/an-ext-aam-adv.png)

Para obter informações sobre cada configuração, clique no ícone de informações ou consulte a [documentação do Adobe Audience Manager](https://docs.adobe.com/content/help/pt-BR/experience-cloud/user-guides/home.translate.html).

## Tipos de ação de extensão do Analytics

Esta seção descreve os tipos de ação disponíveis na extensão do Analytics.

A extensão do Analytics fornece as seguintes ações:

* [Definir variáveis](#set-variables)
* [Enviar sinal](#send-beacon)
* [Limpar variáveis](#clear-variables)

### Definir variáveis {#set-variables}

>[!IMPORTANT]
>
>Não é possível enviar o sinal com a ação &quot;definir variáveis&quot;. Para enviar o beacon, selecione a ação &quot;enviar beacon&quot;.

Você pode escolher entre duas exibições diferentes em **Definir variáveis**:

>[!BEGINTABS]

>[!TAB Fornecer atributos individuais]

Nesta exibição, você pode especificar diferentes variáveis, como `eVars`, `Props`, `Events`.

![A página de exibição de formulário do Adobe Analytics, onde os atributos adicionais estão listados.](../../../images/adobe_analytics_extension_form_view.png)

#### eVars

Defina uma ou mais [eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=pt-BR).

1. Selecione uma eVar na lista suspensa.
1. Especifique se deseja definir o eVar como o valor (Definir como) ou copia (Duplicar de) outro eVar.
1. Forneça um valor Definir como ou selecione o eVar que deseja duplicar.
1. (Opcional) Selecione Adicionar eVar para definir mais eVars.
1. Selecione **[!UICONTROL Keep Changes]**.

#### Props

Defina uma ou mais [props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=pt-BR).

1. Selecione uma prop na lista suspensa.
1. Especifique se deseja definir o prop como o valor (Definir como) ou copiar (Duplicar de) outro eVar.
1. Forneça um valor Definir como ou selecione o eVar do qual deseja duplicar a prop.
1. (Opcional) Clique em **[!UICONTROL Add prop]** para definir mais props.
1. Selecione **[!UICONTROL Keep Changes]**.

#### Eventos

Defina um ou mais [eventos](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=pt-BR).

1. Selecione um evento na lista suspensa.
1. (Opcional) Selecione ou especifique um elemento de dados usado para a [serialização de eventos](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/event-serialization.html?lang=pt-BR).
1. (Opcional) Clique em **[!UICONTROL Add event]** para definir mais eventos.
1. Selecione **[!UICONTROL Keep Changes]**.

>[!TAB Exibição JSON]

Nesta exibição, você pode exibir e editar uma versão JSON da ação **Definir Variáveis**.

![Uma exibição que representa a configuração atual das variáveis definidas no formato JSON na extensão do Adobe Analytics.](../../../images/adobe_analytics_extension_json_view.png)

#### JSON

Na ação **Definir variáveis**, use o modo de exibição JSON para carregar, copiar ou baixar dados JSON e armazená-los em seu dispositivo.

No entanto, existem algumas limitações:

* **Código personalizado**: se você usar o código personalizado para preencher variáveis, ele não aparecerá no modo de exibição JSON. Em vez disso, um alerta é exibido ao visualizar, copiar ou baixar o JSON, indicando que as modificações feitas por meio do código personalizado não serão incluídas.
* **Copiar do atributo de URL**: a cópia de um valor de uma URL não tem suporte na exibição JSON. Um alerta é exibido para indicar essa limitação.
* **Variáveis desativadas**: as variáveis desativadas ou obsoletas são mostradas na exibição JSON e um alerta é exibido informando que as variáveis desativadas foram definidas.
* **Elementos de Dados**: os elementos de dados são representados na exibição JSON. Se os dados JSON forem copiados para outra propriedade de tags, os elementos de dados correspondentes poderão não ser definidos lá e não serão resolvidos corretamente quando forem executados.

>[!ENDTABS]

#### Hierarquia

Defina a variável [Hierarquia](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=pt-BR) do Analytics.

Especifique cada nível na hierarquia.

Se desejar, configure hierarquias adicionais.

#### Nome da página

Este valor se refere ao nome de uma determinada página e corresponde à [`pageName` variável](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/pagename.html) no Analytics.

>[!IMPORTANT]
>
>Em implementações do Adobe Experience Manager, essa variável informa ao AEM onde armazenar o relatório do Analytics buscado. Para garantir que os relatórios sejam mantidos corretamente, a cadeia de caracteres do nome da página deve ser formatada como um caminho para o site separado por dois pontos.
>
>Por exemplo, uma página da Web em `content/we-retail/language-masters/en/men.html` deve ter o valor de nome de página de `content:we-retail:language-masters:en:men`.

#### Outras informações

Especifique outras informações usadas pelas suas páginas.

Essas configurações incluem:

* URL da página
* Servidor
* Canal
* Referenciador
* Campaign
* ID de compra

  Especifique um valor ou um parâmetro de consulta

* Estado
* CEP
* ID da transação

Essas configurações podem ser encontradas no menu &quot;variáveis globais&quot; marcando a caixa de seleção &quot;Configurações adicionais&quot;.

#### Código de página personalizado

**Descrição**

Use o editor para especificar o código de página personalizado.

**Configurações**

1. Selecione **[!UICONTROL Open Editor]**.
1. Digite o código personalizado.
1. Selecione **[!UICONTROL Save]**.

### Enviar sinal {#send-beacon}

#### Incrementar uma visualização de página - s.t()

Selecione se deseja incrementar uma visualização de página.

#### Não incrementar uma visualização de página - s.tl()

Selecione se você não deseja incrementar uma visualização de página.

**Configurações**

1. Selecione um tipo de link.

   Você pode selecionar um dos seguintes:

   * Link personalizado.
   * Link de download.
   * Link de saída.

1. Defina o parâmetro para o link selecionado.
   * Link personalizado: especifique o nome do link.
   * Link de download: especifique um nome de arquivo.
   * Link de saída: especifique o URL de destino.
1. Selecione **[!UICONTROL Keep Changes]**.

### Limpar variáveis {#clear-variables}

Não há opções de configuração se o tipo de ação Limpar variáveis estiver selecionado.
