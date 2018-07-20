---
title: 'Configurar log circular de um banco de dados de caixa de correio: Exchange 2013 Help'
TOCTitle: Configurar log circular de um banco de dados de caixa de correio
ms:assetid: 29cbd7cd-382b-4e0d-8368-2e49e75df2fc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn756374(v=EXCHG.150)
ms:contentKeyID: 62524842
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar log circular de um banco de dados de caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-06-24_

Ao habilitar o log circular de um banco de dados de caixa de correio, o tipo de log circular obtido depende de o banco de dados da caixa de correio ser replicado usando replicação contínua ou não:

  - Se o banco de dados de caixa de correio não é replicado, ele usará o log circular JET. Nesse caso, para habilitar ou desabilitar o log circular JET será necessário fazer a desmontagem e a montagem do banco de dados.

  - Se o banco de dados da caixa de correio é replicado, ele usará o log circular de replicação contínua (CRCL). Nesse caso, habilitar ou desabilitar o CRCL funciona dinamicamente. Não é necessário desmontar e montar novamente o banco de dados.

Para obter mais informações sobre log circular e CRCL, consulte [Exchange Native Data Protection](backup-restore-and-disaster-recovery-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Permissões de banco de dados da caixa de correio" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

## Usar o EAC para configurar o log circular para um banco de dados

1.  No EAC, vá até **Servidores** \> **bancos de dados**.

2.  Selecione o banco de dados de caixa de correio que deseja configurar e clique em ![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Marque ou desmarque a caixa de seleção **Habilitar log circular** e clique em **salvar**.

4.  Se uma operação de desmontagem e montagem for necessária, uma mensagem de aviso será exibida. Clique em **OK** para fechar a mensagem de aviso.
    
    1.  Para desmontar o banco de dados, clique em **Mais**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") e em **Desmontar**. Clique em **sim** quando a mensagem de aviso for exibida.
    
    2.  Para montar o banco de dados, clique em **Mais**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") e em **Montar**. Clique em **sim** quando a mensagem de aviso for exibida.

## Usar o Shell para configurar o log circular de um banco de dados

Este exemplo ativa o log circular do banco de dados DB1.

    Set-MailboxDatabase DB1 -CircularLoggingEnabled $True

Este exemplo desativa o log circular do banco de dados DB1.

    Set-MailboxDatabase DB1 -CircularLoggingEnabled $False

Consulte [Set-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb123971\(v=exchg.150\)) para conhecer outros parâmetros de banco de dados de caixa de correio que você pode configurar.

