---
title: 'Registro no Diário: Exchange 2013 Help'
TOCTitle: Registro no Diário
ms:assetid: 6a20f207-4485-44ef-b010-ec760eb5165b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998649(v=EXCHG.150)
ms:contentKeyID: 50485878
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registro no Diário

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

O registro em diário pode ajudar a organização a atender requisitos legais, regulatórios e organizacionais de conformidade, registrando a comunicação por emails de entrada e de saída. Durante o planejamento para retenção e conformidade de mensagens, é importante compreender o registro no diário, como ele se adapta às diretivas de conformidade da organização e como o Microsoft Exchange Server 2013 ajuda você a proteger mensagens registradas no diário.

**Sumário**

Why journaling is important

Journaling agent

Journal rules

Journal rule replication

Journal reports

Interoperability with Exchange 2010 and Exchange 2007

Troubleshooting

## Por que o registro no diário é importante?

Primeiramente, é importante compreender a diferença entre registro no diário e uma estratégia de arquivamento de dados:

  - *Registro no Diário* é a habilidade para registrar todas as comunicações em uma organização, incluindo comunicação por email, para serem usadas na estratégia de arquivamento ou retenção de email da organização. Para cumprir um número cada vez maior de requisições regulamentares e conformativas, muitas organizações precisam manter registros das comunicações que ocorrem quando os funcionários executam tarefas diárias de negócios.

  - *Arquivamento de dados* refere-se ao backup dos dados, removendo-os do ambiente nativo e armazenando-os em outro local, reduzindo assim a carga do armazenamento de dados. Você pode usar o registro no diário do Exchange como uma ferramenta na sua estratégia de arquivamento ou retenção de emails.

Apesar de o registro no diário não ser requisitado por uma regulamentação específica, é possível conseguir a conformidade através do registro no jornal, sob determinadas regulamentações. Por exemplo, os executivos corporativos em alguns setores financeiros são responsáveis pelas reivindicações que foram feitas por seus funcionários aos respectivos clientes. Para verificar se as reivindicações são precisas, um executivo corporativo pode configurar um sistema em que os gerentes revisam alguma parte da comunicação entre funcionário e cliente regularmente. Todo trimestre os gerentes verificam a conformidade e aprovam a conduta de seus funcionários. Depois que todos os gerentes relatam a aprovação para o executivo corporativo, este relata a conformidade, em nome da empresa, ao corpo regulamentador. Neste exemplo, os emails podem ser uma forma de comunicação entre o funcionário e o cliente que os gerentes devem verificar. Por isso, é possível usar o registro no diário para coletar todas os emails enviados por funcionários que lidam pessoalmente com clientes. Outros mecanismos de comunicação com o cliente podem incluir faxes e telefonemas, que também podem estar sujeitas a regulamentações. O recurso de registrar no diário todas as classes de dados em uma empresa é uma funcionalidade importante da arquitetura de TI.

A lista a seguir mostra algumas das mais conhecidas regulamentações americanas e internacionais em que o registro no diário pode ajudar nas estratégias de conformidade:

  - Sarbanes-Oxley Act de 2002 (SOX)

  - Security Exchange Commission Rule 17a-4 (SEC Rule 17 A-4)

  - National Association of Securities Dealers 3010 & 3110 (NASD 3010 & 3110)

  - Gramm-Leach-Bliley Act (Financial Modernization Act)

  - Financial Institution Privacy Protection Act of 2001

  - Financial Institution Privacy Protection Act of 2003

  - Health Insurance Portability and Accountability Act de 1996 (HIPAA)

  - Uniting and Strengthening America by Providing Appropriate Tools Required to Intercept and Obstruct Terrorism Act de 2001 (Patriot Act)

  - European Union Data Protection Directive (EUDPD)

  - Personal Information Protection Act do Japão

Voltar ao início

## Agente Registro no diário

