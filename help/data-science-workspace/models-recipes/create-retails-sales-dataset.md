---
keywords: Experience Platform;receita de vendas de varejo;Espaço de trabalho de ciência de dados;tópicos populares;receitas
solution: Experience Platform
title: Criar o esquema e o conjunto de dados de vendas de varejo
type: Tutorial
description: Este tutorial fornece os pré-requisitos e os ativos necessários para todos os outros tutoriais do Adobe Experience Platform Data Science Workspace. Após a conclusão, o esquema de Vendas de varejo e os conjuntos de dados estarão disponíveis para você e os membros de sua organização no Experience Platform.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---


# Criar o esquema de vendas de varejo e o conjunto de dados

Este tutorial fornece os pré-requisitos e os ativos necessários para todos os outros [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] tutoriais. Após a conclusão, o esquema de Vendas de varejo e os conjuntos de dados estarão disponíveis para você e os membros de sua organização em [!DNL Experience Platform].

## Introdução

Antes de iniciar este tutorial, você deve ter os seguintes pré-requisitos:
- Acesso a [!DNL Adobe Experience Platform]. Se você não tiver acesso a uma organização no [!DNL Experience Platform], entre em contato com o administrador do sistema antes de continuar.
- Autorização para efetuar [!DNL Experience Platform] Chamadas de API. Conclua o [Autenticar e acessar APIs do Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) tutorial para obter os seguintes valores para concluir com sucesso este tutorial:
   - Autorização: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - Segredo do cliente: `{CLIENT_SECRET}`
   - Certificado do cliente: `{PRIVATE_KEY}`
- Dados de amostra e arquivos de origem para o [Receita de vendas de varejo](../pre-built-recipes/retail-sales.md). Baixar os ativos necessários para esta e outras [!DNL Data Science Workspace] tutoriais da [Repositório Git público do Adobe](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2,7](https://www.python.org/downloads/) e o seguinte [!DNL Python] pacotes:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [ditor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Uma compreensão funcional dos seguintes conceitos usados neste tutorial:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Noções básicas da composição do esquema](../../xdm/schema/field-dictionary.md)

## Criar conjunto de dados e esquema de Vendas de Varejo

O esquema de vendas de varejo e os conjuntos de dados são criados automaticamente usando o script de inicialização fornecido. Siga as etapas abaixo para:

### Configurar arquivos

1. Dentro do [!DNL Experience Platform] pacote de recursos de tutorial, navegue até o diretório `bootstrap`e abrir `config.yaml` usando um editor de texto apropriado.
2. No `Enterprise` insira os seguintes valores:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Edite os valores encontrados em `Platform` , Exemplo mostrado abaixo:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: o caminho base para chamadas de API. Não modifique esse valor.
   - `ims_token`: Seu `{ACCESS_TOKEN}` aqui.
   - `ingest_data`: Para a finalidade deste tutorial, defina este valor como `"True"` para criar os esquemas e conjuntos de dados de Vendas de varejo. Um valor de `"False"` O só criará os esquemas.
   - `build_recipe_artifacts`: Para a finalidade deste tutorial, defina este valor como `"False"` para impedir que o script gere um artefato de fórmula.
   - `kernel_type`: o tipo de execução do artefato Receita. Deixe este valor como `Python` se `build_recipe_artifacts` está definido como `"False"`, caso contrário, especifique o tipo de execução correto.

4. No `Titles` forneça as seguintes informações apropriadamente para os dados de amostra de Vendas de varejo, salve e feche o arquivo após as edições estarem em vigor. Exemplo mostrado abaixo:

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

1. Abra o aplicativo de terminal e navegue até o [!DNL Experience Platform] diretório de recursos do tutorial.
2. Defina o `bootstrap` como o caminho de trabalho atual e execute o `bootstrap.py` [!DNL Python] insira o seguinte comando:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >O script pode levar vários minutos para ser concluído.

## Próximas etapas

Após a conclusão bem-sucedida do script de inicialização, os esquemas de entrada e saída de Vendas de Varejo e os conjuntos de dados podem ser exibidos em [!DNL Experience Platform]. Consulte a [visualizar tutorial de dados do esquema](./preview-schema-data.md)
para obter mais informações.

Você também assimilou com êxito dados de amostra de Vendas de varejo em [!DNL Experience Platform] usando o script de inicialização fornecido.

Para continuar trabalhando com os dados assimilados:
- [Analise seus dados usando o Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Use o Jupyter Notebooks no Data Science Workspace para acessar, explorar, visualizar e entender seus dados.
- [Compactar arquivos de origem em uma fórmula](./package-source-files-recipe.md)
   - Siga este tutorial para saber como trazer seu próprio modelo para o [!DNL Data Science Workspace] empacotando arquivos de origem em um arquivo de fórmula importável.
