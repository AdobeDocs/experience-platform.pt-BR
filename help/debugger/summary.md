---
title: Guia Resumo
description: Saiba como usar a guia Resumo no Adobe Experience Platform Debugger.
keywords: depurador, extensão do Experience Platform Debugger, chrome, extensão, resumo, limpar, solicitações, tela resumo, solução, informações, analytics, target, dtm, audience manager, launch, serviço de id
seo-description: Experience Platform Debugger Summary Screen
seo-title: Summary Tab
uuid: 46b17eaa-b611-43cf-8c6a-67b2e9b9d940
exl-id: 91234125-15c4-4111-9ee4-f3af093a3c4d
source-git-commit: f94bba7eb4763230dae6794eb70a75f53a853c53
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 73%

---

# Guia Resumo

Para executar o Adobe Experience Platform Debugger, abra a página que deseja examinar no navegador e selecione o ícone (![](images/start-icon.jpg)) na barra do navegador. A extensão do é aberta no **Resumo** guia .

![](images/summary.jpg)

Essa tela também mostra informações sobre cada solução da Adobe Experience Cloud. As informações mostradas variam de acordo com a solução, mas geralmente incluem informações como biblioteca e versão da solução (por exemplo, &quot;AppMeasurement v2.9&quot;) e identificadores de conta (como a ID do conjunto de relatórios do Analytics, o código de cliente do Target, a ID de parceiro do Audience Manager, etc).

## Informações mostradas no Experience Platform Debugger

O Experience Platform Debugger mostra as seguintes informações para cada solução:

**Adobe Analytics**

<table id="table_BEB9CC58E59D4D86BC895A8A51D84A2C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Conjuntos de relatórios </p> </td> 
   <td colname="col2"> <p>Um <a href="https://experiencecloud.adobe.com/resources/help/pt_BR/reference/report_suites_admin.html" format="html" scope="external">conjunto de relatórios</a> define o relatório completo e independente de um site escolhido, o conjunto de sites ou o subconjunto de páginas da Web. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versão </p> </td> 
   <td colname="col2"> <p>A versão do <a href="https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=pt-BR" format="html" scope="external"> AppMeasurement</a> definida para a página. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versão do visitante </p> </td> 
   <td colname="col2"> <p>A versão da biblioteca de <a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html?lang=pt-BR" format="html" scope="external">ID de visitante</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nome da página </p> </td> 
   <td colname="col2"> <p>A variável <a href="https://experiencecloud.adobe.com/resources/help/pt_BR/sc/implement/pageName.html" format="html" scope="external">pageName</a> enviada ao Analytics que contém um nome familiar do site. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Módulos </p> </td> 
   <td colname="col2"> <p>Os módulos carregados pelo Adobe Analytics. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Audience Manager**

<table id="table_784AEABADBDA4D14BB9A7A9CB9EF07C3"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Parceiro </p> </td> 
   <td colname="col2"> <p>O <a href="https://experiencecloud.adobe.com/resources/help/pt_BR/aam/r_dil_get_partner.html" format="html" scope="external">nome do parceiro</a> para a instância DIL. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versão </p> </td> 
   <td colname="col2"> <p>O <a href="https://experiencecloud.adobe.com/resources/help/pt_BR/aam/r_api_return_versions_dil.html" format="html" scope="external">número da versão</a> da instância DIL. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>UUID </p> </td> 
   <td colname="col2"> <p>O <a href="https://experiencecloud.adobe.com/resources/help/pt_BR/aam/ids-in-aam.html" format="html" scope="external">identificador de usuário único</a> associado à instância DIL. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Tags do Adobe Experience Platform**

<table id="table_E9574975444A407887E26514D1BB1601"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Nome </p> </td> 
   <td colname="col2"> <p>O nome da tag <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html" format="https" scope="external"> propriedade</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versão </p> </td> 
   <td colname="col2"> <p>A versão da Turbina.</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Data de build </p> </td> 
   <td colname="col2"> <p>A tag <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html" format="https" scope="external"> biblioteca</a> data de compilação </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Ambiente </p> </td> 
   <td colname="col2"> <p>O <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html" format="https" scope="external"> ambiente</a> usada pela biblioteca de tags </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Extensões </p> </td> 
   <td colname="col2"> <p>As extensões usadas na página. </p> </td> 
  </tr> 
 </tbody> 
</table>

**SDK da Web da Adobe Experience Platform**