Em uma organização do Exchange 2013 , todo o tráfego de email é roteado por servidores de Caixa de Correio. Todas as mensagens percorrem pelo menos um servidor com o serviço de Transporte na sua vida útil. O *Agente de registro no diário* é um agente de transporte com foco em conformidade que processa mensagens nos servidores de Caixa de Correio. Ele é disparado nos eventos de transporte de **OnSubmittedMessage** e **OnRoutedMessage**.


> [!NOTE]
> No Exchange 2013, o agente de Registro no Diário e um agente integrado. Agentes integrados não estão incluídos na lista de agentes retornados pelo cmdlet <STRONG>Get-TransportAgent</STRONG>. Para mais detalhes, consulte <A href="transport-agents-exchange-2013-help.md">Agentes de transporte</A>.



O Exchange 2013 fornece as seguintes opções de registro no diário:

  - **Registro padrão no diário**   O registro padrão no diário é configurado em um banco de dados de caixa de correio. Ele permite que o agente de registro no diário registre todas as mensagens envias de e para caixas de correio localizadas em um banco de dados de caixa de correio específico. Para registrar no diário todas as mensagens de e para todos os destinatários e remetentes, você dever configurar esse registro em todos os bancos de dados de caixa de correio em todos os servidores de Caixa de Correio da organização.

  - **Registro premium no diário**   O registro premium no diário permite que o agente de registro no diário execute um registro mais granular, usando as regras de registro no diário. Em vez de registrar no diário todas as caixas de correio de um banco de dados, você pode configurar as regras de registro no diário para que combinem com as necessidades de sua organização de registrar no diário destinatários individuais ou membros de grupos de distribuição. Para usar o registro no diário premium, você deve ter uma CAL (Licença de Acesso para Cliente) do Exchange Enterprise.

Quando você habilita o registro padrão no diário em um banco de dados de caixa de correio, essas informações são salvas no Active Directory e são lidas pelo agente de Registro no Diário. Similarmente, regras de registro no diário configuradas com o registro no diário premium também são salvas no Active Directory e aplicadas ao agente de Registro no Diário. Para obter mais informações sobre como configurar registros no diário padrão e premium, consulte [Gerenciar diário](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/journaling/manage-journaling).

Voltar ao início

## Regras de Diário

Estes são os principais aspectos de regras de diário:

  - **Escopo da regra de registro no diário**   Define quais mensagens são registradas no diário pelo agente de Registro no diário.

  - **Destinatário do registro no diário**   Especifica o endereço SMTP do destinatário para registrar no diário.

  - **Caixa de correio de registro no diário**   Especifica uma ou mais caixas de correio usadas para coletar relatórios de registro no diário.

## Escopo de regra de registro no diário

Você pode usar uma regra de diário para registrar somente mensagens internas, somente mensagens externas ou ambas. A lista a seguir descreve esses escopos:

  - **Somente mensagens internas**   Regras de diário com o escopo definido para registrar as mensagens internas enviadas entre os destinatários dentro da sua organização do Exchange.

  - **Somente mensagens externas**   Regras de diário com o escopo definido para registrar as mensagens externas enviadas para destinatários ou recebidas de remetentes de fora da sua organização do Exchange.

  - **Todas as mensagens**   Regras de diário com o escopo definido para registrar em diário todas as mensagens que passam pela sua organização, independentemente da origem ou do destino. Essas entradas incluem mensagens que já podem ter sido processadas por regras de diário nos escopos Interno e Externo.

## Destinatário do registro no diário

Você pode implementar regras de registro no diário específicas, inserindo o endereço SMTP do destinatário que você deseja registrar no diário. O destinatário pode ser uma caixa de correio, um grupo de distribuição ou um contato do Exchange. Esses destinatários podem estar sujeitos aos requisitos regulamentares ou podem estar envolvidos em trâmites legais em que mensagens de email ou outros meios de comunicação são coletados como evidência. Ao definir destinatários específicos ou grupos de destinatários, você pode configurar facilmente um ambiente de registro no diário que corresponda aos processos da sua organização e atenda aos requisitos legais e regulamentadores. Colocar o foco somente nos destinatários específicos que precisam ser registrados em diário também diminui os custos de armazenamento e outros custos associados à retenção de grandes volumes de dados.

