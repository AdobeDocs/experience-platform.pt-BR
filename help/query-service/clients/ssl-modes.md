---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, conectar, conectar ao serviço de consulta, SSL, ssl, sslmode;
title: Opções de SSL do Serviço de Consulta
description: Saiba mais sobre o suporte SSL para conexões de terceiros com o Adobe Experience Platform Query Service e como se conectar usando o modo SSL verificado-completo.
source-git-commit: 92dac8e75e1ddda860d255ce1b7d278041c89325
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 1%

---

# [!DNL Query Service] Opções de SSL

Para aumentar a segurança, Adobe Experience Platform [!DNL Query Service] fornece suporte nativo para conexões SSL para criptografar comunicações cliente/servidor. Este documento aborda as opções SSL disponíveis para conexões de clientes de terceiros com o [!DNL Query Service] e como se conectar usando o `verify-full` Valor do parâmetro SSL.

## Pré-requisitos

Este documento pressupõe que você já tenha baixado um aplicativo de cliente de desktop de terceiros para uso com os dados da plataforma. Instruções específicas sobre como incorporar a segurança SSL ao se conectar a um cliente de terceiros são encontradas na respectiva documentação do guia de conexão. Para uma lista de todos [!DNL Query Service] clientes suportados, consulte o [visão geral das conexões do cliente](./overview.md).

## Opções de SSL disponíveis {#available-ssl-options}

A Platform oferece suporte a várias opções SSL para atender às suas necessidades de segurança de dados e equilibrar a sobrecarga de processamento da criptografia e da troca de chaves.

Os diferentes `sslmode` os valores de parâmetros fornecem diferentes níveis de proteção. Ao criptografar seus dados em movimento com certificados SSL, ajuda a impedir ataques &quot;man-in-the-middle&quot; (MITM), escuta e representação. A tabela a seguir apresenta um detalhamento dos diferentes modos SSL disponíveis e o nível de proteção que eles oferecem.

>[!NOTE]
>
> O valor SSL `disable` O não é compatível com o Adobe Experience Platform devido à conformidade com a proteção de dados necessária.

| sslmode | Proteção contra escuta | Proteção MITM | Descrição |
|---|---|---|---|
| `allow` | Parcial | Não | A segurança não é uma prioridade, a velocidade e a baixa sobrecarga de processamento são mais importantes. Esse modo só opta pela criptografia se o servidor insistir nela. |
| `prefer` | Parcial | Não | A criptografia não é necessária, mas a comunicação será criptografada se o servidor a suportar. |
| `require` | Sim | Não | A criptografia é necessária em todas as comunicações. A rede é confiável para se conectar ao servidor correto. A validação do certificado SSL do servidor não é necessária. |
| `verify-ca` | Sim | Depende da política de CA | A criptografia é necessária em todas as comunicações. A validação do servidor é necessária antes do compartilhamento dos dados. Isso requer que você configure um certificado raiz no diretório home do PostgreSQL. [Os detalhes são fornecidos abaixo](#instructions) |
| `verify-full` | Sim | Sim | A criptografia é necessária em todas as comunicações. A validação do servidor é necessária antes do compartilhamento dos dados. Isso requer que você configure um certificado raiz no diretório home do PostgreSQL. [Os detalhes são fornecidos abaixo](#instructions). |

>[!NOTE]
>
>A diferença entre `verify-ca` e `verify-full` depende da política da autoridade de certificado raiz (CA). Se você criou sua própria CA local para emitir certificados privados para seus aplicativos, usando `verify-ca` O geralmente oferece proteção suficiente. Se estiver usando uma CA pública, `verify-ca` permite conexões com um servidor que outra pessoa pode ter registrado com a CA. `verify-full` deve ser sempre usada com uma CA raiz pública.

Ao estabelecer uma conexão de terceiros com um banco de dados da plataforma, é recomendável usar `sslmode=require` no mínimo, para garantir uma conexão segura para seus dados em movimento. O `verify-full` O modo SSL é recomendado para uso na maioria dos ambientes sensíveis à segurança.

## Configurar um certificado raiz para verificação de servidor {#root-certificate}

Para garantir uma conexão segura, o uso do SSL deve ser configurado no cliente e no servidor antes da conexão ser feita. Se o SSL estiver configurado apenas no servidor, o cliente poderá enviar informações confidenciais, como senhas, antes que seja estabelecido que o servidor requer alta segurança.

Por padrão, [!DNL PostgreSQL] não executa nenhuma verificação do certificado do servidor. Para verificar a identidade do servidor e garantir uma conexão segura antes do envio de quaisquer dados confidenciais (como parte do SSL) `verify-full` , você deve colocar um certificado raiz (autoassinado) no computador local (`root.crt`) e um certificado folha assinado pelo certificado raiz no servidor.

Se a variável `sslmode` é definido como `verify-full`, libpq verificará se o servidor é confiável, verificando a cadeia de certificados até o certificado raiz armazenado no cliente. Em seguida, verifica se o nome do host corresponde ao nome armazenado no certificado do servidor.

Para permitir a verificação do certificado do servidor, é necessário colocar um ou mais certificados raiz (`root.crt`) na [!DNL PostgreSQL] no diretório inicial. O caminho do arquivo seria semelhante a `~/.postgresql/root.crt`.

## Ative o modo SSL verificado-completo para uso com um modo de terceiros [!DNL Query Service] conexão {#instructions}

Se você precisar de um controle de segurança mais rigoroso do que `sslmode=require`, siga as etapas destacadas para conectar um cliente de terceiros ao [!DNL Query Service] usar `verify-full` Modo SSL.

>[!NOTE]
>
>Há muitas opções disponíveis para obter um certificado SSL. Devido a uma tendência crescente em certificados desonestos, a DigiCert é usada neste guia, pois é um provedor global confiável de soluções TLS/SSL, PKI, IoT e de assinatura.

1. Navegar para [a lista de certificados raiz DigiCert disponíveis](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Pesquisar por &quot;[!DNL DigiCert Global Root CA]&quot; na lista de certificados disponíveis.
1. Selecionar [!DNL **Baixar o PEM**] para baixar o arquivo no computador local.
   ![A lista de certificados raiz DigiCert disponíveis com Baixar PEM foi realçada.](../images/clients/ssl-modes/digicert.png)
1. Renomeie o arquivo de certificado de segurança para `root.crt`.
1. Copie o arquivo para a [!DNL PostgreSQL] pasta. O caminho de arquivo necessário é diferente dependendo do sistema operacional. Se a pasta ainda não existir, crie-a.
   - Se você estiver usando o macOS, o caminho será `/Users/<username>/.postgresql`
   - Se você estiver usando o Windows, o caminho será `%appdata%\postgresql`

>[!TIP]
>
>Para encontrar seu `%appdata%` localização do ficheiro num sistema operacional Windows, prima ⊞ **Win + R** e entrada `%appdata%` no campo de pesquisa.

Depois que a variável [!DNL DigiCert Global Root CA] O arquivo CRT está disponível em seu [!DNL PostgreSQL] , você pode se conectar a [!DNL Query Service] usando o `sslmode=verify-full` ou `sslmode=verify-ca` opção.

## Próximas etapas

Ao ler este documento, você tem uma melhor compreensão das opções SSL disponíveis para conectar um cliente de terceiros ao [!DNL Query Service]e também como ativar a variável `verify-full` Opção SSL para criptografar seus dados em movimento.

Se ainda não o fez, siga as orientações em [conectar um cliente de terceiros ao [!DNL Query Service]](./overview.md).
