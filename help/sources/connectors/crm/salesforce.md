---
title: Visão geral do Salesforce Source Connector
description: Saiba como conectar o Salesforce ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 77941e08df893fab6dfdaf987c56c4d5a3fd4757
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 1%

---

# [!DNL Salesforce]

>[!IMPORTANT]
>
>Agora você pode usar a origem [!DNL Salesforce] ao executar o Adobe Experience Platform no Amazon Web Services (AWS). O Experience Platform em execução no AWS está atualmente disponível para um número limitado de clientes. Para saber mais sobre a infraestrutura de Experience Platform compatível, consulte a [visão geral de várias nuvens do Experience Platform](../../../landing/multi-cloud.md).

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de um sistema CRM de terceiros. O suporte para provedores de CRM inclui [!DNL Salesforce].

## Configure sua origem [!DNL Salesforce] para o Experience Platform no Azure {#azure}

Siga as etapas abaixo para saber como configurar sua conta do [!DNL Salesforce] para o Experience Platform no Azure.

### LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

### Mapeamento de campo de [!DNL Salesforce] para XDM

Para estabelecer uma conexão de origem entre [!DNL Salesforce] e a Platform, os campos de dados de origem [!DNL Salesforce] devem ser mapeados para seus campos XDM de destino apropriados antes de serem assimilados na Platform.

Consulte o seguinte para obter informações detalhadas sobre as regras de mapeamento de campos entre [!DNL Salesforce] conjuntos de dados e a Plataforma:

