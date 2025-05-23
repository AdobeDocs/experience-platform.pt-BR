---
keywords: Experience Platform;solução de problemas;medidas de proteção;diretrizes;
title: Medidas de proteção para a assimilação de dados
description: Saiba mais sobre as medidas de proteção para a assimilação de dados no Adobe Experience Platform.
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: a862e532382472eadf29aee2568c550b1a71211a
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# Medidas de proteção para a assimilação de dados

>[!IMPORTANT]
>
>As garantias para assimilação em lote e por transmissão geralmente são calculadas no nível da organização, e não no nível da sandbox. Isso significa que o uso de dados por sandbox está vinculado ao direito de uso total de licença que corresponde a toda a organização. Além disso, o uso de dados em sandboxes de desenvolvimento é limitado a 10% do total de perfis. Para obter mais informações sobre direitos de uso de licença, leia o [guia de práticas recomendadas de gerenciamento de dados](../landing/license-usage-and-guardrails/data-management-best-practices.md).

As garantias são limites que fornecem orientação para o uso de dados e do sistema, otimização do desempenho e prevenção de erros ou resultados inesperados no Adobe Experience Platform. As garantias podem se referir ao uso ou consumo de dados e processamento em relação aos seus direitos de licenciamento.

>[!IMPORTANT]
>
>Verifique os direitos de licença em seu Pedido de Venda e a [Descrição do Produto](https://helpx.adobe.com/br/legal/product-descriptions.html?lang=pt-BR) correspondente sobre os limites de uso reais, além desta página de medidas de proteção.

Este documento fornece orientação sobre medidas de proteção para a assimilação de dados no Adobe Experience Platform.

## Medidas de proteção para a assimilação em lote

A tabela a seguir descreve as medidas de proteção a serem consideradas ao usar a [API de assimilação em lote](./batch-ingestion/overview.md) ou fontes:

| Tipo de assimilação | Diretrizes | Notas |
| --- | --- | --- |
| Assimilação do data lake usando a API de assimilação em lote | <ul><li>Você pode assimilar até 20 GB de dados por hora no data lake usando a API de assimilação em lote.</li><li>O número máximo de arquivos por lote é 1500.</li><li>O tamanho máximo do lote é de 100 GB.</li><li>O número máximo de propriedades ou campos por linha é 10000.</li><li>O número máximo de lotes por minuto por usuário é 2000.</li></ul> | |
| Assimilação do data lake usando fontes de lote | <ul><li>Você pode assimilar até 200 GB de dados por hora no data lake usando fontes de assimilação em lote como [!DNL Azure Blob], [!DNL Amazon S3] e [!DNL SFTP].</li><li>O tamanho do lote deve estar entre 256 MB e 100 GB. Isso se aplica a dados descompactados e compactados. Quando dados compactados são descompactados no data lake, essas limitações se aplicam.</li><li>O número máximo de arquivos por lote é 1500.</li><li>O tamanho mínimo de um arquivo ou pasta é de 1 byte. Não é possível assimilar arquivos ou pastas de tamanho 0 byte.</li></ul> | Leia a [visão geral das fontes](../sources/home.md) para obter um catálogo de fontes que você pode usar para assimilação de dados. |
| Assimilação em lote para Perfil | <ul><li>O tamanho máximo de uma classe de registro é 100 KB (rígido).</li><li>O tamanho máximo de uma classe ExperienceEvent é 10 KB (rígido).</li></ul> | |
| Número de lotes Profile ou ExperienceEvent assimilados por dia | **O número máximo de lotes de Profile ou ExperienceEvent assimilados por dia é 90 por sandbox.** Isso significa que o total combinado de lotes Profile e ExperienceEvent assimilados a cada dia não pode exceder 90. A ingestão de lotes adicionais afetará o desempenho do sistema. | Este é um limite flexível. É possível ir além de um limite flexível, no entanto, os limites flexíveis fornecem uma diretriz recomendada para o desempenho do sistema. Além disso, essa garantia é de **por sandbox**, não por organização. |
| Assimilação de dados criptografados | O tamanho máximo suportado de um único arquivo criptografado é 1 GB. Por exemplo, embora você possa assimilar 2 ou mais GBs de dados em uma única execução de fluxo de dados, nenhum arquivo individual na execução do fluxo de dados pode exceder 1 GB. | O processo de assimilação de dados criptografados pode levar mais tempo do que a assimilação normal de dados. Leia o [guia da API de assimilação de dados criptografados](../sources/tutorials/api/encrypt-data.md) para obter mais informações. |
| Substituir assimilação em lote | A assimilação de lotes de substituição pode ser até 10x mais lenta do que lotes regulares, portanto, você deve **manter seus lotes de substituição abaixo de dois milhões de registros** para garantir um tempo de execução eficiente e evitar o bloqueio de outros lotes de serem processados na sandbox. | Embora seja possível assimilar lotes que excedam dois milhões de registros, o tempo de assimilação será significativamente maior devido às limitações de pequenas sandboxes. |

{style="table-layout:auto"}

## Medidas de proteção para assimilação por transmissão

Leia a [visão geral da assimilação de streaming](./streaming-ingestion/overview.md) para obter informações sobre as medidas de proteção para a assimilação de streaming.

## Medidas de proteção para fontes de transmissão

A tabela a seguir descreve as medidas de proteção a serem consideradas ao usar as fontes de transmissão:

| Tipo de assimilação | Diretrizes | Notas |
| --- | --- | --- |
| Fontes de transmissão | <ul><li>O tamanho máximo do registro é de 1 MB, com o tamanho recomendado de 10 KB.</li><li>As fontes de transmissão oferecem suporte a entre 4.000 e 5.000 solicitações por segundo ao assimilar no data lake. Isso se aplica a conexões de origem recém-criadas além de conexões de origem existentes. **Observação**: pode levar até 30 minutos para que a transmissão de dados seja completamente processada para o data lake.</li><li>As fontes de transmissão oferecem suporte a no máximo 1500 solicitações por segundo ao assimilar dados para o perfil ou a segmentação por transmissão.</li></ul> | Fontes de transmissão como [!DNL Kafka], [!DNL Azure Event Hubs] e [!DNL Amazon Kinesis] não usam a rota [!DNL Data Collection Core Service] (DCCS) e podem ter limites de taxa de transferência diferentes. Consulte a [visão geral das fontes](../sources/home.md) para obter um catálogo de fontes que podem ser usadas para assimilação de dados. |

{style="table-layout:auto"}

## Próximas etapas

Consulte a documentação a seguir para obter mais informações sobre outras medidas de proteção dos serviços da Experience Platform, informações de latência de ponta a ponta e informações de licenciamento dos documentos Descrição do produto da Real-Time CDP:

* [Medidas de proteção do Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagramas de latência de ponta a ponta](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=pt-BR#end-to-end-latency-diagrams) para vários serviços da Experience Platform.
* [Real-Time Customer Data Platform (B2C Edition - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
