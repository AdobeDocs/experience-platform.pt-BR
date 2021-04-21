---
keywords: Experience Platform, receita de vendas de varejo, Data Science Workspace, tópicos populares, receitas
solution: Experience Platform
title: Criar o esquema de vendas de varejo e o conjunto de dados
topic-legacy: tutorial
type: Tutorial
description: Este tutorial fornece os pré-requisitos e os ativos necessários para todos os outros tutoriais do Adobe Experience Platform Data Science Workspace. Após a conclusão, o esquema de Vendas de varejo e os conjuntos de dados estarão disponíveis para você e para os membros de sua Organização IMS no Experience Platform.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Criar o esquema de vendas de varejo e o conjunto de dados

Este tutorial fornece os pré-requisitos e os ativos necessários para todos os outros tutoriais [!DNL Adobe Experience Platform] [!DNL Data Science Workspace]. Após a conclusão, o esquema de Vendas de varejo e os conjuntos de dados estarão disponíveis para você e para os membros de sua Organização IMS em [!DNL Experience Platform].

## Introdução

Antes de iniciar este tutorial, você deve ter os seguintes pré-requisitos:
- Acesso a [!DNL Adobe Experience Platform]. Se você não tiver acesso a uma Organização IMS em [!DNL Experience Platform], fale com o administrador do sistema antes de continuar.
- Autorização para fazer chamadas de API [!DNL Experience Platform]. Conclua o tutorial [Autenticar e acessar APIs do Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) para obter os seguintes valores para concluir este tutorial com êxito:
   - Autorização: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Segredo do cliente: `{CLIENT_SECRET}`
   - Certificado do cliente: `{PRIVATE_KEY}`
- Dados de exemplo e arquivos de origem para a [Receita de Vendas de Varejo](../pre-built-recipes/retail-sales.md). Baixe os ativos necessários para este e outros tutoriais [!DNL Data Science Workspace] do repositório Git público do Adobe](https://github.com/adobe/experience-platform-dsw-reference/).[
- [Python >= 2.7](https://www.python.org/downloads/) e os seguintes  [!DNL Python] pacotes:
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

1. No pacote de recursos do tutorial [!DNL Experience Platform] , navegue até o diretório `bootstrap` e abra `config.yaml` usando um editor de texto apropriado.
2. Na seção `Enterprise`, insira os seguintes valores:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Edite os valores encontrados na seção `Platform`, Exemplo mostrado abaixo:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` : O caminho base para chamadas de API. Não modifique esse valor.
   - `ims_token` : O seu  `{ACCESS_TOKEN}` vai aqui.
   - `ingest_data` : Para a finalidade deste tutorial, defina esse valor como  `"True"` para criar esquemas e conjuntos de dados de Vendas de Varejo. Um valor de `"False"` só criará os esquemas.
   - `build_recipe_artifacts` : Para a finalidade deste tutorial, defina esse valor como  `"False"` para impedir que o script gere um artefato de Receita.
   - `kernel_type` : O tipo de execução do artefato Recipe. Deixe esse valor como `Python` se `build_recipe_artifacts` estiver definido como `"False"`, caso contrário especifique o tipo de execução correto.

4. Na seção `Titles` , forneça as seguintes informações adequadamente para os dados de amostra de Vendas de varejo, salve e feche o arquivo depois que as edições estiverem em vigor. Exemplo mostrado abaixo:

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

1. Abra o aplicativo de terminal e navegue até o diretório de recursos tutorial [!DNL Experience Platform] .
2. Defina o diretório `bootstrap` como o caminho de trabalho atual e execute o script `bootstrap.py` [!DNL Python] inserindo o seguinte comando:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >O script pode levar vários minutos para ser concluído.

## Próximas etapas

Após a conclusão bem-sucedida do script de bootstrap, os esquemas de entrada e saída de Vendas de Varejo e os conjuntos de dados podem ser exibidos em [!DNL Experience Platform]. Consulte o [tutorial de dados de esquema de visualização](./preview-schema-data.md)
para obter mais informações.

Você também assimilou com sucesso dados de amostra de Vendas de varejo em [!DNL Experience Platform] usando o script de bootstrap fornecido.

Para continuar trabalhando com os dados assimilados:
- [Analise seus dados usando notebooks Jupyter](../jupyterlab/analyze-your-data.md)
   - Use notebooks Jupyter no Data Science Workspace para acessar, explorar, visualizar e entender seus dados.
- [Compactar arquivos de origem em uma Receita](./package-source-files-recipe.md)
   - Siga este tutorial para saber como trazer seu próprio Modelo para [!DNL Data Science Workspace] empacotando arquivos de origem em um arquivo de Receita importante.
