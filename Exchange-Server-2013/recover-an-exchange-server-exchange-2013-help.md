---
title: 'Recuperar um Exchange Server: Exchange 2013 Help'
TOCTitle: Recuperar um Exchange Server
ms:assetid: 46e9a1cf-b64c-43c3-a898-6171176da761
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876880(v=EXCHG.150)
ms:contentKeyID: 50485514
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recuperar um Exchange Server

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Você pode recuperar um servidor perdido usando a opção **Setup /m:RecoverServer** no Microsoft Exchange Server 2013. A maioria das configurações de um computador executando o Exchange 2013 são armazenadas no Active Directory. A opção */m:RecoverServer* reconstrói um servidor do Exchange com o mesmo nome usando as mesmas configurações e outras informações armazenadas no Active Directory.

A recuperação de um servidor do Exchange perdido frequentemente é realizada usando hardware novo. No entanto, você também pode usar um servidor existente.

Este tópico mostra como recuperar um servidor do Exchange 2013 perdido que não seja membro de um DAG (grupo de disponibilidade de banco de dados). Para instruções detalhadas sobre como recuperar um servidor que era membro de um DAG, consulte [Recuperar um servidor membro de grupo de disponibilidade de banco de dados](recover-a-database-availability-group-member-server-exchange-2013-help.md).


> [!TIP]
> Se o Exchange for instalado em um local que não o local padrão, você deverá usar a opção <EM>/TargetDir</EM> para especificar o local dos arquivos binários do Exchange. Se você não usar a opção <EM>/TargetDir</EM>, os arquivos do Exchange serão instalados no local padrão (%programfiles%\Microsoft\Exchange Server\V15).<BR>Para determinar o local de instalação, siga estas etapas: 
> <OL>
> <LI>
> <P>Abra o ADSIEDIT.MSC ou LDP.EXE.</P>
> <LI>
> <P>Navegue para o seguinte local: <STRONG>CN=ExServerName,CN=Servers,CN=First Administrative Group,CN=Administrative Groups,CN=ExOrg Name,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=DomainName,CN=Com</STRONG></P>
> <LI>
> <P>Clique com o botão direito no objeto do servidor Exchange e clique em <STRONG>Propriedades</STRONG>.</P>
> <LI>
> <P>Localize o atributo <STRONG>msExchInstallPath</STRONG>. Este atributo armazena o caminho de instalação atual.</P></LI></OL>



Procurando outras tarefas de gerenciamento relacionadas ao backup e à recuperação de dados? Consulte [Backup, restauração e recuperação de desastres](backup-restore-and-disaster-recovery-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 20 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de infraestrutura do Exchange" do tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - O servidor no qual a recuperação está sendo realizada deve estar executando o mesmo sistema operacional do servidor perdido. Por exemplo, você não pode recuperar um servidor que executava o Exchange 2013 e o Windows Server 2008 R2 em um servidor executando o Windows Server 2012, ou vice-versa. Da mesma forma, não é possível recuperar um servidor que estava executando o Exchange 2013 e o Windows Server 2012 em um servidor executando Windows Server 2012 R2, ou vice-versa.

  - As mesmas letras de unidade de disco no servidor com falha para bancos de dados montados devem existir no servidor em que você está executando a recuperação.

  - O servidor no qual a recuperação está sendo realizada deve ter as mesmas características de desempenho e configuração de hardware do servidor perdido.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Recuperar um Servidor do Exchange Perdido

1.  Redefina a conta de computador do servidor perdido. Para obter etapas detalhadas, consulte [Redefinir uma conta de computador](https://go.microsoft.com/fwlink/p/?linkid=165388).

2.  Instale o sistema operacional adequado e dê ao novo servidor o mesmo nome do servidor perdido. A recuperação não será bem-sucedida se o servidor no qual a recuperação está sendo realizada não tiver o mesmo nome do servidor perdido.

3.  Ingresse o servidor no mesmo domínio do servidor perdido.

4.  Instale os componentes do sistema operacional e pré-requisitos necessários. Para obter detalhes, consulte [Requisitos de sistema do Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md) e [Pré-requisitos do Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

5.  Faça logon no servidor que está sendo recuperado e abra um prompt de comando.

6.  Navegue até os arquivos de instalação do Exchange 2013 e execute o seguinte comando:
    
        Setup /m:RecoverServer /IAcceptExchangeServerLicenseTerms

7.  Depois que a instalação for concluída, mas antes que o servidor recuperado volte à ativa, reconfigure eventuais configurações personalizadas presentes anteriormente no servidor e depois reinicie o servidor.

## Como saber se funcionou?

A conclusão com êxito da Instalação será o indicador principal de que a recuperação foi bem-sucedida. Para verificar se você recuperou um servidor perdido com êxito, faça o seguinte:

  - Abra a ferramentas de Serviços do Windows (services.msc) e verifique se os serviços do Microsoft Exchange foram instalados e estão em execução.

