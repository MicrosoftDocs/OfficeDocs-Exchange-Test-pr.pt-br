---
title: 'Testar UM operação: Exchange 2013 Help'
TOCTitle: Testar UM operação
ms:assetid: 06c9ab4e-8272-47b1-a217-e366f7e9dbaa
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa995957(v=EXCHG.150)
ms:contentKeyID: 56270503
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Testar UM operação

 

_**Aplica-se a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-06-25_

Este tópico explica como usar o Shell para testar a operação do seu sistema de correio de voz. Ao realizar o procedimento a seguir, o servidor da Caixa de Correio que está executando o serviço de Unificação de Mensagens do Microsoft Exchange inicia uma chamada do protocolo SIP de diagnóstico e depois retorna uma variável de estado da integridade dos serviços de UM.

O teste de diagnóstico pode ser executado somente no servidor de Caixa de Correio local, e você não pode testar a operação do servidor de Caixa de Correio usando o EAC.

Para conhecer mais tarefas de gerenciamento relacionadas a servidores de Caixa de Correio e de Acesso para Cliente, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para finalização: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entradas sobre "Servidor de caixa de correio (serviço de UM)" e \&quot;Servidor de Acesso para Cliente (serviço de roteador de chamadas de UM)\&quot;, no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Para realizar os procedimentos a seguir, você deve fazer logon no servidor de Caixa de Correio usando uma conta que seja membro do grupo de Administradores locais.

  - Verifique se o servidor de Caixa de Correio está instalado no mesmo computador que o servidor de Acesso para Cliente ou em um computador separado.

  - Verifique se o servidor de Acesso para Cliente está instalado no mesmo computador que o servidor de Caixa de Correio ou em um computador separado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Use o shell para testar a operação dos serviços de Unificação de Mensagens

Este exemplo realiza testes operacionais e de conectividade no servidor de Caixa de Correio local e depois exibe as informações de conectividade de VoIP (Voz sobre IP).

    Test-UMConnectivity

Este exemplo testa a capacidade do servidor de Acesso para Cliente local de escutar solicitações SIP não criptografadas recebidas na porta TCP 5060.

    Test-UMConnectivity -ListenPort 5060

Este exemplo testa a capacidade do servidor de Acesso para Cliente local de escutar solicitações SIP criptografadas recebidas na porta TCP 5061.

    Test-UMConnectivity -ListenPort 5061


> [!NOTE]
> Use modo 1 quando o parâmetro <CODE>-UMIPGateway</CODE> não for especificado.




> [!NOTE]
> Você pode definir o parâmetro <CODE>-Timeout</CODE> com um valor inferior a 5 segundos. No entanto, recomendamos que você sempre configure esse parâmetro com um valor de 5 segundos ou mais.


