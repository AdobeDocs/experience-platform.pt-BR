---
title: Identidade na coleção de dados
description: Saiba como a Coleção de dados usa ECIDs, CORE IDs, persistência própria e identityMap em implementações da Web.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Identidade na coleção de dados

A Coleta de dados do Adobe usa sinais de identidade para reconhecer visitantes recorrentes e carregar contexto entre experiências. Quando um visitante acessa o site, o Edge Network gera uma Experience Cloud ID (ECID) e a mantém em um cookie primário. Essa ECID é o principal identificador de dispositivo usado em aplicativos da Adobe Experience Cloud e é a base na qual a análise, a personalização e a ativação de público-alvo se baseiam. Na implementação, você pode acessar a ECID do visitante no lado do cliente por meio do comando [`getIdentity`](/help/collection/js/commands/getidentity.md). No nível de sequência de dados, você pode usar [Preparação de dados para coleção de dados](/help/datastreams/data-prep.md) para mapear a ECID em um campo XDM personalizado antes que ele atinja os serviços downstream.

A ECID identifica um dispositivo, não uma pessoa. Para vincular a atividade a uma pessoa conhecida, você pode enviar identificadores adicionais, como uma ID de CRM ou email com hash, juntamente com a ECID usando o XDM [`identityMap`](./identity-map.md). A Adobe recomenda definir um namespace de nível de pessoa como a [identidade principal](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) sempre que houver uma disponível.

Além da ECID padrão, a Coleta de dados é compatível com sinais de identidade adicionais, dependendo da implementação:

* **IDs de dispositivo próprio (FPIDs)**: identificadores de dispositivo que você gera e gerencia na infraestrutura que controla. O Edge Network usa um FPID para [propagar a ECID](./fpid.md), dando a você maior persistência de cookies em propriedades próprias quando as restrições do navegador encurtam a vida útil dos cookies gerenciados pela Adobe.
* **IDs PRINCIPAIS**: um identificador separado, baseado em demdex, que participa de fluxos de trabalho de identidade de terceiros quando cookies de terceiros estão disponíveis. A ID CORE é distinta da ECID e pode ser recuperada através de [`getIdentity`](/help/collection/js/commands/getidentity.md). Para obter detalhes sobre como os contextos de identidade própria e de terceiros funcionam juntos, consulte [Suporte à identidade unificada](./unified-identity-support.md).

Se estiver atualizando a API de Visitante ou reconciliando o comportamento de identidade mais antigo, consulte [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md) para migrar cookies AMCV existentes.

## Coleção própria e de terceiros {#first-party-and-third-party-collection}

O Web SDK sempre define a identidade [cookies](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk) (como `kndctr_` cookies) como cookies próprios no seu domínio, independentemente do ponto de extremidade que recebe a solicitação de coleta de dados. O endpoint de coleção (o domínio para o qual a implementação envia dados) é uma escolha separada que afeta como os navegadores e as políticas de rede tratam a própria solicitação.

**A coleta própria** encaminha as solicitações de coleta de dados por meio de um domínio controlado pela sua organização (por exemplo, `data.example.com`), usando um CNAME que aponte para o Edge Network da Adobe. Como a solicitação permanece no domínio, é menos provável que seja bloqueada por bloqueadores de anúncios ou restrições de rede do navegador. A coleta própria também é um pré-requisito para definir [IDs de dispositivo próprio](./fpid.md) da sua própria infraestrutura de servidor, que é a estratégia de identidade mais durável disponível. A Adobe recomenda usar o [programa de certificados gerenciados pela Adobe](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert) para configurar a coleção própria para sua implementação.

**A coleção de terceiros** envia solicitações diretamente para um [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md) de propriedade da Adobe (como `example.data.adobedc.net`). Embora os cookies de identidade ainda sejam definidos como primários em seu domínio, a própria solicitação vai para um domínio de terceiros, que alguns navegadores e bloqueadores de anúncios podem restringir.

## Escolha o padrão de identidade correto {#choose-your-path}

* **Fortaleça a persistência de identidade nas propriedades próprias**: use as [IDs de dispositivo próprio](./fpid.md) quando as restrições do navegador encurtarem a vida útil do cookie e você precisar de uma continuidade mais forte para análise e personalização nos sites sob seu controle.
* **Enviar identidade de um aplicativo para a Web móvel**: usar o [compartilhamento de identidade de dispositivo móvel para Web](./mobile-to-web.md) quando o visitante iniciar no aplicativo móvel e continuar em um WebView ou página da Web móvel.
* **Mantenha a identidade contínua em seus domínios**: use o [compartilhamento entre domínios](./cross-domain-sharing.md) quando os visitantes se moverem entre as propriedades da Web de sua organização e você quiser relatórios e personalização consistentes.
* **Combinar persistência própria com ativação de terceiros**: use o [Suporte à identidade unificada](./unified-identity-support.md) quando precisar de identificação própria durável junto com fluxos de ativação de terceiros com suporte.
* **Enviar identificadores de nível de pessoa**: use [`identityMap`](./identity-map.md) para enviar IDs do CRM, emails com hash e outros identificadores de nível de pessoa junto com a ECID, para que os serviços downstream possam compilar a atividade para uma pessoa conhecida.
* **Entenda como o consentimento afeta a identidade**: Leia [Consentimento e identidade](./consent.md) para saber como o `defaultConsent` e o `setConsent` controlam quando o Web SDK gera uma ECID, define cookies e envia dados.

Para obter ajuda no diagnóstico de problemas de identidade, como inflação de visitante, inconsistências de ECID ou problemas de FPID, consulte [Solução de problemas de identidade](./troubleshooting.md).
