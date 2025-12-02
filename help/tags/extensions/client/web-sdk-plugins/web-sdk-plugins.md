---
title: Visão geral da extensão de plug-ins comuns do Web SDK
description: Saiba mais sobre a extensão de tag de plug-ins comuns do Web SDK na Adobe Experience Platform.
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '2063'
ht-degree: 0%

---

# Visão geral da extensão de plug-ins comuns do Web SDK

>[!IMPORTANT]
>
>A extensão deve ser usada com a extensão Adobe Experience Platform Web SDK. Para ver informações sobre a versão a ser usada com o AppMeasurement, consulte a visão geral na [Extensão de plug-ins comuns do Analytics](../plugins/overview.md).

Este documento aborda como configurar a extensão de tag de plug-ins do Web SDK e usá-la para aumentar a [extensão do Adobe Experience Platform Web SDK](../web-sdk/overview.md).

## Configurar a extensão de plug-ins comuns do Web SDK

Esta seção fornece uma referência para as opções disponíveis ao configurar a extensão de plug-ins do Web SDK.

>[!IMPORTANT]
>
>A extensão de plug-ins comuns do Web SDK tem como objetivo aumentar a extensão do Adobe Experience Platform Web SDK. No entanto, não é necessário tê-la instalada para que a extensão funcione conforme esperado.

## Adicionar plug-ins à extensão do Adobe Experience Platform Web SDK

Nenhuma configuração é necessária para inicializar ou adicionar um plug-in à biblioteca do usando os seguintes elementos de dados nativos fornecidos pela extensão de plug-ins comuns do Web SDK:

