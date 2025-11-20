---
title: Exportar arrays, mapas e objetos do Real-Time CDP
type: Tutorial
description: Saiba como exportar matrizes, mapas e objetos do Real-Time CDP para destinos de armazenamento na nuvem.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: f7ff10dd6489842adb8de49b3f8634c20d77cc71
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 13%

---

# Exportar arrays, mapas e objetos do Real-Time CDP {#export-arrays-cloud-storage}

>[!AVAILABILITY]
>
>A funcionalidade para exportar matrizes e outros objetos complexos para destinos de armazenamento na nuvem está geralmente disponível para os seguintes destinos: [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md).
>
>Além disso, você pode exportar campos do tipo mapa para os seguintes destinos: [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [API HTTP](/help/destinations/catalog/streaming/http-destination.md), [Hubs de Eventos do Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md).


Saiba como exportar matrizes, mapas e objetos do Real-Time CDP para [destinos de armazenamento na nuvem](/help/destinations/catalog/cloud-storage/overview.md). Além disso, você pode exportar campos do tipo mapa para [destinos corporativos](/help/destinations/destination-types.md#advanced-enterprise-destinations) e [destinos de personalização de borda](/help/destinations/destination-types.md#edge-personalization-destinations) limitados. Leia este documento para entender o fluxo de trabalho de exportação, os casos de uso ativados por essa funcionalidade e as limitações conhecidas. Consulte a tabela abaixo para entender a funcionalidade disponível por tipo de destino.

| Tipo de destino | Capacidade de exportar arrays, mapas e outros objetos personalizados |
|---|---|
| Destinos de armazenamento na nuvem criados pela Adobe (Amazon S3, Azure Blob, Azure Data Lake Storage Gen2, Data Landing Zone, Google Cloud Storage, SFTP) | Sim, com a opção Enable export of arrays, maps, and objects ativada ao configurar uma conexão de destino. |
| Destinos de marketing por email baseados em arquivo (Adobe Campaign, Oracle Eloqua, Oracle Responsys, Salesforce Marketing Cloud) | Não |
| Destinos de armazenamento na nuvem personalizados criados por parceiros existentes (destinos personalizados baseados em arquivo criados por meio do Destination SDK) | Não |
| Destinos empresariais (Amazon Kinesis, Hubs de eventos do Azure, API HTTP) | Parcialmente. Você pode selecionar e exportar objetos do tipo mapa na etapa de mapeamento do fluxo de trabalho de ativação. |
| Destinos de transmissão (por exemplo: Facebook, Braze, Google Customer Match e muito mais) | Não |
| Destinos de personalização do Edge | Não |

{style="table-layout:auto"}

Considere essa página o local de entrada para tudo o que você deseja saber sobre a exportação de arrays, mapas e outros tipos de objetos do Experience Platform.

## Vista de baixo à frente

Obtenha as informações mais importantes sobre a funcionalidade nesta seção e prossiga abaixo para as outras seções no documento para obter informações detalhadas.

* Para destinos de armazenamento na nuvem, a capacidade de exportar matrizes, mapas e objetos depende da sua seleção da opção **Exportar matrizes, mapas, objetos**. Leia mais sobre ele [mais abaixo na página](#export-arrays-maps-objects-toggle).
* Você pode exportar matrizes, mapas e objetos para destinos de armazenamento na nuvem em `JSON` e `Parquet` arquivos. Para destinos de personalização corporativa e de borda, o tipo de dados exportado é `JSON`. Há suporte para públicos-alvo de pessoas e de clientes potenciais, mas não para públicos-alvo de contas.
* Para destinos de armazenamento na nuvem baseados em arquivo, você *pode* exportar matrizes, mapas e objetos para arquivos CSV, mas somente usando a funcionalidade de campos calculados e concatenando-os em uma cadeia de caracteres usando a função `array_to_string`.

## Matrizes e outros tipos de objetos no Experience Platform {#arrays-strings-other-objects}

No Experience Platform, você pode usar [esquemas XDM](/help/xdm/home.md) para gerenciar diferentes tipos de campos. Antes de adicionar suporte a exportações de matriz, você podia exportar campos de tipo de par de valor-chave simples, como cadeias de caracteres do Experience Platform, para os destinos desejados. Um exemplo de um campo com suporte para exportação anterior é `personalEmail.address`:`johndoe@acme.org`.

Outros tipos de campo no Experience Platform incluem campos de matriz. Leia mais sobre [gerenciamento de campos de matriz na interface do Experience Platform](/help/xdm/ui/fields/array.md). Agora é possível exportar objetos de matriz, como o exemplo abaixo.

```
organizations = [{
  id: 123,
  orgName: "Acme Inc",
  founded: 1990,
  latestInteraction: "2024-02-16"
}, {
  id: 456,
  orgName: "Superstar Inc",
  founded: 2004,
  latestInteraction: "2023-08-25"
}, {
  id: 789,
  orgName: 'Energy Corp',
  founded: 2021,
  latestInteraction: "2024-09-08"
}]
```

Além de matrizes, você também pode exportar mapas e objetos do Experience Platform para o destino de armazenamento na nuvem desejado. Leia mais sobre [mapas](/help/xdm/ui/fields/map.md) e [objetos](/help/xdm/ui/fields/object.md) no Experience Platform.

## Pré-requisitos {#prerequisites}

[Conecte](/help/destinations/ui/connect-destination.md) a um destino de armazenamento na nuvem desejado. Prossiga pelas [etapas de ativação para destinos de armazenamento na nuvem](/help/destinations/ui/activate-batch-profile-destinations.md) e vá para a etapa [mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping). Ao se conectar ao destino de nuvem desejado, você deve selecionar a opção **[!UICONTROL Export arrays, maps, objects]** ativada. Obtenha mais informações na seção abaixo.

>[!NOTE]
>
>Para destinos de personalização corporativa e de borda, o suporte à exportação para campos do tipo mapa está disponível sem a necessidade de selecionar uma opção de **[!UICONTROL Export arrays, maps, objects]** ativada. Esse botão não está disponível ou não é necessário ao se conectar a esses tipos de destinos.

## Botão de alternância Exportar matrizes, mapas e objetos {#export-arrays-maps-objects-toggle}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_maps_objects"
>title="Exportar matrizes, mapas e objetos"
>abstract="<p> <b>Ative</b> esta configuração para habilitar a exportação de matrizes, mapas e objetos para arquivos JSON ou Parquet. É possível selecionar esses tipos de objetos na exibição do campo de origem da etapa de mapeamento. Com o botão de alternância ativado, não é possível usar a opção de campos calculados na etapa de mapeamento.</p><p>Com o botão de alternância <b>desativado</b>, é possível usar a opção de campos calculados e aplicar várias funções de transformação de dados ao ativar públicos-alvo. No entanto, você <i>não</i> pode exportar matrizes, mapas e objetos para arquivos JSON ou Parquet e deve configurar um outro destino para essa finalidade.</p>"

Ao se conectar a um destino de armazenamento na nuvem baseado em arquivo, você pode ativar ou desativar o **[!UICONTROL Export arrays, maps, objects]**.

![Exportar matrizes, mapas, objetos alternados exibidos com uma configuração ativada ou desativada, bem como realçar o popover.](/help/destinations/assets/ui/export-arrays-calculated-fields/export-objects-toggle.gif)

**Ative** esta configuração para habilitar a exportação de matrizes, mapas e objetos para arquivos JSON ou Parquet. Você pode selecionar esses tipos de objeto na exibição de campo de origem da [etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) ao ativar públicos para destinos de armazenamento na nuvem. No entanto, com essa configuração ativada, não é possível usar a opção calculated fields para transformar dados na ativação.

Com o botão de alternância **desativado**, é possível usar a opção de campos calculados e aplicar várias funções de transformação de dados ao ativar públicos-alvo. No entanto, não é possível exportar matrizes, mapas e objetos para arquivos JSON ou Parquet e você deve configurar um destino separado para essa finalidade.

## Exportar matrizes, mapas, objetos alternados *em* {#export-arrays-maps-objects-toggle-on}

Com essa configuração ativada, você pode exportar objetos inteiros (por exemplo, `person.name`) e matrizes selecionando-os por meio do seletor de campo de origem na etapa de mapeamento do fluxo de trabalho de ativação.

![Selecionar objetos por meio do seletor de campo de origem na etapa de mapeamento do fluxo de trabalho de ativação.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-object.gif)

Com essa opção selecionada, a interface impede que os usuários usem campos calculados, e o controle **[!UICONTROL Add calculated fields]** é desabilitado, conforme mostrado abaixo. Para usar campos calculados para transformações de dados, configure uma conexão de destino com o botão de alternância desativado.

![Controle de campos calculados desabilitado.](/help/destinations/assets/ui/export-arrays-calculated-fields/calculated-fields-disabled.png)

## Exportar matrizes, mapas, objetos alternados *off* {#export-arrays-maps-objects-toggle-off}

Com essa opção definida como *off*, você pode usar a opção de campos calculados e aplicar várias funções de transformação de dados ao ativar públicos. No entanto, não é possível exportar matrizes, mapas e objetos para arquivos JSON ou Parquet e você deve configurar um destino separado para essa finalidade.

Você *pode* exportar matrizes, mapas e objetos para arquivos CSV usando a funcionalidade de campos calculados e concatená-los em uma cadeia de caracteres usando a função `array_to_string`. [Leia mais](#array-to-string-function-export-arrays) sobre como usar esta função.

Leia mais sobre como trabalhar com campos calculados para [executar transformações nos dados exportados para destinos de armazenamento na nuvem](/help/destinations/ui/data-transformations-calculated-fields.md).

## Arquivos exportados de exemplo {#sample-exported-files}

Usando essa funcionalidade, você pode exportar arquivos Parquet e JSON, nos quais os dados preservam a estrutura do Experience Platform. Veja abaixo um exemplo de um arquivo JSON exportado.

+++ Selecione para exibir o arquivo JSON exportado.

```json
{
  "person_name_firstName": "John",
  "person_name_lastName": "Smith",
  "_acmeinc_customer_hs_main_address_scalar": "Oak Avenue No 12",
  "_acmeinc_customer_hs_locations_array": [
    "home address 12",
    "office address 12"
  ],
  "_acmeinc_customer_hs_date_array": [
    "2024-11-14",
    "2024-11-15"
  ],
  "_acmeinc_customer_hs_customer_obj_emails_array0": "john.smith@example.com",
  "_acmeinc_customer_hs_customer_obj": {
    "emails_array": [
      "john.smith@example.com",
      "j.smith@example.com"
    ],
    "name_scalar": "John Smith"
  },
  "_acmeinc_customer_hs_addresses_array_obj": [
    {
      "is_primary": true,
      "streetName_scalar": "Maple Street",
      "streetNo_int": 12
    },
    {
      "is_primary": false,
      "streetName_scalar": "Pine Road",
      "streetNo_int": 45
    }
  ],
  "_acmeinc_customer_hs_addresses_array_obj0": {
    "is_primary": true,
    "streetName_scalar": "Maple Street",
    "streetNo_int": 12
  }
}
```

+++
