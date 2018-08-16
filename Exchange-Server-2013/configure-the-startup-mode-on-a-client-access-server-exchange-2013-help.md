---
title: 'Configurar modo de inicialização em um servidor de Acesso para Cliente'
TOCTitle: Configurar o modo de inicialização em um servidor de acesso para cliente
ms:assetid: 71cc9061-9e3c-4b4a-8dbe-f590ca5bcee8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673533(v=EXCHG.150)
ms:contentKeyID: 50556207
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o modo de inicialização em um servidor de acesso para cliente

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-15_

Você pode especificar o modo de inicialização para o serviço Microsoft Exchange Unified Messaging roteador de chamadas em um servidor de acesso para cliente. Por padrão, o servidor de acesso para cliente iniciará no modo TCP, mas se você estiver usando a segurança de camada de transporte (TLS) para criptografar voz sobre o tráfego IP (VoIP), você deverá configurar o servidor de acesso para cliente para usar TLS ou modo Dual. É recomendável que os servidores de acesso para cliente sejam configurados para usar Dual como o modo de inicialização. Isso ocorre porque os servidores de todas as caixas de correio e acesso para cliente pode atender a chamadas recebidas para Unificação de mensagens de todos os planos de discagem e os planos de discagem podem ter configurações de segurança diferentes. Se você alterar o modo de inicialização, você deve reiniciar o serviço Microsoft Exchange Unified Messaging roteador de chamada para que a alteração entre em vigor.


> [!IMPORTANT]
> Por padrão, servidores de acesso para cliente estão disponíveis para atender chamadas de entrada. Você não precisa adicionar um servidor de acesso para cliente a um plano de discagem UM processo de chamadas de Unificação de mensagens, a menos que você estiver integrando a Unificação de mensagens e o Microsoft Office Communications Server 2007 R2 ou o Microsoft Lync Server.



Para tarefas de gerenciamento adicionais relacionadas aos servidores de acesso para cliente e Unificação de mensagens, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Servidor de Acesso para Cliente (servidor de roteamento de chamadas de UM)", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Verifique se o servidor de Acesso para Cliente está instalado no mesmo computador que o servidor de Caixa de Correio ou em um computador separado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar o modo de inicialização em um servidor de acesso para cliente

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  Na exibição de lista, selecione o servidor Exchange que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Exchange Server**, clique em **Unificação de Mensagens**.

4.  Em **Definiçõs do Roteador de Chamadas de UM** \> **Modo de inicialização de UM**, selecione um dos seguintes da lista suspensa:
    
      - **TCP**   Use esta opção se não está usando mTLS e está usando apenas os planos de discagem Não protegidos.
    
      - **TLS**   Use essa opção se estiver usando mTLS e se estiver usando somente planos de discagem Protegidos por SIP ou Protegidos.
    
      - **DUPLA**   Use essa opção se estiver usando mTLS e se estiver usando somente planos de discagem Protegidos por SIP ou Protegidos.

5.  Depois de selecionar o modo de inicialização de UM, clique em **Salvar**.

## Usar o Shell para configurar o modo de inicialização em um servidor de acesso para cliente

Este exemplo define o modo de inicialização para um servidor de acesso para cliente chamado `UMCallRouter1` para modo Dual.

    Set-UMCallRouterSettings -Server UMCallRouter1 -UMStartUpMode Dual

Este exemplo define o modo de inicialização para um servidor de acesso para cliente chamado `UMCallRouter1` para o modo TLS.

    Set-UMCallRouterSettings -Server UMCallRouter1 -UMStartUpMode TLS