* [&quot;getAndPersistValue&quot;](web-sdk-plugins.md#getandpersistvalue)
* [&quot;getGeoCoordinates&quot;](#getgeocoordinates)
* [&quot;getNewRepeat&quot;](#getnewrepeat)
* [&quot;getPageName&quot;](#getpagename)
* [&quot;getPreviousValue&quot;](#getpreviousvalue)
* [&quot;getQueryParam&quot;](#getqueryparam)
* [&quot;getTimeParting&quot;](#gettimeparting)
* [&quot;getTimeSinceLastVisit&quot;](#gettimesincelastvisit)
* [&quot;getValOnce&quot;](#getvalonce)
* [&quot;getVisitDuration&quot;](#getvisitduration)
* [&quot;getVisitNum&quot;](#getvisitnum)
* [`p_fo`](#p_fo-page-first-only)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>Esse elemento de dados define cookies e permite armazenar valores gerados pelo usuário em cookies. Consulte a documentação específica do plug-in para obter mais informações.

Permite configurar o [`getAndPersistValue` plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html). O elemento de dados `getAndPersistValue` armazena um valor em um cookie que pode ser recuperado posteriormente durante uma visita.

O elemento de dados `getAndPersistValue` fornece os seguintes argumentos:

* `vtp` (obrigatório): o valor a ser persistido de página em página
* `cn` (opcional): o nome do cookie que armazenará o valor. Se este argumento não estiver definido, o cookie é nomeado como `"s_gapv"`
* `ex` (opcional): o número de dias antes do cookie expirar. Se esse argumento for `0` ou não estiver definido, o cookie expirará no final da visita (após 30 minutos de inatividade).

Se a variável no argumento `vtp` estiver definida, o elemento de dados definirá o cookie e retornará o valor do cookie. Se a variável no argumento `vtp` não estiver definida, o elemento de dados apenas retornará o valor do cookie.

### `getGeoCoordinates`

>[!IMPORTANT]
>
>Este plug-in requer acesso de localização no cliente, mas não lançará uma exceção se não obtê-lo.

Permite configurar o [`getGeoCoordinates` plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html). O elemento de dados `getGeoCoordinates` captura a latitude e a longitude dos dispositivos dos visitantes.

O elemento de dados `getGeoCoordinates` não usa nenhum argumento. Ele retorna um dos seguintes valores:

* `"geo coordinates not available"`: Para dispositivos que não têm dados de localização geográfica disponíveis no momento em que o plug-in é executado. Esse valor é comum na primeira ocorrência da visita, especialmente quando os visitantes precisam primeiro fornecer consentimento sobre o rastreamento de sua localização.
* `"error retrieving geo coordinates"`: quando o plug-in encontra erros ao tentar recuperar o local do dispositivo
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`: Onde `[LATITUDE]/[LONGITUDE]` são a latitude e a longitude, respectivamente.

### `getNewRepeat`

>[!IMPORTANT]
>
>Esse elemento de dados define cookies. Consulte a documentação específica do plug-in para obter mais informações.

Permite configurar o [`getNewRepeat` plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html). O elemento de dados `getNewRepeat` determina se um visitante do site é um novo visitante ou um visitante repetido dentro de um número desejado de dias.

O elemento de dados `getNewRepeat` usa os seguintes argumentos:

* `d` (inteiro, opcional): o número mínimo de dias necessários entre visitas que redefine os visitantes novamente como `"New"`. Se esse argumento não for definido, o padrão será 30 dias.

Esse elemento de dados retornará o valor de `"New"` se o cookie definido pelo elemento de dados não existir ou tiver expirado. Ele retorna o valor `"Repeat"` se o cookie definido pelo elemento de dados existir e o tempo desde a ocorrência atual e o tempo definido no cookie forem maiores que 30 minutos. Esse método retorna o mesmo valor para uma visita inteira.

### `getPageName`

Permite configurar o [`getPageName` plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html). O elemento de dados `getPageName` cria uma versão formatada amigável e fácil de ler da URL atual.

O elemento de dados `getPageName` usa os seguintes argumentos:

* `si` (opcional, cadeia de caracteres): uma ID inserida no início da cadeia de caracteres que representa a ID do site. Esse valor pode ser uma ID numérica ou um nome amigável. Quando não estiver definido, o padrão será o domínio atual.
* `qv` (opcional, cadeia de caracteres): uma lista delimitada por vírgulas de parâmetros da cadeia de caracteres de consulta que, se encontrados na URL, são adicionados à cadeia de caracteres
* `hv` (opcional, string): uma lista de parâmetros delimitada por vírgulas encontrada no hash da URL que, se encontrados na URL, são adicionados à string
* `de` (opcional, string): o delimitador usado para dividir partes individuais da string. O padrão é um pipe (`|`).

O elemento de dados retorna uma string que contém uma versão amigável do URL. Normalmente, essa cadeia de caracteres é atribuída à variável `pageName`, mas também pode ser usada em outras variáveis.

### `getPreviousValue`

>[!IMPORTANT]
>
>Esse elemento de dados define cookies e permite armazenar valores gerados pelo usuário em cookies. Consulte a documentação específica do plug-in para obter mais informações.

Permite configurar o [`getPreviousValue` plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html). O elemento de dados `getPreviousValue` define uma variável como um valor definido em uma ocorrência anterior.

O elemento de dados `getPreviousValue` usa os seguintes argumentos:

* `v` (cadeia de caracteres, obrigatório): a variável que tem o valor que você deseja transmitir para a próxima solicitação de imagem. Uma variável comumente usada é `s.pageName` para recuperar o valor da página anterior.
* `c` (cadeia de caracteres, opcional): o nome do cookie que armazena o valor.  Se este argumento não estiver definido, o padrão será `"s_gpv"`.

Quando você chama esse elemento de dados, ele retorna o valor da string contido no cookie. Em seguida, o plug-in redefine a expiração do cookie e atribui a ele o valor de variável no argumento `v`. O cookie expira após 30 minutos de inatividade.

### `getQueryParam`

Permite configurar o [`getQueryParam` plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html). O elemento de dados `getQueryParam` extrai o valor de qualquer parâmetro de cadeia de caracteres de consulta contido em uma URL. É útil para extrair códigos de campanha, internos e externos, de URLs de páginas iniciais. Também é importante ao extrair termos de pesquisa ou outros parâmetros da string de consulta. Esse elemento de dados fornece recursos robustos para a análise de URLs complexos, incluindo hashes e URLs que contêm vários parâmetros de cadeia de caracteres de consulta.

O elemento de dados `getQueryParam` usa os seguintes argumentos:

* `qsp` (obrigatório): uma lista delimitada por vírgulas com parâmetros da cadeia de caracteres de consulta a serem procurados na URL. Não diferencia maiúsculas de minúsculas.
* `de` (opcional): o delimitador a ser usado se vários parâmetros da cadeia de caracteres de consulta corresponderem. O padrão é uma string vazia.
* `url` (opcional): uma URL, cadeia de caracteres ou variável personalizada da qual extrair os valores de parâmetro da cadeia de caracteres de consulta. O padrão é `window.location`.

Chamar esse elemento de dados retorna um valor dependendo dos argumentos acima e da URL:

* Se um parâmetro de string de consulta correspondente não for encontrado, o método retornará uma string vazia.
* Se um parâmetro de string de consulta correspondente for encontrado, o método retornará o valor do parâmetro da string de consulta.
* Se um parâmetro de string de consulta correspondente for encontrado, mas o valor estiver vazio, o método retornará `true`.
* Se vários parâmetros de cadeia de caracteres de consulta correspondentes forem encontrados, o método retornará uma cadeia de caracteres com cada valor de parâmetro delimitado pela cadeia de caracteres no argumento `de`.

### `getTimeParting`

Permite configurar o [`getTimeParting` plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html). O elemento de dados `getTimeParting` captura os detalhes do tempo de execução de qualquer atividade mensurável que ocorre no site. Esse elemento de dados é importante quando você deseja detalhar métricas em qualquer divisão de tempo repetível, dentro de um intervalo de datas específico. Por exemplo, você pode comparar as taxas de conversão entre dois dias diferentes da semana, como todos os domingos e todas as quintas-feiras. Você também pode comparar períodos do dia, como todas as manhãs e todas as noites.

O elemento de dados `getTimeParting` usa o seguinte argumento:

`t` (opcional, mas recomendado, cadeia de caracteres): O nome do fuso horário para conversão da hora local do visitante.  O padrão é UTC/GMT. Consulte a [Lista de fusos horários do banco de dados TZ](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) na Wikipédia para obter uma lista completa de valores válidos.

Valores válidos comuns incluem:

* `"America/New_York"` para Eastern Time (horário do leste)
* `"America/Chicago"` para Central Time (horário central)
* `"America/Denver"` para Mountain Time (horário das montanhas)
* `"America/Los_Angeles"` para Pacific Time (horário do pacífico)

Chamar esse elemento de dados retorna uma cadeia de caracteres que contém os itens a seguir delimitados por uma barra vertical (`|`):

* O ano atual
* O mês atual
* O dia do mês
* O dia da semana
* A hora atual (AM/PM)

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>Esse elemento de dados define cookies. Consulte a documentação específica do plug-in para obter mais informações.

Permite configurar o [`getTimeSinceLastVisit` plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html). O elemento de dados `getTimeSinceLastVisit` rastreia quanto tempo um visitante levou para retornar ao site após sua última visita.

O elemento de dados `getTimeSinceLastVisit` não usa nenhum argumento. Ele retorna o tempo decorrido desde o último acesso do visitante, simplificado no seguinte formato:

* O tempo entre 30 minutos e uma hora desde a última visita é definido para o referencial de meio minuto que estiver mais próximo. Por exemplo, `"30.5 minutes"`, `"53 minutes"`
* O tempo entre uma hora e um dia é arredondado para o referencial de 1/4 de hora que estiver mais próximo. Por exemplo, `"2.25 hours"`, `"7.5 hours"`
* O tempo maior que um dia é arredondado para o valor referencial de dia que estiver mais próximo. Por exemplo, `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Se um visitante não tiver visitado antes ou o tempo decorrido for superior a dois anos, o valor será definido como `"New Visitor"`.

### `getValOnce`

>[!IMPORTANT]
>
>Esse elemento de dados define cookies e permite armazenar valores gerados pelo usuário em cookies. Consulte a documentação específica do plug-in para obter mais informações.

Permite configurar o [`getValOnce` plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html). O elemento de dados `getValOnce` impede que uma variável seja definida com o mesmo valor mais de uma vez.

O elemento de dados `getValOnce` usa os seguintes argumentos:

* `vtc` (obrigatório, string): a variável cujo valor será verificado para conferir se já teve anteriormente um valor idêntico
* `cn` (opcional, cadeia de caracteres): o nome do cookie que contém o valor a ser verificado. O padrão é `"s_gvo"`
* `et` (opcional, inteiro): a expiração do cookie em dias (ou minutos, dependendo do argumento `ep`). O padrão é `0`, que expira no final da sessão do navegador
* `ep` (opcional, string): somente defina este argumento se o argumento `et` também estiver definido. Defina esse argumento como `"m"` se desejar que o argumento `et` expire em minutos em vez de dias. O padrão é `"d"`, que define o argumento `et` para dias.

Se o argumento `vtc` e o valor do cookie corresponderem um ao outro, esse método retornará uma string vazia. Se o argumento `vtc` e o valor do cookie não corresponderem um ao outro, o método retornará o argumento `vtc` como uma string.

### `getVisitDuration`

>[!IMPORTANT]
>
>Esse elemento de dados define cookies. Consulte a documentação específica do plug-in para obter mais informações.

Permite configurar o [`getVisitDuration` plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html). O elemento de dados `getVisitDuration` rastreia o tempo em minutos do visitante no site até o momento.

O elemento de dados `getVisitDuration` não usa nenhum argumento. Ele retorna um dos seguintes valores:

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` (onde `[x]` é o número de minutos passados desde que o visitante chegou ao site)

### `getVisitNum`

>[!IMPORTANT]
>
>Esse elemento de dados define cookies. Consulte a documentação específica do plug-in para obter mais informações.

Permite configurar o [`getVisitNum` plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html). O elemento de dados `getVisitNum` retorna o número da visita para todos os visitantes que chegam ao site dentro do número desejado de dias.

O elemento de dados `getVisitNum` usa os seguintes argumentos:

* `rp` (opcional, número inteiro OU cadeia de caracteres): o número de dias antes da redefinição do contador do número de visitas.  O padrão é `365` quando um valor não está definido.
   * Quando esse argumento é `"w"`, o contador é reiniciado no final da semana (neste sábado, às 23:00 horas):59
   * Quando esse argumento é `"m"`, o contador é redefinido no final do mês (o último dia deste mês)
   * Quando esse argumento é `"y"`, o contador é reiniciado no final do ano (31 de dezembro)
* `erp` (opcional, booleano): quando o argumento `rp` é um número, esse argumento determina se a expiração do número de visitas deve ser estendida. Se definido como `true`, as ocorrências subsequentes do site redefinirão o contador de número de visitas. Se definido como `false`, as ocorrências subsequentes do site serão estendidas quando o contador de número de visitas é redefinido. O padrão é `true`. Este argumento não é válido quando o argumento `rp` é uma cadeia de caracteres.

O número de visitas aumenta sempre que o visitante retorna ao site após 30 minutos de inatividade. Chamar esse método retorna um número inteiro que representa o número de visita atual do visitante.

### `p_fo` (Somente a primeira página)

Permite configurar o [`p_fo` plug-in do Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html). O elemento de dados `p_fo` é um utilitário que verifica a existência de um objeto JavaScript específico. Se o objeto não existe, o plug-in cria o objeto e retorna `true`. Se o objeto JavaScript já existir na página, ele retornará `false`. Esse elemento de dados é útil para executar o código exatamente uma vez em uma página.

O elemento de dados `p_fo` usa os seguintes argumentos:

* `on` (obrigatório, string): o nome do objeto JavaScript que o elemento de dados cria se o objeto ainda não existir na página.

Se o objeto ainda não existir, esse método retornará `true` e criará o objeto. Se o objeto já existir, esse método retornará `false`.
