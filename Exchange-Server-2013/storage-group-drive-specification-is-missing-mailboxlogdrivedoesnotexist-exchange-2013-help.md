---
title: 'Especificação de unidade de grupo de armazenamento é missing_MailboxLogDriveDoesNotExist: Exchange 2013 Help'
TOCTitle: Especificação de unidade de grupo de armazenamento é missing_MailboxLogDriveDoesNotExist
ms:assetid: fe210f29-60cb-4d34-877e-1356a21dc02a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.mailboxlogdrivedoesnotexist(v=EXCHG.150)
ms:contentKeyID: 50487094
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Especificação de unidade de grupo de armazenamento é missing\_MailboxLogDriveDoesNotExist

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação de recuperação de desastres do Microsoft® Exchange Server 2007 não pode continuar porque a instalação de recuperação de desastres não pode acessar o banco de dados do grupo de armazenamento unidade especificação que foi usada na sua instalação anterior deste servidor.

A instalação de recuperação de desastres do Microsoft Exchange requer que o mesmo armazenamento grupo especificações banco de dados unidade anteriormente usadas para esse servidor pode estar disponível durante a restauração.

Para resolver essa situação, configure as unidades para coincidir com a configuração original da unidade lógica e execute novamente o programa de instalação de recuperação de desastres do Microsoft Exchange.

Atribuir ou alterar uma letra de unidade

1.  Abra **Gerenciamento do computador(Local)**.

2.  Na árvore de console, clique em **Gerenciamento do computador (Local)**, clique em **armazenamento** e clique em **Gerenciamento de disco**.

3.  Do mouse em uma partição, unidade lógica ou volume e, em seguida, clique em **Alterar letra de unidade e caminhos**.

4.  Use um dos seguintes procedimentos:
    
      - Para atribuir uma letra de unidade, clique em **Adicionar**, clique na letra de unidade que você deseja usar e clique em **OK**.
    
      - Para modificar uma letra de unidade, clique nela, clique em **Alterar**, clique na letra de unidade que você deseja usar e clique em **OK**.

Para obter mais informações sobre como atribuir letras de unidade, consulte "Atribuir, alterar ou remover uma letra de unidade" ([https://go.microsoft.com/fwlink/?LinkId=66764](https://go.microsoft.com/fwlink/?linkid=66764)).

