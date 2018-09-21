---
title: 'Definir a porta de escuta TCP em um servidor de acesso para cliente'
TOCTitle: Definir a porta de escuta TCP em um servidor de acesso para cliente
ms:assetid: 5f48f21a-d8d4-48b2-868f-9a3647693841
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673530(v=EXCHG.150)
ms:contentKeyID: 50556209
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir a porta de escuta TCP em um servidor de acesso para cliente

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-09_

Você pode configurar a porta TCP usada para escutar as solicitações de SIP em um servidor de Acesso para Cliente com o serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange. Por padrão, quando você instala um servidor de Acesso para Cliente, o número da porta de escuta TCP SIP é definido como 5060, e o servidor de Acesso para Cliente inicia no modo TCP. A porta de escuta TCP SIP não pode ser configurada usando o EAC. É preciso configurar o número da porta de escuta TCP SIP usando o cmdlet **Set-UMCallRouterSettings**.

Talvez seja necessário configurar a porta de escuta TCP como 5061 se os gateways VoIP, PBXs IP ou controladores de bordas de sessão (SBCs) forem configurados para usar uma porta TCP em vez de a 5060 padrão SIP.

Você só pode configurar o servidor de Acesso para Cliente em portas TCP e TLS. Você não pode configurar as portas para um servidor de Caixa de Correio Exchange 2013. No entanto, você pode usar o cmdlet **Set-UMService** para configurar as portas de escuta TCP e TLS para os servidores de UM do Exchange 2010.

Para conhecer tarefas adicionais relacionadas a servidores de Unificação de Mensagens e de Acesso para Cliente, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Servidor de Acesso para Cliente (servidor de roteamento de chamadas de UM)", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Verifique se você instalou corretamente os servidores de Acesso para Cliente e de Caixa de Correio.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar a porta de escuta TCP em um servidor de Acesso para Cliente

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  Na exibição de lista, selecione o servidor Exchange que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Exchange Server**, clique em **Unificação de Mensagens**.

4.  Em **Configurações do roteador de chamada de UM**, em **Porta de escuta TCP**, insira o número da porta TCP e clique em **Salvar**.

## Usar o Shell para configurar a porta de escuta TCP em um servidor de Acesso para Cliente

Este exemplo define a porta de escuta TCP em um servidor de Acesso chamado `MyClientAccessServer` para Cliente como 5566.

```powershell
Set-UMCallRouterSettings -Server MyClientAccessServer -SipTCPListeningPort 5566
```

