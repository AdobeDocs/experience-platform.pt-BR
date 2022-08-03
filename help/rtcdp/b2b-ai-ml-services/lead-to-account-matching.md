---
title: Lead para a correspondência de contas na CDP em tempo real B2B
type: Documentation
description: Uma visão geral e mais informações sobre o recurso de lead para o recurso de correspondência da conta no Experience Platform CDP B2B.
source-git-commit: 827bd1b930478c3c0b553a9485f98545771a9062
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Lead para a correspondência de contas na CDP em tempo real B2B

## Visão geral {#overview}

O marketing baseado em conta é uma estratégia cada vez mais importante para o marketing B2B. O marketing baseado em conta oferece os seguintes benefícios principais para adquirir clientes específicos de alto valor:

- Limpar ROI
- Alinhamento de vendas e marketing
- Uma abordagem personalizada
- Menos recursos desperdiçados
- Um ciclo de vendas mais curto

O marketing baseado em conta fornece a capacidade de vincular pessoas conhecidas e visitantes anônimos da Web a contas de vendas. Isso permite que as equipes de marketing se envolvam com possíveis clientes potenciais a partir das contas de destino no início da jornada do cliente para aumentar suas chances de conversão. Um registro de pessoa conhecida normalmente inclui parte ou todas as seguintes informações:

- Nome da pessoa
- Endereço de email
- Número do contato
- Nome da empresa
- Site da empresa
- Cargo
- Localização

O lead para a correspondência de contas permite que você participe de perfis de pessoas conhecidas para perfis de contas. Você pode segmentar e direcionar dados em um contexto B2B, como contas, oportunidades e assim por diante. Os perfis de pessoas podem ser classificados nas três categorias a seguir:

- **Perfil da pessoa da conta:** O perfil de pessoa já está associado a pelo menos um perfil de conta por meio do relacionamento de uma fonte de dados. Isso significa que há pelo menos um fragmento de contato.

>[!NOTE]
>
> Os perfis de pessoa da conta não são correspondidos ao executar trabalhos de correspondência de contas.

- **Perfil de pessoa conhecida:** O perfil de pessoa NÃO está associado a nenhum perfil de conta e pelo menos um dos seguintes atributos de perfil de pessoa tem um valor:

   - Endereço de email
   - Nome da empresa
   - Site da empresa

- **Perfil de pessoa anônima:** O perfil de pessoa NÃO está associado a nenhum perfil de conta e nenhum dos atributos de perfil de pessoa a seguir tem um valor:

   - Endereço de email
   - Nome da empresa
   - Site da empresa

>[!NOTE]
>
> Um perfil de pessoa pode estar relacionado a vários perfis de conta. No entanto, o processo de correspondência do lead para a conta só corresponderá à melhor correspondência. Se um conjunto mais amplo de correspondências for necessário, associe o lead à correspondência da conta com o recurso de contas relacionadas.

## Como funciona {#how-it-works}

Os trabalhos executados diariamente usam fatores determinísticos e probabilísticos para corresponder perfis de clientes potenciais conhecidos sem associações de conta existentes. Os perfis de clientes em potencial conhecidos terão um dos seguintes atributos disponíveis:

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> O atributo b2b.personKey.sourceKey deve existir.

Os atributos b2b.companyName, b2b.companyWebsite e b2b.personKey.sourceKey podem ser localizados no grupo de campos b2b no schema de pessoas B2B.

![Esquema de pessoa B2B mostrando atributos](/help/rtcdp/accounts/images/b2b-person-schema.png)

O atributo workEmail pode ser encontrado como um grupo de campos de nível superior no esquema de pessoa B2B.

![Schema de pessoa B2B mostrando workEmail](/help/rtcdp/accounts/images/b2b-person-workemail.png)

Os perfis só terão melhor correspondência se a pontuação de correspondência estiver acima de um limite de confiança interno. Os resultados são salvos em um novo conjunto de dados do sistema da relação de pessoa da conta existente XDM.

O lead para o serviço de correspondência de contas é executado quando um novo instantâneo de perfil de pessoa é disponibilizado uma vez a cada 24 horas. Consulte a documentação para obter mais informações sobre o [configuração do lead para correspondência da conta](/help/rtcdp/accounts/account-profile-ui-guide.md).

## Como visualizar o lead para a saída de correspondência da conta {#how-to-view}

Após a execução do trabalho, os resultados são salvos em um novo conjunto de dados da relação de pessoa da conta existente XDM.

Para visualizar o conjunto de dados, selecione **[!UICONTROL Visualizar conjunto de dados]** no canto superior direito.

![Novo conjunto de dados](/help/rtcdp/accounts/images/b2b-dataset-output.png)

O conjunto de dados inclui as informações da conta correspondente, bem como a pontuação de correspondência do conjunto de dados escolhido. O **[!UICONTROL Origem da Relação]** indica se ele veio do processo de correspondência do lead para a conta.

![Visualizar pontuações e resultados de confiança do conjunto de dados](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## Monitorar trabalhos de correspondência de contas de cliente potencial {#monitoring-jobs}

Você pode monitorar o status da tarefa e as métricas associadas para qualquer lead para tarefas correspondentes à conta por meio do painel.

Consulte a documentação para obter mais informações sobre o [monitorando tarefas para correspondência de contas de cliente potencial](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
