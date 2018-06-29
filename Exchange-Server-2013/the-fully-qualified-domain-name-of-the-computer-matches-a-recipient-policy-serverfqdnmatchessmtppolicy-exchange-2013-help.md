---
title: 'O nome de domínio totalmente qualificado do computador corresponde a um destinatário policy_ServerFQDNMatchesSMTPPolicy: Exchange 2013 Help'
TOCTitle: O nome de domínio totalmente qualificado do computador corresponde a um destinatário policy_ServerFQDNMatchesSMTPPolicy
ms:assetid: f3ea61f8-1788-4cbf-814e-f7c088c1ac47
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.serverfqdnmatchessmtppolicy(v=EXCHG.150)
ms:contentKeyID: 50486993
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O nome de domínio totalmente qualificado do computador corresponde a um destinatário policy\_ServerFQDNMatchesSMTPPolicy

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft® Exchange Server 2007 não pode continuar porque o nome de domínio totalmente qualificado (FQDN) do computador local corresponde ao endereço de Simple Mail Transfer Protocol (SMTP) de uma política de destinatário.

A instalação do Microsoft Exchange requer que o FQDN dos servidores em uma organização do Exchange não corresponder a qualquer endereço SMTP das diretivas de destinatário na mesma organização do Exchange.

Se o FQDN de um computador com o endereço SMTP de uma diretiva de destinatário, essa correspondência pode causar mensagens realizar failover SMTP e travado nas filas MTA.

Para resolver esse problema, renomeie o computador local ou remover ou renomear a diretiva de destinatário e execute novamente o programa de instalação do Microsoft Exchange.

Para renomear o computador local

1.  Abra o **sistema** no **Painel de controle**.

2.  Na guia **Nome do Computador**, clique em **Alterar**.

3.  Em **nome do computador**, digite um novo nome para o computador e, em seguida, clique em **OK**. Você será solicitado a fornecer um nome de usuário e senha de usuário para renomear o computador no domínio.

4.  Clique em **OK** para fechar a caixa de diálogo **Propriedades do sistema**. Você será solicitado a reiniciar o computador para aplicar suas alterações.


> [!IMPORTANT]
> Se o computador que você deseja renomear for um controlador de domínio, consulte "Renomear um controlador de domínio" (<A href="https://go.microsoft.com/fwlink/?linkid=66828">https://go.microsoft.com/fwlink/?LinkId=66828</A>).



Para modificar a política de destinatário endereço SMTP

1.  Inicie o Gerenciador de sistema do Exchange.

2.  Clique em **organização**, clique em **destinatários** e, em seguida, clique em **Diretivas de destinatário**.

3.  Clique duas vezes na política que você deseja alterar.

4.  Clique na guia **Endereços de email** e altere o endereço SMTP apropriado

Para obter mais informações sobre problemas de nomenclatura de política de destinatário, consulte o artigo da Base de Conhecimento Microsoft 288175, "XCON: política de destinatário não pode corresponder ao FQDN de qualquer servidor na organização, 5.4.8 NDRs" ([http://go.microsoft.com/fwlink/?linkid=3052\&kbid=288175](http://go.microsoft.com/fwlink/?linkid=3052%26kbid=288175)).

