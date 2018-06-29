---
title: 'Gerenciar diário: Exchange 2013 Help'
TOCTitle: Gerenciar diário
ms:assetid: d517f27e-f80a-4a06-988c-cbbf981c701d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ651670(v=EXCHG.150)
ms:contentKeyID: 50486717
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar diário

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Registro no diário pode ajudar sua organização a atender aos requisitos de conformidade legais, normativos e organizacionais Registrando as comunicações de email de entrada e saída. Este tópico mostra como executar tarefas básicas relacionadas ao gerenciamento de registro no diário em Exchange 2013 e Exchange Online.

O registro padrão no diário é configurado em um banco de dados de caixa de correio. Ele permite que o agente de registro no diário registre todas as mensagens envias de e para caixas de correio localizadas em um banco de dados de caixa de correio específico. Você pode também usar o registro premium no diário, que permite que o agente de registro no diário execute um registro mais granular, usando as regras de registro no diário. Em vez de registrar no diário todas as caixas de correio de um banco de dados, você pode configurar as regras de registro no diário para que combinem com as necessidades de sua organização de registrar no diário destinatários individuais ou membros de grupos de distribuição. Para usar o registro no diário premium, você deve ter uma CAL (Licença de Acesso para Cliente) do Exchange Enterprise.

Para saber mais sobre registro no diário, consulte [Registro no Diário](journaling-exchange-2013-help.md).

**Conteúdo**

Criar uma regra de diário

Exibir ou modificar uma regra de diário

Habilitar ou desabilitar uma regra de diário

Remover uma regra de diário

Habilitar ou desabilitar o registro no diário de banco de dados por caixa de correio

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Registro em diário" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Uma caixa de correio de registro no diário foi criada ou uma caixa de correio existente está disponível para uso da caixa de correio de registro no diário. Você não pode designar uma caixa de correio Exchange Online como uma caixa de correio de registro no diário. Você pode enviar relatórios de diário para um local arquivamento sistema ou um serviço de arquivamento de terceiros. Se você estiver executando uma implantação híbrida com suas caixas de correio divididos entre os servidores locais e Exchange Online, você pode designar uma caixa de correio local da caixa de correio de registro no diário para suas caixas de correio Exchange Online e no local.
    

    > [!IMPORTANT]
    > Se você configurou uma regra de diário em Exchange Online para enviar que relatórios de diário de uma caixa de correio de registro no diário que não existe ou é um destino inválido, o relatório de diário permanece na fila de transporte em servidores de datacenter da Microsoft. Se isso acontecer, a equipe de datacenter Microsoft tentará entre em contato com a sua organização e pedir que você corrigir o problema para que os relatórios de diário podem ser entregue com êxito uma caixa de correio de registro no diário. Se você ainda não resolvido o problema após dois dias de sendo contatado, Microsoft desabilitará a regra de diário problemáticos.



  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>. Se você estiver tendo problemas com a caixa de correio <STRONG>JournalingReportDNRTo</STRONG>, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=331674">transporte e regras de caixa de correio no Exchange Online não funcionam conforme o esperado</A>.



## Criar uma regra de diário

## Utilize o EAC para criar uma regra de diário

1.  No EAC, vá para **gerenciamento de conformidade** \> **regras de diário** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Em **Regra de diário**, forneça um nome para a regra de diário e preencha os seguintes campos:
    
      - **Se a mensagem for enviada para ou recebida de**   Especifique o destinatário ao qual a regra se destinará. Você pode selecionar um destinatário específico ou aplicar a regra a todas as mensagens.
    
      - **Registrar em diário as seguintes mensagens**   Especifique o escopo de regra de diário. Você pode registrar no diário somente as mensagens internas, somente as mensagens externas ou todas as mensagens, independentemente da origem ou do destino.
    
      - **Enviar relatórios de registro em diário para**   Digite o endereço da caixa de correio de registro no diário que receberá todos os relatórios de diário.
        

        > [!TIP]
        > Você também pode digitar o nome para exibição ou o alias de um usuário de email ou um contato de email da caixa de correio de diário. Nesse caso, relatórios de diário serão enviados para o endereço de email externo do contato de email ou de usuário de email. Mas, conforme explicado anteriormente, o endereço de email externo de um contato de email ou de usuário de email não pode ser o endereço de uma caixa de correio Exchange Online.



3.  Clique em **Salvar**, para criar a regra de diário.

## Utilize o Shell para criar uma regra de diário

