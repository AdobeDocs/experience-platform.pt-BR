---
title: Lead para correspondência de contas no Real-Time CDP B2B
type: Documentation
description: Uma visão geral e mais informações sobre o lead para o recurso de correspondência de contas no Experience Platform CDP B2B.
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 3%

---

# Lead para correspondência de contas no Real-Time CDP B2B

## Visão geral {#overview}

O marketing baseado em conta é uma estratégia cada vez mais importante para o marketing B2B. O marketing baseado em conta oferece os seguintes benefícios principais para adquirir clientes específicos de alto valor:

- Limpar ROI
- Alinhamento de vendas e marketing
- Uma abordagem personalizada
- Menos desperdício de recursos
- Um ciclo de vendas mais curto

O marketing baseado em conta oferece a capacidade de vincular pessoas conhecidas e visitantes anônimos da Web a contas de vendas. Isso permite que as equipes de marketing se envolvam com possíveis leads das contas do target no início da jornada do cliente para aumentar suas chances de conversão. Um registro de pessoa conhecida normalmente inclui parte ou todas as seguintes informações:

- Nome da pessoa
- Endereço de email
- Número de contato
- Nome da empresa
- Site da empresa
- Cargo
- Localização

A correspondência entre lead e conta permite que você associe perfis de pessoas conhecidos a perfis de conta. Em seguida, você pode segmentar e direcionar dados em um contexto B2B, como contas, oportunidades e assim por diante. Os perfis de pessoa podem ser classificados nas três categorias a seguir:

- **Perfil da conta pessoal:** O perfil de pessoa já está associado a pelo menos um perfil de conta por meio do relacionamento de uma fonte de dados. Isso implica que há pelo menos um fragmento de contato.

>[!NOTE]
>
> Os perfis de conta pessoal não são correspondidos ao executar trabalhos de correspondência de leads em contas.

- **Perfil de pessoa conhecida:** O perfil de pessoa NÃO está associado a nenhum perfil de conta e pelo menos um dos seguintes atributos de perfil de pessoa tem um valor:

   - Endereço de email
   - Nome da empresa
   - Site da empresa

- **Perfil de pessoa anônimo:** O perfil de pessoa NÃO está associado a nenhum perfil de conta e nenhum dos seguintes atributos de perfil de pessoa tem um valor:

   - Endereço de email
   - Nome da empresa
   - Site da empresa

>[!NOTE]
>
> Um perfil de pessoa pode estar relacionado a vários perfis de conta. No entanto, o processo de lead para correspondência de contas só corresponderá à melhor correspondência. Se um conjunto mais amplo de correspondências for necessário, associe o lead à correspondência de contas com o recurso de contas relacionadas.

## Como funciona {#how-it-works}

As ordens de produção de execução diária usam fatores determinísticos e probabilísticos para corresponder perfis de clientes potenciais conhecidos sem associações de conta existentes. Os perfis de clientes potenciais conhecidos terão um dos seguintes atributos disponíveis:

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> O atributo b2b.personKey.sourceKey deve existir.

Os atributos b2b.companyName, b2b.companyWebsite e b2b.personKey.sourceKey podem estar localizados no grupo de campos b2b no esquema de pessoa B2B.

![Esquema de pessoa B2B mostrando atributos](/help/rtcdp/accounts/images/b2b-person-schema.png)

O atributo workEmail pode ser encontrado como um grupo de campos de nível superior no esquema de pessoa B2B.

![Esquema de pessoa B2B mostrando workEmail](/help/rtcdp/accounts/images/b2b-person-workemail.png)

Os perfis terão melhor correspondência somente se a pontuação de correspondência estiver acima de um limite de confiança interno. Os resultados são salvos em um novo conjunto de dados do sistema do XDM da relação pessoal da conta existente.

O lead para o serviço de correspondência de contas é executado quando um novo instantâneo do perfil de pessoa é disponibilizado, uma vez a cada 24 horas. Consulte a documentação para obter mais informações sobre o [configuração de lead para correspondência de conta](/help/rtcdp/accounts/account-profile-ui-guide.md).

## Como visualizar o lead para a saída de correspondência de contas {#how-to-view}

Após a execução do trabalho, os resultados são salvos em um novo conjunto de dados do XDM da relação pessoal da conta existente.

Para visualizar o conjunto de dados, selecione **[!UICONTROL Visualizar conjunto de dados]** no canto superior direito.

![Novo conjunto de dados](/help/rtcdp/accounts/images/b2b-dataset-output.png)

O conjunto de dados inclui as informações de conta correspondentes, bem como a pontuação de correspondência do conjunto de dados escolhido. A variável **[!UICONTROL Origem do relacionamento]** indica se veio do processo de conciliação de lead com conta.

![Visualizar pontuações e saída de confiança do conjunto de dados](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## Monitorar lead para trabalhos de correspondência de contas {#monitoring-jobs}

Você pode monitorar o status do trabalho e as métricas associadas para qualquer lead em trabalhos de correspondência de contas por meio do painel.

Consulte a documentação para obter mais informações sobre o [monitoramento de trabalhos de correspondência entre lead e conta](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
