---
title: Padrão de compatibilidade com versões anteriores
description: Saiba mais sobre o padrão de compatibilidade com versões anteriores no Adobe Experience Platform, que garante que as versões atualizadas das extensões de tags sejam compatíveis com as versões anteriores.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 84%

---

# Padrão de compatibilidade com versões anteriores

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

As atualizações para uma extensão de tag no Adobe Experience Platform devem ser compatíveis com versões anteriores da extensão. Isso significa que:

* Quaisquer modificações nos componentes principais das extensões devem ser compatíveis com as versões anteriores. Isso inclui a configuração de extensão, os tipos de evento, os tipos de condição, os tipos de ação, os tipos de elementos de dados e os módulos compartilhados.
* Os componentes criados por um usuário com a versão mais antiga da extensão devem poder passar pela validação em relação aos esquemas fornecidos pela versão mais recente.
* Um usuário do Adobe Experience Platform deve ser capaz de instalar uma versão atualizada de sua extensão e fazer com que tudo o que fez continue a funcionar exatamente como está até fazer alterações deliberadas.

## Alterações permitidas

São permitidos os seguintes tipos de alterações em sua extensão:

1. Você pode adicionar novos componentes (tipos de evento, tipos de condição etc.).
1. Você pode adicionar novos campos opcionais às configurações da extensão.
1. É possível alterar campos obrigatórios para campos opcionais.

## Alterações proibidas

Não são permitidos os seguintes tipos de alterações em sua extensão:

1. Você não pode renomear um componente.
1. Você não pode remover um componente.
1. Não é possível remover um campo de um componente.
1. Não é possível alterar campos opcionais para campos obrigatórios.
1. Não é possível adicionar novos campos obrigatórios.
1. Você não pode alterar a API dos módulos compartilhados existentes.

Se você fizer qualquer uma dessas alterações, qualquer pessoa que tiver instalado sua extensão na propriedade dela começará imediatamente a ter problemas como:

* As regras não são mais renderizadas corretamente porque um dos componentes da regra está procurando um componente que não existe
* Todas as compilações falham porque a Biblioteca inclui um recurso de upstream que não existe mais na Extensão
* Todas as compilações falham porque a Biblioteca inclui um recurso com configurações que falham na validação em relação ao novo esquema

Particularmente neste segundo caso, os usuários podem ser deixados sem uma solução e não podem corrigir sua propriedade para que possam publicar novamente.

## Remoção de funcionalidades

Podem existir cenários em que você tem um motivo de negócios válido e acha que realmente precisa fazer uma alteração proibida (listada acima). Você não pode fazê-lo mesmo assim, mas veja o que pode fazer em vez disso:

1. Desejo remover um componente => Criar um novo componente e substituir o antigo
1. Desejo remover um campo de um componente => Criar um novo componente com esse campo removido e substituir o antigo
1. Desejo alterar um campo opcional para ser obrigatório => Criar um novo componente que exija o campo desejado e substituir o antigo
1. Desejo alterar a API de um módulo compartilhado => Criar um novo módulo compartilhado e substituir o antigo

Você pode ter encontrado uma questão comum. Isso é bom. Ao descontinuar um componente antigo, você notificará os usuários da sua extensão de que ele foi descontinuado e que eles precisam alternar para um novo componente.  Algumas sugestões sobre como se comunicar com os usuários:

* Atualize o nome de exibição do componente antigo para incluir &quot;(Obsoleto)&quot;.
* Atualize a visualização do componente antigo para ter um texto de aviso vermelho grande de que esse componente foi descontinuado e que o usuário deve mudar para o novo componente.
* Atualize o código do módulo para registrar avisos de substituição no console. Lembre-se de que eles serão exibidos para os usuários finais; portanto, devem ser claros e genéricos.
* Envie mensagens de email amigáveis do seu sistema de CRM.

Nos casos em que a funcionalidade antiga não é apenas indesejável, mas na verdade não existe mais em sua solução, há uma etapa adicional que você pode executar, mas somente depois de avisar os usuários e dar-lhes tempo para atualizar.

* Atualize o conteúdo do seu módulo para que ele não faça nada. Isso removerá a funcionalidade da biblioteca implantada do usuário na próxima compilação, mas não danificará nenhuma das regras ou compilações dele.

### Restaurar funcionalidades removidas

Se você já tiver removido a funcionalidade e souber por usuários que há falhas como resultado, será necessário liberar uma nova versão da extensão que restaure os componentes removidos.

Restaurá-los em um estado substituído, como descrito acima, é correto, mas eles precisam existir.

Como exemplo, considere você tenha uma v1.0 com o Componente XYZ que as pessoas estão usando. Em seguida, você lança uma v1.1 sem o Componente XYZ. Os usuários informam que sua extensão danificou as propriedades deles e você precisa corrigi-la. Você deve lançar uma v1.2 que traga de volta o Componente XYZ (talvez em um estado obsoleto; depende de você) e fazer com que seus usuários atualizem para a v1.2 para que tudo funcione novamente.
