---
description: Saiba como definir as configurações de exportação de arquivos para destinos criados com o Destination SDK.
title: Configuração em lote
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 5%

---


# Configuração em lote {#batch-configuration}

Use as opções de configuração de lote no Destination SDK para permitir que os usuários personalizem os nomes de arquivo exportados e configure o agendamento de exportação de acordo com suas preferências.

Ao criar destinos com base em arquivos por meio do Destination SDK, é possível configurar os agendamentos padrão de nomeação e exportação de arquivos ou conceder aos usuários a opção de configurar essas configurações na interface do usuário da plataforma. Por exemplo, você pode configurar comportamentos como:

* Incluindo informações específicas no nome do arquivo, como IDs de segmento, IDs de destino ou informações personalizadas.
* Permitir que os usuários personalizem a nomenclatura de arquivos na interface do usuário da plataforma.
* Configure as exportações de arquivos para que ocorram em intervalos de tempo definidos.
* Defina quais opções de nomeação de arquivo e personalização de agendamento de exportação os usuários podem ver na interface do usuário da plataforma.

As configurações em lote fazem parte da configuração de destino para destinos com base em arquivos.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [use o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Você pode definir as configurações de nomeação de arquivo e programação de exportação por meio do `/authoring/destinations` endpoint . Consulte as páginas de referência da API a seguir para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todas as opções de configuração de lote compatíveis que podem ser usadas para o seu destino e mostra o que os clientes verão na interface do usuário da plataforma.

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações oferecem suporte à funcionalidade descrita nesta página.

| Tipo de integração | Oferece suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Não |
| Integrações baseadas em arquivo (em lote) | Sim |

## Parâmetros compatíveis {#supported-parameters}

Os valores configurados aqui são exibidos na variável [Agendar exportação de segmentos](../../../ui/activate-batch-profile-destinations.md#scheduling) etapa do fluxo de trabalho de ativação de destinos com base em arquivo.

```json
"batchConfig":{
   "allowMandatoryFieldSelection":true,
   "allowDedupeKeyFieldSelection":true,
   "defaultExportMode":"DAILY_FULL_EXPORT",
   "allowedExportMode":[
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
   ],
   "allowedScheduleFrequency":[
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
   ],
   "defaultFrequency":"DAILY",
   "defaultStartTime":"00:00",
   "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
   }
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Booleano | Defina como `true` para permitir que os clientes especifiquem quais atributos de perfil são obrigatórios. O valor padrão é `false`. Consulte [Atributos obrigatórios](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes) para obter mais informações. |
| `allowDedupeKeyFieldSelection` | Booleano | Defina como `true` para permitir que os clientes especifiquem chaves de desduplicação. O valor padrão é `false`.  Consulte [Chaves de desduplicação](../../../ui/activate-batch-profile-destinations.md#deduplication-keys) para obter mais informações. |
| `defaultExportMode` | Enum | Define o modo padrão de exportação de arquivos. Valores compatíveis:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> O valor padrão é `DAILY_FULL_EXPORT`. Consulte a [documentação de ativação em lote](../../../ui/activate-batch-profile-destinations.md#scheduling) para obter detalhes sobre a programação de exportações de arquivos. |
| `allowedExportModes` | Lista | Define os modos de exportação de arquivos disponíveis para os clientes do . Valores compatíveis:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Lista | Define a frequência de exportação de arquivos disponível para os clientes. Valores compatíveis:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Define a frequência padrão de exportação de arquivos.Valores suportados:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> O valor padrão é `DAILY`. |
| `defaultStartTime` | String | Define a hora de início padrão para a exportação de arquivos. Usa o formato de arquivo de 24 horas. O valor padrão é &quot;00:00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | String | *Obrigatório*. Lista de macros de nome de arquivo disponíveis para os usuários escolherem. Isso determina quais itens são anexados aos nomes de arquivo exportados (ID do segmento, nome da organização, data e hora da exportação e outros). Ao definir `defaultFilename`, evite a duplicação de macros. <br><br>Valores compatíveis: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Independentemente da ordem em que você define as macros, a interface do usuário do Experience Platform sempre as exibirá na ordem apresentada aqui. <br><br> If `defaultFilename` está vazio, a variável `allowedFilenameAppendOptions` deve conter pelo menos uma macro. |
| `filenameConfig.defaultFilenameAppendOptions` | String | *Obrigatório*. Macros de nome de arquivo padrão pré-selecionadas que os usuários podem desmarcar.<br><br> As macros nesta lista são um subconjunto das definidas em `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | String | *Opcional*. Define as macros de nome de arquivo padrão para os arquivos exportados. Eles não podem ser substituídos pelos usuários. <br><br>Qualquer macro definida por `allowedFilenameAppendOptions` será anexada após a variável `defaultFilename` macros. <br><br>If `defaultFilename` estiver vazia, você deve definir pelo menos uma macro em `allowedFilenameAppendOptions`. |

{style="table-layout:auto"}

## Configuração do nome do arquivo {#file-name-configuration}

Use macros de configuração de nome de arquivo para definir o que os nomes de arquivo exportados devem incluir. As macros na tabela abaixo descrevem os elementos encontrados na interface do usuário no [configuração do nome do arquivo](../../../ui/activate-batch-profile-destinations.md#file-names) tela.

>[!TIP]
> 
>Como prática recomendada, você sempre deve incluir a variável `SEGMENT_ID` em seus nomes de arquivo exportados. As IDs de segmento são exclusivas, portanto, incluí-las no nome do arquivo é a melhor maneira de garantir que os nomes de arquivo também sejam exclusivos.

| Macro | Rótulo da interface do usuário | Descrição | Exemplo |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destino] | Nome do destino na interface do usuário. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL ID do segmento] | ID exclusiva de segmento gerado por plataforma | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Nome do segmento] | Nome de segmento definido pelo usuário | Assinante de VIP |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL ID de destino] | ID exclusiva, gerada pela plataforma da instância de destino | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Nome do destino] | Nome definido pelo usuário da instância de destino. | Meu destino de publicidade 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Nome da Organização] | Nome da organização do cliente no Adobe Experience Platform. | Meu nome da organização |
| `SANDBOX_NAME` | [!UICONTROL Nome da sandbox] | Nome da sandbox usada pelo cliente. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Data e hora] | `DATETIME` e `TIMESTAMP` ambos definem quando o arquivo foi gerado, mas em formatos diferentes. <br><br><ul><li>`DATETIME` O usa o seguinte formato: AAAMMDD_HHMMSS.</li><li>`TIMESTAMP` O usa o formato Unix de 10 dígitos. </li></ul> `DATETIME` e `TIMESTAMP` são mutuamente exclusivas e não podem ser usadas simultaneamente. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Texto personalizado] | Texto personalizado definido pelo usuário a ser incluído no nome do arquivo. Não pode ser usado em `defaultFilename`. | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL Data e hora] | Carimbo de data e hora de 10 dígitos da hora em que o arquivo foi gerado, no formato Unix. | 1652131584 |

{style="table-layout:auto"}

### Exemplo de configuração do nome do arquivo

O exemplo de configuração abaixo mostra a correspondência entre a configuração usada na chamada da API e as opções mostradas na interface do usuário.

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```

![Imagem da interface do usuário que mostra a tela de configuração do nome do arquivo com macros pré-selecionadas](../../assets/functionality/destination-configuration/file-name-configuration.png)

## Próximas etapas {#next-steps}

Após a leitura deste artigo, você deve ter uma melhor compreensão de como pode configurar os agendamentos de nomeação e exportação de arquivos para seus destinos baseados em arquivos.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Configuração de autenticação do cliente](customer-authentication.md)
* [Autenticação OAuth2](oauth2-authentication.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Atributos da interface do usuário](ui-attributes.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento suportadas](supported-mapping-configurations.md)
* [Delivery de destino](destination-delivery.md)
* [Configuração de metadados de público-alvo](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Qualificações de perfil histórico](historical-profile-qualifications.md)