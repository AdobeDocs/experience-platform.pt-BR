---
title: (Alfa) [!DNL LiveRamp SFTP] conexão
description: Saiba como usar o conector LiveRamp para públicos-alvo integrados do Adobe Real-time Customer Data Platform para o LiveRamp Connect.
hidefromtoc: true
hide: true
source-git-commit: 875610178449ddade78462dc74ea4e3dbadb2907
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 0%

---


# (Alfa) [!DNL LiveRamp - SFTP] conexão {#liveramp-destination}

Use a conexão LiveRamp para públicos integrados do Adobe Real-time Customer Data Platform para [!DNL LiveRamp Connect].

>[!IMPORTANT]
>
><p>Essa conexão de destino está atualmente em estágio alfa e só está disponível para uma seleção limitada de clientes. A funcionalidade e a documentação estão sujeitas a alterações.</p>
&gt;<p>A versão final dessa conexão de destino pode exigir a migração do cliente.</p>


## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar a variável [!DNL LiveRamp SFTP] destino, aqui está um exemplo de caso de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

Como profissional de marketing, desejo enviar públicos do Adobe Experience Platform para identidades integradas no [!DNL LiveRamp Connect] para que eu possa definir usuários como meta em [!DNL CTV] , usando a [!DNL Ramp ID] identificador.

## Pré-requisitos {#prerequisites}

O [!DNL LiveRamp - SFTP] a conexão exporta arquivos usando [SFTP do LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html) armazenamento.

Antes de enviar dados do Experience Platform para o [!DNL LiveRamp SFTP], você precisa de seu [!DNL LiveRamp] credenciais. Entre em contato com seu [!DNL LiveRamp] representante para obter suas credenciais, caso ainda não as tenha.

## Identidades suportadas {#supported-identities}

O LiveRamp SFTP oferece suporte à ativação de identidades, como identificadores baseados em PII, identificadores conhecidos e IDs personalizadas, descritas na seção oficial [Documentação do LiveRamp](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers).