Este exemplo cria a regra de diário Destinatários de Diário de Descoberta para registrar no diário todas as mensagens enviadas e recebidas pelo destinatário user1@contoso.com.

    New-JournalRule -Name "Discovery Journal Recipients" -Recipient user1@contoso.com -JournalEmailAddress "Journal Mailbox" -Scope Global -Enabled $True

## Como saber se funcionou?

Para verificar se você criou com êxito a regra de diário, faça o seguinte:

  - No EAC, verifique se a nova regra de diário criada aparece na guia **Regras de diário**.

  - No Shell, verifique se a nova regra de diário existe executando o seguinte comando (o exemplo abaixo verifica a regra criada no exemplo de Shell acima):
    
        Get-JournalRule "Discovery Journal Recipients"

Voltar ao início

## Exibir ou modificar uma regra de diário

## Use o EAC para exibir ou modificar uma regra de diário

1.  No EAC, vá até **gerenciamento de conformidade** \> **regras de diário**.

2.  Na exibição de lista, você verá todas as regras de diário em sua organização.

3.  Clique duas vezes na regra que você deseja exibir ou modificar.

4.  Em **Regra de diário**, modifique as configurações desejadas. Para obter mais informações sobre as configurações nessa caixa de diálogo, consulte o procedimento Use the EAC to create a journal rule neste tópico.

## Use o Shell para exibir ou modificar uma regra de diário

Esse exemplo exibe uma lista resumida de todas as regras de diário da organização do Exchange:

    Get-JournalRule

Esse exemplo recupera a regra de diário Brokerage Journal Rule e transmite a saída para o comando **Format-List**, para exibir propriedades de regra em formato de lista:

    Get-JournalRule "Brokerage Journal Rule" | Format-List

Se você deseja modificar as propriedades de uma regra específica, será necessário usar o cmdlet [Set-JournalRule](https://technet.microsoft.com/pt-br/library/bb125010\(v=exchg.150\)). Esse exemplo altera o nome da regra de diário `JR-Sales` para `TraderVault`. As configurações de regra a seguir também são alteradas:

  - Destinatário

  - JournalEmailAddress

  - Escopo

<!-- end list -->

    Set-JournalRule JR-Sales -Name TraderVault -Recipient traders@woodgrovebank.com -JournalEmailAddress tradervault@woodgrovebank.com -Scope Internal

## Como saber se funcionou?

Para verificar se você modificou com êxito uma regra de diário, faça o seguinte:

  - No EAC, navegue até **Gerenciamento de Conformidade** \> **Regras de diário**. Clique duas vezes na regra que você modificou e verifique se as alterações foram salvas.

  - No Shell, verifique se você modificou a regra de diário com êxito executando o seguinte comando. Este comando listará as propriedades modificadas junto com o nome da regra (o exemplo abaixo verifica a regra modificada no exemplo de Shell acima):
    
        Get-TransportRule "TraderVault" | Format-List Name,Recipient,JournalEmailAddress,Scope

Voltar ao início

## Habilitar ou desabilitar uma regra de diário


> [!IMPORTANT]
> Quando você desabilita uma regra de diário, o agente de registro no diário interromperá o registro no diário das mensagens direcionadas por essa regra. Enquanto uma regra de diário estiver desabilitada, todas as mensagens que seriam normalmente registradas no diário pela regra não são registradas. Certifique-se de não comprometer os requisitos regulamentares ou de conformidade de sua organização desabilitando uma regra de registro no diário.



## Usar o EAC para habilitar ou desabilitar uma regra de diário

1.  No EAC, vá até **gerenciamento de conformidade** \> **regras de diário**.

2.  Na exibição de lista, na coluna **Habilitar** ao lado do nome da Regra, marque a caixa de seleção para habilitar a regra ou desmarque-a para desabilitá-la.

## Use o shell para habilitar ou desabilitar uma regra de diário

Este exemplo habilita a regra Contoso.

    Enable-JournalRule "Contoso Journal Rule"

Este exemplo desabilita a regra Contoso.

    Disable-JournalRule "Contoso Journal Rule"

## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou com êxito uma regra de diário, faça o seguinte:

  - No EAC, exiba a lista das regras de diário e verifique o status da caixa de seleção na coluna **Habilitar**.

  - No Shell, execute o seguinte comando para retornar uma lista de todas as regras de diário de sua organização, incluindo seu status:
    
        Get-JournalRule | Format-Table Name,Enabled

Voltar ao início

## Remover uma regra de diário

## Usar o EAC para remover uma regra de diário

1.  No EAC, vá até **gerenciamento de conformidade** \> **regras de diário**.

2.  No modo de exibição de lista, selecione a regra que você deseja remover e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

## Utilizar o Shell para remover uma regra de diário

Este exemplo remove a regra de diário Brokerage da regra.

    Remove-JournalRule "Brokerage Journal Rule"

## Como saber se funcionou?

Para verificar se você removeu com êxito a regra de diário, faça o seguinte:

  - No EAC, verifique se a regra removida não aparece mais na guia **Regras de diário**.

  - No Shell, execute o seguinte comando para verificar se a regra removida não aparece mais:
    
        Get-JournalRule

Voltar ao início

## Habilitar ou desabilitar o registro no diário do banco de dados por caixa de correio


> [!WARNING]
> A desabilitação do registro em diário de mensagem em um banco de dados de caixa de correio pode resultar na falta de conformidade da organização com qualquer diretiva de retenção do sistema de mensagens aplicável. Quando você desabilita o registro em diário de mensagem em um banco de dados de caixa de correio, os recibos de diário deixam de ser enviados ou recebidos por caixas de correio nesse banco de dados de caixa de correio.



## Usar o EAC para habilitar ou desabilitar o registro em diário de banco de dados por caixa de correio

1.  Na EAC, vá até **Servidores** \> **Bancos de dados**.

2.  Na exibição de lista, clique duas vezes no banco de dados de caixa de correio para o qual deseja habilitar o registro no diário.

3.  Clique em **Manutenção** e clique em **Procurar** ao lado da caixa **Destinatário do Diário** para selecionar a caixa de correio de registro no diário. Especificar um destinatário de diário permite o registro no diário do banco de dados.
    
    Para desabilitar o registro no diário, remova o destinatário do diário clicando em **Remover X**.

## Usar o Shell para habilitar ou desabilitar o registro no diário de banco de dados por caixa de correio

Este exemplo habilita o registro em diário do banco de dados de caixa de correio Banco de Dados de Vendas e define a caixa de correio de diário do Banco de Dados de Vendas como o destinatário do diário.

    Set-MailboxDatabase "Sales Database" -JournalRecipient "Sales Database Journal Mailbox"

Este exemplo desabilita o registro em diário de banco de dados por caixa de correio no banco de dados de caixa de correio Sales Database.

    Set-MailboxDatabase "Sales Database" -JournalRecipient $Null

Este exemplo desabilita o registro em diário de banco de dados por caixa de correio em todos os bancos de dados de caixa de correio na organização do Exchange. O cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb124924\(v=exchg.150\)) é usado para recuperar todos os bancos de dados de caixa de correio na organização do Exchange e os resultados do cmdlet são redirecionados para o cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb123971\(v=exchg.150\)).

    Get-MailboxDatabase | Set-MailboxDatabase -JournalRecipient $Null

## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou com êxito o registro no diário de banco de dados por caixa de correio, faça o seguinte:

1.  Na EAC, vá até **Servidores** \> **Bancos de dados**.

2.  Clique duas vezes no banco de dados que deseja verificar e selecione a guia **Manutenção**.

3.  Se o destinatário de registro no diário correto estiver listado na caixa **Destinatário do Diário**, você terá habilitado com êxito o registro no diário para o banco de dados de caixa de correio. Se não houver nenhum destinatário de registro no diário listado, o registro no diário será desabilitado para o banco de dados.

<!-- end list -->

  - No Shell, execute o seguinte comando para retornar uma lista de todas as regras de diário de sua organização, incluindo seu status: O registro no diário é habilitado para bancos de dados com um destinatário de diário listado, caso contrário, será desabilitado.
    
        Get-MailboxDatabase | Format-Table Name,JournalRecipient

Voltar ao início

## Para obter mais informações

[Registro no Diário](journaling-exchange-2013-help.md)

[Desabilitar ou habilitar o registro no diário de notificações de chamada perdida e caixa postal](disable-or-enable-journaling-of-voice-mail-and-missed-call-notifications-exchange-2013-help.md)

[New-JournalRule](https://technet.microsoft.com/pt-br/library/bb125242\(v=exchg.150\))

[Get-JournalRule](https://technet.microsoft.com/pt-br/library/aa998866\(v=exchg.150\))

[Set-JournalRule](https://technet.microsoft.com/pt-br/library/bb125010\(v=exchg.150\))

[Enable-JournalRule](https://technet.microsoft.com/pt-br/library/bb123902\(v=exchg.150\))

[Disable-JournalRule](https://technet.microsoft.com/pt-br/library/aa995925\(v=exchg.150\))

[Remove-JournalRule](https://technet.microsoft.com/pt-br/library/bb123489\(v=exchg.150\))

[Set-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb123971\(v=exchg.150\))

