---
title: Visão geral da extensão de plug-ins comuns do SDK da Web
description: Saiba mais sobre a extensão de tag de plug-ins comuns do SDK da Web no Adobe Experience Platform.
source-git-commit: 4edc811f6306cd66f0ebef0a21896624f6c5e181
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 49%

---

# Visão geral da extensão de plug-ins comuns do SDK da Web

>[!IMPORTANT]
>
>A extensão deve ser usada com a extensão Adobe Experience Platform Web SDK. Para ver informações sobre a versão a ser usada com o AppMeasurement, consulte a visão geral no [Extensão de plug-ins comuns do Analytics](../plugins/overview.md).

Este documento aborda como configurar a extensão de tag Plug-ins do SDK da Web e usá-la para aumentar a variável [Extensão do Adobe Experience Platform Web SDK](../sdk/overview.md).

## Configurar a extensão de plug-ins comuns do SDK da Web

Esta seção fornece uma referência para as opções disponíveis ao configurar a extensão de plug-ins do SDK da Web.

>[!IMPORTANT]
>
>A extensão de plug-ins comuns do SDK da Web tem como objetivo aumentar a extensão do SDK da Web do Adobe Experience Platform. No entanto, não é necessário instalá-la para que a extensão funcione conforme esperado.

## Adicionar plug-ins à extensão Adobe Experience Platform Web SDK

Nenhuma configuração é necessária para inicializar ou adicionar um plug-in à sua biblioteca, fora de usar os seguintes elementos de dados nativos que são fornecidos pela extensão de plug-ins comuns do SDK da Web:

