---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão da plataforma Experience 10 de setembro de 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: 26568ebbbe48b5a82e4f6b5cf035c354c11e8ed1

---


# Notas de versão da Adobe Experience Platform

## Data de lançamento: 10 de setembro de 2019

Atualizações dos recursos existentes na Adobe Experience Platform:

* [Ingestão de dados](#ingestion)
* [Área de trabalho da ciência de dados](#dsw)
* [Serviço de Query](#query)

## Ingestão de dados {#ingestion}

A plataforma Adobe Experience fornece um conjunto avançado de recursos para assimilar qualquer tipo e latência de dados. A assimilação de dados da plataforma Adobe Experience oferece várias alternativas para a assimilação de dados, incluindo APIs em lote, APIs de fluxo, conectores nativos da Adobe, parceiros de integração de dados ou a interface do usuário da plataforma Adobe Experience.

**Novos recursos**

| Recurso | Descrição |
| ----------- | ---------- |
| Novo domínio para ingestão de streaming | O `dcs.data.adobe.net` domínio foi movido para o novo domínio comum de coleta de dados `dcs.adobedc.net`. Os usuários devem atualizar suas implementações de acordo com a documentação de ingestão de streaming da plataforma Adobe Experience. Toda a documentação relacionada à assimilação de streaming da plataforma Adobe Experience foi atualizada para usar o novo domínio. |

Para obter mais informações, visite a documentação [de ingestão de](../../ingestion/home.md)dados.

## Área de trabalho da ciência de dados {#dsw}

A Adobe Experience Platform Data Science Workspace é um serviço totalmente gerenciado na Experience Platform que permite que os cientistas de dados gerem informações de dados e conteúdo de forma contínua em soluções da Adobe e sistemas de terceiros, criando e operacionalizando Modelos de Aprendizado de Máquinas. A Data Science Workspace é totalmente integrada à Plataforma e alimenta o ciclo de vida completo da ciência de dados, incluindo a exploração e a preparação de dados XDM, seguido pelo desenvolvimento e operacionalização de Modelos para enriquecer automaticamente o Perfil do cliente em tempo real com os Insights de aprendizado da máquina.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Agendamento de serviços por meio da interface do usuário | Integrado ao Serviço de orquestração de plataformas para automatizar o treinamento e a pontuação do modelo com agendamentos definidos pelo usuário usando a interface do usuário. |
| Galeria de serviços | Navegue, monitore e acesse os serviços de aprendizado de máquina com a capacidade de programar trabalhos de treinamento e pontuação automatizados, tudo isso na Service Gallery reprojetada. |
| JupyterLab 5.0.0 | Melhorias na interface do usuário do JupyterLab. |

**Problemas conhecidos**

* Atualmente, não existe uma forma acessível na Galeria de Serviços para eliminar um Serviço existente. Enquanto isso, consulte a referência [da API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei Machine Learning para excluir um serviço existente por meio de chamadas de API.
* A Galeria de Serviços não tem suporte de paginação para filtrar as execuções de treinamento e pontuação de um Serviço.
* Ao configurar treinamentos programados ou classificações são executados na Galeria de serviços, definir a frequência para hora impede que o agendamento seja aplicado.

Para obter mais informações, visite a Visão geral [da área de trabalho da](../../data-science-workspace/home.md)Data Science.

## Serviço de Query {#query}

O Query Service fornece a capacidade de usar SQL padrão para dados de query na Adobe Experience Platform para suportar uma variedade de casos de uso de análise e gestão de dados. É uma ferramenta sem servidor que permite que você participe de conjuntos de dados do Data Lake e capture os resultados do query como um novo conjunto de dados para uso no relatórios, na Data Science Workspace ou para ingestão no Perfil do cliente em tempo real.

Você pode usar o Serviço de Query para criar ecossistemas de análise de dados, criando uma imagem dos clientes em seus vários canais de interação. Esses canais podem incluir sistemas de ponto de venda, sistemas web, móveis ou CRM.

**Novos recursos**

| Recurso | Descrição |
| -----------| ---------- |
| Melhorias no Editor de Query | Adicionada uma função de gravação que permite salvar um query e trabalhar nele posteriormente. Adição de uma guia &quot;Procurar&quot; à interface de usuário do Query Service na Adobe Experience Platform, que mostra query salvos pelos usuários em sua organização. Implementado um painel &quot;Detalhes do Query&quot; que exibe metadados úteis sobre o query que está sendo visualizado. |
| Novas funções de atribuição | Funções definidas pela Adobe no Serviço de Query para query para atribuição de canal com parâmetros de expiração. |
| Aprimoramentos à sintaxe SQL | Suporte para sintaxe iLike. |
| Gerar conjuntos de dados com um Schema XDM definido | Adicionada uma nova cláusula nos query Criar tabela como seleção (CTAS) que permite especificar um schema de público alvo. |

For more information, refer to the [Query Service documentation](../../query-service/home.md).