Todas as mensagens enviadas ou recebidas dos destinatários de registro no diário que você especificar em uma regra de registro no diário serão registradas. Se você especificar um grupo de distribuição como destinatário de registro no diário, todos os emails enviados ou recebidos dos membros desse grupo serão registrados no diário. Se você não especificar um destinatário de registro no diário, todas as mensagens enviadas ou recebidas de destinatários que correspondam ao escopo da regra de diário serão registradas no diário.

**Destinatários de registro no diário habilitados para Unificação de Mensagens**

Muitas organizações que implementam o registro no diário também podem usar a Unificação de Mensagens (UM) para consolidar sua infraestrutura de email, caixa postal e fax. Entretanto, não é recomendável que o processo de registro no diário gere relatórios das mensagens geradas pela Unificação de Mensagens. Nesses casos, você pode decidir se deseja registrar no diário mensagens de caixa postal e mensagens de notificação de chamada não atendida tratadas por um servidor Exchange com o serviço de Unificação de Mensagens ou se deseja ignorar essas mensagens. Se a sua organização não exigir o registro no diário dessas mensagens, você poderá ignorá-las e, assim, reduzir a quantidade de espaço de armazenamento em disco rígido exigida para armazenar relatórios de registro no diário.


> [!NOTE]
> As mensagens que contêm faxes gerados pelo serviço de Unificação de Mensagens são sempre registradas no diário, mesmo que você desabilite o registro no diário de mensagens de notificação de chamada perdida e caixa postal da Unificação de Mensagens.



Para mais informações sobre como habilitar ou desabilitar mensagens de caixa postal e de notificação de chamada não atendida, consulte [Desabilitar ou habilitar o registro no diário de notificações de chamada perdida e caixa postal](disable-or-enable-journaling-of-voice-mail-and-missed-call-notifications-exchange-2013-help.md).

## Caixa de correio de registro no diário

A caixa de correio de registro no diário é usada para coletar relatórios do diário. A maneira como você configura a caixa de correio de registro no diário depende das políticas e dos requisitos legais e regulamentadores da organização. Você pode especificar uma caixa de correio de registro no diário para coletar mensagens de todas as regras de diário configuradas na organização ou usar diferentes caixas de correio de registro no diário para diferentes regras de diário ou conjuntos dessas regras.


> [!IMPORTANT]
> Não é possível designar uma caixa de correio do Office 365 como uma caixa de correio de registro no diário. Você pode enviar os relatórios do diário para um sistema de arquivamento local ou um serviço de arquivamento de terceiros. Se estiver executando uma implantação híbrida com suas caixas de correio divididas entre servidores locais e o Office 365, você poderá designar uma caixa de correio local como a caixa de correio de registro no diário para suas caixas de correio do Office 365 e caixas de correio locais.




> [!IMPORTANT]
> As caixas de correio de diário contêm informações confidenciais. Deve-se proteger as caixas de correio de diário porque elas coletam mensagens que são enviadas para e de destinatários em sua organização. Essas mensagens podem fazer parte de procedimentos legais ou podem estar sujeitas a requisitos de regulamentação. Várias leis exigem que as mensagens permaneçam invioláveis antes de serem submetidas a uma autoridade investigadora. Recomendamos que crie diretivas que controlem quem pode acessar as caixas de correio de diário em sua organização, limitando o acesso a apenas aqueles indivíduos com necessidade direta de acessá-las. Converse com seus representantes legais para verificar se sua solução de registro no diário está em conformidade com todas as leis e regulamentações aplicáveis à sua organização.




