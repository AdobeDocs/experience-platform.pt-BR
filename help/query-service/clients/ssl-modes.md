---
keywords: Experience Platform;home;tópicos populares;Serviço de consulta;serviço de consulta;conectar;conectar ao serviço de consulta;SSL;ssl;sslmode;
title: Opções SSL do Serviço de Consulta
description: Saiba mais sobre o suporte SSL para conexões de terceiros ao Serviço de consulta da Adobe Experience Platform e como se conectar usando o modo SSL verify-full.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 1%

---

# [!DNL Query Service] opções de SSL

Para maior segurança, o Adobe Experience Platform [!DNL Query Service] fornece suporte nativo para conexões SSL para criptografar comunicações cliente/servidor. Este documento aborda as opções de SSL disponíveis para conexões de clientes de terceiros com o [!DNL Query Service] e como se conectar usando o valor do parâmetro SSL `verify-full`.

## Pré-requisitos

Este documento supõe que você já tenha baixado um aplicativo de cliente de desktop de terceiros para uso com seus dados do Experience Platform. Instruções específicas sobre como incorporar segurança SSL ao se conectar com um cliente de terceiros são encontradas em sua respectiva documentação do guia de conexão. Para obter uma lista de todos os clientes [!DNL Query Service] compatíveis, consulte a [visão geral das conexões de clientes](./overview.md).

## Opções de SSL disponíveis {#available-ssl-options}

O Experience Platform oferece suporte a várias opções de SSL para atender às suas necessidades de segurança de dados e equilibrar a sobrecarga de processamento da criptografia e da troca de chaves.

Os diferentes valores de parâmetro `sslmode` fornecem diferentes níveis de proteção. Ao criptografar seus dados em movimento com certificados SSL, ajuda a impedir ataques &quot;man-in-the-middle&quot; (MITM), espionagem e representação. A tabela abaixo fornece um detalhamento dos diferentes modos SSL disponíveis e o nível de proteção fornecido.

>[!NOTE]
>
> O valor SSL `disable` não tem suporte da Adobe Experience Platform devido à conformidade de proteção de dados necessária.

