---
title: 'Migrar de pastas gerenciadas: Exchange 2013 Help'
TOCTitle: Migrar de pastas gerenciadas
ms:assetid: 6796a79d-501e-4216-9370-77965bc5835d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298032(v=EXCHG.150)
ms:contentKeyID: 52058824
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Migrar de pastas gerenciadas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

No Microsoft Exchange Server 2013, o gerenciamento de registros de mensagem (MRM) é realizado usando marcas de retenção e políticas de retenção. Uma política de retenção é um grupo de marcas de retenção que pode ser aplicado a uma caixa de correio. Para mais detalhes, consulte [Marcas e políticas de retenção](retention-tags-and-retention-policies-exchange-2013-help.md). Pastas gerenciadas, que a tecnologia MRM introduziu no Exchange Server 2007, não são suportadas.

Uma caixa de correio que tenha uma diretiva de caixa de correio de pasta gerenciada aplicada pode ser migrada para usar uma diretiva de retenção. Para fazer isso, é preciso criar marcas de retenção equivalentes às pastas gerenciadas vinculadas à diretiva de caixa de correio de pasta gerenciada do usuário.


> [!IMPORTANT]
> Antes de você migrar de pastas gerenciadas para diretivas de retenção no seu ambiente de produção, recomendamos testar o processo em um ambiente de teste.




> [!TIP]
> Você pode colocar caixas de correio sob bloqueio local para interromper o processamento das políticas de retenção ou políticas de caixa de correio de pasta gerenciada. Colocar caixas de correio sob bloqueio local pode ser útil em cenários de migração para evitar excluir mensagens ou movê-las para o arquivo morto até que as configurações da nova política sejam testadas nas caixas de correio de teste ou num número pequeno caixas de correio em produção. Para obter detalhes, consulte <A href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">Retenção local de uma caixa de correio em retenção</A>.



Para mais tarefaas de gerenciamento relacionadas à MRM, veja [Procedimentos de gerenciamento de registros de mensagens](messaging-records-management-procedures-exchange-2013-help.md).

## Comparando marcas de retenção com pastas gerenciadas

Ao contrário das pastas gerenciadas, que exigem que os usuários movam os itens para elas com base nas configurações de retenção, marcas de retenção podem ser aplicadas a uma pasta ou item individual na caixa de correio. Este processo possui um impacto mínimo no fluxo de trabalho do usuário e nos métodos de organização de email. Quando uma pasta tem marcas de retenção aplicadas, todos os itens dessa pasta herdam as configurações de retenção. Os usuários podem especificar as configurações de retenção com a aplicação de diferentes marcas de retenção a itens individuais dessa pasta.

As pastas gerenciadas suportam diferentes configurações de conteúdo gerenciado para uma pasta, cada uma com uma classe diferente de mensagem (tais como itens de email ou itens de calendário). As marcas de retenção não exigem um objeto separado de configurações de conteúdo gerenciado porque as configurações de retenção estão especificadas nas propriedades da marca. Não há suporte para criar marcas de retenção para classes particulares de mensagem, com exceção de uma marca de política padrão (DPT) para mensagens da caixa postal. As marcas de retenção não permitem que você use o registro em diário realizado pelo Assistente de Pasta Gerenciada.


> [!TIP]
> As regras de diário, usadas para enviar cópias das mensagens com um relatório do diário para uma caixa de correio de registro em diário, são impostas no pipeline de transporte pelo agente de Registro em Diário e são independentes do MRM. Para mais detalhes, consulte <A href="journaling-exchange-2013-help.md">Registro no Diário</A>.



A seguinte tabela compara a funcionalidade de MRM disponível ao se usar marcas de retenção ou pastas gerenciadas.

