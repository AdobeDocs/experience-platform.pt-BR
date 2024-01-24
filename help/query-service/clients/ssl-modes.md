---
keywords: Experience Platform;início;tópicos populares;Serviço de consulta;serviço de consulta;conectar;conectar ao serviço de consulta;SSL;ssl;sslmode;
title: Opções SSL do Serviço de Consulta
description: Saiba mais sobre o suporte SSL para conexões de terceiros ao Serviço de consulta da Adobe Experience Platform e como se conectar usando o modo SSL verify-full.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 229ce98da8f1c97e421ef413826b0d23754d16df
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 1%

---

# [!DNL Query Service] Opções de SSL

Para maior segurança, o Adobe Experience Platform [!DNL Query Service] O oferece suporte nativo a conexões SSL para criptografar comunicações de cliente/servidor. Este documento aborda as opções de SSL disponíveis para conexões de clientes de terceiros com o [!DNL Query Service] e como se conectar usando o `verify-full` Valor do parâmetro SSL.

## Pré-requisitos

Este documento supõe que você já tenha baixado um aplicativo de cliente de desktop de terceiros para uso com os dados da plataforma. Instruções específicas sobre como incorporar segurança SSL ao se conectar com um cliente de terceiros são encontradas em sua respectiva documentação do guia de conexão. Para obter uma lista de todas as [!DNL Query Service] clientes suportados, consulte a seção [visão geral das conexões de clientes](./overview.md).

## Opções de SSL disponíveis {#available-ssl-options}

A Platform oferece suporte a várias opções SSL para atender às suas necessidades de segurança de dados e equilibrar a sobrecarga de processamento da criptografia e do intercâmbio de chaves.

Os diferentes `sslmode` Os valores de parâmetro do fornecem diferentes níveis de proteção. Ao criptografar seus dados em movimento com certificados SSL, ajuda a impedir ataques &quot;man-in-the-middle&quot; (MITM), espionagem e representação. A tabela abaixo fornece um detalhamento dos diferentes modos SSL disponíveis e o nível de proteção fornecido.

>[!NOTE]
>
> O valor SSL `disable` O não é compatível com o Adobe Experience Platform devido à conformidade necessária com a proteção de dados.

