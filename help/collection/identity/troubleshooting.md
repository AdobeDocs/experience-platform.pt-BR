---
title: Solução de problemas de identidade na coleção de dados
description: Diagnosticar problemas comuns de identidade em implementações do Web SDK, incluindo aumento de visitantes, inconsistências de ECID, conflitos de cookies e problemas de FPID.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# Solução de problemas de identidade na coleção de dados

Os problemas de identidade geralmente surgem como sintomas nos relatórios downstream (contagens infladas de visitantes, perfis fragmentados ou personalização interrompida) em vez de erros na própria implementação. Esta página ajuda a diagnosticar e resolver os problemas de identidade mais comuns em implementações do Web SDK. Para obter informações sobre como a identidade funciona na Coleção de dados, consulte a [visão geral da identidade](./overview.md).

## Inspecionar valores de identidade {#inspect-identity}

Antes de solucionar um problema específico, recupere os valores de identidade atuais que o Web SDK está usando. Use o comando [`getIdentity`](/help/collection/js/commands/getidentity.md) para exibir a ECID e outros sinais de identidade:

```js
alloy("getIdentity", { namespaces: ["ECID", "CORE"] }).then(function(result) {
  console.log("ECID:", result.identity.ECID);
  console.log("CORE ID:", result.identity.CORE);
  console.log("Edge region:", result.edge.regionID);
});
```

Você também pode inspecionar valores de identidade nas ferramentas de desenvolvedor do navegador:

1. Abra a guia **Aplicativo** (Chrome/Edge) ou **Armazenamento** (Firefox/Safari).
2. Procure cookies com o prefixo `kndctr_` em seu domínio. O cookie `kndctr_<ORG_ID>_AdobeOrg_identity` contém a ECID.
3. Abra a guia **Rede** e localize uma solicitação de `interact` ou `collect` para a Edge Network. Inspecione a carga da solicitação para `identityMap` e a carga da resposta para identificadores de identidade.

## Problemas comuns {#common-issues}

+++**Inflação na contagem de visitantes**

**Sintoma**: os relatórios do Analytics mostram mais visitantes únicos do que o esperado ou a mesma pessoa aparece como vários visitantes em várias sessões.

**Causas possíveis**:

