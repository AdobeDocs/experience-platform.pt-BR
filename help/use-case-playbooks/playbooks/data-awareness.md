---
solution: Experience Platform
title: Visão geral do reconhecimento de dados nos manuais de caso de uso
description: Saiba como acelerar o tempo de implantação copiando os ativos gerados na sandbox inspiradora final para outras sandboxes.
badgeBeta: label="Beta" type="Informative"
source-git-commit: 5b6b69d69a088f58d10f41debde859294285360d
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---


# Visão geral do reconhecimento de dados nos manuais de caso de uso

Os manuais de casos de uso são modelos de marketing projetados para gerar ativos, como públicos, esquemas ou jornadas, para casos de uso de marketing comum. No Adobe Experience Platform, esses modelos fazem referência a vários campos padrão e grupos de campos. No entanto, em certos casos, você já pode ter configurado seus próprios esquemas, campos e grupos de campos. Isso pode tornar alguns dos ativos gerados pelos modelos de caso de uso, como jornadas, incompatíveis com seus dados. Leia este tutorial para entender como usar a funcionalidade de reconhecimento de dados para alinhar e complementar melhor os ativos gerados com seus ativos existentes.

## Pré-requisitos {#prerequisites}

Antes de ler este tutorial, navegue pelo [modelos de manual de caso de uso disponíveis](/help/use-case-playbooks/playbooks/discover.md#search-and-filter) e [criar uma instância](/help/use-case-playbooks/playbooks/create-share-reuse.md) de um manual preferencial.

A criação de uma instância gera um conjunto de ativos, como jornadas, segmentos, esquemas e mensagens na sandbox inspiradora. Leia para saber como copiar esses ativos em outras sandboxes.

### Criar e publicar um pacote {#create-publish-package}

1. Para importar objetos da sandbox inspiradora para outra sandbox, navegue até uma instância desejada de um manual de casos de uso e selecione **[!UICONTROL Publicar em uma sandbox diferente]** para exportar os artefatos como um pacote.

   ![GIF mostrando as diferentes instâncias de caso de uso](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. Depois de selecionar a variável **[!UICONTROL Publicar em uma sandbox diferente]** será exibida uma modal. Preencha o nome e a descrição opcional e selecione **[!UICONTROL Criar]**. Esta etapa agrupa os ativos gerados em um pacote que pode ser importado para uma sandbox diferente.

   ![Um modal para criar um pacote](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. Navegue até a **Sandboxes** no lado esquerdo da navegação e selecione a guia **Pacotes** , localize o pacote e publique-o. Para publicar um pacote que esteja em estado de rascunho, siga as etapas da seção [ferramentas de sandbox](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish) documento.

   ![Pacote em estado de rascunho ou não publicado](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![Publicação do pacote](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. Depois que a publicação for bem-sucedida, na página de navegação de pacotes, você deverá ver um **+** botão ativado ao lado do nome.

   ![Guia Pacotes na página Sandboxes](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > O pacote não pode ser importado enquanto ainda estiver no modo de rascunho. Portanto, abra a página de detalhes do pacote e publique o pacote.

5. Selecione o **+** controle para iniciar o fluxo de trabalho para importar os ativos gerados pelo manual do caso de uso para a **[!UICONTROL Sandbox do Target]**. Selecione uma sandbox de destino e confirme o nome do pacote que deseja importar usando a lista suspensa. Adicione os detalhes do job, como nome e descrição do job, antes de prosseguir para a próxima etapa.

   ![Inicie o fluxo de trabalho de importação, selecione target, confirme o pacote e adicione detalhes do trabalho.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

   >[!NOTE]
   >
   > Você pode importar pacotes somente para outras sandboxes de desenvolvimento. A sandbox de produção está desativada para essas importações.

6. No **[!UICONTROL Exibir dependências]** etapa, você pode mapear esquemas e copiar outros ativos da sandbox inspiradora para a sandbox de destino. A variável **[!UICONTROL Concluir]** estará desativado até que você mapeie cada schema.

   ![Mapeie esquemas na etapa &quot;Exibir dependências&quot;, ativando o botão Concluir.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### Mapear esquemas {#map-schemas}

1. Mapeie o primeiro esquema. A caixa de diálogo Mapeamento de esquema exibe uma lista suspensa para selecionar o esquema de destino. Se o esquema de origem for um esquema de perfil, então não haverá outras opções de esquema de destino além da variável [esquema de perfil de união individual](/help/xdm/classes/individual-profile.md). Você pode ver as recomendações de mapeamento geradas automaticamente entre os Dados de origem e os Campos de destino quando a página é exibida pela primeira vez. Você pode editar os mapeamentos selecionando o campo de destino e, em seguida, selecionando um novo campo. Se você fizer alterações nos mapeamentos sugeridos, use o **Validar** botão para validar os novos mapeamentos e exibir os erros que podem estar vinculados aos novos mapeamentos. Selecionar **Salvar** após a conclusão do mapeamento.

   ![Caixa de diálogo Mapeamento de esquema com uma lista suspensa para selecionar um esquema de destino.](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. Continue mapeando todos os campos nos esquemas. Se o esquema for um [esquema de evento](/help/xdm/classes/experienceevent.md), a caixa de diálogo mostra uma lista suspensa onde você pode visualizar todos os esquemas de evento na sandbox de destino.

   ![Selecionar um schema de público alvo na lista suspensa](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. Selecione um esquema entre os esquemas disponíveis na **Sandbox do Target**.

   ![Selecionar um esquema](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. Conclua o mapeamento e selecione **Salvar**.

   ![Salvar mapeamento](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. Depois de concluir o mapeamento de todos os campos nos esquemas, selecione **Concluir** para concluir o workflow de importação.

   ![Concluir o fluxo](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > Não é possível realizar ações em nenhum ativo, exceto os esquemas, pois esta é uma sandbox inspiradora, mas eles são exibidos como dependências do pacote.

### Status da importação {#import-status}

1. Você é redirecionado automaticamente para a [**Importações**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) página onde você pode ver o progresso da sua importação.

   ![Página que mostra o progresso da importação](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. Enquanto o pacote é importado, os ativos do pacote são criados na sandbox de destino. Uma vez concluídos, eles referenciarão os campos que você acabou de mapear no processo de importação. O processo agora está concluído e os ativos da sandbox inspiradora agora também estão presentes na sandbox de destino para você testar.

   ![Ativos gerados na sandbox de destino](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## Próximas etapas

Depois de ler este guia, agora você tem uma melhor compreensão de como aproveitar os manuais de casos de uso juntamente com o [ferramentas de sandbox](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) para criar jornadas executáveis que façam referência aos seus esquemas. Saiba mais sobre o comum [Casos de uso do Real-Time CDP](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).