* [`getAndPersistValue`](#getAndPersistValue)
* [`getGeoCoordinates`](#getGeoCoordinates)
* [`getNewRepeat`](#getNewRepeat)
* [`getPagename`](#getPagename)
* [`getPreviousValue`](#getPreviousValue)
* [`getQueryParam`](#getQueryParam)
* [`getTimeParting`](#getTimeParting)
* [`getTimeSinceLastVisit`](#getTimeSInceLastVisit)
* [`getValOnce`](#getValOnce)
* [`getVisitDuration`](#getVisitDuration)
* [`getVisitNum`](#getVisitNum)
* [&quot;Fo&quot;](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>Esse elemento de dados define cookies e permite armazenar valores gerados pelo usuário em cookies. Consulte a documentação específica do plug-in para obter mais informações.

Permite que você configure e configure a variável [`getAndPersistValue` Plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html). O `getAndPersistValue` o elemento de dados armazena um valor em um cookie que pode ser recuperado posteriormente durante uma visita.

O `getAndPersistValue` o elemento de dados fornece os seguintes argumentos:

* `vtp` (obrigatório): o valor a ser persistido de página em página
* `cn` (opcional): o nome do cookie que armazenará o valor. Se este argumento não estiver definido, o cookie é nomeado como `"s_gapv"`
* `ex` (opcional): o número de dias antes do cookie expirar. Se esse argumento for `0` ou não estiver definido, o cookie expirará no final da visita (após 30 minutos de inatividade).

Se a variável na variável `vtp` for definido, o elemento de dados definirá o cookie e retornará o valor do cookie. Se a variável na variável `vtp` não estiver definido, então o elemento de dados retornará apenas o valor do cookie.

### `getGeoCoordinates`

>[!IMPORTANT]
>
>Este plug-in requer acesso de localização no cliente, mas não lançará uma exceção se não obtê-lo.

Permite que você configure e configure a variável [`getGeoCoordinates` Plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html). O `getGeoCoordinates` o elemento de dados captura a latitude e a longitude dos dispositivos dos visitantes.

O `getGeoCoordinates` o elemento de dados não usa nenhum argumento. Ele retorna um dos valores a seguir:

* `"geo coordinates not available"`: para dispositivos que não têm dados de localização geográfica disponíveis no momento em que o plug-in é executado. Esse valor é comum na primeira ocorrência da visita, especialmente quando os visitantes precisam primeiro fornecer consentimento em relação ao rastreamento de sua localização.
* `"error retrieving geo coordinates"`: quando o plug-in encontra erros ao tentar recuperar o local do dispositivo.
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`: onde [LATITUDE]/[LONGITUDE] são a latitude e a longitude, respectivamente.

### `getNewRepeat`

>[!IMPORTANT]
>
>Esse elemento de dados define cookies. Consulte a documentação específica do plug-in para obter mais informações.

Permite que você configure e configure a variável [`getNewRepeat` Plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html). O `getNewRepeat` elemento de dados determina se um visitante do site é um novo visitante ou um visitante repetido dentro de um número desejado de dias.

O `getNewRepeat` o elemento de dados usa os seguintes argumentos:

* `d` (número inteiro, opcional): o número mínimo de dias necessários entre visitas que redefine os visitantes novamente como `"New"`. Se esse argumento não for definido, o padrão será 30 dias.

Esse elemento de dados retorna o valor de `"New"` se o cookie definido pelo elemento de dados não existir ou tiver expirado. Retorna o valor de `"Repeat"` se o cookie definido pelo elemento de dados existir e a quantidade de tempo desde a ocorrência atual e o tempo definido no cookie forem maiores que 30 minutos. Esse método retorna o mesmo valor para uma visita inteira.

### `getPageName`

Permite que você configure e configure a variável [`getPageName` Plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html). O `getPageName` o elemento de dados cria uma versão formatada amigável e fácil de ler do URL atual.

O `getPageName` o elemento de dados usa os seguintes argumentos:

* `si` (opcional, string): uma ID inserida no início da string que representa a ID do site. Esse valor pode ser uma ID numérica ou um nome amigável. Quando não estiver definido, o padrão será o domínio atual.
* `qv` (opcional, string): uma lista, delimitada por vírgulas, de parâmetros da string de consulta que, se encontrados no URL, são adicionados à string
* `hv` (opcional, string): uma lista de parâmetros delimitada por vírgulas encontrada no hash do URL que, se encontrados no URL, são adicionados à string
* `de` (opcional, string): o delimitador usado para dividir partes individuais da string. O padrão é uma barra vertical (`|`).

O elemento de dados retorna uma string que contém uma versão amigável do URL. Normalmente, essa string é atribuída à variável `pageName`, mas também pode ser usada em outras variáveis.

### `getPreviousValue`

>[!IMPORTANT]
>
>Esse elemento de dados define cookies e permite armazenar valores gerados pelo usuário em cookies. Consulte a documentação específica do plug-in para obter mais informações.

Permite que você configure e configure a variável [`getPreviousValue` Plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html). O `getPreviousValue` o elemento de dados define uma variável como um valor definido em uma ocorrência anterior.

O `getPreviousValue` o elemento de dados usa os seguintes argumentos:

* `v` (string, obrigatório): a variável que tem o valor que você deseja transmitir para a próxima solicitação de imagem. Uma variável comumente usada para recuperar o valor da página anterior é `s.pageName`.
* `c` (string, opcional): o nome do cookie que armazena o valor.  Se esse argumento não estiver definido, ele assumirá `"s_gpv"` como padrão.

Quando você chama esse elemento de dados, ele retorna o valor da string contido no cookie. Em seguida, o plug-in redefine a validade do cookie e atribui a ele o valor de variável no argumento `v`. O cookie expira após 30 minutos de inatividade.

### `getQueryParam`

Permite que você configure e configure a variável [`getQueryParam` Plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html). O `getQueryParam` o elemento de dados extrai o valor de qualquer parâmetro de string de consulta contido em um URL. É útil para extrair códigos de campanha, internos e externos, de URLs de páginas iniciais. Também é importante ao extrair termos de pesquisa ou outros parâmetros da string de consulta. Esse elemento de dados fornece recursos robustos na análise de URLs complexos, incluindo hashes e URLs contendo vários parâmetros de string de consulta.

O `getQueryParam` o elemento de dados usa os seguintes argumentos:

* `qsp` (obrigatório): uma lista delimitada por vírgulas com parâmetros da string de consulta a serem procurados no URL. Não diferencia maiúsculas e minúsculas.
* `de` (opcional): o delimitador a ser usado se vários parâmetros da string de consulta corresponderem. O padrão é uma string vazia.
* `url` (opcional): um URL, string ou variável personalizados usados para extrair os valores de parâmetro da string de consulta. O padrão é `window.location`.

Chamar esse elemento de dados retorna um valor dependendo dos argumentos acima e do URL:

* Se um parâmetro de string de consulta correspondente não for encontrado, o método retornará uma string vazia.
* Se um parâmetro de string de consulta correspondente for encontrado, o método retornará o valor do parâmetro da string de consulta.
* Se um parâmetro de string de consulta correspondente for encontrado, mas o valor estiver vazio, o método retornará `true`.
* Se vários parâmetros de string de consulta correspondentes forem encontrados, o método retornará uma string com cada valor de parâmetro delimitado pela string no argumento `de`.

### `getTimeParting`

Permite que você configure e configure a variável [`getTimeParting` Plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html). O `getTimeParting` o elemento de dados captura os detalhes do tempo em que qualquer atividade mensurável ocorre no site. Esse elemento de dados é importante quando você deseja detalhar métricas em qualquer divisão de tempo repetível em um determinado intervalo de datas. Por exemplo, você pode comparar as taxas de conversão de dois dias diferentes da semana, como todos os domingos e todas as quintas-feiras. Você também pode comparar períodos do dia, como todas as manhãs e todas as noites.

O `getTimeParting` o elemento de dados usa o seguinte argumento:

`t` (opcional, mas recomendado, string): o nome do fuso horário para conversão da hora local do visitante.  O padrão é UTC/GMT. Consulte a [Lista de fusos horários do banco de dados TZ](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) na Wikipédia para obter uma lista completa de valores válidos.

Valores válidos comuns incluem:

* `"America/New_York"` para Eastern Time (horário do leste)
* `"America/Chicago"` para Central Time (horário central)
* `"America/Denver"` para Mountain Time (horário das montanhas)
* `"America/Los_Angeles"` para Pacific Time (horário do pacífico)

Chamar esse elemento de dados retorna uma string que contém o seguinte delimitado por uma barra vertical (`|`):

* O ano atual
* O mês atual
* O dia do mês
* O dia da semana
* A hora atual (AM/PM)

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>Esse elemento de dados define cookies. Consulte a documentação específica do plug-in para obter mais informações.

Permite que você configure e configure a variável [`getTimeSinceLastVisit` Plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html). O `getTimeSinceLastVisit` o elemento de dados rastreia quanto tempo um visitante levou para retornar ao site após sua última visita.

O `getTimeSinceLastVisit` o elemento de dados não usa nenhum argumento. Ele retorna o tempo decorrido desde o último acesso do visitante, simplificado no seguinte formato:

* O tempo entre 30 minutos e uma hora desde a última visita é definido para o referencial de meio minuto que estiver mais próximo. Por exemplo, `"30.5 minutes"`, `"53 minutes"`
* O tempo entre uma hora e um dia é arredondado para o referencial de 1/4 de hora que estiver mais próximo. Por exemplo, `"2.25 hours"`, `"7.5 hours"`
* O tempo maior que um dia é arredondado para o valor referencial de dia que estiver mais próximo. Por exemplo, `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Se um visitante não tiver visitado antes ou o se tempo decorrido for superior a dois anos, o valor será definido como `"New Visitor"`.

### `getValOnce`

>[!IMPORTANT]
>
>Esse elemento de dados define cookies e permite armazenar valores gerados pelo usuário em cookies. Consulte a documentação específica do plug-in para obter mais informações.

Permite que você configure e configure a variável [`getValOnce` Plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html). O `getValOnce` o elemento de dados impede que uma variável seja definida com o mesmo valor mais de uma vez.

O `getValOnce` o elemento de dados usa os seguintes argumentos:

* `vtc` (obrigatório, string): a variável cujo valor será verificado para conferir se já teve anteriormente um valor idêntico
* `cn` (opcional, string): o nome do cookie que contém o valor a ser verificado. O padrão é `"s_gvo"`
* `et` (opcional, número inteiro): a validade do cookie em dias (ou minutos, dependendo do argumento `ep`). O padrão é `0`, que expira no final da sessão do navegador
* `ep` (opcional, string): somente defina esse argumento se o argumento `et` também estiver definido. Configure esse argumento como `"m"` se desejar que o argumento `et` expire em minutos em vez de dias. O padrão é `"d"`, que define o argumento `et` para dias.

Se o argumento `vtc` e o valor do cookie corresponderem, esse método retornará uma string vazia. Se o argumento `vtc` e o valor do cookie não corresponderem, o método retornará o argumento `vtc` como uma string.

### `getVisitDuration`

>[!IMPORTANT]
>
>Esse elemento de dados define cookies. Consulte a documentação específica do plug-in para obter mais informações.

Permite que você configure e configure a variável [`getVisitDuration` Plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html). O `getVisitDuration` o elemento de dados rastreia o tempo em minutos que o visitante esteve no site até o momento.

O `getVisitDuration` o elemento de dados não usa nenhum argumento. Ele retorna um dos valores a seguir:

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` (onde `[x]` é o número de minutos passados desde que o visitante chegou ao site)

### `getVisitNum`

>[!IMPORTANT]
>
>Esse elemento de dados define cookies. Consulte a documentação específica do plug-in para obter mais informações.

Permite que você configure e configure a variável [`getVisitNum` Plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html). O `getVisitNum` o elemento de dados retorna o número da visita para todos os visitantes que chegam ao site dentro do número desejado de dias.

O `getVisitNum` o elemento de dados usa os seguintes argumentos:

* `rp` (opcional, número inteiro OU string): o número de dias antes da redefinição do contador do número de visitas.  O valor padrão é `365` quando um valor não está definido.
   * Quando esse argumento é `"w"`, o contador é reiniciado no final da semana (neste sábado, às 23:59)
   * Quando esse argumento é `"m"`, o contador é redefinido no final do mês (o último dia deste mês)
   * Quando esse argumento é `"y"`, o contador é reiniciado no final do ano (31 de dezembro)
* `erp` (opcional, booleano): Quando o argumento `rp` é um número, esse argumento determina se a expiração do número de visitas deve ser estendida. Se definido como `true`, as ocorrências subsequentes do site redefinirão o contador de número de visitas. Se definido como `false`, as ocorrências subsequentes do site serão estendidas quando o contador de número de visitas é redefinido. O padrão é `true`. Esse argumento não é válido quando o argumento `rp` é uma string.

O número de visitas aumenta sempre que o visitante retorna ao site após 30 minutos de inatividade. Chamar esse método retorna um número inteiro que representa o número de visita atual do visitante.

### `p_fo` (Somente a primeira página)

Permite que você configure e configure a variável [`p_fo` Plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html). O `p_fo` o elemento de dados é um utilitário que verifica a existência de um objeto JavaScript específico. Se o objeto não existir, o plug-in criará o objeto e retornará `true`. Se o objeto JavaScript já existir na página, ele retornará `false`. Esse elemento de dados é útil para executar o código exatamente uma vez em uma página.

O `p_fo` o elemento de dados usa os seguintes argumentos:

* `on` (obrigatório, string): O nome do objeto JavaScript que o elemento de dados cria se o objeto ainda não existir na página.

Se o objeto ainda não existir, esse método retornará `true` e criará o objeto. Se o objeto já existir, esse método retornará `false`.