| Causa | Como identificar | Resolução |
| --- | --- | --- |
| Duração do cookie curto | Verifique a expiração dos cookies do `kndctr_` no navegador. Se expirarem em 7 dias ou menos, as políticas do navegador provavelmente restringem a duração do cookie. | Implementar [IDs de dispositivo primário (FPIDs)](./fpid.md) definidos de um servidor usando um registro DNS A/AAAA para maior persistência de cookies. |
| FPID ausente na primeira solicitação | Inspecione a primeira solicitação do Edge Network no carregamento da página. Se nenhum cookie FPID estiver presente, o Edge Network gerará uma nova ECID. Se o FPID for definido após a primeira solicitação, a ECID gerada nessa primeira solicitação se tornará órfã. | Defina o cookie FPID antes que o Web SDK envie sua primeira solicitação. Consulte [Quando definir o cookie](./fpid.md#when-to-set-cookie). |
| `orgId` incompatibilidade entre domínios | Compare o valor da configuração `orgId` entre seus domínios. Valores incompatíveis causam escopos de identidade separados. | Use o mesmo [`orgId`](/help/collection/js/commands/configure/orgid.md) em todos os domínios da organização. |
| Banner de consentimento excluindo cookies | Se a implementação do consentimento limpar todos os cookies antes que o consentimento seja concedido e, em seguida, o Web SDK for inicializado, uma nova ECID será gerada. | Configure seu banner de consentimento para preservar os cookies do `kndctr_` ou atrasar a inicialização do Web SDK até que o consentimento seja estabelecido. Consulte também [Consentimento e identidade](./consent.md). |
| Cookies FPID definidos pela JavaScript | Os cookies definidos com o uso de `document.cookie` estão sujeitos a restrições do navegador (ITP, ETP) que limitam seu tempo de vida, às vezes até 24 horas. | Defina cookies FPID do servidor usando um registro DNS A/AAAA, não do JavaScript. |

+++

+++**A ECID altera inesperadamente entre páginas**

**Sintoma**: a ECID é diferente em páginas diferentes do mesmo domínio ou muda em cada carregamento de página.

**Etapas de diagnóstico**:

1. Confirme se o cookie de identidade `kndctr_` está presente em ambas as páginas. Se estiver ausente em uma página, verifique se o Web SDK está configurado nessa página.
2. Verifique se o domínio do cookie está definido de forma ampla o suficiente. Um cookie definido em `shop.example.com` não está disponível em `www.example.com`. Certifique-se de que a coleção própria e a infraestrutura de definição de cookies usem o mesmo escopo de domínio.
3. Verifique o JavaScript que apaga os cookies na navegação (por exemplo, scripts agressivos de consentimento de cookies ou ferramentas de privacidade).
4. Se estiver usando um aplicativo de página única, verifique se o Web SDK está configurado uma vez na inicialização do aplicativo, não reinicializado em cada alteração de rota. A reinicialização pode gerar uma nova ECID.

+++

+++**O FPID não está propagando a ECID**

**Sintoma**: você definiu um cookie FPID, mas `getIdentity` retorna uma ECID que não é consistente entre as visitas, ou o FPID não aparece nas cargas de solicitação do Edge Network.

**Etapas de diagnóstico**:

1. **Verifique o formato do cookie FPID**: o FPID deve ser um [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122) válido. Abra as ferramentas de desenvolvedor do seu navegador, localize o cookie FPID e confirme se o valor corresponde ao padrão `xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx`.
2. **Verificar o nome do cookie na sequência de dados**: se estiver usando o [método de cookie da sequência de dados](./fpid.md#setting-cookie-datastreams), o nome do cookie configurado na sequência de dados deve corresponder exatamente ao nome do cookie definido pelo seu servidor.
3. **Confirme se o cookie foi enviado na solicitação**: na guia Rede, inspecione o cabeçalho `Cookie` na solicitação do Edge Network. O cookie FPID deve ser incluído.
4. **Verificar prioridade da identidade**: se uma ECID existente já estiver armazenada em um cookie `kndctr_`, ela terá prioridade sobre o FPID. O FPID só propaga uma nova ECID quando nenhuma ECID existente está presente. Consulte [Como os FPIDs funcionam](./fpid.md#how-fpids-work) para obter a ordem de prioridade completa.
5. **Validar o CNAME**: se estiver usando o método de cookie de sequência de dados, confirme se a coleção própria CNAME está configurada corretamente e se as solicitações foram roteadas por meio dele.

+++

+++**A identidade entre domínios não está funcionando**

**Sintoma**: um visitante que clica de um de seus domínios para outro é tratado como um novo visitante no domínio de destino.

**Etapas de diagnóstico**:

1. **Verificar a URL**: inspecione a URL de destino quando o visitante clicar no link. Ele deve conter um parâmetro de sequência de consulta `adobe_mc`. Se o parâmetro estiver ausente, o domínio de origem não o anexará. Consulte [Implementar compartilhamento entre domínios](./cross-domain-sharing.md#implement-cross-domain-sharing).
2. **Verificar o tempo**: o parâmetro `adobe_mc` expira após cinco minutos. Se a página de destino levar muito tempo para carregar (por exemplo, devido a redirecionamentos ou rede lenta), o parâmetro pode expirar antes que o Web SDK possa lê-lo.
3. **Verificar `orgId` correspondência**: ambos os domínios devem usar o mesmo [`orgId`](/help/collection/js/commands/configure/orgid.md). IDs de organização incompatíveis fazem com que o domínio de destino rejeite a identidade entregue.
4. **Confirmar se o Web SDK está no destino**: a página de destino deve ter o Web SDK instalado e configurado. Sem ele, o parâmetro `adobe_mc` é ignorado.
5. **Verificar remoção da URL**: alguns serviços de redirecionamento, CDNs ou lógica do lado do servidor removem parâmetros desconhecidos da cadeia de caracteres de consulta. Verifique se `adobe_mc` sobrevive a qualquer redirecionamento intermediário entre as páginas de origem e destino.

+++

+++**A transferência de identidade de dispositivo móvel para Web está falhando**

**Sintoma**: um visitante que inicia no aplicativo móvel e abre um WebView ou navegador móvel é tratado como um novo visitante no lado da Web.

**Etapas de diagnóstico**:

1. **Verificar a URL**: registre a URL que está sendo passada para o WebView. Ele deve conter um parâmetro `adobe_mc` gerado por [`getUrlVariables`](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables).
2. **Verificar versões do SDK**: a extensão do Mobile Identity para Edge Network deve ser versão 1.1.0 ou posterior, e o Web SDK deve ser versão 2.11.0 ou posterior.
3. **Verificar o tempo**: como o compartilhamento entre domínios, o parâmetro `adobe_mc` expira após cinco minutos. Certifique-se de que o WebView seja carregado imediatamente após a construção do URL.
4. **Confirmar correspondência de `orgId`**: a ID da organização da Experience Cloud deve ser a mesma nas configurações de SDK móvel e Web SDK.

+++
