---
title: idMigrationEnabled
description: Permite que o Web SDK leia cookies AMCV.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# `idMigrationEnabled`

A propriedade `idMigrationEnabled` permite que o Web SDK leia cookies AMCV definidos por implementações anteriores do Adobe Experience Cloud. Se sua organização atualizar sua implementação para o Web SDK, essa configuração permitirá uma transição mais suave para o serviço atual da Adobe Experience Cloud ID. Essa configuração é importante para que você não veja um aumento acentuado em visitantes únicos ao atualizar para o Web SDK.

Se sua organização executar uma nova implementação do Web SDK, ativar essa configuração não terá impacto na coleta de dados ou na identificação do visitante. Não há desvantagens em deixá-lo ativado para todas as implementações.

## Como a migração de identidade funciona {#how-it-works}

A API de visitante armazena a Experience Cloud ID (ECID) em um cookie chamado `AMCV_<ORG_ID>`. Quando `idMigrationEnabled` é `true` (padrão), o Web SDK lê automaticamente a ECID do cookie AMCV e a usa como a identidade do visitante na primeira solicitação Edge Network.

1. Um visitante chega em uma página que agora usa o Web SDK em vez da API do visitante.
1. O Web SDK verifica se há um cookie de identidade `kndctr_` existente (seu próprio formato de cookie). Se nenhum for encontrado, ele procurará por um cookie `AMCV_`.
1. Se um cookie `AMCV_` for encontrado, o Web SDK extrai a ECID e a usa para inicializar a identidade do visitante.
1. O Web SDK define um novo cookie de identidade `kndctr_` com a mesma ECID.
1. Em visitas subsequentes, o Web SDK usa o cookie `kndctr_` diretamente. O cookie `AMCV_` não é mais necessário.

Para que a migração funcione, o Web SDK deve ser configurado com o mesmo [`orgId`](/help/collection/js/commands/configure/orgid.md) usado pela API de visitante e deve ser implantado no mesmo domínio (ou em um subdomínio do mesmo domínio pai) em que o cookie AMCV foi definido.

## Cenários de migração compatíveis

A migração de ID é compatível com os seguintes padrões de transição:

* **Algumas páginas ainda usam a API de Visitante, enquanto outras usam o Web SDK**: o SDK lê os cookies AMCV existentes e grava um novo cookie com a ECID existente. Ele também grava cookies AMCV para que as páginas que ainda usam a API de visitante continuem a reconhecer o mesmo visitante.
* **Web SDK e API de visitante estão presentes na mesma página**: se o cookie AMCV não estiver definido, o SDK procurará a API de visitante na página e a usará para obter a ECID.
* **O site foi totalmente transferido para o Web SDK**: você pode deixar a migração habilitada por um período para que os visitantes existentes baseados em AMCV mantenham a continuidade enquanto seus cookies são transferidos.

>[!IMPORTANT]
>
>Não carregue a API de visitante e o Web SDK na mesma página ao mesmo tempo, a menos que tenha confirmado que o cookie AMCV já está definido. A execução de ambas as bibliotecas em uma única página pode causar condições de corrida, em que cada biblioteca tenta gerenciar a identidade de forma independente, gerando potencialmente ECIDs duplicadas ou conflitantes.

## Desativando migração {#turn-off-migration}

Depois que todo o site for executado no Web SDK e nenhum visitante carregar apenas um cookie `AMCV_` sem um cookie `kndctr_` correspondente, você poderá desabilitar com segurança a migração de identidade definindo `idMigrationEnabled` como `false`. Esta é uma pequena otimização de desempenho e reduz a área da superfície da sua lógica de identidade.

Como diretriz, aguarde até que o tempo de vida máximo do cookie AMCV tenha decorrido após a última página ter sido migrada. Se os cookies AMCV tiverem uma expiração de dois anos, aguarde dois anos após a página final ter sido cortada para o Web SDK. Na prática, a maioria das organizações desativa a migração mais cedo (após alguns meses) e aceita um valor insignificante de inflação devido ao pequeno número de visitantes que retornam pela primeira vez após uma longa ausência.

## Atualizações de características do Audience Manager

Quando dados formatados em XDM são enviados para o Audience Manager durante a migração, esses dados devem ser convertidos em sinais. Suas características devem ser atualizadas para refletir as novas chaves fornecidas pelo XDM. Este processo é facilitado com a [ferramenta BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management).

## Migração de ID de terceiros {#third-party-id}

Se sua implementação da API de visitante usou IDs de terceiros (o cookie `demdex.net`), o Web SDK também poderá migrá-las. Configure de [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) a `true` na sua configuração do Web SDK. O Web SDK lê o cookie Demdex existente e inclui a identidade de terceiros em suas solicitações do Edge Network, seguindo o mesmo padrão de migração do cookie AMCV.

## Validação {#validation}

Para verificar se a migração de identidade está funcionando corretamente:

1. Abra uma página que tenha usado anteriormente a API de visitante (agora usando o Web SDK) em um navegador que tenha um cookie `AMCV_` existente.
2. Nas ferramentas do desenvolvedor, verifique se um cookie de identidade `kndctr_` foi definido e se a ECID corresponde ao do cookie `AMCV_`.
3. Após a implantação, compare as contagens de visitantes únicos antes e depois da migração para o mesmo período de tempo. Um pico significativo em visitantes únicos pode indicar que a migração não está transportando identidades.

>[!TIP]
>
>Use `getIdentity` para recuperar programaticamente a ECID para comparação:
>
>```js
>alloy("getIdentity", { namespaces: ["ECID"] }).then(function(result) {
>   console.log("ECID:", result.identity.ECID);
>});
>```

## Configurar `idMigrationEnabled` {#configure}

Defina o booleano `idMigrationEnabled` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o Web SDK, o padrão será `true`. Defina essa propriedade se desejar desativar a capacidade de ler cookies AMCV definidos pela API do visitante. A maioria das organizações não precisa definir essa propriedade.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## Habilitar a migração de ID de visitante usando a extensão de tag da Web SDK

Essas configurações podem ser definidas na extensão de marca do Web SDK usando [configurações de identidade](/help/tags/extensions/client/web-sdk/configure/identity.md).
