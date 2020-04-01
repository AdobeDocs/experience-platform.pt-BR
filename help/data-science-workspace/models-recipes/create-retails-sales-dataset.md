---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Criar o schema de vendas de varejo e o conjunto de dados
topic: Tutorial
translation-type: tm+mt
source-git-commit: 91c7b7e285a4745da20ea146f2334510ca11b994

---


# Criar o schema de vendas de varejo e o conjunto de dados

Este tutorial fornece os pré-requisitos e os ativos necessários para todos os outros tutoriais da Adobe Experience Platform Data Science Workspace. Após a conclusão, o schema de vendas de varejo e os conjuntos de dados estarão disponíveis para você e para os membros da organização IMS na plataforma da experiência.

## Introdução

Antes de iniciar este tutorial, você deve ter os seguintes pré-requisitos:
- Acesso à Adobe Experience Platform. Se você não tiver acesso a uma organização IMS na plataforma Experience, fale com o administrador do sistema antes de prosseguir.
- Autorização para fazer chamadas à API da plataforma Experience. Complete o tutorial [Autenticar e acessar as APIs](../../tutorials/authentication.md) da plataforma Adobe Experience para obter os seguintes valores para concluir este tutorial com êxito:
   - Autorização: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Client secret: `{CLIENT_SECRET}`
   - Certificado do cliente: `{PRIVATE_KEY}`
- Dados de amostra e arquivos de origem para a Receita [de Vendas de](../pre-built-recipes/retail-sales.md)Varejo. Baixe os ativos necessários para este e outros tutoriais da Data Science Workspace do repositório [público do](https://github.com/adobe/experience-platform-dsw-reference/)Adobe Git.
- [Python >= 2.7](https://www.python.org/downloads/) e as seguintes embalagens Python:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [ditador](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Um entendimento prático dos seguintes conceitos usados neste tutorial:
   - [Modelo de dados de experiência (XDM)](../../xdm/home.md)
   - [Noções básicas da composição do schema](../../xdm/schema/field-dictionary.md)

## Criar schema de vendas de varejo e conjunto de dados

O schema de vendas de varejo e os conjuntos de dados são criados automaticamente usando o script de inicialização fornecido. Siga as etapas abaixo para:

### Configurar arquivos

1. No pacote de recursos do tutorial da plataforma de experiência, navegue até o diretório `bootstrap`e abra `config.yaml` usando um editor de texto apropriado.
2. Na `Enterprise` seção, insira os seguintes valores:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Edite os valores encontrados na `Platform` seção, Exemplo mostrado abaixo:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` : O caminho base para chamadas de API. Não modifique esse valor.
   - `ims_token` : O seu `{ACCESS_TOKEN}` vai aqui.
   - `ingest_data` : Para a finalidade deste tutorial, defina esse valor como `"True"` a fim de criar os schemas de vendas de varejo e os conjuntos de dados. Um valor de apenas `"False"` criará os schemas.
   - `build_recipe_artifacts` : Para a finalidade deste tutorial, defina esse valor como `"False"` para impedir que o script gere um artefato de Receita.
   - `kernel_type` : O tipo de execução do artefato de Receita. Deixe esse valor como `Python` se `build_recipe_artifacts` estivesse definido como `"False"`, caso contrário, especifique o tipo de execução correto.

4. Na `Titles` seção, forneça as seguintes informações adequadamente para os dados de amostra de Vendas de varejo, salve e feche o arquivo depois que as edições estiverem em vigor. Exemplo mostrado abaixo:

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

1. Abra o aplicativo de terminal e navegue até o diretório de recursos do tutorial da plataforma de experiência.
2. Defina o `bootstrap` diretório como o caminho de trabalho atual e execute o script `bootstrap.py` python digitando o seguinte comando:

   ```bash
   python bootstrap.py
   ```

   > [!NOTE] O script pode levar vários minutos para ser concluído.

## Próximas etapas

Após a conclusão com êxito do script de inicialização, os schemas de entrada e saída e os conjuntos de dados do Retail Sales podem ser exibidos na Experience Platform. Consulte o tutorial de dados de schema de [pré-visualização](./preview-schema-data.md)para obter mais informações.

Você também assimilou com êxito dados de amostra de Vendas de varejo na Experience Platform usando o script de inicialização fornecido.

Para continuar trabalhando com os dados ingeridos:
- [Analise seus dados usando notebooks Jupyter](../jupyterlab/analyze-your-data.md)
   - Use notebooks Júpiter na Data Science Workspace para acessar, explorar, visualizar e entender seus dados.
- [Empacotar arquivos de origem em uma Receita](./package-source-files-recipe.md)
   - Siga este tutorial para saber como trazer seu próprio Modelo para a Data Science Workspace, empacotando arquivos de origem em um arquivo de Receita importante.