### Marcas de retenção vs. pastas gerenciadas

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Funcionalidade</th>
<th>Marcas de retenção</th>
<th>Pastas gerenciadas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Especificam configurações de retenção para pastas padrão (como caixa de entrada)</p></td>
<td><p>Usam marcas de diretiva de retenção (RPTs)</p></td>
<td><p>Usam pastas padrão gerenciadas</p></td>
</tr>
<tr class="even">
<td><p>Especificam configurações de retenção para toda a caixa de correio</p></td>
<td><p>Usam uma marca de diretiva padrão (DPT)</p></td>
<td><p>Use as pastas gerenciadas padrões</p></td>
</tr>
<tr class="odd">
<td><p>Usam configurações de retenção para pastas personalizadas</p></td>
<td><p>Usam marcas pessoais</p></td>
<td><p>Usando pastas personalizadas gerenciadas</p></td>
</tr>
<tr class="even">
<td><p>Exigem configurações de conteúdo gerenciado</p></td>
<td><p>Não (configurações de retenção incluídas em uma marca de retenção)</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Usam configurações de retenção para diferentes classes de mensagem (como mensagens de email, caixa postal ou itens de calendário)</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Oferecem suporte à ação Mover para arquivo morto, que move uma mensagem para a caixa de correio de arquivo morto do usuário.</p></td>
<td><p>Sim</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>Oferecem suporte à ação Mover para pasta gerenciada</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Permitem registro no diário usando o Assistente de pasta gerenciada</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Diretiva aplicada a usuário</p></td>
<td><p>Diretiva de retenção</p></td>
<td><p>Diretiva de caixa de correio de pasta gerenciada</p></td>
</tr>
<tr class="even">
<td><p>Número máximo de diretivas que podem ser aplicadas a um usuário de caixa de correio</p></td>
<td><p>1</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>Processado pelo Assistente de pasta gerenciada</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Suporte ao cliente</p></td>
<td><p>Microsoft Outlook 2010 e</p></td>
<td><p>Outlook 2010, Office Outlook 2007 e Outlook Web App</p></td>
</tr>
</tbody>
</table>


## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 20 minutos.

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - Você não pode usar o centro de administração do Exchange (EAC) para criar marcas de retenção com base em políticas de retenção.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Migrar usuários da caixa de correio a partir das pastas gerenciadas

Na sequência, são apresentadas etapas gerais para migrar usuários dessa diretiva de caixa de correio de pasta gerenciada para uma diretiva de retenção. Esta etapa é detalhada posteriormente neste tópico:

1.  Colete informações sobre diretivas de caixa de correio de pasta gerenciada aplicada a todas as caixas de correio de Exchange 2010 e Exchange 2007, pastas em cada diretiva gerenciadas e configurações de conteúdo para cada pasta gerenciada gerenciado. Você pode usar o EMC ou o Shell em um servidor Exchange 2010 ou Exchange 2007 obter essas informações.

2.  Crie marcas de retenção para a migração.

3.  Crie uma diretiva de retenção e vincule as marcas de retenção recém-criadas à diretiva.

4.  Remova a política de caixa de correio de pasta gerenciada e depois aplique a política de retenção para as caixas de correio do usuário.
    

    > [!IMPORTANT]
    > Após você aplicar uma diretiva de retenção a um usuário e o Assistente de Pasta Gerenciada ser executado, as pastas gerenciadas na caixa de correio do usuário se tornarão não gerenciadas.



Para os próximos procedimentos, as caixas de correio da Contoso têm uma diretiva de caixa de correio de pasta gerenciada aplicada contendo as seguintes pastas gerenciadas.

### Pastas gerenciadas para Contoso

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Pasta gerenciada</th>
<th>Configurações de conteúdo gerenciado</th>
<th>Retenção habilitada</th>
<th>Tempo de retenção</th>
<th>Ação de retenção</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Corp-DeletedItems</p></td>
<td><p>CS-Corp-DeletedItems</p></td>
<td><p>Sim</p></td>
<td><p>30 dias</p></td>
<td><p>Excluir e Permitir Recuperação</p></td>
</tr>
<tr class="even">
<td><p>Corp-SentItems</p></td>
<td><p>CS-Corp-SentItems</p></td>
<td><p>Sim</p></td>
<td><p>1.825 dias</p></td>
<td><p>Mover para Itens Excluídos</p></td>
</tr>
<tr class="odd">
<td><p>Corp-JunkMail</p></td>
<td><p>CS-Corp-JunkMail</p></td>
<td><p>Sim</p></td>
<td><p>30 dias</p></td>
<td><p>Excluir Permanentemente</p></td>
</tr>
<tr class="even">
<td><p>Corp-EntireMailbox</p></td>
<td><p>CS-Corp-EntireMailbox</p></td>
<td><p>Sim</p></td>
<td><p>365 dias</p></td>
<td><p>Mover para Itens Excluídos</p></td>
</tr>
<tr class="odd">
<td><p>30 dias</p></td>
<td><p>CS-30Days</p></td>
<td><p>Sim</p></td>
<td><p>30 dias</p></td>
<td><p>Mover para Itens Excluídos</p></td>
</tr>
<tr class="even">
<td><p>5 anos</p></td>
<td><p>CS-5Years</p></td>
<td><p>Sim</p></td>
<td><p>1.825 dias</p></td>
<td><p>Mover para Itens Excluídos</p></td>
</tr>
<tr class="odd">
<td><p>Nunca expirar</p></td>
<td><p>CS-NeverExpire</p></td>
<td><p>Não</p></td>
<td><p>365 dias</p></td>
<td><p>Não se aplica</p></td>
</tr>
</tbody>
</table>