No [etapa de mapeamento](#map) do workflow de ativação, você deve definir os target mappings como atributos personalizados.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados na [!DNL LiveRamp SFTP] destino. |
| Frequência de exportação | **[!UICONTROL Lote diário]** | À medida que os perfis são atualizados no Experience Platform com base na avaliação de segmentos, os perfis (identidades) são atualizados uma vez por dia depois da plataforma de destino. Leia mais sobre [destinos com base em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para autenticar para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Ligar ao destino]**.

**Autenticação SFTP com senha** {#sftp-password}

![Exemplo de captura de tela mostrando como autenticar no destino usando o SFTP com senha](../../assets/catalog/advertising/liveramp/liveramp-sftp-password.png)

* **[!UICONTROL Nome do usuário]**: O nome de usuário de seu [!DNL LiveRamp SFTP] local de armazenamento.
* **[!UICONTROL Senha]**: A senha de seu [!DNL LiveRamp SFTP] local de armazenamento.
* **[!UICONTROL Chave de criptografia PGP/GPG]**: Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Exiba um exemplo de uma chave de criptografia corretamente formatada na imagem abaixo. Se você fornecer uma chave de criptografia, também deverá fornecer um **[!UICONTROL ID de subchave de criptografia]** no [detalhes do destino](#destination-details) seção.

   ![Imagem que mostra um exemplo de uma chave PGP formatada corretamente na interface do usuário](../../assets/catalog/advertising/liveramp/pgp-key.png)

**SFTP com autenticação de chave SSH** {#sftp-ssh}

![Exemplo de captura de tela mostrando como autenticar para o destino usando a chave SSH](../../assets/catalog/advertising/liveramp/liveramp-sftp-ssh.png)

* **[!UICONTROL Nome do usuário]**: O nome de usuário de seu [!DNL LiveRamp SFTP] local de armazenamento.
* **[!UICONTROL Chave SSH]**: O privado [!DNL SSH] chave usada para fazer logon em sua [!DNL LiveRamp SFTP] local de armazenamento. A chave privada deve ser formatada como uma [!DNL Base64]-encoded string e não devem ser protegidas por senha.

   * Para conectar seu [!DNL SSH] para [!DNL LiveRamp SFTP] você deve enviar um tíquete por meio de [!DNL LiveRamp]Portal de suporte técnico do e forneça sua chave pública. Consulte mais informações na seção [Documentação do LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL Chave de criptografia PGP/GPG]**: Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Se você fornecer uma chave de criptografia, também deverá fornecer um **[!UICONTROL ID de subchave de criptografia]** no [detalhes do destino](#destination-details) seção. Exiba um exemplo de uma chave de criptografia corretamente formatada na imagem abaixo.

   ![Imagem que mostra um exemplo de uma chave PGP formatada corretamente na interface do usuário](../../assets/catalog/advertising/liveramp/pgp-key.png)

### Preencha os detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="ID de subchave de criptografia"
>abstract="O ID de subchave usado para criptografia, com base na chave de criptografia pública do LiveRamp. Esse campo será necessário se você tiver fornecido uma chave de criptografia na etapa de autenticação."
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="Saiba como obter a ID da subchave."

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Captura de tela da interface do usuário da plataforma que mostra como preencher os detalhes para o seu destino](../../assets/catalog/advertising/liveramp/liveramp-connection-details.png)

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Caminho da pasta]**: O caminho para o [!DNL LiveRamp] `uploads` subpasta que hospedará os arquivos exportados. O `uploads` é adicionado automaticamente ao caminho da pasta.
   * Por exemplo, se você deseja exportar seus arquivos para o `uploads/my_export_folder`, digite `my_export_folder` no **[!UICONTROL Caminho da pasta]** campo.
* **[!UICONTROL Formato de compactação]**: Selecione o tipo de compactação que o Experience Platform deve usar para os arquivos exportados. As opções disponíveis são **[!UICONTROL GZIP]** ou **[!UICONTROL Nenhum]**.
* **[!UICONTROL ID de subchave de criptografia]**: A subchave usada para criptografia, com base na variável [!DNL LiveRamp] chave de criptografia pública. Esse campo é necessário se você tiver fornecido uma chave de criptografia no [autenticação](#authenticate) etapa. Consulte a [!DNL LiveRamp] [documentação de criptografia](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) para saber como obter a ID da subchave.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, leia o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar dados do público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Programação {#scheduling}

No [!UICONTROL Agendamento] crie um agendamento de exportação para cada segmento, com as configurações mostradas abaixo.

>[!IMPORTANT]
>
>Todos os segmentos ativados para esse destino devem ser configurados exatamente com o mesmo agendamento, como mostrado abaixo.

* **[!UICONTROL Opções de exportação de arquivo]**: [!UICONTROL Exportar arquivos completos]. [Exportações de arquivo incremental](../../ui/activate-batch-profile-destinations.md#export-incremental-files) no momento, não são compatíveis com o [!DNL LiveRamp] destino.
* **[!UICONTROL Frequência]**: [!UICONTROL Diariamente]
* Defina o tempo de exportação como **[!UICONTROL Após a avaliação do segmento]**. Exportações e [exportações de arquivos por demanda](../../ui/export-file-now.md) no momento, não são compatíveis com o [!DNL LiveRamp] destino.
* **[!UICONTROL Data]**: Selecione as horas de início e término da exportação conforme desejar.

![Captura de tela da interface do usuário da plataforma que mostra a etapa de agendamento de segmento.](../../assets/catalog/advertising/liveramp/liveramp-segment-scheduling.png)

No momento, o nome de arquivo exportado não é configurável pelo usuário. Todos os arquivos exportados para a [!DNL LiveRamp SFTP] os destinos são nomeados automaticamente com base no seguinte template:

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Captura de tela da interface do usuário da plataforma que mostra o modelo de nome de arquivo exportado.](../../assets/catalog/advertising/liveramp/liveramp-file-name.png)

Por exemplo, o nome de um arquivo exportado para uma organização chamada [!DNL Luma] pode ser semelhante a:

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### Mapear atributos e identidades {#map}

No **[!UICONTROL Mapeamento]** , é possível selecionar quais atributos e identidades deseja exportar para seus perfis.

>[!IMPORTANT]
>
>Este destino suporta a ativação de um namespace de identidade de origem por fluxo de ativação. Se precisar exportar vários namespaces de identidade, como `Email` e `Phone`, você deve [criar um fluxo de ativação separado](../../ui/activate-batch-profile-destinations.md) para cada identidade.

No **[!UICONTROL Mapeamento]** , a **[!UICONTROL Campo de destino]** mapping define o nome do cabeçalho da coluna no arquivo CSV exportado. Você pode alterar os cabeçalhos da coluna CSV no arquivo exportado para qualquer nome amigável que desejar, fornecendo um nome personalizado para a variável **[!UICONTROL Campo de destino]**.

1. No **[!UICONTROL Mapeamento]** etapa , selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.

   ![Captura de tela da interface do usuário do Experience Platform mostrando a tela Mapeamento.](../../assets/catalog/advertising/liveramp/liveramp-add-new-mapping.png)

2. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar atributos]** e selecione o atributo XDM que deseja mapear ou escolha a variável **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade para mapear para o seu destino.

   ![Captura de tela da interface do usuário do Experience Platform mostrando a tela Mapeamento de origem.](../../assets/catalog/advertising/liveramp/liveramp-source-mapping.png)

3. No **[!UICONTROL Selecionar campo de destino]** , insira o nome do atributo para o qual deseja mapear o campo de origem selecionado. O nome do atributo definido aqui refletirá no arquivo CSV exportado como um cabeçalho de coluna.

   ![Captura de tela da interface do usuário do Experience Platform mostrando a tela de Mapeamento do destino.](../../assets/catalog/advertising/liveramp/liveramp-target-mapping.png)

   Você também pode inserir o nome do atributo digitando-o diretamente no **[!UICONTROL Campo de destino]**.

   ![Captura de tela da interface do usuário do Experience Platform mostrando a tela de Mapeamento do destino.](../../assets/catalog/advertising/liveramp/liveramp-target-field.png)

Depois de adicionar todos os mapeamentos desejados, selecione **[!UICONTROL Próximo]** e finalize o workflow de ativação.

## Dados exportados / Validar exportação de dados {#exported-data}

Seus dados são exportados para o [!DNL LiveRamp SFTP] local de armazenamento que você configurou como arquivos CSV.

Ao exportar arquivos para o [!DNL LiveRamp SFTP] destino, a Platform gera um arquivo CSV para cada [ID da política de mesclagem](../../../profile/merge-policies/overview.md).

Por exemplo, considere os seguintes segmentos:

* Segmento A (Política de mesclagem 1)
* Segmento B (Política de mesclagem 2)
* Segmento C (Política de mesclagem 1)
* Segmento D (Política de mesclagem 1)

A plataforma exportará dois arquivos CSV para [!DNL LiveRamp SFTP]:

* Um arquivo CSV contendo segmentos A, C e D;
* Um arquivo CSV contendo o segmento B.

Os arquivos CSV exportados contêm perfis com os atributos selecionados e o status do segmento correspondente, em colunas separadas, com o nome do atributo e as IDs do segmento como cabeçalhos de coluna.

Os perfis incluídos nos arquivos exportados podem corresponder a um dos seguintes status de qualificação de segmento:

* `Active`: O perfil está qualificado para o segmento no momento.
* `Expired`: O perfil não está mais qualificado para o segmento, mas se qualificou no passado.
* `""`(string vazia): O perfil nunca foi qualificado para o segmento.


Por exemplo, um arquivo CSV exportado com um `email` e 3 segmentos podem ter esta aparência:

```csv
email,aa2e3d98-974b-4f8b-9507-59f65b6442df,45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

Como a Platform gera um arquivo CSV para cada [ID da política de mesclagem](../../../profile/merge-policies/overview.md), também gera uma execução de fluxo de dados separada para cada ID de política de mesclagem.

Isso significa que a variável **[!UICONTROL Identidades ativadas]** e **[!UICONTROL Perfis recebidos]** nas [execuções do fluxo de dados](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) são agregadas para cada grupo de segmentos que usam a mesma política de mesclagem, em vez de serem exibidas para cada segmento.

Como consequência de execuções de fluxo de dados serem geradas para um grupo de segmentos que usam a mesma política de mesclagem, os nomes de segmentos não são exibidos na variável [painel de monitoramento](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![Capturas de tela da interface do usuário do Experience Platform mostrando a métrica de identidades ativadas.](../../assets/catalog/advertising/liveramp/liveramp-metrics.png)

## Fazer upload de dados exportados para o LiveRamp {#upload-to-liveramp}

Após seus dados terem sido exportados com sucesso para a [!DNL LiveRamp - SFTP] você deve fazer upload dos dados para o [!DNL LiveRamp] plataforma.

Consulte a **Próximas etapas** na seção [obter seus dados no LiveRamp](https://docs.liveramp.com/connect/en/getting-your-data-into-liveramp.html) documentação para obter mais instruções.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, leia a [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

Para obter mais detalhes sobre como configurar o armazenamento SFTP do LiveRamp, consulte o [documentação oficial](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
