---
title: Tratamento de erros
description: Saiba como os erros são tratados na API do Reactor.
exl-id: 336c0ced-1067-4519-94e1-85aea700fce6
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 99%

---

# Tratamento de erros

Quando ocorre um problema ao ser feita uma chamada à API do Reactor, um erro pode ser retornado de uma das seguintes maneiras:

* **Erros imediatos**: ao ser executada uma solicitação que resulta em erro imediato, uma resposta de erro é retornada pela API, e o status HTTP reflete o tipo geral de erro que ocorreu.
* **Erros atrasados**: ao ser executada uma solicitação de API que resulta em erro atrasado (como uma atividade assíncrona), a API pode retornar um erro no `meta.status_details` de um recurso relacionado.

## Formato de erro

As respostas de erro têm como objetivo se adequar às [especificações de erro da JSON:API](http://jsonapi.org/format/#errors) e, em geral, seguem esta estrutura:

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
| `id` | Um identificador exclusivo para essa ocorrência específica do problema. |
| `status` | O código do status HTTP aplicável a esse problema, expresso como um valor de string. |
| `code` | Um código de erro específico do aplicativo, expresso como um valor de string. |
| `title` | Um resumo curto e em formato legível por humanos do problema que **não deve ser alterado** de ocorrência para ocorrência, exceto para fins de localização. |
| `detail` | Uma explicação em formato legível por humanos específica a essa ocorrência do problema. Assim como `title`, o valor desse campo pode ser localizado. |
| `source` | Um objeto que contém referências à origem do erro, incluindo, opcionalmente, qualquer um dos seguintes membros:<ul><li>`pointer`: uma string [JSON Pointer (RFC6901)](https://datatracker.ietf.org/doc/html/rfc6901) que faz referência à entidade associada no documento de solicitação (como `/data` para um objeto de dados principal ou `/data/attributes/title` para um atributo específico).</li></ul> |
| `meta` | Um objeto que contém metadados não padrão sobre o erro. |

{style=&quot;table-layout:auto&quot;}

## Referência de erro

A tabela a seguir lista os diferentes erros que a API pode retornar.

| Título do erro | Descrição |
| --- | --- |
| `authentication-failure` | O token de acesso IMS é inválido. Você pode obter um novo token de acesso fazendo um novo logon. Ou para contas técnicas, gerando um novo JWT e mudando para um token de acesso IMS. |
| `connection-refused` | Não foi possível estabelecer uma conexão com o servidor. |
| `decrypt-bad-passphrase` | Não foi possível descriptografar os dados com a senha fornecida. |
| `decrypt-failed` | Não foi possível descriptografar os dados com a chave privada fornecida. Verifique se a chave funciona localmente e se os espaços em branco foram removidos. |
| `decrypt-no-data` | Não é possível descriptografar os dados sem uma chave privada. Forneça uma chave privada criptografada. |
| `delegate-descriptor-unresolved` | A extensão não forneceu a definição esperada deste descritor delegado. Talvez a extensão precise ser atualizada. |
| `deleted-resources` | Os recursos que você está tentando adicionar à biblioteca foram excluídos. |
| `environment-in-use` | Um ambiente só pode ser atribuído a uma biblioteca por vez. A primeira opção é escolher outro ambiente. A segunda opção é liberar esse ambiente movendo a biblioteca para outro ambiente ou excluindo-a. |
| `environment-required` | Para que você possa criar um build, deve haver um ambiente atribuído à biblioteca. |
| `extension-not-found` | A extensão que define um elemento de dados ou um componente de regra não está incluída na biblioteca. Verifique se todas as extensões necessárias foram adicionadas à biblioteca. |
| `extension-package-path-error` | Um caminho definido em extension.json foi construído incorretamente. |
| `extension-package-transform-definition-error` | Você definiu uma transformação inválida para uma propriedade de objeto. Cada propriedade de objeto pode ter uma transformação definida, que deve ser uma transformação de arquivo ou de função. |
| `extension-package-zip-error` | Ocorreu um erro ao descompactar o Pacote de extensão ou ao compactar os arquivos para distribuição. |
| `host-in-use` | Um host não poderá ser excluído se estiver sendo usado por um ou mais ambientes. |
| `host-required` | O ambiente atribuído a esta biblioteca não tem um host válido. Verifique qual ambiente está atribuído à biblioteca. Em seguida, atribua um host válido a esse ambiente. |
| `host-type-error` | Somente os hosts SFTP precisam ter credenciais verificadas antes de serem usados. Portanto, o pré-teste só está disponível para esse tipo de host. |
| `illegal-custom-code-transform` | Você não tem permissão para usar a transformação customCode. Especifique uma função ou um arquivo de transformação. |
| `ims-not-authorized` | Ocorreu um erro desconhecido ao autorizar a conta. Tente novamente mais tarde. |
| `ims-session-error` | Há um problema na sessão iniciada. Saia e faça logon novamente. |
| `internal-error` | Ocorreu um erro interno. Aguarde alguns minutos e tente novamente. Se o problema persistir, entre em contato com o Atendimento ao cliente. |
| `invalid-data_element` | Não é possível adicionar um elemento de dados inválido a uma biblioteca. |
| `invalid-embed_code` | Esse não é um código integrado válido ou você está tentando vinculá-lo a um ambiente de desenvolvimento ou de preparo. Os códigos integrados do Dynamic Tag Management (DTM) só podem ser vinculados a ambientes de produção. |
| `invalid-extension` | Não é possível adicionar uma extensão inválida a uma biblioteca. |
| `invalid-extension_package_id` | Só é possível modificar algumas das propriedades de objetos de um Pacote de extensão. Aquela que você tentou modificar não é uma das que são permitidas. |
| `invalid-new-owner-org-id` | A ID de organização atribuída é inválida. |
| `invalid-org` | Sua organização principal não tem acesso à API. Verifique se está usando a organização correta. |
| `invalid-rule` | Não é possível adicionar uma regra inválida a uma biblioteca. |
| `invalid-settings-syntax` | Foi encontrado um erro de sintaxe ao serem analisadas as configurações de JSON. |
| `library-file-not-found` | Um arquivo necessário definido em extension.json não foi encontrado no pacote compactado. |
| `minification-error` | Não foi possível compilar o código devido a um código inválido. |
| `multiple-revisions` | Somente uma revisão de cada recurso pode ser incluída em uma biblioteca. |
| `no-available-orgs` | Esta conta de usuário não pertence a um perfil de produto com acesso a tags. Use o Admin Console para adicionar este usuário a um perfil de produto com direito de acesso a tags. |
| `not-authorized` | Essa conta de usuário não tem as permissões necessárias para executar esta ação. |
| `not-found` | Não foi possível localizar o registro. Verifique a id do objeto que você está tentando recuperar. |
| `not-unique` | O nome que você está tentando usar já está em uso. Para esse recurso, a propriedade &#39;name&#39; deve ser exclusiva. |
| `public-release-not-authorized` | O lançamento público das extensões é coordenado por `launch-ext-dev@adobe.com`. Consulte o documento sobre [lançamento de extensões](../../extension-dev/submit/release.md) para obter mais informações. |
| `read-only` | Esse recurso é somente leitura e não pode ser modificado. |
| `session-timeout` | A sessão de usuário expirou. Saia e faça logon novamente. |
| `sftp-authentication-failed` | Falha na autenticação para a conexão SFTP. |
| `sftp-connection-timeout` | A conexão SFTP atingiu o tempo limite. |
| `sftp-exception` | Foi encontrada uma exceção ao ser usado o SFTP para se conectar ao servidor. |
| `sftp-status-exception` | Foi encontrada uma exceção SFTP durante a tentativa de comunicação com o servidor. |
| `socket-error` | Foi encontrado um erro de soquete durante a tentativa de comunicação com o servidor. |
| `ssh-disconnect` | A sessão SSH foi desconectada. |
| `timeout-error` | A conexão com o servidor atingiu o tempo limite. |
| `unknown-error` | Ocorreu um erro inesperado. Tente novamente mais tarde ou entre em contato com o Atendimento ao cliente e explique o que você estava fazendo quando isso ocorreu. |
| `unsupported-custom-code-language` | Foi fornecido um idioma de código personalizado que não é compatível. |
| `upgraded-extension-required` | Depois de instalar uma atualização de extensão, você deve incluí-la em todas as bibliotecas até que a atualização chegue à produção. A única exceção será se a extensão ainda não tiver sido publicada. |
| `upstream-build-required` | É necessário um build bem-sucedido para a Biblioteca upstream para que você possa criá-la. |

{style=&quot;table-layout:auto&quot;}
