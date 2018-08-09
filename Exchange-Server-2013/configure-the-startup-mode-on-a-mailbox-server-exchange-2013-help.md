---
title: 'Configurar inicialização em servidor de caixa de correio: Exchange 2013 Help'
TOCTitle: Configurar o modo de inicialização em um servidor de caixa de correio
ms:assetid: 4457d6a0-52bd-4269-8cb5-d34d7fe9bfc3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423544(v=EXCHG.150)
ms:contentKeyID: 50556191
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o modo de inicialização em um servidor de caixa de correio

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-15_

Você pode especificar o modo de inicialização do serviço de Unificação de Mensagens do Microsoft Exchange em um servidor de Caixa de Correio. Por padrão, o servidor de Caixa de Correio inicia em modo TCP, mas se você estiver usando o protocolo TLS para criptografar tráfego VoIP, será preciso configurar o servidor de Caixa de Correio para que use TLS ou modo Duplo. Recomendamos que os servidores de Caixa de Correio sejam configurados para usar Duplo como o modo de inicialização. Isso porque todos os servidores de Acesso para Cliente e servidores de Caixa de Correio podem atender chamadas de entrada para todos os planos de discagem da UM e esses planos de discagem podem ter diferentes configurações de segurança (não protegido, SIP protegido, ou Protegido). Se o modo de inicialização for alterado, o serviço de Unificação de Mensagens do Microsoft Exchange deve ser reiniciado para que as alterações tenham efeito.


> [!IMPORTANT]
> Por padrão, os servidores de Caixa de Correio estão disponíveis para atender chamadas. Não é necessário adicionar um servidor de Caixa de Correio a um plano de discagem de UM para processar chamadas de UM a menos que você esteja integrando a UM e Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server.



Para conhecer tarefas de gerenciamento adicionais relacionadas a Unificação de Mensagens e a servidores de Caixa de Correio, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Servidor de Caixa de Correio (serviço de UM)" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Verifique se o servidor de Caixa de Correio está instalado no mesmo computador que um servidor de Acesso para Cliente ou em um computador separado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar o modo de inicialização em um servidor de Caixa de Correio

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  Na exibição de lista, selecione o servidor Exchange que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Exchange Server**, clique em **Unificação de Mensagens**.

4.  Em **Configurações do Serviço da UM** \> **Modo de inicialização da UM**, selecione um na lista suspensa:
    
      - **TCP**   Use essa opção se não estiver usando mTLS e se estiver usando somente planos de discagem Desprotegidos.
    
      - **TLS**   Use essa opção se estiver usando mTLS e se estiver usando somente planos de discagem Protegidos por SIP ou Protegidos.
    
      - **DUPLA**   Use essa opção se estiver usando mTLS e se estiver usando somente planos de discagem Protegidos por SIP ou Protegidos.

5.  Depois de selecionar o modo de inicialização de UM, clique em **Salvar**.

## Usar o Shell para configurar o modo de inicialização em um servidor de Caixa de Correio

Este exemplo define o modo de inicialização para um servidor de Caixa de Correio chamado `MyUMServer1` como modo Duplo.

    Set-UMService -Identity MyUMServer1 -UMStartUpMode Dual

Este exemplo define o modo de inicialização para um servidor de Caixa de Correio chamado `MyUMServer1` como modo TLS.

    Set-UMService -Identity MyUMServer1 -UMStartUpMode TLS

