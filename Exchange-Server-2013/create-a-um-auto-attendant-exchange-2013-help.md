---
title: 'Criar um Atendedor Automático da UM: Exchange 2013 Help'
TOCTitle: Criar um Atendedor Automático da UM
ms:assetid: 773f53fb-d80f-4a79-8bd3-bd753942489f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998875(v=EXCHG.150)
ms:contentKeyID: 50485949
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.CreateAutoAttendantWizardForm.CreateAutoAttendantWizardPage
ms.translationtype: MT
---

# Criar um Atendedor Automático da UM

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-03-08_

Depois de criar um atendedor automático de Unificação de mensagens (UM), as chamadas de entrada para um número de telefone externo que um operador humano atendidas normalmente são respondidas pelo atendedor automático. Ao contrário com outros componentes de Unificação de mensagens, como UM planos de discagem e gateways IP de UM, você não é necessários para criar atendedores automáticos. No entanto, atendedores automáticos ajuda interna e chamadores externos localizar usuários ou departamentos que existem em uma organização e transferir chamadas para eles.

Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para criar um atendedor automático

1.  
    
    No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem da UM**, selecione o plano de discagem da UM que deseja adicionar a um atendedor automático e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **Plano de discagem de UM**, em **Atendedores automáticos de UM**, clique em **New**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Na página de **atendedor automático de UM novo**, insira as seguintes informações:
    
      - **Nome**   Use essa caixa para criar o nome de exibição do atendedor automático de UM. O nome do atendedor automático da UM é necessário e deve ser exclusivo. Porém, ele é usado apenas para fins de exibição no EAC e no Shell.
        
        Se for necessário alterar o nome de exibição do atendedor automático após sua criação, primeiro você deverá excluir o atendedor automático de UM existente e criar outro atendedor com o nome adequado. Se sua organização usa vários atendedores automáticos do UM, é recomendável usar nomes significativos para seus atendedores automáticos do UM. O tamanho máximo do nome do atendedor automático do UM é 64 caracteres, podendo incluir espaços.
        
        Embora você possa nomear um novo atendedor automático para incluir espaços, se você integrar a Unificação de mensagens com o Office Communications Server 2007 R2 ou Microsoft Lync Server, o nome do atendedor automático não pode incluir espaços. Portanto, se você criou um atendedor automático com espaços no nome de exibição e você estiver integrando com o Office Communications Server 2007 R2 ou o Lync Server, você deve primeiro exclua esse atendedor automático e, em seguida, criar outro atendedor automático que não incluem espaços no nome de exibição.
    
      - **Criar este atendedor automático como habilitado**    Marque esta caixa de seleção para habilitar o atendedor automático atender chamadas de entrada quando você concluir o novo UM Atendedor Assistente automático. Por padrão, um novo atendedor automático é criado como desabilitada.
        
        Se você decidir criar UM atendedor automático como desabilitada, você pode usar o EAC ou o Shell para habilitar o atendedor automático após concluir o assistente.
    
      - **Configurar o atendedor automático para responder a comandos de voz**   Marque essa caixa de seleção para habilitar o atendedor automático de UM para voz. Se o atendedor automático for habilitado para fala, os chamadores poderão responder aos prompts do sistema ou a prompts personalizados usados pelo atendedor automático de UM usando entradas de discagem por tom ou voz. Por padrão, quando um atendedor automático é criado, não está habilitado para fala.
        
        Para os chamadores usar um atendedor automático habilitado para fala, você deve instalar o pacote de idiomas de Unificação de mensagens apropriado que contém o suporte de reconhecimento automático de fala (ASR) e configure as propriedades do atendedor automático para usar esse idioma.
    
      - **Números de acesso**    Use esta caixa para inserir os números de ramal ou números de telefone que os chamadores usarão para alcançar o atendedor automático. Digite um número de ramal ou o número de telefone na caixa e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para adicionar o número na lista. O número de dígitos no número de ramal ou número de telefone que você fornece não deve coincidir com o número de dígitos para um número de ramal configurados no plano de discagem de Unificação de mensagens associado. Isso ocorre porque as chamadas diretas têm permissão para atendedores automáticos.
        
        O número de números de ramal ou números de telefone inseridos é ilimitado. No entanto, você pode criar o novo atendedor automático sem um número de ramal listado. Um número de ramal ou o número de telefone não é exigido.
        
        Você pode editar ou remover um número de ramal existente ou o número de telefone. Para editar um número de ramal existente ou o número de telefone, clique em **Editar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Para remover um número de ramal existente ou o número de telefone da lista, clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

4.  Clique em **Salvar**.

## Usar o Shell para criar um atendedor automático de UM

Este exemplo cria um atendedor automático de UM chamado `MyUMAutoAttendant` que pode aceitar chamadas de entrada, mas não está habilitado para fala.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 55000 -Enabled $false

Este exemplo cria um atendedor automático de UM habilitado para fala chamado `MyUMAutoAttendant`.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true

