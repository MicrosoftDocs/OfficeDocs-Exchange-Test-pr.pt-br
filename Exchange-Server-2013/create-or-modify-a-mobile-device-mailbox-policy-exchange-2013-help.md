---
title: 'Criar ou modificar uma política de caixa de correio de dispositivo móvel'
TOCTitle: Criar ou modificar uma política de caixa de correio de dispositivo móvel
ms:assetid: b4a37a81-25e3-40ff-a18a-a62ae4493635
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124315(v=EXCHG.150)
ms:contentKeyID: 50486445
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar ou modificar uma política de caixa de correio de dispositivo móvel

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-16_

Uma política de caixa de correio de dispositivo móvel permite que você aplique um conjunto comum de segurança e configurações de dispositivo móvel para um grupo de usuários. Você pode criar políticas de caixa de correio de vários dispositivos móveis. Cada destinatário em sua organização deve ter uma diretiva de caixa de correio de dispositivo móvel atribuída a eles. Quando você instala o Microsoft Exchange Server 2013, uma política de caixa de correio de dispositivo móvel padrão é criada e novos usuários recebem automaticamente essa política. Para atribuir a usuários específicos para uma diretiva de caixa de correio de dispositivo móvel, consulte [Adicionar ou remover usuários de uma política de caixa de correio móvel](add-or-remove-users-from-a-mobile-mailbox-policy-exchange-2013-help.md).

Para obter informações adicionais relacionadas a políticas de caixa de correio de dispositivo móvel, consulte [Políticas de caixa de correio para dispositivos móveis](mobile-device-mailbox-policies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar cada procedimento: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Política de caixa de correio de dispositivo móvel", no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Criar uma nova política de caixa de correio de dispositivo móvel

Você pode usar o EAC ou o Shell para criar uma nova política de caixa de correio de dispositivo móvel.

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Política de caixa de correio de dispositivo móvel", no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

## Usar o EAC para criar uma nova política de caixa de correio de dispositivo móvel

Você pode criar uma nova diretiva de caixa de correio de dispositivo móvel usando o EAC.


> [!TIP]
> Você só pode definir um subconjunto das configurações de diretiva de caixa de correio de dispositivo móvel no EAC. Para definir configurações de diretiva de caixa de correio de dispositivo móvel, você precisará usar o Shell.



1.  No EAC, clique em **Mobile** \> **Políticas de caixa de correio de dispositivo móvel** e, em seguida, clique em **novo**.

2.  Use as várias caixas de seleção e listas suspensas para definir as configurações para a política de caixa de correio de dispositivo móvel.
    

    > [!WARNING]
    > Selecione <STRONG>Esta é a política padrão</STRONG> para tornar a nova diretiva de caixa de correio móvel a diretiva de caixa de correio móvel padrão. Depois de fazer uma política de caixa de correio móvel a política padrão, todos os novos usuários serão atribuídos essa diretiva automaticamente quando forem criados.



3.  Clique em **Salvar**.

## Use o Shell para criar uma nova política de caixa de correio de dispositivo móvel

Você criar uma nova diretiva de caixa de correio de dispositivo móvel usando o cmdlet New-MobileDeviceMailboxPolicy .


> [!WARNING]
> Há dois cmdlets que pode ser usados para criar uma nova política de caixa de correio de dispositivo móvel. O cmdlet <STRONG>New-ActiveSyncMailboxPolicy</STRONG> e os cmdlets <STRONG>New-MobileDeviceMailboxPolicy</STRONG> executar tarefas idênticas. Em uma versão futura do Microsoft Exchange Server, o cmdlet <STRONG>New-ActiveSyncMailboxPolicy</STRONG> será removido. Recomendamos que você atualize seus scripts e procedimentos para usar o cmdlet <STRONG>New-MobileDeviceMailboxPolicy</STRONG> .



1.  No Shell, execute o comando a seguir.
    
        New-MobileDeviceMailboxPolicy -Name:"Management" -AllowBluetooth:$true -AllowBrowser:$true -AllowCamera:$true -AllowPOPIMAPEmail:$false -PasswordEnabled:$true -AlphanumericPasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:10 -AllowWiFi:$true -AllowStorageCard:$true -AllowPOPIMAPEmail:$false

## Como saber se funcionou?

Para verificar se você criou com êxito uma política de caixa de correio de dispositivo móvel, use uma das seguintes opções:

1.  No EAC, clique em **Mobile** \> **políticas de caixa de correio de dispositivo móvel** e confirme se a nova política é exibida no modo de exibição de lista.

2.  No Shell, execute o comando a seguir.
    
        Get-MobileDeviceMailboxPolicy -Identity <PolicyName> 

## Editar uma política existente de caixa de correio de dispositivo móvel

Se desejar editar uma política de caixa de correio de dispositivo móvel, você pode usar o EAC ou o Shell.

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Política de caixa de correio de dispositivo móvel", no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

## Usar o EAC para editar uma política de caixa de correio de dispositivo móvel

Você pode editar uma política de caixa de correio de dispositivo móvel usando o EAC.


> [!TIP]
> Você só pode editar um subconjunto das configurações de diretiva de caixa de correio de dispositivo móvel no EAC. Para editar a todas as configurações de diretiva de caixa de correio dispositivo móvel, você precisará usar o Shell.



1.  No EAC, clique em **Mobile** \> **Políticas de caixa de correio de dispositivo móvel**.

2.  Selecione uma política de exibição de lista e clique no botão **Editar**.

3.  Use as guias **Geral** e **segurança** para editar as configurações de diretiva de caixa de correio de dispositivo móvel.

4.  Clique em **Salvar** para atualizar a política.

## Use o Shell para editar configurações de diretiva de caixa de correio de dispositivo móvel

Você pode usar o Shell para editar uma política de caixa de correio de dispositivo móvel.


> [!WARNING]
> Há dois cmdlets que pode ser usados para editar uma política de caixa de correio de dispositivo móvel. O cmdlet Set-ActiveSyncMailboxPolicy e os cmdlets Set-MobileDeviceMailboxPolicy executar tarefas idênticas. Em uma versão futura do Microsoft Exchange Server, o cmdlet <STRONG>Set-ActiveSyncMailboxPolicy</STRONG> será removido. Recomendamos que você atualize seus scripts e procedimentos para usar o cmdlet <STRONG>Set-MobileDeviceMailboxPolicy</STRONG> .



1.  No Shell, execute o comando a seguir.
    
        Set-MobileDeviceMailboxPolicy -Identity:Default -DevicePasswordEnabled:$true -AlphanumericDevicePasswordRequired:$true -PasswordRecoveryEnabled:$true -MaxEmailAgeFilter:ThreeDays -AllowWiFi:$false -AllowStorageCard:$true -AllowPOPIMAPEmail:$false -IsDefault:$true -AllowTextMessaging:$true -Confirm:$true

## Como saber se funcionou?

Para verificar se você teve êxito ao editar uma política de caixa de correio de dispositivo móvel, siga um destes procedimentos:

1.  No EAC, clique em **Mobile** \> **Política de caixa de correio de dispositivo móvel** e escolha uma diretiva específica. No painel de detalhes, você verá um número das configurações de diretiva listados.

2.  No Shell, execute o comando a seguir.
    
        Get-MobileDeviceMailboxPolicy -Identity <PolicyName>

