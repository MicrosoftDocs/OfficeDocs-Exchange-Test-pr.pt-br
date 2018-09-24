---
title: 'Configurar o número de chamadas de entrada em um servidor de caixa de correio'
TOCTitle: Configurar o número de chamadas de entrada em um servidor de caixa de correio
ms:assetid: 419e1de9-2bf8-48a8-824d-2a536b0a6d90
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997637(v=EXCHG.150)
ms:contentKeyID: 50556171
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o número de chamadas de entrada em um servidor de caixa de correio

 

_**Aplica-se a:** Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-23_

Você pode configurar o número de conexões consecutivas de entrada que um servidor de Caixa de Correio que executa o serviço de Unificação de Mensagens do Microsoft Exchange aceitará. Isso inclui todas as chamadas de entrada, incluindo o Outlook Voice Access, atendimento de chamada, atendedores automáticos e chamadas de fax. Quando o número de conexões simultâneas em um servidor de Caixa de Correio aumenta, são necessários mais recursos de sistema do que quando o número de chamadas simultâneas é reduzido. A redução do número de chamadas simultâneas é especialmente importante em computadores mais lentos em que os serviços de Unificação de Mensagens estejam instalados. O intervalo do número de chamadas de voz simultâneas é de 0 a 200. O padrão é 100.

Para tarefas adicionais relacionadas à Unificação de Mensagens e a servidores de Caixa de Correio, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Servidor de Caixa de Correio (serviço de UM)" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Verifique se você instalou corretamente os servidores de Acesso para Cliente e de Caixa de Correio.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar o número de chamadas de entrada em um servidor de Caixa de Correio

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  Na exibição de lista, selecione o servidor Exchange que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Exchange Server**, clique em **Unificação de Mensagens**.

4.  Em **Configurações do Serviço UM**, sob **Número máximo de chamadas permitidas**, insira um número de 0 a 200 e clique em **Salvar**.

## Usar o Shell para configurar o número de chamadas de entrada em um servidor de Caixa de Correio

Este exemplo define o número de chamadas de voz de entrada, do Outlook Voice Access e de fax que podem ser aceitas por um servidor de Caixa de Correio chamado `MyMailboxServer1` como 50.

```powershell
Set-UMService -Identity MyMailboxServer1 -MaxCallsAllowed 50
```

