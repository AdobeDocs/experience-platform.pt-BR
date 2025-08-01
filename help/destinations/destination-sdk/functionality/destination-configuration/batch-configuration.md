---
description: Saiba como definir as configurações de exportação de arquivo para destinos criados com o Destination SDK.
title: Configuração em lote
exl-id: 0ffbd558-a83c-4c3d-b4fc-b6f7a23a163a
source-git-commit: a149e0b96b68c8ac61e355cf8605742feb4eec41
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 2%

---

# Configuração em lote {#batch-configuration}

Use as opções de configuração em lote no Destination SDK para permitir que os usuários personalizem os nomes dos arquivos exportados e configurem o agendamento de exportação de acordo com suas preferências.

Ao criar destinos baseados em arquivo por meio do Destination SDK, é possível configurar a nomenclatura de arquivo padrão e os agendamentos de exportação ou dar aos usuários a opção de definir essas configurações na interface do usuário do Experience Platform. Por exemplo, você pode configurar comportamentos como:

* Incluindo informações específicas no nome do arquivo, como IDs de público-alvo, IDs de destino ou informações personalizadas.
* Permitir que os usuários personalizem a nomeação de arquivos na interface do usuário do Experience Platform.
* Configure as exportações de arquivos para que ocorram em intervalos de tempo definidos.
* Defina quais opções de nomenclatura de arquivo e personalização de agendamento de exportação os usuários podem ver na interface do usuário do Experience Platform.

