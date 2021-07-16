---
title: Tratamento de erros
description: Saiba como os erros são tratados na API do reator.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 1%

---

# Tratamento de erros

Quando ocorre um problema ao chamar a API do reator, um erro pode ser retornado de uma das seguintes maneiras:

* **Erros** imediatos: Ao executar uma solicitação que resulta em um erro imediato, uma resposta de erro é retornada pela API, com o status HTTP refletindo o tipo geral de erro que ocorreu.
* **Erros** atrasados: Ao executar uma solicitação de API que resulta em um erro atrasado (como uma atividade assíncrona), um erro pode ser retornado pela API no  `meta.status_details` de um recurso relacionado.

## Formato de erro

As respostas de erro têm o objetivo de estar em conformidade com a [JSON:API errors Specification](http://jsonapi.org/format/#errors) e, em geral, seguem a seguinte estrutura:

```json
{
  "errors": [
    {
      "id": "8a5526da-ab12-4be9-b084-2efe537f388c",
      "status": "404",
      "code": "not-found",
      "title": "Record Not Found",
      "meta": {
        "request_id": "jfb0dQ2e0XVTkQ6AOfEJFfTDjguw9x3d"
      },
      "source": {
        "pointer": "/data"
      }
    }
  ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `id` | Um identificador exclusivo para esta ocorrência específica do problema. |
| `status` | O código de status HTTP aplicável a esse problema, expresso como um valor de string. |
| `code` | Um código de erro específico do aplicativo, expresso como um valor de string. |
| `title` | Um resumo curto e legível do problema que **não deve alterar** de ocorrência para ocorrência, exceto para fins de localização. |
| `detail` | Uma explicação legível por humanos específica para essa ocorrência do problema. Como `title`, o valor deste campo pode ser localizado. |
| `source` | Um objeto que contém referências à origem do erro, incluindo, opcionalmente, qualquer um dos seguintes membros:<ul><li>`pointer`: uma string  [JSON Pointer (RFC6901)](https://datatracker.ietf.org/doc/html/rfc6901) que faz referência à entidade associada no documento de solicitação (como  `/data` para um objeto de dados primário ou  `/data/attributes/title` para um atributo específico).</li></ul> |
| `meta` | Um objeto que contém metadados não padrão sobre o erro. |

{style=&quot;table-layout:auto&quot;}

## Referência de erro

A tabela a seguir lista os diferentes erros que a API pode retornar.

| Título do erro | Descrição |
| --- | --- |
| `authentication-failure` | O token de acesso IMS é inválido. Você pode obter um novo token de acesso entrando novamente. Ou para contas técnicas, gerando um novo JWT e alternando para um token de acesso IMS. |
| `connection-refused` | Não foi possível estabelecer uma conexão com o servidor. |
| `decrypt-bad-passphrase` | Não foi possível descriptografar os dados com a senha fornecida. |
| `decrypt-failed` | Não foi possível descriptografar os dados com a chave privada fornecida. Verifique se a chave funciona localmente e se o espaço em branco foi cortado. |
| `decrypt-no-data` | Os dados não podem ser descriptografados sem uma chave privada. Forneça uma chave privada criptografada. |
| `delegate-descriptor-unresolved` | A extensão não forneceu a definição esperada deste descritor delegado. A extensão pode precisar ser atualizada. |
| `deleted-resources` | Os recursos que você está tentando adicionar à Biblioteca foram excluídos. |
| `environment-in-use` | Um Ambiente só pode ser atribuído a uma Biblioteca por vez. A opção 1 é escolher um ambiente diferente. A opção 2 é liberar esse Ambiente movendo a Biblioteca para outro Ambiente ou excluindo a Biblioteca. |
| `environment-required` | A Biblioteca deve ter um Ambiente atribuído antes de criar uma Build. |
| `extension-not-found` | A extensão que define um elemento de dados ou componente de regra não está incluída na biblioteca. Verifique se todas as extensões necessárias foram adicionadas à biblioteca. |
| `extension-package-path-error` | Um caminho definido em extension.json foi construído incorretamente. |
| `extension-package-transform-definition-error` | Você definiu uma transformação inválida para uma propriedade de objeto. Cada propriedade de objeto pode ter uma transformação definida e deve ser uma transformação de arquivo ou uma transformação de função. |
| `extension-package-zip-error` | Ocorreu um erro ao descompactar o ExtensionPackage ou compactar os arquivos para distribuição. |
| `host-in-use` | Um host não pode ser excluído se um ou mais ambientes estiverem usando. |
| `host-required` | O Ambiente atribuído a esta Biblioteca não tem um Host válido. Verifique qual ambiente está atribuído à biblioteca. Em seguida, atribua um Host válido a esse Ambiente. |
| `host-type-error` | Somente os hosts SFTP precisam ter credenciais verificadas antes de serem usados, de modo que o pré-teste só está disponível para esse tipo de host. |
| `illegal-custom-code-transform` | Você não tem permissão para usar a transformação customCode. Especifique uma função ou transformação de arquivo. |
| `ims-not-authorized` | Ocorreu um erro desconhecido ao autorizar a sua conta. Tente novamente mais tarde. |
| `ims-session-error` | Há um problema com a sessão de logon. Saia e faça logon novamente. |
| `internal-error` | Ocorreu um erro interno. Aguarde alguns minutos e tente novamente. Se o problema persistir, entre em contato com o Atendimento ao cliente. |
| `invalid-data_element` | Um elemento de dados inválido não pode ser adicionado a uma biblioteca. |
| `invalid-embed_code` | Esse não é um código incorporado válido ou você está tentando vinculá-lo a um ambiente de desenvolvimento ou de preparo. Os códigos incorporados do Dynamic Tag Management (DTM) só podem ser vinculados a ambientes de produção. |
| `invalid-extension` | Não é possível adicionar uma extensão inválida a uma biblioteca. |
| `invalid-extension_package_id` | Você só pode modificar algumas das propriedades de objetos de um Pacote de extensão. Você tentou modificar um dos que não é permitido. |
| `invalid-new-owner-org-id` | A ID de organização que você tentou atribuir não é uma ID de organização válida. |
| `invalid-org` | Sua organização ativa não tem acesso à API. Verifique se você está usando a Organização correta. |
| `invalid-rule` | Não é possível adicionar uma regra inválida a uma biblioteca. |
| `invalid-settings-syntax` | Foi encontrado um erro de sintaxe ao analisar as configurações JSON. |
| `library-file-not-found` | Não foi possível encontrar um arquivo necessário definido em extension.json dentro do pacote zip. |
| `minification-error` | Não foi possível compilar o código devido ao código inválido ou ao código ES6. |
| `multiple-revisions` | Somente uma revisão de cada recurso pode ser incluída em uma biblioteca. |
| `no-available-orgs` | Esta conta de usuário não pertence a um perfil de produto que tem acesso a tags. Use o Admin Console para adicionar este usuário a um perfil de produto com direitos de tags. |
| `not-authorized` | Essa conta de usuário não tem as permissões necessárias para executar essa ação. |
| `not-found` | Não foi possível localizar o registro. Verifique a id do objeto que você está tentando recuperar. |
| `not-unique` | O nome que você está tentando usar já está em uso. Para esse recurso, a propriedade &#39;name&#39; deve ser exclusiva. |
| `public-release-not-authorized` | A versão pública das extensões é coordenada por `launch-ext-dev@adobe.com`. Consulte o documento em [extensões de lançamento](../../extension-dev/submit/release.md) para obter mais informações. |
| `read-only` | Este recurso é somente leitura e não pode ser modificado. |
| `session-timeout` | A sessão de usuário expirou. Saia e faça logon novamente. |
| `sftp-authentication-failed` | Falha na autenticação para a conexão SFTP. |
| `sftp-connection-timeout` | A conexão SFTP atingiu o tempo limite. |
| `sftp-exception` | Exceção encontrada ao usar o SFTP para se conectar ao servidor. |
| `sftp-status-exception` | Foi encontrada uma exceção SFTP ao tentar comunicar com o servidor. |
| `socket-error` | Foi encontrado um erro de soquete ao tentar comunicar com o servidor. |
| `ssh-disconnect` | A sessão SSH foi desconectada. |
| `timeout-error` | A conexão com o servidor atingiu o tempo limite. |
| `unknown-error` | Ocorreu um erro inesperado. Tente novamente mais tarde ou ligue para o Atendimento ao cliente e explique o que estava fazendo quando aconteceu. |
| `unsupported-custom-code-language` | Foi fornecido um idioma de código personalizado que não é suportado. |
| `upgraded-extension-required` | Depois de instalar uma atualização de extensão, você deve incluí-la em todas as bibliotecas até que a atualização chegue à produção. A única exceção é se a extensão ainda não tiver sido publicada. |
| `upstream-build-required` | É necessária uma Build bem-sucedida para a Biblioteca upstream antes que você possa criar esta. |

{style=&quot;table-layout:auto&quot;}
