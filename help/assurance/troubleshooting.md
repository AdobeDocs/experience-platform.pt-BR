---
title: Guia de solução de problemas do Adobe Experience Platform Assurance
description: Este documento descreve soluções para problemas comuns ao usar o Adobe Experience Platform Assurance.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---


# Solução de problemas do Adobe Experience Platform Assurance

Se tiver problemas para fazer com que o Assurance funcione, consulte sugestões nos tópicos de problema a seguir para resolver problemas encontrados com frequência.

Para permitir uma implementação mais suave e descobrir possíveis problemas, verifique se o SDK está ativado por [Ativar o registro de depuração](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) na seção Introdução .

Você pode alterar os níveis de log do SDK usando o [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API.

## Problemas no dispositivo e no aplicativo

### O código QR não abre o aplicativo

* Acesse o link diretamente. Copie o link de **Detalhes da sessão**. Cole-o na barra de endereços do navegador do dispositivo para abri-lo. Se não abrir, consulte a seção [O aplicativo não abrirá o link](#app-does-not-open-link).
* Use um leitor QR diferente. Para iOS 11 ou superior, use o aplicativo de foto para ler o código QR.

### O aplicativo não abre link

* Verifique se a implementação do deep link está configurada corretamente no aplicativo.
   * **Android:** Deep Links (Links De Aplicativo)
      * [Criar deep links para o contexto do aplicativo](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** Esquema de URL personalizado ou links universais
      * [Definição de um esquema de URL personalizado para seu aplicativo](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [Suporte a links universais no seu aplicativo](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>Para Android, a variável `startSession` A API não precisa ser chamada explicitamente. Para o iOS, use a API conforme descrito em [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### A sobreposição de autenticação é exibida, mas o aplicativo falha ao se conectar

* Garanta a conectividade com a Internet do dispositivo por meio do navegador da Web do dispositivo.
* Se o aplicativo nunca tiver se conectado com êxito ao serviço de garantia, verifique se ele está configurado corretamente para o Assurance. Consulte as instruções para instalar o [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md) Biblioteca do SDK.
* Verifique se a sessão corresponde ao link e se está inserida corretamente para a sessão esperada. Consulte [Mensagem de log &quot;As informações da OrgID não estão disponíveis&quot;](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (isso é incomum e relevante somente se você tiver acesso a mais de uma instância ORG).

### Depuração do Adobe Analytics

**Status de pós-processamento - Sem sinalizador de depuração**

Na exibição Eventos do Analytics , se os eventos falharem com o status pós-processado &quot;Sem sinalizador de depuração&quot;, a versão atual do SDK do Adobe Analytics ou do Assurance talvez não seja compatível com o recurso Depuração do Analytics.
Atualize as extensões do SDK do Adobe Analytics e do Assurance para as versões mais recentes para resolver esse problema.

| Requisito mínimo de versão | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance | > 1.0.0 | > 1.0.0 |

### Reagir à compatibilidade nativa com o MobileCore e o AEPAsAssurance

| Versão do AEP Assurance | Versão principal do Mobile | Instalar instrução |
| --------------------- | ------------------- | ------------------- |
| response-native-aepAssurance v2.x.x | [response-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| response-native-aepAssurance v3.x.x | [response-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

Se estiver usando `react-native-acpcore` com o Assurance, o aplicativo React Native pode falhar ao criar com uma das seguintes mensagens de erro:

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

ou

```
AppDelegate: AEPAssurance.h file not found
```

**Solução**

Se isso ocorrer, baixe seu `react-native-aepassurance` usando o seguinte comando npm:

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

Esse erro ocorre porque a variável `react-native-acpcore` extensão é **only** compatível com `react-native-aepassurance` versões 2.x.x e posteriores.
