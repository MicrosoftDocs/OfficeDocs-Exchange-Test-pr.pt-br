---
title: 'Gerenciamento de registros de mensagens: Exchange 2013 Help'
TOCTitle: Gerenciamento de registros de mensagens
ms:assetid: 0dd92e9c-881e-43c0-9bbf-f41fdc9dfd87
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335093(v=EXCHG.150)
ms:contentKeyID: 50484939
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciamento de registros de mensagens

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-02-01_

Os usuários enviem e recebam email todos os dias. Se permanecerá sem gerenciamento, o volume de email gerado e recebidas por dia pode inundar usuários, a produtividade do usuário do impacto e expor sua organização a riscos. Como resultado, o gerenciamento do ciclo de vida de email é um componente essencial para a maioria das organizações.

Gerenciamento de registros de mensagens (MRM) é a tecnologia de gerenciamento de registros no Exchange Server 2013 e Exchange Online que ajuda as organizações a gerenciar o ciclo de vida de email e reduzir os riscos legais associados ao email. Implantar o MRM pode ajudar sua organização de várias maneiras:

  - **Atender aos requisitos de negócios**   Dependendo de sua organização de políticas de mensagens, talvez seja necessário manter mensagens de email importantes por um determinado período. Por exemplo, caixa de correio de um usuário pode conter mensagens críticas relacionadas à estratégia de negócios, as transações, desenvolvimento de produtos ou interações do cliente.

  - **Atender a requisitos legais e normativos**   Muitas organizações têm um requisito legal ou normativos para armazenar mensagens por um período designado e remover mensagens anteriores a esse período. Armazenamento de mensagens mais do que o necessário pode aumentar os riscos legais ou financeiras da sua organização.

  - **Aumentar a produtividade do usuário**   Se permanecerá sem gerenciamento, o volume crescente de email nas caixas de correio dos usuários também pode afetar sua produtividade. Por exemplo, embora inscrições de boletim informativo e notificações automatizadas podem ter valor informativo quando são recebidas, os usuários talvez não removê-los após a leitura (geralmente eles estiver nunca lido). Muitos desses tipos de mensagens não têm um valor de retenção, além de alguns dias. Usando o MRM para remover essas mensagens pode ajudar a reduzir a desorganização informações nas caixas de correio dos usuários, melhorando a produtividade.

  - **Melhore o gerenciamento de armazenamento**   Devido a expectativas orientadas pelos serviços de email do consumidor livre, muitos usuários manter mensagens antigas por um longo período ou nunca removê-los. Manter caixas de correio grandes está se tornando rapidamente uma prática padrão e os usuários não precisam ser forçados para alterar seus hábitos de trabalho com base em cotas restritivas de caixas de correio. No entanto, a retenção de mensagens, além do período que é necessário para os negócios, motivos legais ou normativos também aumenta os custos de armazenamento.

MRM oferece flexibilidade para implementar a política de gerenciamento de registros que melhor atenda aos requisitos da sua organização. Com um bom entendimento de MRM, arquivamento In-loco e retenção In-loco, você pode ajudar a atender às suas metas de gerenciamento do armazenamento de caixa de correio e requisitos normativos de retenção de reunião.

Procurando tarefas de gerenciamento relacionadas a MRM? Consulte [Procedimentos de gerenciamento de registros de mensagens](messaging-records-management-procedures-exchange-2013-help.md).

## MRM no Exchange Server 2013 e Exchange Online

No Exchange Server 2013 e Exchange Online, o MRM é realizada com o uso de marcas de retenção e políticas de retenção. Marcas de retenção são usadas para aplicar configurações de retenção a uma caixa de correio inteira e pastas de caixa de correio de padrão como entrada e itens excluídos. Você também pode criar e implantar marcas de retenção que o Outlook 2010 e posterior e os usuários do Outlook Web App podem usar para aplicar a pastas ou mensagens individuais. Depois que eles são criados, você pode adicionar marcas de retenção a uma política de retenção e aplica a política aos usuários. Assistente de pasta gerenciada processa caixas de correio e aplica as configurações de retenção na política de retenção do usuário. Para saber mais sobre as políticas de retenção, consulte [Marcas e políticas de retenção](retention-tags-and-retention-policies-exchange-2013-help.md).

Quando uma mensagem atinge sua idade de retenção especificada na marca de retenção aplicável, o Assistente de pasta gerenciada executará a ação de retenção especificada pela marca. As mensagens podem ser excluídas permanentemente ou excluídas com a capacidade de recuperá-los. Se um arquivo morto tenha sido provisionado para o usuário, você também pode usar marcas de retenção para mover itens para o arquivo de In-loco do usuário.

## Estratégias MRM

Você pode usar as políticas de retenção para impor a retenção de mensagem básica para uma caixa de correio inteira ou para pastas padrão específico. Embora existam várias estratégias para implantar o MRM, aqui estão alguns dos mais comuns:

**Remover todas as mensagens após um período especificado**   Nessa estratégia, você deve implementar uma única política MRM que remove todas as mensagens após um determinado período. Essa estratégia, não há nenhuma classificação de mensagens. Você pode implementar essa diretiva criando uma marca de política única padrão (DPT) da caixa de correio. No entanto, isso não garante que as mensagens são retidas para o período especificado. Os usuários ainda podem excluir mensagens antes que o período de retenção for atingido.

