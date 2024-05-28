---
title: Criptografia de dados no Adobe Experience Platform
description: Saiba como os dados são criptografados em trânsito e em repouso no Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 4f67df5d3667218c79504535534de57f871b0650
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# Criptografia de dados no Adobe Experience Platform

O Adobe Experience Platform é um sistema eficiente e extensível que centraliza e padroniza os dados de experiência do cliente em todas as soluções corporativas. Todos os dados usados pela Platform são criptografados em trânsito e em repouso para manter seus dados seguros. Este documento descreve os processos de criptografia da Platform em alto nível.

O diagrama de fluxo de processo a seguir ilustra como o Experience Platform assimila, criptografa e mantém dados:

![Um diagrama que ilustra como os dados são assimilados, criptografados e mantidos pelo Experience Platform.](../images/governance-privacy-security/encryption/flow.png)

## Dados em trânsito {#in-transit}

Todos os dados em trânsito entre a Platform e qualquer componente externo são conduzidos por conexões seguras e criptografadas usando HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

Em geral, os dados são trazidos para a Platform de três maneiras:

- [Coleta de dados](../../collection/home.md) Os recursos do permitem que sites e aplicativos móveis enviem dados para o Edge Network da plataforma para preparo e preparação para assimilação.
- [Conectores de origem](../../sources/home.md) transmita dados diretamente para a Platform a partir de aplicativos da Adobe Experience Cloud e outras fontes de dados corporativas.
- As ferramentas ETL não-Adobe (extrair, transformar, carregar) enviam dados para o [API de assimilação em lote](../../ingestion/batch-ingestion/overview.md) para consumo.

Depois que os dados forem trazidos para o sistema e [criptografado em repouso](#at-rest), Os serviços da Platform enriquecem e exportam os dados das seguintes maneiras:

- [Destinos](../../destinations/home.md) permite ativar dados para aplicativos Adobe e aplicativos de parceiros.
- Aplicativos da plataforma nativa, como [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=pt-BR) e [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/ajo-home?lang=pt-BR) O também pode usar os dados.

### Suporte ao protocolo mTLS {#mtls-protocol-support}

Agora você pode usar o MTLS (Mutual Transport Layer Security) para garantir segurança aprimorada em conexões de saída com o [Destino da API HTTP](../../destinations/catalog/streaming/http-destination.md) e ADOBE JOURNEY OPTIMIZER [ações personalizadas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions). O mTLS é um método de segurança completo para autenticação mútua que garante que ambas as partes que compartilham informações sejam quem afirmam ser antes que os dados sejam compartilhados. O mTLS inclui uma etapa adicional em comparação ao TLS, na qual o servidor também solicita o certificado do cliente e o verifica ao final.

Se você quiser [usar mTLS com ações personalizadas do Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration) e workflows de destino da API HTTP do Experience Platform, o endereço do servidor inserido na interface da ação do cliente do Adobe Journey Optimizer ou na interface do usuário de Destinos deve ter os protocolos TLS desativados e somente o mTLS ativado. Se o protocolo TLS 1.2 ainda estiver habilitado nesse endpoint, nenhum certificado será enviado para a autenticação de cliente. Isso significa que para usar mTLS com esses workflows, o terminal de servidor de &quot;recebimento&quot; deve ser um mTLS **somente** ponto de extremidade de conexão habilitado.

>[!IMPORTANT]
>
>Nenhuma configuração adicional é necessária na ação personalizada do Adobe Journey Optimizer ou no destino da API HTTP para ativar o mTLS. Esse processo ocorre automaticamente quando um terminal habilitado para mTLS é detectado. O Common Name (CN) e o Subject Alternative Names (SAN) de cada certificado estão disponíveis na documentação como parte do certificado e podem ser usados como uma camada adicional de validação de propriedade, se desejar.
>
>O RFC 2818, publicado em maio de 2000, substitui o uso do campo Nome comum (CN) em certificados HTTPS para verificação do nome da entidade. Em vez disso, ele recomenda o uso da extensão &quot;Nome alternativo da entidade&quot; (SAN) do tipo &quot;nome dns&quot;.

### Baixar certificados {#download-certificates}

>[!NOTE]
>
>É sua responsabilidade manter o certificado público atualizado. Verifique regularmente o certificado, especialmente quando a data de expiração estiver próxima. Você deve marcar esta página para manter a cópia mais recente em seu ambiente.

Se você quiser verificar a CN ou a SAN para fazer a validação adicional de terceiros, é possível baixar os certificados relevantes aqui:

- [O certificado público do Adobe Journey Optimizer](../images/governance-privacy-security/encryption/AJO-public-certificate.pem)
- [O certificado público do Serviço de Destinos](../images/governance-privacy-security/encryption/destinations-public-cert.pem).

## Dados em repouso {#at-rest}

Os dados assimilados e usados pela Platform são armazenados no data lake, um armazenamento de dados altamente granular que contém todos os dados gerenciados pelo sistema, independentemente da origem ou do formato de arquivo. Todos os dados mantidos no data lake são criptografados, armazenados e gerenciados em um local isolado [[!DNL Microsoft Azure Data Lake] Armazenamento](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) que é exclusiva da sua organização.

Para obter detalhes sobre como os dados em repouso são criptografados no Armazenamento Azure Data Lake, consulte o [documentação oficial do Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Próximas etapas

Este documento forneceu uma visão geral de alto nível de como os dados são criptografados na Platform. Para obter mais informações sobre procedimentos de segurança na Platform, consulte a visão geral na [governança, privacidade e segurança](./overview.md) no Experience League ou dê uma olhada no [Informe oficial de segurança da plataforma](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
