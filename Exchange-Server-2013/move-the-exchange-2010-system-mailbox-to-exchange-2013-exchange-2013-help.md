---
title: 'Mover a caixa de correio de sistema do Exchange 2010 para o Exchange 2013'
TOCTitle: Mover a caixa de correio de sistema do Exchange 2010 para o Exchange 2013
ms:assetid: a3b03c4e-0bc7-41a2-885c-e9cac37566c8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn249849(v=EXCHG.150)
ms:contentKeyID: 54913446
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mover a caixa de correio de sistema do Exchange 2010 para o Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Em Exchange 2010, a caixa de correio do sistema é uma caixa de correio de arbitragem usada para armazenar dados de toda a organização, como logs, metadados para pesquisas de descoberta eletrônica e dados Unificação de mensagens, como menus, de auditoria do administrador do Microsoft Exchange planos de discagem e saudações personalizadas. A caixa de correio de sistema do Microsoft Exchange é denominada **SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}**; o nome para exibição é **Microsoft Exchange**.

Quando você atualiza sua organização existente do Exchange 2010 para Exchange 2013, você precisa mover a caixa de correio de sistema do Microsoft Exchange para um banco de dados de caixa de correio em um servidor de caixa de correio Exchange 2013. Você deve mover esta caixa de correio depois de instalado e verificado Exchange 2013. Se você não mover esta caixa de correio do sistema para Exchange 2013, os seguintes problemas ocorrerá quando Exchange 2010 e Exchange 2013 coexistirem em sua organização do Exchange:

  - Exchange 2013 as tarefas não são salvas para o log de auditoria do administrador. Quando você executa o cmdlet **Search-AdminAuditLog** ou tenta exportar o log de auditoria do administrador no EAC, você receberá um erro que diz que você não pode criar uma pesquisa de log de auditoria do administrador porque a caixa de correio do sistema, SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}, está localizada em um servidor que não está executando o Exchange 2013. Um erro do Microsoft Exchange com uma ID de Evento de 5000 também é registrado no log dos Aplicativos do Windows cada vez que um comando é executado.

  - Não é possível executar pesquisas de descoberta eletrônica usando o EAC ou o Shell no Exchange 2013. Pesquisas de caixa de correio podem ser criadas e na fila, mas eles não podem ser iniciados. Um erro com uma identificação de evento de 6 é registrado no log de gerenciamento do MsExchange, indicando que o cmdlet **Start-MailboxSearch** falhou. No entanto, você pode pesquisar caixas de correio usando o Shell e o painel de controle do Exchange (ECP) em Exchange 2010.

Você também precisa mover a caixa de correio de sistema do Microsoft Exchange para Exchange 2013 como parte da atualização Exchange 2010 Unificação de mensagens para Exchange 2013.

Para mais informações sobre a atualização para o Exchange 2013, consulte os tópicos a seguir:

  - [Atualizar do Exchange 2010 para o Exchange 2013](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)

  - [Atualizar UM do Exchange 2010 para UM do Exchange 2013](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para finalização: 20 minutos. O tempo real pode variar dependendo do tamanho da caixa de correio do sistema.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada de "Movimentação de Caixa de Correio e Permissões de Migração" em [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Execute o comando a seguir no Exchange 2013 para obter a identidade e a versão dos servidores Exchange e dos bancos de dados da caixa de correio que contém as caixas de correio do sistema na sua organização.
    
        Get-Mailbox -Arbitration | FL Name,DisplayName,ServerName,Database,AdminDisplayVersion
    
    A propriedade **AdminDisplayVersion** indica a versão do Exchange que o servidor está executando. O valor `Version 14.x` indica Exchange 2010; o valor `Version 15.x` indica Exchange 2013.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o EAC para mover a caixa de correio do sistema

1.  No EAC, vá em **Destinatários** \> **Migração**.

2.  Clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"), e depois clique em **Mover para uma base de dados diferente**.

3.  Na página **Nova movimentação da caixa de correio local**, clique em **Selecione os usuários que você deseja mover**, e depois clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

4.  Na página **Selecionar Caixa de Correio** page, adicione a caixa de entrada que possui as seguintes propriedades:
    
      - O nome de exibição é **Microsoft Exchange**.
    
      - O alias do endereço de email da caixa de correio é **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}**.

5.  Clique em **OK**, e depois clique em **Avançar**.

6.  Na página **Configuração de movimentação**, digite o nome do lote de migração e depois clique em **Navegar** ao lado da caixa **Banco de dados de destino**.

7.  Na página **Selecionar banco de dados da Caixa de Correio**, adicione o banco de dados da caixa de correio para o qual será movida a caixa de correio do sistema. Verifique se a versão do banco de dados da caixa de correio que você selecionou é a Versão 15. x, o que indica que o banco de dados está localizado em um servidor do Exchange 2013.

8.  Clique em **OK**, e depois clique em **Avançar**.

9.  Na página **Inicie o lote**, selecione as opções de iniciar e finalizar automaticamente a solicitação de migração, e depois clique em **Novo**.

## Use o Shell para mover a caixa de correio do sistema

Primeiro execute o comando a seguir no Exchange 2013 para obter os nomes e as versões de todos os bancos de dados de caixa de correio na sua organização.

    Get-MailboxDatabase -IncludePreExchange2013 | FL Name,Server,AdminDisplayVersion

Após identificar o nome dos bancos de dados de caixa de correio na sua organização, execute o seguinte comando no Exchange 2013 para mover a caixa de correio do sistema do Microsoft Exchange para um banco de dados localizado em um servidor do Exchange 2013.

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | New-MoveRequest -TargetDatabase <name of Exchange 2013 database>

## Como saber se funcionou?

Para verificar se você moveu com sucesso a caixa de correio do sistema do Microsoft Exchange para um banco de dados de caixa de correio localizado no servidor Exchange 2013, execute o comando a seguir no Shell.

    Get-Mailbox -Arbitration -Identity "SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}" | FL Database,ServerName,AdminDisplayVersion

Se o valor da propriedade **AdminDisplayVersion** for **Versão 15.x (Compilação xxx.x)**, isto verifica se a caixa de correio do sistema reside em um banco de dados que está localizado em um servidor do Exchange 2013.

Após mover a caixa de correio do sistema do Microsoft Exchange para o Exchange 2013, você também será capaz de realizar com sucesso as seguintes tarefas administrativas:

  - Execute o cmdlet **Search-AdminAuditLog**.

  - Exporte o log de auditoria do administrador no EAC.

  - Crie com sucesso e inicie pesquisas de Descoberta Eletrônica usando o EAC ou o Shell no Exchange 2013.

