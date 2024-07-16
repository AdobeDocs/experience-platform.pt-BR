---
solution: Experience Platform
title: Visão geral do reconhecimento de dados nos manuais de caso de uso
description: Saiba como acelerar o tempo de implantação copiando os ativos gerados na sandbox inspiradora final para outras sandboxes.
role: Developer
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Ativos gerados pelo manual do Publish para outras sandboxes {#publish-to-other-sandboxes}

Os manuais de casos de uso são modelos de marketing criados para gerar ativos, como públicos, esquemas ou jornadas, para casos de uso de marketing comum. Você pode testar os ativos criados por manuais na sandbox inspiradora e, quando estiver pronto, poderá importar os ativos para outras sandboxes de desenvolvimento para testes adicionais com os dados disponíveis nessas sandboxes. Quando estiver satisfeito com o teste, você poderá mover os ativos das sandboxes de desenvolvimento para as sandboxes de produção.

No entanto, em certos casos, você já pode ter configurado seus próprios esquemas, campos e grupos de campos em outras sandboxes de desenvolvimento. Isso pode tornar alguns dos ativos gerados pelos modelos de caso de uso, como jornadas, incompatíveis com seus dados. Para entender como usar a funcionalidade de reconhecimento de dados para alinhar e complementar melhor os ativos gerados com seus ativos existentes, leia este tutorial.

## Pré-requisitos {#prerequisites}

Antes de ler este tutorial, navegue pelos [modelos disponíveis de manual de casos de uso](/help/use-case-playbooks/playbooks/choose.md#search-and-filter) e [crie uma instância](/help/use-case-playbooks/playbooks/create-share-reuse.md) de um manual preferencial.

A criação de uma instância gera um conjunto de ativos, como jornadas, segmentos, esquemas e mensagens na sandbox inspiradora. Leia para saber como copiar esses ativos em outras sandboxes.

### Criar e publicar um pacote {#create-publish-package}

>[!NOTE]
>
> Você pode importar pacotes somente para outras sandboxes de desenvolvimento. Depois de fazer todas as alterações ou atualizações necessárias, você pode importar os ativos ou pacotes dessas sandboxes de desenvolvimento para a produção. Não é possível importar diretamente das sandboxes de manuais de caso de uso para a produção.

1. Para importar objetos da sandbox inspiradora para outra sandbox, navegue até uma instância desejada de um manual de caso de uso e selecione **[!UICONTROL Publish para outra sandbox]** para exportar os artefatos como um pacote.

   ![GIF mostrando as diferentes instâncias de caso de uso](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. Depois de selecionar o botão **[!UICONTROL Publish para uma sandbox diferente]**, uma modal será exibida. Preencha o nome e a descrição opcional e selecione **[!UICONTROL Criar]**. Esta etapa agrupa os ativos gerados em um pacote que pode ser importado para uma sandbox diferente.

   ![Um modal para criar um pacote](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. Navegue até a página **Sandboxes** no lado esquerdo da navegação e selecione a guia **Pacotes**, localize seu pacote e publique-o. Para publicar um pacote no estado de rascunho, siga as etapas do documento [ferramenta de sandbox](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish).

   ![Pacote em estado de rascunho ou não publicado](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![Publicando o pacote](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. Depois que a publicação for bem-sucedida, na página de navegação de pacotes, você deverá ver um botão **+** habilitado ao lado do nome.

   ![Guia Pacotes na página Sandboxes](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > O pacote não pode ser importado enquanto ainda estiver no modo de rascunho. Portanto, abra a página de detalhes do pacote e publique o pacote.

5. Selecione o controle **+** e inicie o fluxo de trabalho para importar os ativos gerados pelo manual do caso de uso para a **[!UICONTROL sandbox do Target]**. Selecione uma sandbox de destino e confirme o nome do pacote que deseja importar usando a lista suspensa. Adicione os detalhes do job, como nome e descrição do job, antes de prosseguir para a próxima etapa.

   ![Iniciar fluxo de trabalho de importação, selecionar destino, confirmar pacote, adicionar detalhes do trabalho.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. Na etapa **[!UICONTROL Exibir dependências]**, é possível mapear esquemas e copiar outros ativos da sandbox inspiradora para a sandbox de destino. O botão **[!UICONTROL Concluir]** estará desabilitado até que você mapeie cada esquema.

   ![Mapear esquemas na etapa &#39;Exibir dependências&#39;, habilitando o botão Concluir.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### Mapear esquemas {#map-schemas}

1. Mapeie o primeiro esquema. A caixa de diálogo Mapeamento de esquema exibe uma lista suspensa para selecionar o esquema de destino. Se o esquema de origem for um esquema de perfil, então não há outras opções de esquema de destino além do [esquema de perfil de união individual](/help/xdm/classes/individual-profile.md). Você pode ver as recomendações de mapeamento geradas automaticamente entre os Dados do Source e os Campos de destino quando a página é exibida pela primeira vez. Você pode editar os mapeamentos selecionando o campo de destino e, em seguida, selecionando um novo campo. Se você modificar os mapeamentos sugeridos, use o botão **Validar** para validar os novos mapeamentos e exibir erros que possam estar vinculados aos novos mapeamentos. Selecione **Salvar** depois que o mapeamento for concluído.

   ![Caixa de diálogo de mapeamento de esquema com uma lista suspensa para selecionar um esquema de destino.](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. Continue mapeando todos os campos nos esquemas. Se o esquema for um [esquema de evento](/help/xdm/classes/experienceevent.md), a caixa de diálogo mostrará uma lista suspensa na qual você poderá exibir todos os esquemas de evento na sandbox de destino.

   ![Selecione um esquema de destino na lista suspensa](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. Selecione um esquema entre os esquemas disponíveis na **sandbox do Target**.

   ![Selecionar um esquema](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. Conclua o mapeamento e selecione **Salvar**.

   ![Salvar mapeamento](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. Depois de concluir o mapeamento de todos os campos nos esquemas, selecione **Concluir** para concluir o fluxo de trabalho de importação.

   ![Concluir o fluxo](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > Não é possível modificar nenhum ativo, exceto os esquemas, pois esta é uma sandbox inspiradora, mas eles são exibidos porque são dependências do pacote.

### Status da importação {#import-status}

1. Você será redirecionado automaticamente para a página [**Importações**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details), onde poderá ver o progresso da sua importação.

   ![Página mostrando o progresso da importação](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. Enquanto o pacote é importado, os ativos do pacote são criados na sandbox de destino. Uma vez concluídos, eles fazem referência aos campos mapeados durante o processo de importação. O processo agora está concluído e os ativos da sandbox inspiradora agora também estão presentes na sandbox de destino para você testar.

   ![Ativos gerados na sandbox de destino](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## Próximas etapas

Depois de ler este guia, agora você tem uma melhor compreensão de como aproveitar os manuais de casos de uso juntamente com as [ferramentas de sandbox](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) para criar jornadas executáveis que fazem referência aos seus esquemas. Saiba mais sobre os [casos de uso comuns do Real-Time CDP](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).