> [!IMPORTANT]
> Caixas de correio de registro no diário devem aceitar mensagens até um tamanho igual ou maior que o tamanho máximo da mensagem que você definiu em sua organização. Se você tiver configurado exceções à MaxSendSize e MaxReceiveSize na caixa de correio de um usuário individual que são maiores do que a definição geral do TransportConfig, você deve definir a caixa de correio de registro no diário MaxSendSize e MaxReceiveSize adequadamente para garantir Se as mensagens enviadas para o registro no diário e não colocados na fila rejeitadas ou aceitos. Mensagens rejeitadas pela caixa de correio de registro no diário serão repetidas periodicamente, fazendo com que o crescimento do banco de dados desnecessárias e desperdício de recursos. Além disso, é recomendável que você configure uma caixa de correio de registro no diário alternativa para impedir que outras situações não entregues ocorra.



## Caixa de correio de registro no diário alternativa

Quando a caixa de correio de registro no diário não estiver disponível, não é recomendável que os relatórios de registro no diário que não puderam ser entregues coletem as filas de emails nos servidores Caixa de Correio. Em vez disso, você pode configurar uma caixa de correio de registro no diário alternativa para armazenar esses relatórios de diário. A caixa de correio de registro no diário alternativa recebe os relatórios de diário como anexos nas notificações de falha na entrega (NDRs) geradas quando a caixa de correio de diário ou o servidor em que ela está localizada recusar a entrega do relatório de diário ou ficar indisponível.

Quando a caixa de correio de registro no diário ficar disponível novamente, você poderá usar o recurso **Enviar Novamente** do Office Outlook para enviar os relatórios do diário para entrega à caixa de correio de registro no diário.

Quando você configura uma caixa de correio de registro no diário alternativa, todos os relatórios do diário que são rejeitados ou não podem ser entregues em toda a organização do Exchange são entregues à caixa de correio de registro no diário alternativa. Portanto, é importante verificar se a caixa de correio de registro no diário alternativa e o servidor de caixa de correio onde ela está localizada podem oferecer suporte a muitos relatórios de diário.


> [!CAUTION]
> Se você configurar uma caixa de correio de registro no diário alternativa, será preciso monitorar a caixa de correio para garantir que ela não fique indisponível ao mesmo tempo que as caixas de correio do diário. Se a caixa de correio de registro no diário alternativa ficar indisponível e rejeitar relatórios de diário, os relatórios de diário rejeitados serão perdidos e não poderão ser recuperados.



Como a caixa de correio de registro no diário alternativa coleta todos os relatórios de diário rejeitados de toda a organização do Exchange, você deve verificar se isso não viola nenhuma lei ou regulamentação que se aplique à sua organização. Se houver leis ou regulamentações que proíbam sua organização de permitir que relatórios de diário enviados a caixas de correio de registro no diário diferentes sejam armazenados na mesma caixa de correio de registro no diário alternativa, talvez você não possa configurar uma caixa de correio de registro no diário alternativa. Discuta o assunto com seus representantes legais para determinar se você pode usar uma caixa de correio de registro no diário alternativa.

Ao configurar a caixa de correio de registro no diário alternativa, você deverá usar os mesmos critérios que usou para configurar a caixa de correio de registro no diário.


> [!IMPORTANT]
> A caixa de correio de registro no diário alternativa deve ser tratada como uma caixa de correio dedicada especial. Nenhuma das mensagens endereçadas diretamente à caixa de correio de registro no diário alternativa é registrada no diário.



Voltar ao início

## Replicação de regra de registro no diário

As regras de registro no diário são armazenadas no Active Directory e aplicadas a todos os servidores de Caixa de Correio na organização do Exchange 2013. Quando você cria, modifica ou remove uma regra de registro no diário, a alteração é replicada para todos os servidores do Active Directory na organização. Todos os servidores de Caixa de Correio na organização podem recuperar a configuração da regra de registro no diário atualizada dos servidores do Active Directory e aplicá-la às regras novas ou modificadas de registro no diário.

Ao replicar todas as regras de diário na organização, o Exchange 2013 permite que você forneça um conjunto consistente de regras de diário para a organização. Todas as mensagens que passam pela sua organização do Exchange 2013 estão sujeitas às mesmas regras de diário.