## Como fazer isso?

## Etapa 1: Criar marcas de retenção para a migração

Entrada "Gerenciamento de registros de mensagem", no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Há dois métodos que você pode usar para esta etapa:

  - **Criar marcas de retenção com base nas pastas gerenciadas e suas configurações de conteúdos gerenciados**   Com este método, você usa o cmdlet **New-RetentionPolicyTag** com o parâmetro *ManagedFolderToUpgrade* . Quando você especifica esse parâmetro, a marca de retenção correspondente é aplicada automaticamente à pasta gerenciada.
    

    > [!IMPORTANT]
    > Se a pasta gerenciada para a qual você deseja fazer a portabilidade possuir várias configurações de conteúdo gerenciado para diferentes classes de mensagem, apenas uma marca de retenção é criada e o maior tempo de retenção de todas as configurações de conteúdo gerenciado é usado como o tempo de retenção para a marca para a qual foi feita a portabilidade, independente da classe da mensagem das configurações de conteúdo gerenciado.<BR>Por exemplo, analise as configurações de conteúdo gerenciado a seguir para a pasta gerenciada Corp-DeletedItems.



  - **Criar marcas de retenção especificando manualmente as configurações de retenção**   Com este método, você usa o cmdlet **New-RetentionPolicyTag** sem o parâmetro *ManagedFolderToUpgrade* . Quando esse parâmetro não é especificado, qualquer marca de diretiva de retenção adicionada à política é aplicada às pastas padrão, e a marca de diretiva padrão é aplicada a toda a caixa de correio. Entretanto, qualquer marca pessoal adicionada à diretiva não é aplicada automaticamente às pastas gerenciadas.


> [!TIP]
> Se você estiver em um ambiente misto com servidores Exchange 2013 e Exchange 2010, você pode usar o Assistente de <STRONG>Pasta gerenciada de porta</STRONG> no Console de gerenciamento do Exchange (EMC) em um servidor de Exchange 2010 para facilmente porta de pasta gerenciada e correspondente gerenciado a configuração de conteúdo para marcas de retenção.



**Criar marcas de retenção com base em pastas gerenciadas**

Este exemplo cria marcas de retenção com base nas configurações de conteúdo gerenciado correspondentes mostradas na diretiva de caixa de correio de pasta gerenciada da Contoso.

    New-RetentionPolicyTag Corp-DeletedItems -ManagedFolderToUpgrade Corp-DeletedItems
    New-RetentionPolicyTag Corp-SentItems -ManagedFolderToUpgrade Corp-SentItems
    New-RetentionPolicyTag Corp-JunkMail -ManagedFolderToUpgrade Corp-JunkMail
    New-RetentionPolicyTag Corp-EntireMailbox -ManagedFolderToUpgrade Corp-EntireMailbox
    New-RetentionPolicyTag 30Days -ManagedFolderToUpgrade 30Days
    New-RetentionPolicyTag 5Years -ManagedFolderToUpgrade 5Years
    New-RetentionPolicyTag NeverExpire -ManagedFolderToUpgrade NeverExpire