- [Contatos](../adobe-applications/mapping/salesforce.md#contact)
- [Clientes potenciais](../adobe-applications/mapping/salesforce.md#lead)
- [Contas](../adobe-applications/mapping/salesforce.md#account)
- [Oportunidades](../adobe-applications/mapping/salesforce.md#opportunity)
- [Funções do contato da oportunidade](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campanhas](../adobe-applications/mapping/salesforce.md#campaign)
- [Membros da campanha](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Relação de contato da conta](../adobe-applications/mapping/salesforce.md#account-contact-relation)

### Configurar o namespace [!DNL Salesforce] e o utilitário de geração automática de esquema

Para usar a origem [!DNL Salesforce] como parte de [!DNL B2B-CDP], primeiro você deve configurar um utilitário [!DNL Postman] para gerar automaticamente seus namespaces e esquemas [!DNL Salesforce]. A documentação a seguir fornece informações adicionais sobre a configuração do utilitário [!DNL Postman]:

- Você pode baixar a coleção de utilitários de geração automática de namespace e esquema e o ambiente deste [repositório do GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Para obter informações sobre como usar APIs da plataforma, incluindo detalhes sobre como coletar valores para cabeçalhos necessários e ler chamadas de API de exemplo, consulte o manual em [introdução às APIs da plataforma](../../../landing/api-guide.md).
- Para obter informações sobre como gerar suas credenciais para APIs da plataforma, consulte o tutorial sobre [autenticação e acesso a APIs do Experience Platform](../../../landing/api-authentication.md).
- Para obter informações sobre como configurar o [!DNL Postman] para APIs da Platform, consulte o tutorial em [configuração do console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md).

Com um console de desenvolvedor da Platform e o [!DNL Postman] configurado, agora é possível começar a aplicar os valores de ambiente apropriados ao seu ambiente [!DNL Postman].

+++Exibir o guia da tabela de variáveis

A tabela a seguir contém valores de exemplo, bem como informações adicionais sobre como preencher o ambiente [!DNL Postman]:

| Variable | Descrição | Exemplo |
| --- | --- | --- |
| `CLIENT_SECRET` | Um identificador exclusivo usado para gerar o `{ACCESS_TOKEN}`. Consulte o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | O JSON Web Token (JWT) é uma credencial de autenticação usada para gerar seu {ACCESS_TOKEN}. Consulte o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como gerar seu `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Um identificador exclusivo usado para autenticar chamadas para APIs Experience Platform. Consulte o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | O token de autorização necessário para completar chamadas para APIs de Experience Platform. Consulte o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Com relação a [!DNL Marketo], esse valor é fixo e sempre é definido como: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | O contêiner `global` contém todas as classes, grupos de campos de esquema, tipos de dados e esquemas fornecidos por parceiros de Adobe e Experience Platform padrão. Com relação a [!DNL Marketo], esse valor é fixo e sempre é definido como `global`. | `global` |
| `PRIVATE_KEY` | Uma credencial usada para autenticar sua instância do [!DNL Postman] para APIs Experience Platform. Consulte o tutorial sobre configuração do console do desenvolvedor e [configuração do console do desenvolvedor e  [!DNL Postman]](../../../landing/postman.md) para obter instruções sobre como recuperar o {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Uma credencial usada para integrar ao Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | O Sistema Identity Management (IMS) fornece a estrutura para autenticação de serviços da Adobe. Com relação a [!DNL Marketo], esse valor é fixo e sempre é definido como: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir acesso a seus membros. Consulte o tutorial em [configuração do console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md) para obter instruções sobre como recuperar as informações de `{ORG_ID}`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | O nome da partição de sandbox virtual que você está usando. | `prod` |
| `TENANT_ID` | Uma ID usada para garantir que os recursos criados tenham o namespace adequado e estejam contidos na organização. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | O endpoint de URL para o qual você está fazendo chamadas de API. Este valor é fixo e está sempre definido como: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | O identificador exclusivo da sua conta [!DNL Marketo]. Consulte o tutorial em [autenticando sua [!DNL Marketo] instância](../adobe-applications/marketo/marketo-auth.md) para obter informações sobre como recuperar sua `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | A ID da organização da sua conta [!DNL Salesforce]. Consulte o [[!DNL Salesforce] guia](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) a seguir para obter mais informações sobre como adquirir a ID da organização do [!DNL Salesforce]. | `00D4W000000FgYJUA0` |
| `has_abm` | Um valor booleano que indica se você assinou o [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Um valor booleano que indica se você assinou o [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

+++

### Execute os scripts

Com a coleção e o ambiente [!DNL Postman] configurados, agora é possível executar o script por meio da interface [!DNL Postman].

Na interface [!DNL Postman], selecione a pasta raiz do utilitário gerador automático e, em seguida, selecione **[!DNL Run]** no cabeçalho superior.

![pasta-raiz](../../images/tutorials/create/salesforce/root-folder.png)

A interface [!DNL Runner] é exibida. Aqui, verifique se todas as caixas de seleção estão marcadas e selecione **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

Uma solicitação bem-sucedida cria os namespaces B2B e esquemas de acordo com as especificações beta.

## Configurar a origem do [!DNL Salesforce] para o Experience Platform no Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform executadas no Amazon Web Services (AWS). O Experience Platform em execução no AWS está atualmente disponível para um número limitado de clientes. Para saber mais sobre a infraestrutura de Experience Platform compatível, consulte a [visão geral de várias nuvens do Experience Platform](../../../landing/multi-cloud.md).

Siga as etapas abaixo para saber como configurar sua conta do [!DNL Salesforce] para o Experience Platform no Amazon Web Services (AWS).

### Pré-requisitos

Para conectar sua conta do [!DNL Salesforce] ao Experience Platform em uma região do AWS, você deve ter:

- Uma conta [!DNL Salesforce] com acesso à API.
- Um [!DNL Salesforce Connected App] que você pode usar para habilitar o fluxo de OAuth JWT_BEARER.
- As permissões necessárias em [!DNL Salesforce] para acessar dados.

Incluir na lista de permissões Você também deve adicionar os seguintes endereços IP ao seu arquivo para conectar sua conta do [!DNL Salesforce] ao Experience Platform no Amazon Web Services (AWS):

- `34.193.63.59`
- `44.217.93.240`
- `44.194.79.229`

### Criar um [!DNL Salesforce Connected App]

Primeiro, use o seguinte para criar um par de certificados/chaves de arquivos PEM.

```shell
openssl req -newkey rsa:4096 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem  
```

1. No painel [!DNL Salesforce], selecione as configurações (![O ícone de configurações.](/help/images/icons/settings.png)) e selecione **[!DNL Setup]**.
2. Navegue até [!DNL App Manager] e selecione **[!DNL New Connection App]**.
3. Forneça um nome para o aplicativo e permita que o restante dos campos seja preenchido automaticamente.
4. Habilitar a caixa para [!DNL Enable OAuth Settings].
5. Defina uma URL de retorno de chamada. Como isso não será usado para JWT, você pode usar `https://localhost`.
6. Habilitar a caixa para [!DNL Use Digital Signatures].
7. Faça upload do arquivo cert.pem criado anteriormente.

#### Adicionar permissões necessárias

Adicione as seguintes permissões:

1. Gerenciar dados do usuário por meio das APIs (api)
2. Acessar permissões personalizadas (custom_permissions)
3. Acessar o serviço de URL de identidade (id, perfil, email, endereço, telefone)
4. Acessar identificadores exclusivos (openid)
5. Executar solicitações a qualquer momento (refresh_token, offline_access)

Após adicionar suas permissões, habilite a caixa para **[!DNL Issue JSON Web Token (JWT)-based access tokens for named user]**.

Em seguida, selecione **[!DNL Save]**, **[!DNL Continue]** e **[!DNL Manage Customer Details]**. Use o painel de detalhes do consumidor para recuperar o seguinte:

- **Chave do consumidor**: posteriormente, você usará essa chave do consumidor como sua ID de cliente ao autenticar sua conta do [!DNL Salesforce] no Experience Platform.
- **Segredo do consumidor**: posteriormente, você usará esse segredo do consumidor como sua ID de cliente ao autenticar sua conta do [!DNL Salesforce] no Experience Platform.

### Autorizar o usuário [!DNL Salesforce] para o Aplicativo Conectado

Siga as etapas abaixo para obter autorização para usar o Aplicativo conectado:

1. Navegue até **[!DNL Manage Connected Apps]**.
2. Selecione **[!DNL Edit]**.
3. Configure **[!DNL Permitted Users]** como **[!DNL Admin approved users are pre-authorized]** e selecione **[!DNL Save]**.
4. Navegue até **[!DNL Settings]> [!DNL Manage Users] >[!DNL Profiles]**.
5. Edite o perfil associado ao usuário.
6. Navegue até **[!DNL Connected App Access]** e selecione o aplicativo criado em uma etapa anterior.

### Gerar token de portador JWT

Siga as etapas abaixo para gerar o token do portador JWT.

#### Converter par de chaves em pkcs12

Para gerar o token do portador JWT, primeiro use o seguinte comando para converter o certificado/par de chaves em formato pkcs12. Durante esta etapa, você também deve **definir uma senha de exportação** quando solicitado.

```shell
openssl pkcs12 -export -in cert.pem -inkey key.pem -name jwtcert >jwtcert.p12
```

#### Criar armazenamento de chaves java baseado em pkcs12

Em seguida, use o seguinte comando para criar um keystore java com base no pkcs12 que você acabou de gerar. Durante esta etapa, você também deve **definir uma senha de armazenamento de chaves de destino** quando solicitado. Além disso, você deve fornecer a senha de exportação anterior como a senha do armazenamento de chaves de origem.

```shell
keytool -importkeystore -srckeystore jwtcert.p12 -destkeystore keystore.jks -srcstoretype pkcs12 -alias jwtcert
```

#### Confirme se o keystroke.jks inclui um alias jwtcert

Em seguida, use o comando a seguir para confirmar se o seu `keystroke.jks` inclui um alias `jwtcert`. Durante esta etapa, você será solicitado a fornecer a senha do armazenamento de chaves de destino que foi gerada na etapa anterior.

```shell
keytool -keystore keystore.jks -list
```

#### Gerar token assinado

Finalmente, use a classe java JWTExample abaixo para gerar seu token assinado.

```java
package org.example;
 
import org.apache.commons.codec.binary.Base64;
 
import java.io.*;
import java.security.*;
import java.text.MessageFormat;
 
public class Main {
 
    public static void main(String[] args) {
 
        String header = "{\"alg\":\"RS256\"}";
        String claimTemplate = "'{'\"iss\": \"{0}\", \"sub\": \"{1}\", \"aud\": \"{2}\", \"exp\": \"{3}\"'}'";
 
        try {
            StringBuffer token = new StringBuffer();
 
            //Encode the JWT Header and add it to our string to sign
            token.append(Base64.encodeBase64URLSafeString(header.getBytes("UTF-8")));
 
            //Separate with a period
            token.append(".");
 
            //Create the JWT Claims Object
            String[] claimArray = new String[5];
            claimArray[0] = "{CLIENT_ID}";
            claimArray[1] = "{AUTHORIZED_SALESFORCE_USERNAME}";
            claimArray[2] = "{SALESFORCE_LOGIN_URL}";
            claimArray[3] = Long.toString((System.currentTimeMillis() / 1000) + 2629746*4);
            MessageFormat claims;
            claims = new MessageFormat(claimTemplate);
            String payload = claims.format(claimArray);
 
            //Add the encoded claims object
            token.append(Base64.encodeBase64URLSafeString(payload.getBytes("UTF-8")));
 
            //Load the private key from a keystore
            KeyStore keystore = KeyStore.getInstance("JKS");
            keystore.load(new FileInputStream("path/to/keystore"), "keystorepassword".toCharArray());
            PrivateKey privateKey = (PrivateKey) keystore.getKey("jwtcert", "privatekeypassword".toCharArray());
 
            //Sign the JWT Header + "." + JWT Claims Object
            Signature signature = Signature.getInstance("SHA256withRSA");
            signature.initSign(privateKey);
            signature.update(token.toString().getBytes("UTF-8"));
            String signedPayload = Base64.encodeBase64URLSafeString(signature.sign());
 
            //Separate with a period
            token.append(".");
 
            //Add the encoded signature
            token.append(signedPayload);
 
            System.out.println(token.toString());
 
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

| Propriedade | Configurações  |
| --- | --- |
| `claimArray[0]` | Atualize `claimArray[0]` com sua ID de cliente. |
| `claimArray[1]` | Atualize `claimArray[1]` com o nome de usuário [!DNL Salesforce] autorizado no aplicativo. |
| `claimArray[2]` | Atualize `claimArray[2]` com sua URL de logon [!DNL Salesforce]. |
| `claimArray[3]` | Atualize `claimArray[3]` com uma data de expiração formatada em milissegundos desde a época. Por exemplo, `3660624000000` é 12-31-2085. |
| `/path/to/keystore` | Substitua `/path/to/keystore` pelo caminho correto para seu keystore.jks |
| `keystorepassword` | Substitua `keystorepassword` pela senha do keystore de destino. |
| `privatekeypassword` | Substitua `privatekeypassword` pela senha do keystore de origem. |

## Próximas etapas

Após concluir o pré-requisito configurado para sua conta do [!DNL Salesforce], você pode prosseguir para conectar sua conta do [!DNL Salesforce] ao Experience Platform e assimilar seus dados do CRM. Leia a documentação abaixo para obter mais informações:

### Conectar [!DNL Salesforce] à plataforma usando APIs

A documentação abaixo fornece informações sobre como conectar o [!DNL Salesforce] à Plataforma usando APIs ou a interface do usuário:

- [Conectar o Salesforce ao Experience Platform usando a API de serviço de fluxo](../../tutorials/api/create/crm/salesforce.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma origem de CRM usando a API do Serviço de Fluxo](../../tutorials/api/collect/crm.md)

### Conectar [!DNL Salesforce] à Plataforma usando a interface

- [Criar uma conexão de origem do Salesforce na interface](../../tutorials/ui/create/crm/salesforce.md)
- [Criar um fluxo de dados para uma conexão de CRM na interface](../../tutorials/ui/dataflow/crm.md)