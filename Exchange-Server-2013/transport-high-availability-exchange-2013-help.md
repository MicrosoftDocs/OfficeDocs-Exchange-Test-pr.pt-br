---
title: 'Alta disponibilidade de transporte: Exchange 2013 Help'
TOCTitle: Alta disponibilidade de transporte
ms:assetid: e9ec6d05-f441-4cca-8592-8f7469948299
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657506(v=EXCHG.150)
ms:contentKeyID: 50486926
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alta disponibilidade de transporte

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-15_

No Microsoft Exchange Server 2013, alta disponibilidade de transporte é responsável por manter cópias redundantes de mensagens antes e depois que as mensagens são entregues com êxito. Exchange 2013 aprimorou os recursos de alta disponibilidade de transporte introduzidos em Exchange Server 2010, por exemplo, redundância de sombra e o transporte dumpster, para ajudar a garantir que as mensagens não são perdidas em trânsito.

Aqui está um resumo das melhorias de alta disponibilidade de transporte principais na Exchange 2013:

  - Redundância de sombra cria uma cópia redundante da mensagem em outro servidor antes que a mensagem for aceito ou reconhecida. Suporte do servidor de envio ou falta de suporte para redundância de sombra é irrelevante.

  - Redundância de sombra reconhece tanto a grupos de disponibilidade de banco de dados (DAGs) e sites do Active Directory como limites de alta disponibilidade de transporte. Isso reduz o número de servidores que pode manter cópias redundantes de mensagens e elimina o tráfego de manutenção de mensagem redundantes desnecessários em DAGs ou do Active Directory sites.
    
    Para obter mais informações, consulte [Redundância de sombra](shadow-redundancy-exchange-2013-help.md).

  - O transporte dumpster foi melhorada e agora se chama a *rede de segurança*. Safety Net armazena as mensagens que foram processadas com êxito pelo serviço de transporte em servidores de caixa de correio. Safety Net funciona melhor para servidores de caixa de correio em um DAG, mas também opera Safety Net para vários servidores de caixa de correio no mesmo site do Active Directory que não pertencem a um DAG.

  - Safety Net propriamente dito é agora redundante em outro servidor. Isso é importante para evitar um único ponto de falha no Exchange 2013, porque o serviço de transporte e os bancos de dados de caixa de correio estão localizados no servidor de caixa de correio.
    
    Para obter mais informações, consulte [Rede de Segurança](safety-net-exchange-2013-help.md).

O diagrama a seguir fornece uma visão geral de como funciona a alta disponibilidade de transporte no Exchange 2013.

![Visão geral de alta disponibilidade de transporte](images/JJ657506.88f2284d-8afe-4c8f-94a6-cd4c097a55d8(EXCHG.150).gif "Visão geral de alta disponibilidade de transporte")

1.  Um servidor de caixa de correio Exchange 2013 mailbox01 recebe uma mensagem de um servidor SMTP que está fora do limite de alta disponibilidade de transporte. O *limite de alta disponibilidade de transporte* é um DAG ou um site do Active Directory em ambientes não são DAG. A mensagem foi vêm de um servidor SMTP de terceiros, de um servidor SMTP de Internet intermediadas por proxy através de um servidor de acesso para cliente ou de outro servidor Exchange 2013.

2.  Antes de confirmar o recebimento da mensagem, Mailbox01 inicia uma nova sessão de SMTP para outro servidor de caixa de correio Exchange 2013 chamado Mailbox03 que está dentro dos limites de alta disponibilidade de transporte e Mailbox03 faz uma cópia de sombra da mensagem. Em ambientes de DAG, um servidor de sombra em um site remoto do Active Directory é o preferencial. Mailbox01 é o servidor primário, mantendo a mensagem principal e Mailbox03 é o servidor de sombra que contém a mensagem de sombra.

3.  Serviço de transporte em Mailbox01 processa a mensagem principal.
    
    1.  Neste exemplo, a caixa de correio do destinatário está localizada no Mailbox01, portanto, o serviço de transporte transmite a mensagem para o serviço de transporte de caixa de correio local.
    
    2.  O serviço de transporte de caixa de correio entrega a mensagem para o banco de dados de caixa de correio local.
    
    3.  Mailbox01 enfileira um status de descarte de Mailbox03 que indica a mensagem principal foi processada com êxito e Mailbox01 move uma cópia da mensagem principal para a rede principal de segurança local. Observe que a mensagem se move entre as filas de dentro do mesmo banco de dados de fila.

4.  Mailbox03 periodicamente sonda Mailbox01 para o status de descarte da mensagem principal.

5.  Quando Mailbox03 determina que mailbox01 processadas com êxito a mensagem principal, Mailbox03 move a mensagem de sombra no local Safety Net da sombra. Observe que a mensagem se move entre as filas de dentro do mesmo banco de dados de fila.

A mensagem é mantida no principal Safety Net e sombra Safety Net até que a mensagem expira com base em um valor de tempo limite configurável. Se um failover de banco de dados de caixa de correio ocorre antes que a mensagem expire, o principal Safety Net em Mailbox01 reenvia a mensagem. Se o Mailbox01 não estiver disponível, a sombra Safety Net em Mailbox03 assume e reenvia a mensagem.

## Redundância de mensagem no serviço Front End Transport em servidores de acesso para cliente

Um servidor de acesso para cliente não tem nenhuma filas de mensagens. É um servidor de proxy sem estado que usa o serviço de Front End Transport para aceitar conexões SMTP de entrada e o proxy de serviço-los ao transporte em um servidor de caixa de correio. O serviço Front End Transport mantém a sessão SMTP com o servidor de envio aberta, enquanto a mensagem principal é transmitida para o serviço de transporte em um servidor de caixa de correio e uma cópia de sombra da mensagem é feita pelo serviço de transporte em um servidor de caixa de correio diferente dentro dos limites de alta disponibilidade de transporte. Somente depois que a mensagem principal e a mensagem de sombra são criados com êxito, o final dos dados comando SMTP será enviado para o servidor de envio SMTP através do servidor de acesso para cliente.

