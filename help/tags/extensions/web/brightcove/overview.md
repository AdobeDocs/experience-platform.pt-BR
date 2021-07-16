---
title: Visão geral da extensão de rastreamento de vídeo BrightCove
description: Saiba mais sobre a extensão da tag BrightCove Video Tracking no Adobe Experience Platform.
source-git-commit: 5da1fd18e0032c5e3d6695639f98a7ee683819f1
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 40%

---

# Visão geral da extensão de rastreamento de vídeo BrightCove

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

## Pré-requisitos

Cada propriedade de tag no Adobe Experience Platform precisa das seguintes extensões instaladas e configuradas na tela Extension:

* Adobe Analytics
* Serviço do Experience Cloud Visitor ID
* Extensões principais instaladas

Use o trecho de código &quot;Código incorporado na página (avançado)&quot; no HTML de cada página da Web em que um reprodutor de vídeo deve ser renderizado. O trecho HTML &quot;Código incorporado na página (avançado)&quot; pode ser encontrado na [documentação do Brightcove](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). O link a seguir fornece mais informações sobre [como gerar código incorporado para players de visualização e vídeo publicados](https://studio.support.brightcove.com/players/generating-player-embed-code.html).

Esta extensão versão 1.1.0 é compatível com a incorporação de vários vídeos do BrightCove em uma única página da Web. Se houver várias `id` propriedades nas tags incorporadas avançadas, verifique se cada uma tem valores exclusivos. Por exemplo, `player1`, `player2` e assim por diante.

>[!NOTE]
>
>Em páginas com vários vídeos, cada vídeo usa o mesmo conjunto de configurações na regra de tags executada nessa página. Por exemplo, se você criar uma regra com um evento que é acionado no vídeo 50% concluído, cada vídeo na página acionará a regra no ponto de sinalização de 50%.

Se a página da Web que usa essa extensão interagir com o vídeo antes que o script relevante tenha sido totalmente carregado, há duas ações que você pode tomar para corrigir o problema. Em primeiro lugar, é possível carregar a biblioteca de tags de forma síncrona e, em segundo lugar, colocar o elemento `<script type="text/javascript">\_satellite.pageBottom();\</script\>` antes de o vídeo ser incorporado na página.

Consulte a [documentação da API do BrightCove](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer) para obter mais informações sobre os métodos e eventos de componentes usados nesta extensão.

## Elementos de dados

Há sete elementos de dados disponíveis na extensão, e nenhum deles precisa ser configurado.

* **Posição do indicador de reprodução:** quando esse elemento de dados é chamado em uma regra de tag, ele registra, em segundos, o local da posição do indicador de reprodução na linha do tempo do vídeo.
* **ID da conta do vídeo:** esse elemento de dados registra a ID da conta do Brightcove que publicou o vídeo.
* **Duração do vídeo:** esse elemento de dados registra a duração total, em segundos, do conteúdo do vídeo. Além disso, uma Métrica calculada pode ser criada no Analytics para converter o número em segundos, em minutos ou horas.
* **Suporte para anúncio de vídeo:**  esse elemento de dados especifica se os anúncios são ou não compatíveis com o vídeo.
* **ID do vídeo:** esse elemento de dados especifica a ID do BrightCove associada ao vídeo.
* **Nome do vídeo:** esse elemento de dados especifica o nome descritivo ou amigável do vídeo.
* **Tags de vídeo:** esse elemento de dados especifica os scripts específicos associados ao vídeo.

## Eventos

Há sete eventos disponíveis na extensão. Somente o rastreamento de ponto de sinalização personalizado requer configuração.

* **Custom Cue Point Tracking:** esse evento dispara quando o vídeo atinge a porcentagem limite de vídeo especificada. Por exemplo, se um vídeo tiver 60 segundos e o ponto de sinalização especificado for 50%, o evento será acionado na marca de 30 segundos.

>[!NOTE]
>
>Esse evento dispara toda vez que esse ponto de sinalização é atingido. Por exemplo, se o usuário atingir a marca de 50%, buscar o vídeo antes da marca de 50% e, em seguida, atingir a marca de 50% novamente, o gatilho será acionado novamente.

* **Vídeo concluído:** esse evento dispara quando um vídeo é totalmente concluído.
* **Metadados de vídeo carregados:** esse evento é acionado quando o reprodutor recebe informações de duração e dimensão iniciais.
* **Pausar vídeo:** esse evento é acionado quando o vídeo é pausado.
* **Resumo do vídeo:** esse evento é acionado quando o conteúdo do vídeo é retomado após um evento de pausa.
* **Alteração na tela do vídeo:** o evento é acionado quando o vídeo é alternado para dentro ou para fora do modo de tela cheia.
* **Início do vídeo:** esse evento é acionado quando o conteúdo do vídeo é iniciado pela primeira vez.

## Uso

Uma regra de tag pode ser definida para cada evento de vídeo (os sete eventos listados acima). Crie uma regra de tag específica para cada evento que deseja rastrear. Caso não queira rastrear um evento, basta omitir a criação de uma regra para ele.

As regras têm três ações:

1. Definir as variáveis do Adobe Analytics. (Crie elementos de dados para todos ou alguns dos elementos de dados listados acima.)
1. Enviar o sinal do Adobe Analytics.
1. Limpar as variáveis do Adobe Analytics.

## Exemplo de regra de tag para &quot;Início do vídeo&quot;

Os seguintes objetos de extensão de vídeo devem ser incluídos:

* **Eventos**

   1. &quot;Início do vídeo&quot;: este evento faz com que a regra seja acionada quando os visitantes começam a reproduzir um vídeo do BrightCove.

* **Condição**

   1. None

* **Ações**

   1. Em uma ação &quot;Set Variables&quot; do Analytics, defina:

      * O evento para **Início do vídeo** (exemplo: event17)
      * Uma prop/eVar para o elemento de dados **Nome do vídeo** (exemplo: eVar10)
      * Uma prop/eVar para o elemento de dados **Duração do vídeo** (exemplo: eVar11)
      * Uma prop/eVar para o elemento de dados **Local do vídeo atual** (exemplo: eVar12)
   1. A ação &quot;Send Beacon&quot; do Analytics (`s.tl`)
   1. A ação &quot;Clear Variables&quot; do Analytics


>[!TIP]
>
>Para aqueles que não desejam provisionar várias eVars ou props para cada elemento de vídeo, há um método alternativo. Os valores do elemento de dados podem ser concatenados na interface do usuário da coleta de dados. Em seguida, são analisados nos relatórios de classificação usando a ferramenta Criador de regras de classificação. Consulte a documentação da [ferramenta Criador de regras de classificação](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=pt-BR) para obter mais informações. Por fim, elas são aplicadas como um segmento no Analysis Workspace.
>
>Para fazer isso, crie um novo elemento de dados chamado &quot;Video MetaData&quot; e programe-o para reunir todos os elementos de dados de vídeo (listados acima) e concatená-los juntos.

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