| sslmode | Proteção contra espionagem | Proteção MITM | Descrição |
|---|---|---|---|
| `allow` | Parcial | Não | A segurança não é uma prioridade, a velocidade e uma baixa sobrecarga de processamento são mais importantes. Esse modo só optará pela criptografia se o servidor insistir nela. |
| `prefer` | Parcial | Não | A criptografia não é necessária, mas a comunicação será criptografada se o servidor permitir. |
| `require` | Sim | Não | A criptografia é necessária em todas as comunicações. A rede é confiável para se conectar ao servidor correto. A validação do certificado SSL do servidor não é necessária. |
| `verify-ca` | Sim | Depende da política de CA | A criptografia é necessária em todas as comunicações. A validação do servidor é necessária antes que os dados sejam compartilhados. Isso requer que você configure um certificado raiz em seu [!DNL PostgreSQL] diretório inicial. [Os detalhes são fornecidos abaixo](#instructions) |
| `verify-full` | Sim | Sim | A criptografia é necessária em todas as comunicações. A validação do servidor é necessária antes que os dados sejam compartilhados. Isso requer que você configure um certificado raiz em seu [!DNL PostgreSQL] diretório inicial. [Os detalhes são fornecidos abaixo](#instructions). |

>[!NOTE]
>
>A diferença entre `verify-ca` e `verify-full` depende da política da autoridade de certificação (CA) raiz. Se você criou sua própria CA local para emitir certificados privados para seus aplicativos, usando `verify-ca` O geralmente fornece proteção suficiente. Se estiver usando uma CA pública, `verify-ca` permite conexões com um servidor que outra pessoa pode ter registrado com a CA. `verify-full` deve ser sempre usado com uma CA raiz pública.

Ao estabelecer uma conexão de terceiros com um banco de dados da Platform, é recomendável usar `sslmode=require` no mínimo, para garantir uma conexão segura para seus dados em movimento. A variável `verify-full` O modo SSL é recomendado para uso na maioria dos ambientes sensíveis à segurança.

## Configurar um certificado raiz para verificação do servidor {#root-certificate}

>[!IMPORTANT]
>
>Os certificados TLS/SSL em ambientes de Produção para a API Postgres interativa do serviço de consulta foram atualizados na quarta-feira, 24 de janeiro de 2024.<br>Embora esse seja um requisito anual, nessa ocasião o certificado raiz na cadeia também foi alterado, pois o provedor de certificados TLS/SSL do Adobe atualizou sua hierarquia de certificados. Isso pode afetar determinados clientes Postgres se a lista de Autoridades de certificação não tiver o certificado raiz. Por exemplo, um cliente PSQL CLI pode precisar ter os certificados raiz adicionados a um arquivo explícito `~/postgresql/root.crt`, caso contrário, poderá resultar em um erro. Por exemplo, `psql: error: SSL error: certificate verify failed`. Consulte a [Documentação oficial do PostgreSQL](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) para obter mais informações sobre esse problema.<br>O certificado raiz a ser adicionado pode ser baixado de [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

Para garantir uma conexão segura, o uso do SSL deve ser configurado no cliente e no servidor antes que a conexão seja feita. Se o SSL só estiver configurado no servidor, o cliente poderá enviar informações confidenciais, como senhas, antes de se estabelecer que o servidor requer alta segurança.

Por padrão, [!DNL PostgreSQL] O não executa nenhuma verificação do certificado do servidor. Para verificar a identidade do servidor e garantir uma conexão segura antes que quaisquer dados confidenciais sejam enviados (como parte do SSL) `verify-full` ), você deve colocar um certificado raiz (autoassinado) no computador local (`root.crt`) e um certificado folha assinado pelo certificado raiz no servidor.

Se a variável `sslmode` está definido como `verify-full`, libpq verificará se o servidor é confiável verificando a cadeia de certificados até o certificado raiz armazenado no cliente. Em seguida, ele verifica se o nome do host corresponde ao nome armazenado no certificado do servidor.

Para permitir a verificação do certificado do servidor, coloque um ou mais certificados raiz (`root.crt`) no [!DNL PostgreSQL] arquivo no seu diretório inicial. O caminho do arquivo seria semelhante a `~/.postgresql/root.crt`.

## Ativar o modo Verificar SSL completo para uso com terceiros [!DNL Query Service] conexão {#instructions}

Se você precisar de um controle de segurança mais rigoroso do que `sslmode=require`, você pode seguir as etapas destacadas para conectar um cliente de terceiros ao [!DNL Query Service] usar `verify-full` Modo SSL.

>[!NOTE]
>
>Há muitas opções disponíveis para obter um certificado SSL. Devido a uma tendência crescente em certificados não autorizados, a DigiCert é usada neste guia, pois eles são um provedor global confiável de soluções de alta garantia TLS/SSL, PKI, IoT e assinatura.

1. Navegue até [a lista de certificados raiz DigiCert disponíveis](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Pesquisar por &quot;[!DNL DigiCert Global Root G2]&quot; na lista de certificados disponíveis.
1. Selecionar [!DNL **Baixar PEM**] para baixar o arquivo no computador local.
   ![A lista de certificados raiz DigiCert disponíveis com Download PEM realçado.](../images/clients/ssl-modes/digicert.png)
1. Renomeie o arquivo de certificado de segurança para `root.crt`.
1. Copie o arquivo para a [!DNL PostgreSQL] pasta. O caminho de arquivo necessário é diferente dependendo do seu sistema operacional. Se a pasta ainda não existir, crie-a.
   - Se você estiver usando o macOS, o caminho será `/Users/<username>/.postgresql`
   - Se você estiver usando o Windows, o caminho será `%appdata%\postgresql`

>[!TIP]
>
>Para encontrar o `%appdata%` local do arquivo em um sistema operacional Windows, pressione Windows **Win + R** e entrada `%appdata%` no campo de pesquisa.

Depois que a variável [!DNL DigiCert Global Root G2] O arquivo CRT está disponível em [!DNL PostgreSQL] , você pode se conectar a [!DNL Query Service] usando o `sslmode=verify-full` ou `sslmode=verify-ca` opção.

## Próximas etapas

Ao ler este documento, você compreenderá melhor as opções de SSL disponíveis para conectar um cliente de terceiros ao [!DNL Query Service]e também como habilitar a função `verify-full` Opção SSL para criptografar seus dados em movimento.

Se ainda não tiver feito isso, siga as orientações em [conexão de um cliente de terceiros ao [!DNL Query Service]](./overview.md).