| sslmode | Proteção contra espionagem | Proteção MITM | Descrição |
|---|---|---|---|
| `allow` | Sim | Não | A criptografia é necessária em todas as comunicações. A rede é confiável para se conectar ao servidor correto. |
| `prefer` | Sim | Não | A criptografia é necessária em todas as comunicações. A rede é confiável para se conectar ao servidor correto. |
| `require` | Sim | Não | A criptografia é necessária em todas as comunicações. A rede é confiável para se conectar ao servidor correto. A validação do certificado SSL do servidor não é necessária. |
| `verify-ca` | Sim | Depende da política de CA | A criptografia é necessária em todas as comunicações. A validação do servidor é necessária antes que os dados sejam compartilhados. Isso requer que você configure um certificado raiz no seu diretório base do [!DNL PostgreSQL]. [Detalhes fornecidos abaixo](#instructions) |
| `verify-full` | Sim | Sim | A criptografia é necessária em todas as comunicações. A validação do servidor é necessária antes que os dados sejam compartilhados. Isso requer que você configure um certificado raiz no seu diretório base do [!DNL PostgreSQL]. [Os detalhes são fornecidos abaixo](#instructions). |

>[!NOTE]
>
>A diferença entre `verify-ca` e `verify-full` depende da política da CA (autoridade de certificação) raiz. Se você criou sua própria CA local para emitir certificados privados para seus aplicativos, o uso do `verify-ca` geralmente fornece proteção suficiente. Se estiver usando uma CA pública, o `verify-ca` permitirá conexões com um servidor que outra pessoa pode ter registrado com a CA. `verify-full` deve ser sempre usado com uma CA raiz pública.

Ao estabelecer uma conexão de terceiros com um banco de dados do Experience Platform, é recomendável usar o `sslmode=require` no mínimo para garantir uma conexão segura para seus dados em movimento. O modo SSL `verify-full` é recomendado para uso na maioria dos ambientes sensíveis à segurança.

## Configurar um certificado raiz para verificação do servidor {#root-certificate}

>[!IMPORTANT]
>
>Os certificados TLS/SSL em ambientes de Produção para a API Postgres interativa do serviço de consulta foram atualizados na quarta-feira, 24 de janeiro de 2024.<br>Embora esse seja um requisito anual, neste momento o certificado raiz na cadeia também foi alterado, pois o provedor de certificados TLS/SSL da Adobe atualizou sua hierarquia de certificados. Isso pode afetar determinados clientes Postgres se a lista de Autoridades de certificação não tiver o certificado raiz. Por exemplo, um cliente PSQL CLI pode precisar ter os certificados raiz adicionados a um arquivo explícito `~/postgresql/root.crt`, caso contrário, isso pode resultar em um erro. Por exemplo, `psql: error: SSL error: certificate verify failed`. Consulte a [documentação oficial do PostgreSQL](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) para obter mais informações sobre esse problema.<br>O certificado raiz a ser adicionado pode ser baixado de [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

Para garantir uma conexão segura, o uso do SSL deve ser configurado no cliente e no servidor antes que a conexão seja feita. Se o SSL só estiver configurado no servidor, o cliente poderá enviar informações confidenciais, como senhas, antes de se estabelecer que o servidor requer alta segurança.

Por padrão, [!DNL PostgreSQL] não executa nenhuma verificação do certificado do servidor. Para verificar a identidade do servidor e garantir uma conexão segura antes que dados confidenciais sejam enviados (como parte do modo SSL `verify-full`), você deve colocar um certificado raiz (autoassinado) no computador local (`root.crt`) e um certificado folha assinado pelo certificado raiz no servidor.

Se o parâmetro `sslmode` estiver configurado como `verify-full`, a libpq verificará se o servidor é confiável verificando a cadeia de certificados até o certificado raiz armazenado no cliente. Em seguida, ele verifica se o nome do host corresponde ao nome armazenado no certificado do servidor.

Para permitir a verificação do certificado do servidor, você deve colocar um ou mais certificados raiz (`root.crt`) no arquivo [!DNL PostgreSQL] em seu diretório base. O caminho do arquivo seria semelhante a `~/.postgresql/root.crt`.

## Habilitar o modo SSL verify-full para uso com uma conexão [!DNL Query Service] de terceiros {#instructions}

Se você precisar de um controle de segurança mais rigoroso que o `sslmode=require`, poderá seguir as etapas destacadas para conectar um cliente de terceiros ao [!DNL Query Service] usando o modo SSL do `verify-full`.

>[!NOTE]
>
>Há muitas opções disponíveis para obter um certificado SSL. Devido a uma tendência crescente em certificados não autorizados, a DigiCert é usada neste guia, pois eles são um provedor global confiável de soluções de alta garantia TLS/SSL, PKI, IoT e assinatura.

1. Navegue até [a lista de certificados raiz DigiCert disponíveis](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Pesquise por &quot;[!DNL DigiCert Global Root G2]&quot; na lista de certificados disponíveis.
1. Selecione [!DNL **Baixar PEM**] para baixar o arquivo no computador local.
   ![A lista de certificados raiz DigiCert disponíveis com Download PEM realçado.](../images/clients/ssl-modes/digicert.png)
1. Renomeie o arquivo de certificado de segurança para `root.crt`.
1. Copie o arquivo para a pasta [!DNL PostgreSQL]. O caminho de arquivo necessário é diferente dependendo do seu sistema operacional. Se a pasta ainda não existir, crie-a.
   - Se você estiver usando o macOS, o caminho é `/Users/<username>/.postgresql`
   - Se você estiver usando o Windows, o caminho é `%appdata%\postgresql`

>[!TIP]
>
>Para encontrar o local do arquivo `%appdata%` em um sistema operacional Windows, pressione Windows **Win + R** e insira `%appdata%` no campo de pesquisa.

Depois que o arquivo CRT [!DNL DigiCert Global Root G2] estiver disponível na pasta [!DNL PostgreSQL], você poderá se conectar a [!DNL Query Service] usando a opção `sslmode=verify-full` ou `sslmode=verify-ca`.

## Próximas etapas

Ao ler este documento, você compreenderá melhor as opções de SSL disponíveis para conectar um cliente de terceiros ao [!DNL Query Service] e também como habilitar a opção SSL `verify-full` para criptografar seus dados em movimento.

Se ainda não tiver feito isso, siga as orientações em [conectando um cliente de terceiros ao [!DNL Query Service]](./overview.md).