As definições de configuração em lote fazem parte da configuração de destino para destinos baseados em arquivo.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama na documentação de [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [usar o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Você pode definir as configurações de nomenclatura de arquivo e agenda de exportação por meio do ponto de extremidade `/authoring/destinations`. Consulte as seguintes páginas de referência de API para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todas as opções de configuração em lote compatíveis que você pode usar para o seu destino e mostra o que os clientes verão na interface do Experience Platform.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1&rbrace;.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Não |
| Integrações baseadas em arquivo (lote) | Sim |

## Parâmetros compatíveis {#supported-parameters}

Os valores configurados aqui são exibidos na etapa [Agendar exportação de público-alvo](../../../ui/activate-batch-profile-destinations.md#scheduling) do fluxo de trabalho de ativação dos destinos baseados em arquivo.

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
      "ONCE",
      "WEEKLY",
      "MONTHLY"
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
   "segmentGroupingEnabled": true
   }
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Booleano | Defina como `true` para permitir que os clientes especifiquem quais atributos de perfil são obrigatórios. O valor padrão é `false`. Consulte [Atributos obrigatórios](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes) para obter mais informações. |
| `allowDedupeKeyFieldSelection` | Booleano | Defina como `true` para permitir que os clientes especifiquem chaves de desduplicação. O valor padrão é `false`.  Consulte [Chaves de desduplicação](../../../ui/activate-batch-profile-destinations.md#deduplication-keys) para obter mais informações. |
| `defaultExportMode` | Enumeração | Define o modo de exportação de arquivo padrão. Valores compatíveis:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> O valor padrão é `DAILY_FULL_EXPORT`. Consulte a [documentação de ativação em lote](../../../ui/activate-batch-profile-destinations.md#scheduling) para obter detalhes sobre o agendamento de exportações de arquivos. |
| `allowedExportModes` | Lista | Define os modos de exportação de arquivo disponíveis para clientes. Valores compatíveis:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Lista | Define a frequência de exportação de arquivos disponível para os clientes. Valores compatíveis:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li><li>`WEEKLY`</li><li>`MONTHLY`</li></ul> |
| `defaultFrequency` | Enumeração | Define a frequência de exportação de arquivo padrão. Valores compatíveis:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> O valor padrão é `DAILY`. |
| `defaultStartTime` | String | Define a hora de início padrão da exportação de arquivos. Usa o formato de arquivo de 24 horas. O valor padrão é &quot;00:00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | String | *Obrigatório*. Lista de macros de nome de arquivo disponíveis para os usuários escolherem. Isso determina quais itens são anexados a nomes de arquivo exportados (ID de público-alvo, nome da organização, data e hora da exportação e outros). Ao configurar `defaultFilename`, evite a duplicação de macros. <br><br>Valores com suporte: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Independentemente da ordem em que você define as macros, a interface do usuário do Experience Platform sempre as exibirá na ordem apresentada aqui. <br><br> Se `defaultFilename` estiver vazio, a lista `allowedFilenameAppendOptions` deverá conter pelo menos uma macro. |
| `filenameConfig.defaultFilenameAppendOptions` | String | *Obrigatório*. Macros de nome de arquivo padrão pré-selecionadas que os usuários podem desmarcar.<br><br> As macros nesta lista são um subconjunto das definidas em `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | String | *Opcional*. Define as macros de nome de arquivo padrão para os arquivos exportados. Eles não podem ser substituídos por usuários. <br><br>Qualquer macro definida por `allowedFilenameAppendOptions` será anexada após as `defaultFilename` macros. <br><br>Se `defaultFilename` estiver vazio, você deverá definir pelo menos uma macro em `allowedFilenameAppendOptions`. |
| `segmentGroupingEnabled` | Booleano | Define se os públicos ativados devem ser exportados em um único arquivo ou em vários arquivos, com base na [política de mesclagem](../../../../profile/merge-policies/overview.md) do público-alvo. Valores compatíveis: <ul><li>`true`: exporta um arquivo por política de mesclagem.</li><li>`false`: exporta um arquivo por público, independentemente da política de mesclagem. Esse é o comportamento padrão. Você pode obter o mesmo resultado omitindo esse parâmetro totalmente.</li></ul> |

{style="table-layout:auto"}

## Configuração do nome do arquivo {#file-name-configuration}

Use macros de configuração de nome de arquivo para definir o que os nomes de arquivo exportados devem incluir. As macros na tabela abaixo descrevem elementos encontrados na interface do usuário na tela [configuração de nome de arquivo](../../../ui/activate-batch-profile-destinations.md#file-names).

>[!TIP]
> 
>Como prática recomendada, você sempre deve incluir a macro `SEGMENT_ID` nos nomes de arquivos exportados. As IDs de segmento são exclusivas, portanto, incluí-las no nome do arquivo é a melhor maneira de garantir que os nomes de arquivo também sejam exclusivos.

| Macro | Rótulo da interface | Descrição | Exemplo |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destino] | Nome do destino na interface do usuário. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL ID do segmento] | ID de público-alvo exclusiva gerada pela Experience Platform | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Nome do segmento] | Nome de público definido pelo usuário | assinante do VIP |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL ID de Destino] | ID exclusiva gerada pela Experience Platform da instância de destino | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Nome do Destino] | Nome definido pelo usuário da instância de destino. | Meu destino do Advertising 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Nome da Organização] | Nome da organização do cliente no Adobe Experience Platform. | Nome da Minha Organização |
| `SANDBOX_NAME` | [!UICONTROL Nome da sandbox] | Nome da sandbox usada pelo cliente. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Data e hora] | `DATETIME` e `TIMESTAMP` definem quando o arquivo foi gerado, mas em formatos diferentes. <br><br><ul><li>`DATETIME` usa o seguinte formato: AAAAMMDD_HHMMSS.</li><li>`TIMESTAMP` usa o formato Unix de 10 dígitos. </li></ul> `DATETIME` e `TIMESTAMP` são mutuamente exclusivos e não podem ser usados simultaneamente. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Texto personalizado] | Texto personalizado definido pelo usuário a ser incluído no nome do arquivo. Não pode ser usado em `defaultFilename`. | Meu_Texto_Personalizado |
| `TIMESTAMP` | [!UICONTROL Data e hora] | Carimbo de data e hora de 10 dígitos da hora em que o arquivo foi gerado, no formato Unix. | 1652131584 |
| `MERGE_POLICY_ID` | [!UICONTROL ID da Política de Mesclagem] | A ID da [política de mesclagem](../../../../profile/merge-policies/overview.md) usada para gerar o público exportado. Use essa macro quando estiver agrupando públicos exportados em arquivos, com base na política de mesclagem. Use esta macro junto com `segmentGroupingEnabled:true`. | e8591fdb-2873-4b12-b63e-15275b1c1439 |
| `MERGE_POLICY_NAME` | [!UICONTROL Nome da Política de Mesclagem] | O nome da [política de mesclagem](../../../../profile/merge-policies/overview.md) usada para gerar o público exportado. Use essa macro quando estiver agrupando públicos exportados em arquivos, com base na política de mesclagem. Use esta macro junto com `segmentGroupingEnabled:true`. | Minha política de mesclagem personalizada |

{style="table-layout:auto"}

### Exemplo de configuração do nome do arquivo

O exemplo de configuração abaixo mostra a correspondência entre a configuração usada na chamada de API e as opções mostradas na interface do usuário.

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

![Imagem da interface do usuário mostrando a tela de configuração de nome de arquivo com macros pré-selecionadas](../../assets/functionality/destination-configuration/file-name-configuration.png)

## Próximas etapas {#next-steps}

Depois de ler este artigo, você deverá entender melhor como configurar a nomenclatura de arquivos e os cronogramas de exportação para seus destinos baseados em arquivo.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Configuração de autenticação do cliente](customer-authentication.md)
* [Autorização OAuth2](oauth2-authorization.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Atributos da interface](ui-attributes.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento compatíveis](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Configuração de metadados de público](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Qualificações do perfil histórico](historical-profile-qualifications.md)