<table id="table_DC76D63FA6EF4891906B9E1D3E4A8A6C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Versão da biblioteca </p> </td> 
   <td colname="col2"> <p>O número da <a href="https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-ext-release-notes.html" format="html" scope="external">versão da biblioteca</a> do SDK da Web da Adobe Experience Platform. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Namespace</p> </td> 
   <td colname="col2"> <p>O nome identificado na extensão.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID da propriedade </p> </td> 
   <td colname="col2"> <p>O nome da propriedade de tag especificada na extensão </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Domínio de borda </p> </td> 
   <td colname="col2"> <p>O domínio do qual a extensão da Adobe Experience Platform envia e recebe dados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID da organização IMS </p> </td> 
   <td colname="col2"> <p>A organização para a qual você deseja enviar os dados na Adobe, conforme especificado na extensão. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Registro ativado </p> </td> 
   <td colname="col2"> <p>Especifica se o registro foi ativado para esta propriedade.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Serviço da Adobe Experience Cloud ID**

<table id="table_274CFCEFA8F34D16BB546B4669EC0209"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>ID da organização da Experience Cloud </p> </td> 
   <td colname="col2"> <p>A <a href="https://experiencecloud.adobe.com/resources/help/pt_BR/mcvid/" format="https" scope="external"> ID da organização</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versão </p> </td> 
   <td colname="col2"> <p>A versão da biblioteca de <a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html" format="html" scope="external">ID de visitante</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Target**

<table id="table_D30E0CD20FB04E41862B22655136E043"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Código do cliente </p> </td> 
   <td colname="col2"> <p>O <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/deploy-at-js/implementing-target-without-a-tag-manager.html" format="html" scope="external"> Código de cliente</a> do Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versão </p> </td> 
   <td colname="col2"> <p>Sua versão atual do <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/target-atjs-versions.html" format="html" scope="external"> at.js</a> ou mbox.js. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nome da solicitação global </p> </td> 
   <td colname="col2"> <p>A <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external">mbox global</a> se refere à única chamada de servidor feita na parte superior de cada página da Web na implementação do Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Evento de carregamento de página </p> </td> 
   <td colname="col2"> <p>O tipo de <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html?lang=pt-BR" format="html" scope="external">evento</a> acionado quando a página é carregada. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nome da solicitação </p> </td> 
   <td colname="col2"> <p>O nome de uma solicitação ao redor de um <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external"> local</a> na página. Disponível sem autenticação somente se você implementar o ouvinte de eventos de Depuração no código ou gerenciador de tags e ativar os <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> tokens de resposta</a> necessários na interface do usuário do Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nome da atividade </p> </td> 
   <td colname="col2"> <p>O nome da <a href="https://experienceleague.adobe.com/docs/target/using/activities/activities.html" format="html" scope="external"> campanha ou atividade</a> do Target. Disponível sem autenticação somente se você implementar o ouvinte de eventos de Depuração no código ou gerenciador de tags e ativar os <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> tokens de resposta</a> necessários na interface do usuário do Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID da atividade </p> </td> 
   <td colname="col2"> <p>A ID da atividade do Target. Disponível sem autenticação somente se você implementar o ouvinte de eventos de Depuração no código ou gerenciador de tags e ativar os <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> tokens de resposta</a> necessários na interface do usuário do Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nome da experiência </p> </td> 
   <td colname="col2"> <p>O nome da <a href="https://experienceleague.adobe.com/docs/target/using/experiences/experiences.html" format="html" scope="external"> experiência</a> do Target. Disponível sem autenticação somente se você implementar o ouvinte de eventos de Depuração no código ou gerenciador de tags e ativar os <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> tokens de resposta</a> necessários na interface do usuário do Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID da experiência </p> </td> 
   <td colname="col2"> <p>A ID da experiência do Target. Disponível sem autenticação somente se você implementar o ouvinte de eventos de Depuração no código ou gerenciador de tags e ativar os <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> tokens de resposta</a> necessários na interface do usuário do Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Oferta Nome</p> </td> 
   <td colname="col2"> <p>O nome da <a href="https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html" format="html" scope="external"> oferta</a> do Target. Disponível sem autenticação somente se você implementar o ouvinte de eventos de Depuração no código ou gerenciador de tags e ativar os <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> tokens de resposta</a> necessários na interface do usuário do Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID da oferta </p> </td> 
   <td colname="col2"> <p>A ID da oferta do Target. Disponível sem autenticação somente se você implementar o ouvinte de eventos de Depuração no código ou gerenciador de tags e ativar os <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> tokens de resposta</a> necessários na interface do usuário do Target. </p> </td> 
  </tr> 
 </tbody> 
</table>