**Mover mensagens para arquivar caixas de correio**   Essa estratégia, você implementar políticas MRM que mover itens para a caixa de correio de arquivo morto do usuário. Uma caixa de correio de arquivamento fornece armazenamento adicional para usuários manter o antigo e pouco acessados conteúdo. Marcas de retenção que mover itens também são conhecidas como *políticas de arquivamento*. Dentro da mesma política de retenção, você pode combinar um DPT e marcas pessoais para mover itens e um DPT, RPTs e marcas pessoais para excluir itens. Para saber mais sobre políticas de arquivamento, consulte:

  - **Exchange Server 2013:**  [Arquivamento In-loco do Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md)

  - **Exchange Online:**  [Caixas de correio de arquivo morto no Exchange Online](https://technet.microsoft.com/pt-br/library/dn922147\(v=exchg.150\))


> [!TIP]
> &nbsp;&nbsp;&nbsp;Em uma implantação híbrida do Exchange, você pode habilitar uma caixa de correio de arquivo morto baseada em nuvem para uma caixa de correio principal local. Se você atribuir uma política de arquivo morto a uma caixa de correio local, os itens serão transferidos para o arquivo morto baseado em nuvem. Se um item for transferido para a caixa de correio de arquivo morto, nenhuma cópia será mantida na caixa de correio local. Se a caixa de correio local for colocada em espera, uma política de arquivo morto ainda moverá os itens para a caixa de correio de arquivo morto baseada em nuvem, na qual serão preservados durante o período especificado pela retenção.



**Remover mensagens com base no local de pasta**   Essa estratégia, você implementar políticas MRM com base no local de email. Por exemplo, você pode especificar que as mensagens na caixa de entrada são mantidas por um ano e mensagens na pasta Lixo eletrônico são mantidas por 60 dias. Você pode implementar essa diretiva usando uma combinação de marcas de diretiva de retenção (RPTs) para cada pasta padrão que você deseja configurar e um DPT para a caixa de correio inteira. O DPT se aplica a todas as pastas personalizadas e todas as pastas padrão que não têm uma RPT aplicada.


> [!TIP]
> No Exchange 2013, você pode criar RPTs para as pastas de calendário e tarefas. Se você não quiser itens nessas pastas ou outras pastas padrão para expirar, você pode criar uma marca de retenção desabilitado para essa pasta padrão.



**Permitir que usuários classificar mensagens**   Essa estratégia, você implementar políticas MRM que incluem uma configuração de retenção de linha de base para todas as mensagens, mas permitir que os usuários classificar as mensagens com base em requisitos normativos ou de negócios. Nesse caso, os usuários se tornam uma parte importante de sua estratégia de gerenciamento de registros - frequentemente terem a melhor compreensão do valor de retenção da mensagem.

Os usuários podem aplicar configurações de retenção diferente para mensagens que precisam ser retidos por um período maior ou menor. Você pode implementar essa diretiva usando uma combinação dos seguintes procedimentos:

  - Um DPT para a caixa de correio

  - Marcas pessoais que os usuários podem aplicar para pastas personalizadas ou mensagens individuais

  - (Opcional) RPTs adicionais para expirar itens em pastas específicas padrão

Por exemplo, você pode usar uma política de retenção com marcas pessoais que têm um período de retenção mais curto (por exemplo, dois dias, uma semana ou mês), bem como marcas pessoais que têm um período de retenção maior (por exemplo, uma, duas ou cinco anos). Os usuários podem aplicar marcas pessoais com os mais curtos períodos de retenção para itens como inscrições de boletim informativo que perdem seu valor em dias de recebimento-los e aplicar as marcas de períodos mais longos para preservar itens que têm um valor comercial alto. Eles também podem automatizar o processo usando regras de caixa de entrada no Outlook para aplicar uma marca pessoal a mensagens que correspondam às condições de regra.

**Mensagens de reter para fins de descoberta eletrônica**   Nessa estratégia, você implementar políticas MRM que removam mensagens de caixas de correio após um período especificado, mas também mantêm-los na pasta itens recuperáveis para fins de [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md) , mesmo se as mensagens foram excluídas pelo usuário ou por outro processo.

Você pode atender a esse requisito, usando uma combinação de políticas de retenção e [Retenção local e Retenção de litígio](in-place-hold-and-litigation-hold-exchange-2013-help.md) ou litígio. Políticas de retenção remover mensagens da caixa de correio após o período especificado. Retenção baseada em tempo de In-loco ou litígio preserva as mensagens que foram excluídas ou modificadas antes que o período. Por exemplo, para manter as mensagens por sete anos, você pode criar uma política de retenção com um DPT que exclui mensagens em sete anos e litígio para armazenar mensagens por sete anos. Mensagens que não são removidas por usuários serão excluídas depois sete anos; mensagens excluídas pelos usuários antes do período do ano sete serão mantidas na pasta itens recuperáveis por sete anos. Para saber mais sobre esta pasta, consulte [Pasta Itens Recuperáveis](recoverable-items-folder-exchange-2013-help.md).

Opcionalmente, você pode usar marcas pessoais e RPTs para permitir que usuários limpar suas caixas de correio. No entanto, o bloqueio In-loco e retenção de litígio continua a manter as mensagens excluídas até que o período de retenção expira.


> [!TIP]
> Um baseadas em tempo bloqueio In-loco ou retenção de litígio é semelhante à que foi modo informal conhecido como um <EM>aplicação legais de retenção</EM> no Exchange 2010. Aplicação de retenção legal foi implementado, definindo o período de retenção de item excluído de um banco de dados de caixa de correio ou caixa de correio individual. Entretanto, a retenção de item excluído manterá itens excluídos e modificados com base na data excluída. Bloqueio in-loco e retenção de litígio preserva itens com base na data em que eles estiver recebidos ou criados. Isso garante que as mensagens são preservadas para pelo menos o período especificado.



## Para saber mais

[Registros de mensagens terminologia de gerenciamento no Exchange 2013](messaging-records-management-terminology-in-exchange-2013-exchange-2013-help.md)

[Marcas e políticas de retenção](retention-tags-and-retention-policies-exchange-2013-help.md)

