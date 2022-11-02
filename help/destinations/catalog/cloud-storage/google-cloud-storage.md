---
title: (Beta) Conexão de armazenamento em nuvem Google
description: Saiba como se conectar ao Google Cloud Storage e ativar segmentos ou exportar conjuntos de dados.
source-git-commit: 97a39e12d916e4fbd048c0fb9ddfa9bdfa10d438
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 0%

---

# (Beta) [!DNL Google Cloud Storage] conexão

>[!IMPORTANT]
>
>No momento, esse destino está na versão Beta e só está disponível para um número limitado de clientes. Para solicitar acesso à [!DNL Google Cloud Storage] entre em contato com o representante do Adobe e forneça [!DNL Organization ID].

## Visão geral {#overview}

Criar uma conexão de saída ao vivo para [!DNL Google Cloud Storage] para exportar periodicamente arquivos de dados do Adobe Experience Platform para seus próprios buckets.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema aplicáveis, conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Em lote]** | Destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Configuração de pré-requisito para conectar [!DNL Google Cloud Storage] account {#prerequisites}

Para conectar a Platform ao [!DNL Google Cloud Storage], você deve primeiro habilitar a interoperabilidade para [!DNL Google Cloud Storage] conta. Para acessar a configuração de interoperabilidade, abra [!DNL Google Cloud Platform] e selecione **[!UICONTROL Configurações]** do **[!UICONTROL Armazenamento na nuvem]** no painel de navegação.

![Destaque o painel Google Cloud Platform com Configurações e Armazenamento na nuvem.](/help/sources/images/tutorials/create/google-cloud-storage/nav.png)

O **[!UICONTROL Configurações]** será exibida. Aqui, você pode ver informações sobre seu [!DNL Google] ID do projeto e detalhes sobre seu [!DNL Google Cloud Storage] conta. Para acessar as configurações de interoperabilidade, selecione **[!UICONTROL Interoperabilidade]** no cabeçalho superior.

![A guia Interoperability destacada no painel da Google Cloud Platform.](/help/sources/images/tutorials/create/google-cloud-storage/project-access.png)

O **[!UICONTROL Interoperabilidade]** contém informações sobre autenticação, chaves de acesso e o projeto padrão associado à sua conta de serviço. Para gerar uma nova ID de chave de acesso e uma chave de acesso secreta para sua conta de serviço, selecione **[!UICONTROL Criar uma chave para uma conta de serviço]**.

![A opção Create a key for a service account control realçada no painel da Google Cloud Platform.](/help/sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Você pode usar a ID da chave de acesso recém-gerada e a chave de acesso secreta para conectar [!DNL Google Cloud Storage] para a Platform.

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](/help/destinations/ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para autenticar para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Ligar ao destino]**.

* **[!UICONTROL ID da chave de acesso]**: Uma sequência de 61 caracteres alfanuméricos usada para autenticar o [!DNL Google Cloud Storage] para a Platform. Para obter informações sobre como obter esse valor, leia a [pré-requisitos](#prerequisites) acima.
* **[!UICONTROL Chave de acesso secreta]**: Uma string codificada em base64, de 40 caracteres, usada para autenticar seu [!DNL Google Cloud Storage] para a Platform. Para obter informações sobre como obter esse valor, leia a [pré-requisitos](#prerequisites) acima.
* **[!UICONTROL Chave de criptografia]**: Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Sua chave pública deve ser escrita como uma [!DNL Base64-encoded] string. Visualize um exemplo de uma chave corretamente formatada e codificada em base64 no link da documentação abaixo. A parte central é encurtada por brevidade.

   ![Imagem mostrando um exemplo de uma chave PGP corretamente formatada e criptografada em base64 na interface do usuário](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Para obter mais informações sobre esses valores, leia a [Chaves HMAC do Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guia. Para obter etapas sobre como gerar sua própria ID de chave de acesso e chave de acesso secreta, consulte [[!DNL Google Cloud Storage] visão geral da fonte](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Nome do bucket]**: Insira o nome do [!DNL Google Cloud Storage] bucket a ser usado por este destino.
* **[!UICONTROL Caminho da pasta]**: Insira o caminho para a pasta de destino que hospedará os arquivos exportados.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Programação

No **[!UICONTROL Agendamento]** , você pode [configurar o cronograma de exportação](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) para seu [!DNL Google Cloud Storage] e você também pode [configurar o nome dos arquivos exportados](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mapear atributos e identidades {#map}

No **[!UICONTROL Mapeamento]** , é possível selecionar quais campos de atributo e identidade serão exportados para seus perfis. Você também pode optar por alterar os cabeçalhos no arquivo exportado para qualquer nome amigável que desejar. Para obter mais informações, visualize o [etapa de mapeamento](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) no tutorial ativar interface do usuário de destinos em lote.

## (Beta) Exportar conjuntos de dados {#export-datasets}

Esse destino é compatível com exportações de conjunto de dados. Para obter informações completas sobre como configurar exportações de conjunto de dados, leia a [tutorial exportar conjuntos de dados](/help/destinations/ui/export-datasets.md).

## Validar exportação de dados bem-sucedida {#exported-data}

Para verificar se os dados foram exportados com êxito, verifique seu [!DNL Google Cloud Storage] e verifique se os arquivos exportados contêm as populações de perfis esperadas.
