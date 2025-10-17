---
title: Pacotes de extensão privados compartilhados
description: Saiba como compartilhar pacotes de extensão privados em Tags do Adobe Experience Platform.
source-git-commit: f45f58b4679b619708204cdb0c18174a4836ce8d
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# Pacotes de extensão privados compartilhados

As Marcas do Adobe Experience Platform agora oferecem suporte a **[!UICONTROL Autorizações de Uso]**, um recurso poderoso que permite compartilhar com segurança pacotes de extensão privados com parceiros confiáveis sem torná-los disponíveis publicamente no catálogo de extensões. Esse recurso cria uma ponte segura entre as organizações, permitindo que você aproveite o código de extensão personalizado umas das outras e, ao mesmo tempo, mantenha a privacidade e o controle sobre suas soluções proprietárias.

## Compartilhamento de pacotes de extensão com outras organizações

>[!NOTE]
>
>Os pacotes de extensão devem ter uma versão privada ou pública para serem compartilhados por meio de [!UICONTROL Autorizações de Uso]. As versões marcadas como Disponibilidade de desenvolvimento não estão qualificadas para compartilhamento e não aparecerão na lista suspensa de autorização. Isso se aplica mesmo se uma versão anterior (por exemplo, 1.0.0) já tiver sido compartilhada. As versões mais recentes (por exemplo, 1.0.1) devem ser tornadas pelo menos privadas antes de serem autorizadas ou instaladas por organizações receptoras.
>
>Todas as orientações sobre o compartilhamento de pacotes de extensão privados também se aplicam se você optar posteriormente por tornar esses pacotes públicos. As mesmas considerações sobre visibilidade, controle de versão, segurança, compatibilidade, suporte e documentação permanecem relevantes, independentemente do status de disponibilidade do pacote.

Os pacotes de extensão públicos e privados podem ser compartilhados por meio de [!UICONTROL Autorizações de Uso], embora as extensões na disponibilidade de Desenvolvimento não possam ter autorizações vinculadas a eles.

As organizações geralmente desenvolvem extensões especializadas adaptadas às suas necessidades comerciais exclusivas. Essas extensões podem conter lógica proprietária, integrações personalizadas ou configurações confidenciais que não devem ser disponibilizadas publicamente. As autorizações de uso resolvem esse desafio habilitando:

- **Compartilhamento seletivo**: compartilhar extensões privadas somente com organizações parceiras confiáveis
- **Privacidade mantida**: manter código de extensão confidencial fora do catálogo público
- **Desenvolvimento colaborativo**: permitir que parceiros confiáveis se beneficiem de suas soluções personalizadas
- **Acesso controlado**: mantenha o controle total sobre quem pode acessar e usar suas extensões privadas

O processo de compartilhamento envolve dois participantes principais:

1. **Organização de compartilhamento**: a organização que possui e compartilha o pacote de extensão privado
2. **Organização recebedora**: a organização confiável que obtém acesso à extensão compartilhada

Quando uma versão privada é compartilhada, a organização de recebimento obtém acesso a essa versão específica, criando uma conexão direta entre as duas organizações. Se uma versão mais recente for posteriormente tornada privada, ela também estará disponível para a organização recebedora sem exigir etapas adicionais de sua parte.

## Criar uma autorização de uso de pacote de extensão

Para compartilhar uma extensão, navegue até a interface da Coleção de dados e selecione **[!UICONTROL Marcas]** na navegação à esquerda. Aqui, selecione uma propriedade existente ou crie uma nova propriedade.

Depois de selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensões]** na navegação à esquerda e selecione a guia **[!UICONTROL Autorizações de Uso]**.

Aqui, você vê uma lista de autorizações compartilhadas existentes organizadas em duas categorias:

- **Compartilhado com esta organização**: extensões que outras organizações compartilharam com você.
- **Compartilhado com outras organizações**: extensões que você compartilhou com outras organizações.

Selecione **[!UICONTROL Adicionar Autorização]**.

![A guia [!UICONTROL Autorizações de Uso] mostrando uma lista de extensões compartilhadas com esta organização, destacando [!UICONTROL Adicionar Autorização]](../images/shared-extensions/add-authorization.png)

>[!IMPORTANT]
>
>Você deve obter o **`Organization ID`** da organização de destino, o proprietário da organização. Organizações não podem ser pesquisadas por nome.

Selecione a **[!UICONTROL Extensão]** que você deseja compartilhar de suas extensões disponíveis na lista suspensa. A lista exibe as extensões de propriedade da sua organização, juntamente com o status de disponibilidade. As extensões cuja versão mais recente está na disponibilidade de **Desenvolvimento** não aparecerão nesta lista.

Em seguida, insira a ID da organização de recebimento e selecione **[!UICONTROL Salvar]**.

![A página [!UICONTROL Criar autorização de uso de pacote de extensão] mostrando uma extensão selecionada e a ID de organização da Adobe inserida, destacando [!UICONTROL Salvar]](../images/shared-extensions/save-authorization.png)

Você retornou à guia [!UICONTROL Autorizações de Uso], onde é possível ver a extensão na lista **[!UICONTROL Compartilhado com outras organizações]**. O status mostrará **Aguardando Aprovação** até que a organização recebedora aprove a autorização. Nesse momento, ela será atualizada para **Aprovada**.