Para obter informações detalhadas de sintaxes e parâmetros, consulte [New-RetentionPolicyTag](https://technet.microsoft.com/pt-br/library/dd335226\(v=exchg.150\)).

**Criar marcas de retenção manualmente**


> [!TIP]
> Você pode usar o EAC também para criar marcas de retenção manualmente (sem ser baseado nas configurações em pastas gerenciadas). Para obter detalhes, consulte <A href="create-a-retention-policy-exchange-2013-help.md">Criar uma política de retenção</A>.



Este exemplo cria marcas de retenção com base nas pastas gerenciadas e nas configurações de conteúdo gerenciado correspondentes mostradas na diretiva de caixa de correio de pasta gerenciada da Contoso. As configurações de retenção são especificadas manualmente sem o uso do parâmetro *ManagedFolderToUpgrade*.

    New-RetentionPolicyTag Corp-DeletedItems -Type DeletedItems -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction DeleteAndAllowRecovery
    New-RetentionPolicyTag Corp-SentItems -Type SentItems -RetentionEnabled $true -AgeLimitforRetention 1825 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag Corp-JunkMail -Type JunkMail -RetentionEnabled $true -AgeLimitforRetention 30 -RetentionAction PermanentlyDelete
    New-RetentionPolicyTag Corp-EntireMailbox -Type All -RetentionEnabled $true -AgeLimitForRetention 365 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag 30Days -Type Personal -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag 5Years -Type Personal -RetentionEnabled $true -AgeLimitForRetention 1825 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag NeverExpire -Type Personal -RetentionEnabled $false

Para obter informações detalhadas de sintaxes e parâmetros, consulte [New-RetentionPolicyTag](https://technet.microsoft.com/pt-br/library/dd335226\(v=exchg.150\)).

## Etapa 2: Criar uma diretiva de retenção

Entrada "Gerenciamento de registros de mensagem", no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!TIP]
> Você também pode usar o EAC para criar uma política de retenção e adicionar marcas de retenção à política. Para obter detalhes, consulte <A href="create-a-retention-policy-exchange-2013-help.md">Criar uma política de retenção</A>.



Este exemplo cria uma diretiva de retenção RP-Corp e vincula as marcas de retenção recém-criadas à diretiva.

    New-RetentionPolicy RP-Corp -RetentionPolicyTagLinks Corp-DeletedItems,Corp-SentItems,Corp-JunkMail,Corp-EntireMailbox,30Days,NeverExpire

Para obter informações detalhadas de sintaxes e parâmetros, consulte [New-RetentionPolicy](https://technet.microsoft.com/pt-br/library/dd297970\(v=exchg.150\)).

## Etapa 3: Remova a política de caixa de correio de pasta gerenciada das caixas de correio do usuário

Entrada "Aplicando políticas de retenção", no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Este exemplo remove a politica da caixa de correio de pasta gerenciada e qualquer pasta da caixa de correio de Ken Kwok. Pastas gerenciadas que possuem qualquer mensagem não são removidas.

    Set-Mailbox -Identity Kwok -RemoveManagedFolderAndPolicy RP-Corp

## Etapa 4: Aplicar a diretiva de retenção a caixas de correio do usuário

Entrada "Aplicando políticas de retenção", no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!TIP]
> Você também pode usar o EAC para aplicar uma política de retenção para os usuários. Para obter detalhes, consulte <A href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">Aplicar uma política de retenção a caixas de correio</A>.



Este exemplo aplica a diretiva de retenção recém-criada RP-Corp à caixa de correio do usuário Ken Kwok.

    Set-Mailbox -Identity Kwok -RetentionPolicy RP-Corp

Para obter informações detalhadas de sintaxes e parâmetros, consulte [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Como saber se essa tarefa funcionou?

Para verificar se você migrou de pastas gerenciadas para políticas de retenção, faça o seguinte;

  - Gere um relatório de todas as caixas de correio de usuário e da política de retenção aplicada aos mesmos.
    
    Este comando recupera a política de retenção aplicada a todas as caixas de correio em uma organização e o status de retenção.
    
        Get-Mailbox -ResultSize unlimited -Filter {Name -NotLike "DiscoverySearch*�?} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto

  - Após o Assitente de Pasta Gerenciada ter processado uma caixa de correio com uma política de retenção, use o cmdlet [Get-RetentionPolicyTag](https://technet.microsoft.com/pt-br/library/dd298009\(v=exchg.150\)) para recuperar as marcas de retenção provisionadas na caixa de correio do usuário.
    
    Este comando reccupera as marcas de retenção efetivamente aplicadas na caixa de coreeio de April Stewart.
    
        Get-RetentionPolicyTag -Mailbox astewart

