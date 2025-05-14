---
title: Criptografia de dados no Adobe Experience Platform
description: Saiba como os dados são criptografados em trânsito e em repouso no Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: f6eaba4c0622318ba713c562ba0a4c20bba02338
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Criptografia de dados no Adobe Experience Platform

O Adobe Experience Platform é um sistema eficiente e extensível que centraliza e padroniza os dados de experiência do cliente em todas as soluções corporativas. Todos os dados usados pelo Experience Platform são criptografados em trânsito e em repouso para manter seus dados protegidos. Este documento descreve os processos de criptografia da Experience Platform em alto nível.

O diagrama de fluxo de processo a seguir ilustra como o Experience Platform assimila, criptografa e mantém dados:

![Um diagrama que ilustra como os dados são assimilados, criptografados e mantidos pelo Experience Platform.](../images/governance-privacy-security/encryption/flow.png)

## Dados em trânsito {#in-transit}

Todos os dados em trânsito entre o Experience Platform e qualquer componente externo são conduzidos por conexões seguras e criptografadas usando HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

Em geral, os dados são trazidos para a Experience Platform de três maneiras:

- Os recursos de [Coleção de dados](../../collection/home.md) permitem que sites e aplicativos móveis enviem dados para o Experience Platform Edge Network para preparo e preparação para assimilação.
- [Conectores Source](../../sources/home.md) transmitem dados diretamente para a Experience Platform a partir de aplicativos Adobe Experience Cloud e outras fontes de dados corporativas.
- Ferramentas ETL (extract, transform, load) não-Adobe enviam dados para a [API de assimilação em lote](../../ingestion/batch-ingestion/overview.md) para consumo.

Depois que os dados forem trazidos para o sistema e [criptografados em repouso](#at-rest), os serviços da Experience Platform enriquecem e exportam os dados das seguintes maneiras:

- [Destinos](../../destinations/home.md) permitem ativar dados para aplicativos da Adobe e aplicativos de parceiros.
- Aplicativos nativos do Experience Platform, como o [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=pt-BR) e o [Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/ajo-home), também podem usar os dados.

### Suporte ao protocolo mTLS {#mtls-protocol-support}

Agora você pode usar o mTLS (Mutual Transport Layer Security) para garantir segurança aprimorada em conexões de saída com o [destino da API HTTP](../../destinations/catalog/streaming/http-destination.md) e as [ações personalizadas](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions) do Adobe Journey Optimizer. O mTLS é um método de segurança completo para autenticação mútua que garante que ambas as partes que compartilham informações sejam quem afirmam ser antes que os dados sejam compartilhados. O mTLS inclui uma etapa adicional em comparação ao TLS, na qual o servidor também solicita o certificado do cliente e o verifica ao final.

Se você deseja [usar mTLS com ações personalizadas do Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration) e fluxos de trabalho de destino da API HTTP do Experience Platform, o endereço do servidor inserido na interface de ação do cliente do Adobe Journey Optimizer ou na interface de Destinos deve ter os protocolos TLS desabilitados e somente o mTLS habilitado. Se o protocolo TLS 1.2 ainda estiver habilitado nesse endpoint, nenhum certificado será enviado para a autenticação de cliente. Isso significa que para usar mTLS com esses fluxos de trabalho, o ponto de extremidade do servidor de &quot;recebimento&quot; deve ser um ponto de extremidade de conexão habilitado para mTLS **only**.

>[!IMPORTANT]
>
>Nenhuma configuração adicional é necessária na ação personalizada do Adobe Journey Optimizer ou no destino da API HTTP para ativar o mTLS. Esse processo ocorre automaticamente quando um terminal habilitado para mTLS é detectado. O Common Name (CN) e o Subject Alternative Names (SAN) de cada certificado estão disponíveis na documentação como parte do certificado e podem ser usados como uma camada adicional de validação de propriedade, se desejar.
>
>O RFC 2818, publicado em maio de 2000, substitui o uso do campo Nome comum (CN) em certificados HTTPS para verificação do nome da entidade. Em vez disso, ele recomenda o uso da extensão &quot;Nome alternativo da entidade&quot; (SAN) do tipo &quot;nome dns&quot;.

### Baixar certificados {#download-certificates}

>[!NOTE]
>
>Você é responsável por garantir que seus sistemas usem um certificado público válido. Revise regularmente seus certificados, especialmente quando a data de expiração estiver próxima. Use a API para recuperar e atualizar certificados antes que expirem.

Links de download direto para certificados mTLS públicos não são mais fornecidos. Em vez disso, use o [ponto de extremidade de certificado público](../../data-governance/mtls-api/public-certificate-endpoint.md) para recuperar certificados. Este é o único método suportado para acessar os certificados públicos atuais. Ela garante que você sempre receba certificados válidos e atualizados para suas integrações.

Integrações que dependem de criptografia baseada em certificado devem atualizar seus workflows para oferecer suporte à recuperação automatizada de certificados usando a API do. Depender de links estáticos ou atualizações manuais pode resultar no uso de certificados expirados ou revogados, resultando em integrações com falha.

#### Automação do ciclo de vida do certificado {#certificate-lifecycle-automation}

A Adobe agora automatiza o ciclo de vida do certificado para integrações mTLS, melhorando a confiabilidade e evitando interrupções do serviço. Os certificados públicos são:

- Reemitido 60 dias antes da expiração.
- Revogado 30 dias antes da expiração.

Esses intervalos continuarão sendo encurtados de acordo com as [diretrizes em evolução do CA/B Forum](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days), que visam reduzir a duração dos certificados para no máximo 47 dias.

Se você usou links nesta página anteriormente para baixar certificados, atualize seu processo para recuperá-los exclusivamente por meio da API.

## Dados em repouso {#at-rest}

Os dados assimilados e usados pelo Experience Platform são armazenados no data lake, um armazenamento de dados altamente granular que contém todos os dados gerenciados pelo sistema, independentemente da origem ou do formato de arquivo. Todos os dados persistentes no data lake são criptografados, armazenados e gerenciados em uma instância isolada do [[!DNL Microsoft Azure Data Lake] Armazenamento](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) que é exclusiva de sua organização.

Para obter detalhes sobre como os dados em repouso são criptografados no Armazenamento Azure Data Lake, consulte a [documentação oficial do Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Próximas etapas

Este documento forneceu uma visão geral de alto nível sobre como os dados são criptografados no Experience Platform. Para obter mais informações sobre procedimentos de segurança no Experience Platform, consulte a visão geral sobre [governança, privacidade e segurança](./overview.md) no Experience League ou consulte o [whitepaper de segurança do Experience Platform](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