![A guia [!UICONTROL Autorizações de Uso] mostrando uma lista de extensões compartilhadas com outras organizações, destacando a nova autorização](../images/shared-extensions/new-authorization.png)

>[!TIP]
>
>Você também pode compartilhar extensões diretamente no **[!UICONTROL Catálogo de extensões]** selecionando o menu () no cartão de extensão e selecionando a opção de compartilhamento no menu.

Quando uma autorização está ativa, a extensão compartilhada exibe um emblema ***Compartilhamento*** no catálogo, indicando que está sendo compartilhado com outras organizações.

![A guia [!UICONTROL Catálogo] mostrando a extensão compartilhada com o selo](../images/shared-extensions/sharing-badge.png)

## Autorizar e gerenciar extensões compartilhadas

>[!NOTE]
>
>Como uma organização recebedora, você só pode aprovar ou rejeitar extensões compartilhadas. Não é possível gerenciar ou modificar os detalhes da autorização, pois eles são controlados pela organização de compartilhamento.

Para autorizar uma extensão compartilhada para sua organização, navegue até a interface da Coleção de dados, selecione **[!UICONTROL Marcas]** na navegação à esquerda e selecione a propriedade. Em seguida, selecione **[!UICONTROL Extensões]** na navegação à esquerda e selecione a guia **[!UICONTROL Autorizações de uso]**.

Você pode ver uma lista de extensões compartilhadas, incluindo aquelas **Aguardando Aprovação** na seção **[!UICONTROL Compartilhado com esta organização]**. Selecione a extensão que você deseja aprovar e selecione **[!UICONTROL Aprovar]**.

![A guia [!UICONTROL Autorizações de Uso] mostrando uma lista de extensões compartilhadas com esta organização com a extensão Aguardando Aprovação selecionada, destacando [!UICONTROL Aprovar]](../images/shared-extensions/approve-authorization.png)

>[!NOTE]
>
>Você também pode rejeitar uma solicitação na guia **[!UICONTROL Autorizações de uso]** se a extensão compartilhada não for mais exigida pela sua organização.

Selecione **[!UICONTROL OK]** na caixa de diálogo **[!UICONTROL Usos de Autorização]**.

![A caixa de diálogo [!UICONTROL Usos da Autorização], destacando [!UICONTROL OK]](../images/shared-extensions/confirmation.png)

Você retornou à guia [!UICONTROL Autorizações de Uso], onde é possível ver a extensão, e agora mostra o status **Aprovado**.

![A guia [!UICONTROL Autorizações de Uso] mostrando uma lista de extensões compartilhadas com esta organização, destacando a extensão com o status Aprovado](../images/shared-extensions/approved-authorization.png)

Depois que a autorização é aprovada, a extensão é disponibilizada no catálogo e pode ser instalada e usada como qualquer outra extensão. A extensão compartilhada exibe um selo ***Recebimento*** indicando que é uma extensão compartilhada com você por outra organização.

![A guia [!UICONTROL Catálogo] mostrando a extensão compartilhada com o selo &quot;Recebendo&quot;](../images/shared-extensions/receiving-badge.png)

## Revogação de autorizações

Como organização responsável, você pode excluir uma autorização a qualquer momento, independentemente de seu status atual (Aguardando aprovação, Rejeitada ou Aprovada).

**Se sua extensão nunca foi tornada pública:**
- Qualquer versão privada da organização de recebimento já instalada continuará a aparecer na lista de extensões instaladas.
- Se a organização receptora nunca tiver instalado sua extensão, ela não aparecerá mais em nenhum lugar na interface.

**Se sua extensão foi tornada pública:**
- Qualquer versão privada instalada pela organização receptora permanecerá visível na lista de extensões instaladas.
- Se nunca instalaram sua versão privada, ainda verão a versão pública mais recente no catálogo e poderão instalá-la.
- Eles também podem fazer downgrade da sua versão privada para a versão pública mais recente disponível, se desejado.

Ao revogar uma autorização, a organização receptora mantém determinados direitos para proteger suas implementações existentes:

- **Uso contínuo**: a organização de recebimento pode continuar usando qualquer versão privada que já tenha sido instalada, mesmo após você revogar o acesso.
- **Proteção de compilação**: se a organização de recebimento instalou sua v1.0.0 privada e você depois liberar uma v1.0.1 privada, ela não verá a versão mais recente, mas poderá continuar compilando com a v1.0.0 sem interrupções.
- **Atualizações futuras**: se você tornar sua extensão pública posteriormente (por exemplo, lançando a v2.0.0 publicamente), a organização recebedora poderá atualizar sua v1.0.0 privada diretamente para a nova v2.0.0 pública.

>[!IMPORTANT]
>
>A revogação da autorização não quebra compilações ou implementações existentes. As organizações de recebimento mantêm acesso a todas as versões privadas já instaladas para garantir a continuidade dos negócios.

## Próximas etapas

Este documento demonstrou como usar o recurso de extensão compartilhado no Experience Platform. Para obter informações sobre desenvolvimento de extensão, consulte o [guia do usuário de desenvolvimento de extensão](./getting-started.md).

Para obter uma visão geral de alto nível do desenvolvimento de extensões no Experience Platform, consulte a [documentação de visão geral](./overview.md).
