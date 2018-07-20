---
title: 'Definir a configuração de segurança de VoIP: Exchange 2013 Help'
TOCTitle: Definir a configuração de segurança de VoIP
ms:assetid: b5335654-c766-4f3f-883c-f31263e1d9c1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201721(v=EXCHG.150)
ms:contentKeyID: 50486449
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir a configuração de segurança de VoIP

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2014-10-16_

Você pode habilitar voz sobre segurança IP (VoIP) para um plano de discagem de Unificação de mensagens (UM). Por padrão, quando um plano de discagem UM é criado, ele usará o modo não seguro ou sem criptografia. Servidores Exchange podem atender as chamadas para um ou vários planos de discagem de Unificação de mensagens e podem atender as chamadas para os planos de discagem que tenham diferentes configurações de segurança de VoIP. No Office 365 e o Exchange Online protegido modo é necessário e não pode ser desabilitado.

Quando você configura o plano de discagem de UM para utilizar o modo Protocolo de Iniciação de Sessão (SIP) protegido ou seguro, os servidores Exchange que atenderam as chamadas para o plano de discagem de UM irão criptografar o tráfego de sinalização SIP (para SIP protegido) ou os canais de mídia de Protocolo de Transporte em Tempo Real (RTP) e o tráfego de sinalização SIP (para o modo seguro).


> [!IMPORTANT]
> Para implantações híbridas e locais ao configurar o SipTCPListeningPort, SipTLSListeningPort ou o UMStartUpMode em um servidor de Acesso para Cliente executando o serviço de Roteador de Chamada da Unificação de Mensagens do Microsoft Exchange ou um servidor de Caixa de Correio que está executando o serviço de Unificação de Mensagens do Microsoft Exchange, será necessário configurar as regras de Firewall do Windows corretamente para permitir o tráfego de rede SIP e RTP.



Para mais tarefas de gerenciamento relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o EAC para configurar a segurança de VoIP em um plano de discagem de UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**, selecione o plano de discagem de UM no qual deseja alterar a segurança de VoIP e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, clique em **Configurar**.

3.  Em **Geral**, no **Modo de segurança de VoIP**, selecione uma das seguintes opções:
    
      - **SIP protegido**
    
      - **Não protegido** (padrão)
    
      - **Protegido**

4.  Clique em **Salvar**.

## Use o Shell para configurar a segurança VoIP em um plano de discagem de UM

Este exemplo configura um plano de discagem UM chamado `MySecureDialPlan` para criptografar o tráfego SIP e RTP.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Secured

Este exemplo configura um plano de discagem de UM chamado `MySecureDialPlan` para criptografar o tráfego SIP mas não o RTP.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity SIPsecured

Este exemplo configura um plano de discagem de UM chamado`MySecureDialPlan` para criptografar o tráfego SIP e RTP.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Unsecured

