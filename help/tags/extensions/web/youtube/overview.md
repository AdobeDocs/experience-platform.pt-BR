---
title: Visão geral da extensão de rastreamento de vídeo do YouTube
description: Saiba mais sobre a extensão de tag de rastreamento de vídeo do YouTube na Adobe Experience Platform.
exl-id: 703f7b04-f72f-415f-80d6-45583fa661bc
source-git-commit: bbaf272313d5a8afe33178598063164792f4d8c0
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 97%

---

# Visão geral da extensão de rastreamento de vídeo do YouTube

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

**Pré-requisitos**

Cada propriedade de tag da Adobe Experience Platform exige que as seguintes extensões sejam instaladas e configuradas na tela Extensões:

* Adobe Analytics
* Serviço do Experience Cloud Visitor ID
* Extensão principal

Use o trecho de código [&quot;Incorpore um reprodutor usando uma tag \&lt;iframe\>&quot;](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds) dos documentos de desenvolvedor do Google no HTML de cada página da Web em que um reprodutor de vídeo deve ser renderizado.

Esta extensão, versão 2.0.1, aceita a incorporação de um ou mais vídeos do YouTube em uma única página da Web inserindo um atributo `id` com um valor único na tag de script iframe e anexando `enablejsapi=1` e `rel=0` ao final do valor de atributo `src`, se ainda não estiver incluído. Por exemplo:

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

Essa extensão também foi projetada para verificar dinamicamente se há um valor de atributo de identificador exclusivo, como `player1`, independendemente de os parâmetros de sequência de consulta `enablejsapi` e `rel` existirem e de os respectivos valores esperados estarem corretos. Como resultado, a tag do script do YouTube pode ser adicionada a uma página da Web com ou sem o atributo `id` e se os parâmetros da sequência de consulta `enablejsapi` e `rel` estão ou não incluídos.

>[!NOTE]
>
>Em páginas com mais de um vídeo, cada um usa o mesmo conjunto de configurações definido na regra de tag executada nessa página. Por exemplo, se você criar uma regra com um evento que é acionado no vídeo 50% concluído, cada vídeo na página acionará a regra no ponto de sinalização de 50%.

A extensão depende da seguinte lógica para reescrever os iFrames:

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

Portanto, haverá uma pequena oscilação depois que a página for carregada. Esse comportamento é esperado.

## Elementos de dados

Há seis elementos de dados disponíveis na extensão, e nenhum deles precisa ser configurado.

* **Posição do indicador de reprodução:** registra o local, em segundos, da posição do indicador de reprodução na linha do tempo do vídeo quando ele é chamado em uma regra de tag.
* **ID do vídeo:** especifica a ID do YouTube associada ao vídeo.
* **Nome do vídeo:** especifica o nome descritivo ou amigável do vídeo.
* **URL do vídeo:** retorna o URL do YouTube.com para o vídeo atualmente carregado/reproduzido.
* **Duração do vídeo:** registra a duração total, em segundos, do conteúdo de vídeo.
* **Versão da extensão:** esse elemento de dados registra a versão da Extensão de rastreamento do YouTube, como &quot;Video Tracking_YouTube_2.0.0&quot;, por exemplo.

## Eventos

Há oito eventos disponíveis na extensão. Somente o Rastreamento de ponto de sinalização personalizado precisa ser configurado.

* **Vídeo pronto:** acionado quando o vídeo está sinalizado e pronto para ser reproduzido.
* **Início do vídeo:** acionado quando o vídeo é iniciado pela primeira vez e quando `player.getCurrentTime() === 0`
* **Repetição de vídeo:** acionado quando o vídeo é sinalizado e reproduzido novamente após o início. Esse acionador será ativado a cada repetição.
* **Pausa do vídeo:** acionado quando o vídeo é pausado.
* **Retomada do vídeo:** acionado quando o vídeo é retomado e quando `player.getCurrentTime() !== 0`
* **Rastreamento de sinalização personalizado:** acionado quando o vídeo atinge a porcentagem limite de vídeo especificada..
Por exemplo, se um vídeo tiver 60 segundos e o ponto de sinalização especificado for 50%, o evento será acionado quando a posição do indicador de reprodução for igual a 30 segundos. O rastreamento do ponto de sinalização se aplica à reprodução inicial e à repetição. Observe que se o usuário buscar em um ponto de sinalização, o evento não será acionado. Os eventos de ponto de sinalização só são acionados quando o indicador de reprodução cruza o local do ponto de sinalização calculado na linha do tempo e o player de vídeo está reproduzindo.
* **Buffer de vídeo:** acionado quando o player baixa determinada quantidade de dados antes de começar a reproduzir o vídeo.
* **Vídeo encerrado:** acionado quando um vídeo é totalmente concluído.

## Uso

Uma regra de tag pode ser definida para cada evento de vídeo (os sete eventos listados acima). Crie uma regra específica de tag para cada evento que desejar rastrear. Caso não queira rastrear um evento, bastará omitir a criação de uma regra para ele.

As regras têm três ações:

* **Definir variáveis:** defina as variáveis do Adobe Analytics (mapeie para todos os elementos de dados incluídos ou alguns deles).
* **Enviar beacon:** envie o beacon do Adobe Analytics como uma chamada de rastreamento de link personalizado e forneça um valor &quot;Nome do link&quot;.
* **Limpar variáveis:** limpe as variáveis do Adobe Analytics.

## Exemplo de regra de tag para &quot;Início do vídeo&quot;

Os objetos de extensão de vídeo a seguir devem ser incluídos.

* **Eventos**: &quot;Início do vídeo&quot; (esse evento faz com que a regra seja acionada quando o visitante começa a reproduzir um vídeo do YouTube.)

* **Condição**: nenhuma

* **Ações**: Use a **Extensão do Analytics** para a ação &quot;Definir variáveis&quot; para mapear:

   * O evento para Início do vídeo,
   * Uma prop/eVar para o elemento de dados Duração do vídeo
   * Uma prop/eVar para o elemento de dados ID do vídeo
   * Uma prop/eVar para o elemento de dados Nome do vídeo
   * Uma prop/eVar para o elemento de dados URL do vídeo

   Em seguida, inclua a ação &quot;Enviar beacon&quot; (`s.tl`) com o nome do link &quot;iniciar vídeo&quot;, seguido da ação &quot;Limpar variáveis&quot;.

>[!TIP]
> 
>Para implementações em que não é possível usar várias eVars ou props para cada elemento de vídeo, os valores do elemento de dados podem ser concatenados na Platform, analisados em relatórios de classificação usando a ferramenta Construtor de regras de classificação, conforme explicado em [https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=pt-BR](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=pt-BR), e aplicados como um segmento no Analysis Workspace.

Para concatenar valores de informações de vídeo, crie um novo elemento de dados chamado &quot;Metadados de vídeo&quot; e programe-o para obter todos os elementos de dados de vídeo (listados acima) e reuni-los. Por exemplo:

```javascript
var r = [];

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```
