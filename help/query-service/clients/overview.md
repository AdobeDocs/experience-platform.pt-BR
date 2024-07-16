---
keywords: Experience Platform;página inicial;tópicos populares;Serviço de consulta;serviço de consulta;conectar;conectar ao serviço de consulta;aqua data studio;Aqua data Studio;Pesquisador;observador;Postico;postico;Power BI;power bi;psql;rstudio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: Conectar clientes ao serviço de consulta
description: Este documento explica como se conectar ao Serviço de consulta de vários aplicativos de cliente de desktop e como verificar essas conexões.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Conectar clientes a [!DNL Query Service]

Esta seção explica como se conectar ao [!DNL Query Service] a partir de vários aplicativos de cliente de desktop e como verificar essas conexões. O [!DNL Query Service] usa o protocolo [!DNL PostgreSQL], portanto, as instruções desta seção explicam como usar ferramentas e drivers do [!DNL PostgreSQL] para conectar e gravar consultas.

>[!IMPORTANT]
>
>Os certificados TLS/SSL em ambientes de Produção para a API Postgres interativa do serviço de consulta foram atualizados na quarta-feira, 24 de janeiro de 2024.<br>Embora esse seja um requisito anual, nesta ocasião o certificado raiz na cadeia também foi alterado, pois o provedor de certificados TLS/SSL do Adobe atualizou sua hierarquia de certificados. Isso pode afetar determinados clientes Postgres se a lista de Autoridades de certificação não tiver o certificado raiz. Por exemplo, um cliente PSQL CLI pode precisar ter os certificados raiz adicionados a um arquivo explícito `~/postgresql/root.crt`, caso contrário, isso pode resultar em um erro. Por exemplo, `psql: error: SSL error: certificate verify failed`. Consulte a [documentação oficial do PostgreSQL](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) para obter mais informações sobre esse problema.<br>O certificado raiz a ser adicionado pode ser baixado de [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

São fornecidas instruções para os seguintes clientes:

- [[!DNL Aqua Data Studio]](./aqua-data-studio.md)
- [[!DNL DbVisualizer]](./dbvisulaizer.md)
- [[!DNL Looker]](./looker.md)
- [[!DNL Postico (Mac)]](./postico.md)
- [[!DNL Power BI (PC)]](./power-bi.md)
- [[!DNL PSQL]](./psql.md)
- [[!DNL RStudio]](./rstudio.md)
- [[!DNL Tableau]](./tableau.md)

>[!IMPORTANT]
>
>Como usuário do Power BI e do Tableau, você pode conectar o Customer Journey Analytics às ferramentas de BI na guia de credenciais do Serviço de consulta. Consulte a documentação de credenciais para obter instruções sobre como [conectar suas ferramentas de BI ao Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).
