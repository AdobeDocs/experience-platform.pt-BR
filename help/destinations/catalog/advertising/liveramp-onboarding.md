---
title: LiveRamp - Conexão de integração
description: Saiba como usar o conector do LiveRamp para integrar públicos do Adobe Real-time Customer Data Platform ao LiveRamp Connect.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: 5da570aaa0c6a8972d1c3d2c5b3bec9e733c1851
workflow-type: tm+mt
source-wordcount: '1830'
ht-degree: 3%

---

# Conexão com o [!DNL LiveRamp - Onboarding] {#liveramp-onboarding}

Use o [!DNL LiveRamp - Onboarding] conexão com públicos integrados do Adobe Real-time Customer Data Platform para [!DNL LiveRamp Connect].

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL LiveRamp - Onboarding] destino, este é um exemplo de caso de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

Como profissional de marketing, desejo enviar públicos-alvo do Adobe Experience Platform para integrar identidades no [!DNL LiveRamp Connect] para que eu possa direcionar os usuários em dispositivos móveis, Web aberta, redes sociais e [!DNL CTV] plataformas, usando o [!DNL Ramp ID] identificador.

## Pré-requisitos {#prerequisites}

A variável [!DNL LiveRamp - Onboarding] a conexão exporta arquivos usando [SFTP do LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html) armazenamento.

Antes de enviar dados do Experience Platform para [!DNL LiveRamp - Onboarding], você precisa do seu [!DNL LiveRamp] credenciais. Entre em contato com [!DNL LiveRamp] representante para obter suas credenciais, se você ainda não as tiver.

## Identidades suportadas {#supported-identities}

[!DNL LiveRamp - Onboarding] O suporta a ativação de identidades, como identificadores baseados em PII, identificadores conhecidos e IDs personalizadas, descritos no documento [Documentação do LiveRamp](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers).

No [etapa de mapeamento](#map) do workflow de ativação, você deve definir os target mappings como atributos personalizados.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve todos os públicos-alvo que você pode exportar para esse destino.

Esse destino oferece suporte à ativação de públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md).

Além disso, esse destino também suporta a ativação dos públicos-alvo adicionais descritos na tabela abaixo.

