---
keywords: Experience Platform; home; tópicos populares;[!DNL PostgreSQL];[!DNL PostgreSQL];PostgreSQL
solution: Experience Platform
title: Criar uma conexão de origem PostgreSQL na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem PostgreSQL usando a interface do usuário do Adobe Experience Platform.
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: eea815f72c1e807f4ad6ca6273ba18a9da09ac6e
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 2%

---

# Crie um [!DNL PostgreSQL] conexão de origem na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um [!DNL PostgreSQL] conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL PostgreSQL] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/databases.md).

### Obter credenciais necessárias

Para acessar o [!DNL PostgreSQL] conta em [!DNL Platform], você deve fornecer o seguinte valor:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A string de conexão associada à [!DNL PostgreSQL] conta. O [!DNL PostgreSQL] o padrão da string de conexão é: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |

Para obter mais informações sobre a introdução, consulte esta seção [[!DNL PostgreSQL] documento](https://www.postgresql.org/docs/9.2/app-psql.html).

#### Habilitar criptografia SSL para a cadeia de conexão

Você pode ativar a criptografia SSL para o [!DNL PostgreSQL] string de conexão anexando sua string de conexão com as seguintes propriedades:

| Propriedade | Descrição | Exemplo |
| --- | --- | --- |
| `EncryptionMethod` | Permite habilitar a criptografia SSL em seu [!DNL PostgreSQL] dados. | <uL><li>`EncryptionMethod=0`(Desativado)</li><li>`EncryptionMethod=1`(Ativado)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Valida o certificado enviado pelo seu [!DNL PostgreSQL] banco de dados quando `EncryptionMethod` é aplicada. | <uL><li>`ValidationServerCertificate=0`(Desativado)</li><li>`ValidationServerCertificate=1`(Ativado)</li></ul> |

Este é um exemplo de um [!DNL PostgreSQL] cadeia de conexão anexada com criptografia SSL: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Conecte seu [!DNL PostgreSQL] account

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL PostgreSQL] para [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Bancos de dados]** categoria , selecione **[!UICONTROL Banco de Dados PostgreSQL]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL PostgreSQL] conector.

![](../../../../images/tutorials/create/postgresql/catalog.png)

O **[!UICONTROL Conectar-se a[!DNL PostgreSQL]]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e [!DNL PostgreSQL] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/postgresql/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL PostgreSQL] conta com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![](../../../../images/tutorials/create/postgresql/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL PostgreSQL] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados para [!DNL Platform]](../../dataflow/databases.md).
