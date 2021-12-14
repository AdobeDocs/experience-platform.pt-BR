---
keywords: Experience Platform, receita de vendas de varejo, Data Science Workspace, tópicos populares, receitas
solution: Experience Platform
title: Criar o esquema de vendas de varejo e o conjunto de dados
topic-legacy: tutorial
type: Tutorial
description: Este tutorial fornece os pré-requisitos e os ativos necessários para todos os outros tutoriais do Adobe Experience Platform Data Science Workspace. Após a conclusão, o esquema de Vendas de varejo e os conjuntos de dados estarão disponíveis para você e para os membros de sua Organização IMS no Experience Platform.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---


# Criar o esquema de vendas de varejo e o conjunto de dados

Este tutorial fornece os pré-requisitos e os ativos necessários para todos os outros [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] tutoriais. Após a conclusão, o esquema de Vendas de varejo e os conjuntos de dados estarão disponíveis para você e para os membros de sua Organização IMS em [!DNL Experience Platform].

## Introdução

Antes de iniciar este tutorial, você deve ter os seguintes pré-requisitos:
- Acesso ao [!DNL Adobe Experience Platform]. Se você não tiver acesso a uma Organização IMS no [!DNL Experience Platform], fale com o administrador do sistema antes de continuar.
- Autorização de [!DNL Experience Platform] Chamadas de API. Complete o [Autenticar e acessar APIs do Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) tutorial para obter os seguintes valores para concluir com sucesso este tutorial:
   - Autorização: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Segredo do cliente: `{CLIENT_SECRET}`
   - Certificado do cliente: `{PRIVATE_KEY}`
- Dados de amostra e arquivos de origem do [Receita de Vendas de Varejo](../pre-built-recipes/retail-sales.md). Baixe os ativos necessários para este e outros [!DNL Data Science Workspace] tutoriais da [Repositório Git Adobe public](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2,7](https://www.python.org/downloads/) e o seguinte [!DNL Python] pacotes:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [ditador](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Um entendimento prático dos seguintes conceitos usados neste tutorial:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Noções básicas da composição do schema](../../xdm/schema/field-dictionary.md)

## Criar esquema de vendas de varejo e conjunto de dados

O esquema Vendas de varejo e os conjuntos de dados são criados automaticamente usando o script de bootstrap fornecido. Siga as etapas abaixo em ordem:

### Configurar arquivos

1. Dentro do [!DNL Experience Platform] pacote de recursos tutorial, navegue até o diretório `bootstrap`e abrir `config.yaml` usando um editor de texto adequado.
2. Em `Enterprise` , insira os seguintes valores:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Edite os valores encontrados no `Platform` , Exemplo mostrado abaixo:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: O caminho base para chamadas de API. Não modifique esse valor.
   - `ims_token`: Seu `{ACCESS_TOKEN}` vai aqui.
   - `ingest_data`: Para a finalidade deste tutorial, defina esse valor como `"True"` para criar esquemas e conjuntos de dados de Vendas de Varejo. Um valor de `"False"` criará somente os schemas.
   - `build_recipe_artifacts`: Para a finalidade deste tutorial, defina esse valor como `"False"` para impedir que o script gere um artefato de Receita.
   - `kernel_type`: O tipo de execução do artefato Recipe. Deixe esse valor como `Python` if `build_recipe_artifacts` está definida como `"False"`, caso contrário, especifique o tipo de execução correto.

4. Em `Titles` , forneça as seguintes informações adequadamente para os dados de amostra de Vendas de varejo, salve e feche o arquivo depois que as edições estiverem em vigor. Exemplo mostrado abaixo:

   ```yaml
   Titles:
       input_class_title: retail_sales_input_class
       input_mixin_title: retail_sales_input_mixin
       input_mixin_definition_title: retail_sales_input_mixin_definition
       input_schema_title: retail_sales_input_schema
       input_dataset_title: retail_sales_input_dataset
       file_replace_tenant_id: DSWRetailSalesForXDM0.9.9.9.json
       file_with_tenant_id: DSWRetailSales_with_tenant_id.json
       is_output_schema_different: "True"
       output_mixin_title: retail_sales_output_mixin
       output_mixin_definition_title: retail_sales_output_mixin_definition
       output_schema_title: retail_sales_output_title
       output_dataset_title: retail_sales_output_dataset
   ```

### Executar o script de inicialização

1. Abra o aplicativo de terminal e navegue até o [!DNL Experience Platform] diretório de recursos tutorial.
2. Defina as `bootstrap` diretório como o caminho de trabalho atual e execute o `bootstrap.py` [!DNL Python] inserindo o seguinte comando:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >O script pode levar vários minutos para ser concluído.

## Próximas etapas

Após a conclusão bem-sucedida do script de bootstrap, os esquemas de entrada e saída de Vendas de Varejo e os conjuntos de dados podem ser exibidos em [!DNL Experience Platform]. Consulte a [tutorial visualizar dados do schema](./preview-schema-data.md)
para obter mais informações.

Você também assimilou com sucesso dados de amostra de Vendas de varejo no [!DNL Experience Platform] usando o script bootstrap fornecido.

Para continuar trabalhando com os dados assimilados:
- [Analise seus dados usando notebooks Jupyter](../jupyterlab/analyze-your-data.md)
   - Use notebooks Jupyter no Data Science Workspace para acessar, explorar, visualizar e entender seus dados.
- [Compactar arquivos de origem em uma Receita](./package-source-files-recipe.md)
   - Siga este tutorial para saber como trazer seu próprio modelo para o [!DNL Data Science Workspace] empacotando arquivos de origem em um arquivo de Receita importável.
