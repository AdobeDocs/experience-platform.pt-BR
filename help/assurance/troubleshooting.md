---
title: Guia de solução de problemas do Adobe Experience Platform Assurance
description: Este documento descreve soluções para problemas comuns ao usar o Adobe Experience Platform Assurance.
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---

# Solução de problemas do Adobe Experience Platform Assurance

Se você estiver tendo problemas para fazer com que o Assurance funcione, consulte as sugestões nos tópicos a seguir do problema para resolver problemas comuns.

Para permitir uma implementação mais suave e descobrir possíveis problemas, verifique se o registro do SDK está ativado por [Habilitar o log de depuração](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) na seção Introdução.

Você pode alterar os níveis de log do SDK usando o [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API.

## Problemas no dispositivo e no aplicativo

### O código QR não abre o aplicativo

* Acesse o link diretamente. Copiar o link de **Detalhes da sessão**. Cole-o na barra de endereços do navegador do dispositivo para abri-lo. Se não abrir, consulte a seção [O aplicativo não abrirá o link](#app-does-not-open-link).
* Use um leitor QR diferente. No iOS 11 ou superior, use o aplicativo Foto para ler o código QR.

### O aplicativo não abre o link

* Verifique se a implementação do deep link está configurada corretamente no aplicativo.
   * **Android:** Deep Links (links de aplicativos)
      * [Criar deep links para o contexto de aplicativos](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** Esquema de URL personalizado ou links universais
      * [Definição de um esquema de URL personalizado para seu aplicativo](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [Suporte a links universais no aplicativo](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>Para Android, o `startSession` A API não precisa ser chamada explicitamente. Para o iOS, use a API conforme descrito em [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### A sobreposição de autenticação é exibida, mas o aplicativo falha ao se conectar

* Verifique a conectividade do dispositivo com a Internet por meio do navegador da Web do dispositivo.
* Se o aplicativo nunca se conectou com êxito ao serviço do Assurance, verifique se ele está configurado corretamente para o Assurance. Consulte as instruções de instalação do [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md) Biblioteca do SDK.
* Verifique se a sessão corresponde ao link e está sendo inserida corretamente para a sessão esperada. Consulte [Mensagem de log &quot;As informações da OrgID não estão disponíveis&quot;](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (isso é incomum e relevante somente se você tiver acesso a mais de uma instância ORG).

### Depuração do Adobe Analytics

**Status do pós-processamento - Sem sinalizador de depuração**

Na visualização Eventos do Analytics, se os eventos falharem com o status pós-processado &quot;Sem sinalizador de depuração&quot;, sua versão atual do Adobe Analytics ou do Assurance SDK pode não ser compatível com o recurso Depuração do Analytics.
Atualize as extensões do Adobe Analytics e do Assurance SDK para as versões mais recentes para resolver esse problema.

| Exigência de versão mínima | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance | > 1.0.0 | > 1.0.0 |

### Compatibilidade do React Native MobileCore e do AEPAssurance

| Versão de garantia da AEP | Versão Mobile Core | Instruções de instalação |
| --------------------- | ------------------- | ------------------- |
| react-native-aepassurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

Se você estiver usando `react-native-acpcore` com o Assurance, o aplicativo React Native pode falhar ao criar com uma das seguintes mensagens de erro:

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

ou

```
AppDelegate: AEPAssurance.h file not found
```

**Solução**

Se isso ocorrer, faça o downgrade do `react-native-aepassurance` usando o seguinte comando npm:

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

Esse erro ocorre porque `react-native-acpcore` a extensão é **somente** compatível com `react-native-aepassurance` versões 2.x.x e posteriores.