| Tipo de público | Descrição |
---------|----------|
| Uploads personalizados | Públicos-alvo [importado](../../../segmentation/ui/overview.md#importing-an-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público-alvo com os identificadores (nome, número de telefone ou outros) usados no [!DNL LiveRamp - Onboarding] destino. |
| Frequência de exportação | **[!UICONTROL Lote diário]** | Como os perfis são atualizados em Experience Platform com base na avaliação do público-alvo, os perfis (identidades) são atualizados uma vez por dia downstream para a plataforma de destino. Leia mais sobre [destinos baseados em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

**Autenticação SFTP com senha** {#sftp-password}

![Captura de tela de exemplo mostrando como autenticar no destino usando SFTP com senha](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-password.png)

* **[!UICONTROL Nome de usuário]**: O nome de usuário do [!DNL LiveRamp - Onboarding] local de armazenamento.
* **[!UICONTROL Senha]**: A senha do [!DNL LiveRamp - Onboarding] local de armazenamento.
* **[!UICONTROL Chave de criptografia PGP/GPG]**: como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Veja um exemplo de uma chave de criptografia formatada corretamente na imagem abaixo. Se você fornecer uma chave de criptografia, deverá também fornecer uma **[!UICONTROL ID da subchave de criptografia]** no [detalhes do destino](#destination-details) seção.

  ![Imagem que mostra um exemplo de uma chave PGP formatada corretamente na interface](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)

**SFTP com autenticação de chave SSH** {#sftp-ssh}

![Captura de tela de exemplo mostrando como autenticar no destino usando a chave SSH](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-ssh.png)

* **[!UICONTROL Nome de usuário]**: O nome de usuário do [!DNL LiveRamp - Onboarding] local de armazenamento.
* **[!UICONTROL Chave SSH]**: O privado [!DNL SSH] chave usada para fazer logon no seu [!DNL LiveRamp - Onboarding] local de armazenamento. A chave privada deve ser formatada como um [!DNL Base64]-encoded e não deve ser protegido por senha.

   * Para conectar seu [!DNL SSH] chave para o [!DNL LiveRamp - Onboarding] , você deve enviar um tíquete por meio do [!DNL LiveRamp]do portal de suporte técnico da e forneça sua chave pública. Veja mais informações na seção [Documentação do LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL Chave de criptografia PGP/GPG]**: como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Se você fornecer uma chave de criptografia, deverá também fornecer uma **[!UICONTROL ID da subchave de criptografia]** no [detalhes do destino](#destination-details) seção. Veja um exemplo de uma chave de criptografia formatada corretamente na imagem abaixo.

  ![Imagem que mostra um exemplo de uma chave PGP formatada corretamente na interface](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="ID da subchave de criptografia"
>abstract="A ID da subchave usada para criptografia, com base na chave de criptografia pública do LiveRamp. Esse campo será necessário se você tiver fornecido uma chave de criptografia na etapa de autenticação."
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="Saiba como obter a ID da subchave"

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Captura de tela da interface do usuário da plataforma mostrando como preencher detalhes para o seu destino](../../assets/catalog/advertising/liveramp-onboarding/liveramp-connection-details.png)

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL Caminho da pasta]**: O caminho para o [!DNL LiveRamp] `uploads` que hospedará os arquivos exportados. A variável `uploads` O prefixo é adicionado automaticamente ao caminho da pasta. [!DNL LiveRamp] A recomenda a criação de uma subpasta dedicada para deliveries do Adobe Real-Time CDP para manter os arquivos separados de quaisquer outros feeds existentes e garantir que toda a automação seja executada sem problemas.
   * Por exemplo, se você deseja exportar seus arquivos para `uploads/my_export_folder`, digite `my_export_folder` no **[!UICONTROL Caminho da pasta]** campo.
* **[!UICONTROL Formato de compactação]**: selecione o tipo de compactação que o Experience Platform deve usar para os arquivos exportados. As opções disponíveis são **[!UICONTROL GZIP]** ou **[!UICONTROL Nenhum]**.
* **[!UICONTROL ID da subchave de criptografia]**: A subchave usada para criptografia, com base no [!DNL LiveRamp] chave de criptografia pública. Este campo será necessário se você tiver fornecido uma chave de criptografia na [autenticação](#authenticate) etapa. Consulte a [!DNL LiveRamp] [documentação de criptografia](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) para saber como obter a ID da subchave.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, leia o manual no [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar dados do público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Programação {#scheduling}

No [!UICONTROL Agendamento] crie um agendamento de exportação para cada público-alvo, com as configurações mostradas abaixo.

* **[!UICONTROL Opções de exportação de arquivo]**: [!UICONTROL Exportar arquivos completos]. [Exportações incrementais de arquivos](../../ui/activate-batch-profile-destinations.md#export-incremental-files) no momento, não são compatíveis com o [!DNL LiveRamp] destino.
* **[!UICONTROL Frequência]**: [!UICONTROL Diariamente]
* **[!UICONTROL Data]**: selecione as horas de início e término da exportação conforme desejado.

![Captura de tela da interface do usuário da Platform mostrando a etapa de agendamento de público-alvo.](../../assets/catalog/advertising/liveramp-onboarding/liveramp_scheduling_screenshot.png)

O nome do arquivo exportado não pode ser configurado pelo usuário no momento. Todos os arquivos exportados para o [!DNL LiveRamp - Onboarding] Os destinos são nomeados automaticamente com base no seguinte modelo:

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Captura de tela da interface do usuário da plataforma mostrando o modelo de nome de arquivo exportado.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-file-name.png)

Por exemplo, o nome de um arquivo exportado para uma organização chamada [!DNL Luma] pode ser semelhante a:

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### Mapear atributos e identidades {#map}

No **[!UICONTROL Mapeamento]** etapa, você pode selecionar quais atributos e identidades deseja exportar para seus perfis.

>[!IMPORTANT]
>
>Este destino dá suporte à ativação de um namespace de identidade de origem por fluxo de ativação. Se precisar exportar vários namespaces de identidade, como `Email` e `Phone`, você deve [criar um fluxo de ativação separado](../../ui/activate-batch-profile-destinations.md) para cada identidade.

No **[!UICONTROL Mapeamento]** etapa, a variável **[!UICONTROL Campo de destino]** O mapeamento define o nome do cabeçalho da coluna no arquivo CSV exportado. Você pode alterar os cabeçalhos de coluna CSV no arquivo exportado para qualquer nome amigável que desejar, fornecendo um nome personalizado para a **[!UICONTROL Campo de destino]**.

>[!IMPORTANT]
>
>Para quaisquer alterações feitas nos campos de público-alvo após a entrega inicial do arquivo para [!DNL LiveRamp], notifique seu [!DNL LiveRamp] equipe de conta ou [enviar um tíquete para o suporte do LiveRamp](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#creating-a-support-case) para garantir que as alterações sejam refletidas no processo de automação.

1. No **[!UICONTROL Mapeamento]** etapa, selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.

   ![Captura de tela da interface do Experience Platform mostrando a tela Mapeamento.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-add-new-mapping.png)

2. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar atributos]** categoria e selecione o atributo XDM que deseja mapear ou escolha o **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade para mapear ao seu destino.

   ![Captura de tela da interface do Experience Platform mostrando a tela Mapeamento de origem.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-source-mapping.png)

3. No **[!UICONTROL Selecionar campo de destino]** , informe o nome do atributo para o qual você deseja mapear o campo de origem selecionado. O nome do atributo definido aqui refletirá no arquivo CSV exportado como um cabeçalho de coluna.

   ![Captura de tela da interface do Experience Platform mostrando a tela Target Mapping.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-mapping.png)

   Você também pode inserir o nome do atributo digitando-o diretamente na **[!UICONTROL Campo de destino]**.

   ![Captura de tela da interface do Experience Platform mostrando a tela Target Mapping.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-field.png)

Depois de adicionar todos os mapeamentos desejados, selecione **[!UICONTROL Próxima]** e conclua o fluxo de trabalho de ativação.

## Dados exportados / Validar exportação de dados {#exported-data}

Seus dados são exportados para o [!DNL LiveRamp - Onboarding] local de armazenamento que você configurou, como arquivos CSV.

Ao exportar arquivos para o [!DNL LiveRamp - Onboarding] destino, a Platform gera um arquivo CSV para cada [ID da política de mesclagem](../../../profile/merge-policies/overview.md).

Por exemplo, vamos considerar os seguintes públicos-alvo:

* Público-alvo A (política de mesclagem 1)
* Público-alvo B (política de mesclagem 2)
* Público-alvo C (política de mesclagem 1)
* Audience D (política de mesclagem 1)

A Platform exportará dois arquivos CSV para [!DNL LiveRamp - Onboarding]:

* Um arquivo CSV contendo os públicos-alvo A, C e D;
* Um arquivo CSV contendo o público-alvo B.

Os arquivos CSV exportados contêm perfis com os atributos selecionados e o status de público-alvo correspondente, em colunas separadas, com o nome do atributo e `audience_namespace:audience_ID` pares como cabeçalhos de coluna, conforme mostrado no exemplo abaixo:

`ATTRIBUTE_NAME, AUDIENCE_NAMESPACE_1:AUDIENCE_ID_1, AUDIENCE_NAMESPACE_2:AUDIENCE_ID_2,..., AUDIENCE_NAMESPACE_X:AUDIENCE_ID_X`

Os perfis incluídos nos arquivos exportados podem corresponder a um dos seguintes status de qualificação de público-alvo:

* `Active`: o perfil está qualificado para o público-alvo no momento.
* `Expired`: o perfil não está mais qualificado para o público-alvo, mas se qualificou no passado.
* `""`(sequência de caracteres vazia): o perfil nunca se qualificou para o público-alvo.

Por exemplo, um arquivo CSV exportado com um `email` atributo, dois públicos-alvo originados do Experience Platform [Serviço de segmentação](../../../segmentation/home.md), e um [importado](../../../segmentation/ui/overview.md#importing-an-audience) público externo, pode ter esta aparência:

```csv
email,ups:aa2e3d98-974b-4f8b-9507-59f65b6442df,ups:45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,CustomerAudienceUpload:7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

No exemplo acima, a variável `ups:aa2e3d98-974b-4f8b-9507-59f65b6442df` e `ups:45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f` descrevem os públicos-alvo provenientes do Serviço de segmentação, enquanto `CustomerAudienceUpload:7729e537-4e42-418e-be3b-dce5e47aaa1e` descreve um público-alvo importado para o Platform as a [upload personalizado](../../../segmentation/ui/overview.md#importing-an-audience).

Como a Platform gera um arquivo CSV para cada [ID da política de mesclagem](../../../profile/merge-policies/overview.md), ele também gera um fluxo de dados separado para cada ID de política de mesclagem.

Isto significa que a **[!UICONTROL Identidades ativadas]** e **[!UICONTROL Perfis recebidos]** métricas no [execuções de fluxo de dados](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) As páginas são agregadas para cada grupo de públicos-alvo que usam a mesma política de mesclagem, em vez de serem exibidas para cada público-alvo.

Como consequência da geração de execuções de fluxo de dados para um grupo de públicos-alvo que usam a mesma política de mesclagem, os nomes dos públicos-alvo não são exibidos no [painel de monitoramento](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![Captura de tela da interface do Experience Platform mostrando a métrica de identidades ativadas.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-metrics.png)

## Carregar dados exportados para o LiveRamp {#upload-to-liveramp}

Após os dados serem exportados com êxito para o [!DNL LiveRamp - Onboarding] armazenamento, você deve fazer upload dos dados para o [!DNL LiveRamp] plataforma.

Para obter mais informações sobre como fazer upload dos arquivos da [!DNL LiveRamp - Onboarding] armazenamento para um [!DNL LiveRamp] público-alvo, consulte a seguinte documentação: [Considerações ao fazer upload do primeiro arquivo para um público-alvo](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

Para obter mais detalhes sobre como configurar [!DNL LiveRamp - Onboarding] armazenamento, consulte a seção [documentação oficial](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