> [!IMPORTANT]
> Replicação de regras de diário em uma organização é dependente Active Directory replicação. Tempo de replicação entre os controladores de domínio Active Directory varia dependendo do número de sites na organização e a velocidade dos links e outros fatores fora do controle de Microsoft Exchange. Quando você implementa as regras de diário em sua organização, considere os atrasos de replicação. Para obter mais informações sobre a replicação Active Directory, consulte <A href="https://go.microsoft.com/fwlink/?linkid=274904">Introdução ao gerenciamento de topologia usando o Windows PowerShell e de replicação do Active Directory</A>.




> [!IMPORTANT]
> Cada servidor de Caixa de Correio guarda, no cache, a associação ao grupo de distribuição, para evitar repetidas viagens de ida e volta ao Active Directory. O cache de grupos expandidos reduz o número de solicitações que cada servidor de Caixa de Correio deve fazer a um controlador de domínio do Active Directory. Por padrão, as entradas no cache de grupos expandido expiram em quatro horas. Assim, se você especificar um grupo de distribuição como o destinatário do registro no diário, as alterações na associação no grupo de distribuição podem não serem aplicadas às regras de registro no diário até que o cache dos grupos expandidos esteja atualizado. Para forçar uma atualização imediata do cache do destinatário, você deve interromper e iniciar o serviço de Transporte do Microsoft Exchange. Isso deve ser feito em cada servidor de Caixa de Correio em que você deseja forçar a atualização do cache do destinatário.



Voltar ao início

## Relatórios de diário

O *relatório de registro no diário* é a mensagem que o agente de Registro no diário gera quando uma mensagem corresponde a uma regra de registro no diário e deve ser enviada à caixa de correio de Registro no diário. A mensagem original que corresponde à regra de registro no diário é incluída inalterada como um anexo ao relatório de registro no diário. O corpo de um relatório de registro no diário contém informações da mensagem original, como o endereço de email do remetente, o assunto da mensagem, a ID da mensagem e os endereços de email de destinatário. Isso também é chamado de registro no diário do NOTEo envelope e é o único método de registro no diário suportado pelos Exchange 2013.

## Relatórios de registro no diário e mensagens protegidas por IRM

Ao implantar o registro no diário em um ambiente do Exchange 2013, você deve considerar os relatórios de registro no diário e mensagens protegidas por IRM. As mensagens protegidas por IRM irão afetar os recursos de pesquisa e descoberta de sistemas de arquivamento de terceiros que não tenham suporte RMS integrado. No Exchange 2013, você pode configurar a Descriptografia de Relatório de Registro no Diário, para salvar uma cópia em texto não-criptografado da mensagem no relatório de registro no diário.

Voltar ao início

## Interoperabilidade com o Exchange 2007

Não há muita diferença entre a funcionalidade de registro no diário no Exchange 2013, Exchange 2010 e Exchange 2007. No entanto, em Exchange 2010 e posterior, a instalação cria um contêiner separado no Active Directory para armazenar as regras de diário. Quando você configura o primeiro Exchange 2010 ou posterior server em uma organização Exchange 2007, a instalação cria uma cópia das regras de diário existente em Exchange 2007 e armazenando-as no novo contêiner. Quando terminar a instalação, as regras de diário em ambas as versões do Exchange são consistentes.

Após a instalação, se você alterar a configuração da regra de diário no Exchange 2010 (ou posterior), você deve fazer a mesma alteração nos servidores de Exchange 2007 para certificar-se de que eles estão consistentes. Da mesma forma, as alterações feitas em diário regras em Exchange 2007 devem ser também ser feitas no Exchange 2010 ou posterior. Você também pode exportar regras de diário do Exchange 2007 e importá-los para Exchange 2013.

Voltar ao início

## Solução de problemas

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).. Se você estiver tendo problemas com a caixa de correio **JournalingReportDNRTo**, consulte [transporte e regras de caixa de correio no Exchange Online não funcionam conforme o esperado](https://go.microsoft.com/fwlink/p/?linkid=331674).

