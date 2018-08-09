---
title: 'Atribuir um certificado para os serviços de UM e o roteador de chamada UM'
TOCTitle: Atribuir um certificado para os serviços de Unificação de mensagens e o roteador de chamada UM
ms:assetid: 8a900e5f-9779-4213-92d7-ec157b15fbc5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn205140(v=EXCHG.150)
ms:contentKeyID: 54651979
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Atribuir um certificado para os serviços de Unificação de mensagens e o roteador de chamada UM

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-29_

Você pode usar o EAC ou o Shell para atribuir uma interna, autoassinada infraestrutura de chave pública (PKI) ou um certificado comercial de terceiros para serviços específicos do Exchange. Quando você usa o cmdlet **New-ExchangeCertificate** para atribuir o certificado aos serviços do Exchange com o parâmetro *Services* , você será solicitado para atribuir o certificado aos serviços do Exchange. Se você usar o EAC para criar um certificado, o Assistente de novo certificado do Exchange não solicita que você atribua o certificado aos serviços do Exchange. Você precisa editar as propriedades do certificado e atribuir o certificado selecionando quais serviços você deseja atribuí-lo a.

Diferentes serviços têm requisitos de certificado diferente. Por exemplo, alguns serviços só podem exigir um nome de servidor nas caixas **Nome de entidade** ou **Nome alternativo da entidade** de um certificado e outros serviços podem exigir um nome de domínio totalmente qualificado (FQDN). Certifique-se de que o nome do certificado pode suportar os usos necessários para os serviços que você ativá-la para.


> [!WARNING]
> Certificados autoassinados não podem ser usados quando você estiver integrando a Unificação de mensagens (UM) com o Microsoft Lync Server.



Para conhecer tarefas de gerenciamento adicionais relacionadas ao gerenciamento de certificados para Unificação de Mensagens, consulte [Implantar certificados para os procedimentos de Unificação de mensagens](deploying-certificates-for-um-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gerenciamento de certificado" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) e entrada "Serviço de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md) . Você também deve fazer logon usando uma conta que seja membro do grupo Administradores local nesse computador.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para atribuir um certificado para os serviços de Unificação de mensagens e o roteador de chamada UM

1.  No EAC, navegue até **servidores** \> **certificados**.

2.  Na exibição de lista, selecione o certificado que você deseja atribuir aos serviços de Unificação de mensagens e o roteador de chamada UM e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página *\<Certificate name\>* , selecione **Serviços** e selecione **UM** e **roteador de chamadas de Unificação de mensagens**.

4.  Clique em **Salvar**.

## Usar o Shell para atribuir um certificado para os serviços de Unificação de mensagens e o roteador de chamada UM

Este exemplo atribui um certificado para os serviços de Unificação de mensagens e o roteador de chamada UM.

    Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'

