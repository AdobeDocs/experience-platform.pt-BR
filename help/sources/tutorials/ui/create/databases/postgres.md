---
keywords: Experience Platform;página inicial;tópicos populares;[!DNL PostgreSQL];[!DNL PostgreSQL];PostgreSQL
solution: Experience Platform
title: Criar uma conexão PostgreSQL Source na interface
type: Tutorial
description: Saiba como criar uma conexão de origem PostgreSQL usando a interface do usuário do Adobe Experience Platform.
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 2%

---

# Criar uma conexão de origem [!DNL PostgreSQL] na interface

Os conectores do Source no Adobe Experience Platform fornecem a capacidade de assimilar dados obtidos externamente de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL PostgreSQL] usando a interface do usuário [!DNL Experience Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL PostgreSQL] válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

Para acessar sua conta do [!DNL PostgreSQL] em [!DNL Experience Platform], você deve fornecer o seguinte valor:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão associada à sua conta [!DNL PostgreSQL]. O padrão da cadeia de conexão [!DNL PostgreSQL] é: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |

Para obter mais informações sobre a introdução, consulte este [[!DNL PostgreSQL] documento](https://www.postgresql.org/docs/9.2/app-psql.html).

#### Habilitar criptografia SSL para sua cadeia de conexão

Você pode habilitar a criptografia SSL para a cadeia de conexão [!DNL PostgreSQL] anexando sua cadeia de conexão com as seguintes propriedades:

| Propriedade | Descrição | Exemplo |
| --- | --- | --- |
| `EncryptionMethod` | Permite habilitar a criptografia SSL nos dados do [!DNL PostgreSQL]. | <uL><li>`EncryptionMethod=0`(Desabilitado)</li><li>`EncryptionMethod=1`(Habilitado)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Valida o certificado enviado pelo banco de dados [!DNL PostgreSQL] quando `EncryptionMethod` é aplicado. | <uL><li>`ValidationServerCertificate=0`(Desabilitado)</li><li>`ValidationServerCertificate=1`(Habilitado)</li></ul> |

Este é um exemplo de uma cadeia de conexão [!DNL PostgreSQL] anexada com criptografia SSL: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Conectar sua conta do [!DNL PostgreSQL]

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL PostgreSQL] ao [!DNL Experience Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Databases]**, selecione **[!UICONTROL PostgreSQL DB]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector [!DNL PostgreSQL].

![](../../../../images/tutorials/create/postgresql/catalog.png)

A página **[!UICONTROL Conectar-se a[!DNL PostgreSQL]]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e suas credenciais do [!DNL PostgreSQL]. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/postgresql/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL PostgreSQL] com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![](../../../../images/tutorials/create/postgresql/existing.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL PostgreSQL]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o  [!DNL Experience Platform]](../../dataflow/databases.md).
