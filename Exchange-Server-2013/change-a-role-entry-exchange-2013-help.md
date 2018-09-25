---
title: 'Alterar uma entrada de função: Exchange 2013 Help'
TOCTitle: Alterar uma entrada de função
ms:assetid: 5aa4f39c-16a4-4815-ac4f-2cdcfa2b3ee1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298005(v=EXCHG.150)
ms:contentKeyID: 50485652
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterar uma entrada de função

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

Cada entrada da função de gerenciamento em uma função de gerenciamento representa um único cmdlet. Ao adicionar parâmetros para ou remoção de parâmetros de uma entrada de função, que é adicionado a uma função de gerenciamento, você controla se esses parâmetros estão disponíveis nesse cmdlet. Para obter mais informações sobre entradas de função de gerenciamento no Microsoft Exchange Server 2013, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

Você não pode modificar as entradas de função em funções de gerenciamento internas.


> [!NOTE]  
> Este tópico não aborda como modificar entradas de função de gerenciamento sem escopo em uma função de gerenciamento sem escopo. Para obter mais informações sobre como modificar entradas de função sem escopo, consulte <A href="create-a-role-exchange-2013-help.md">Criar uma função</A>.




> [!CAUTION]  
> Para adicionar ou remover parâmetros de uma entrada de função, você deve usar os parâmetros <EM>AddParameter</EM> ou <EM>RemoveParameter</EM> . Se você omitir o parâmetro <EM>AddParameter</EM> ou <EM>RemoveParameter</EM> quando você executa o cmdlet <STRONG>Set-ManagementRoleEntry</STRONG> , somente os parâmetros especificados usando o parâmetro <EM>Parameters</EM> serão incluídos na entrada da função. Todos os outros parâmetros na entrada da função serão removidos.



Procurando outras tarefas de gerenciamento relacionadas a funções? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "funções de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Se você deseja adicionar parâmetros a uma entrada de função, os parâmetros que você adicionar devem existir na entrada da função na função pai. Os parâmetros também devem existir no cmdlet que você especificar.

  - Se você deseja remover parâmetros de uma entrada de função, os parâmetros que você remova não podem existir nas entradas de função de qualquer funções filhas. Você deve remover os parâmetros das entradas de função das funções filhas. Use o procedimento "Usar o Shell para remover um ou mais parâmetros de uma entrada de função" posteriormente neste tópico para remover os parâmetros das entradas de função de todas as funções filhas.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]  
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell Para adicionar um ou mais parâmetros a uma entrada de função

Para adicionar os parâmetros para uma entrada de função, você precisa especificar os parâmetros que você deseja adicionar usando o parâmetro *Parameters* . Em seguida, você precisará especificar o parâmetro *AddParameter* para indicar que você deseja executar uma operação adicionar.

Para adicionar parâmetros a uma entrada de função, use a sintaxe a seguir.

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter
```

Este exemplo adiciona os parâmetros *EmailAddresses* e *Type* para o cmdlet **Set-Mailbox** na função de administradores do destinatário.

```powershell
Set-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" -Parameters EmailAddresses, Type -AddParameter
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd351162\(v=exchg.150\)).

## Usar o Shell para remover um ou mais parâmetros de uma entrada de função

Para remover os parâmetros de uma entrada de função, você precisa especificar os parâmetros que você deseja remover usando o parâmetro *Parameters* . Em seguida, você precisará especificar o parâmetro *RemoveParameter* para indicar que você deseja realizar uma operação remove.

Para remover parâmetros de uma entrada de função, use a sintaxe a seguir.

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter
```

Este exemplo remove os parâmetros *Port*, *ProtocolLoggingLevel*e *SmartHostAuthMechanism* do cmdlet **Set-SendConnector** na função Tier 1 administradores do servidor.

```powershell
Set-ManagementRoleEntry "Tier 1 Server Administrators\Set-SendConnector" -Parameters Port, ProtocolLoggingLevel, SmartHostAuthMechanism -RemoveParameter
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd351162\(v=exchg.150\)).

## Usar o Shell para remover todos os parâmetros de uma entrada de função

Para remover todos os parâmetros de uma entrada de função, você precisará especificar o valor `$Null` no parâmetro *Parameters* . Você não precisa incluir o parâmetro *RemoveParameters* .

Removendo todos os parâmetros de uma entrada de função é mais útil quando você deseja disponibilizar apenas alguns parâmetros em um cmdlet e excluir todos os outros parâmetros. Se você não desejar que a função tenham acesso a um cmdlet, remova a entrada de função associada da função completamente, em vez de simplesmente removendo os parâmetros. Para obter mais informações sobre como remover uma entrada de função de uma função, consulte [Remover uma entrada de função de uma função](remove-a-role-entry-from-a-role-exchange-2013-help.md).


> [!CAUTION]  
> As operações de remoção não podem ser desfeitas. Se você removeu por engano todos os parâmetros de uma entrada de função, será preciso adicioná-los manualmente outra vez.



Para remover todos os parâmetros de uma entrada de função, use a sintaxe a seguir.

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters $Null 
```

Este exemplo remove todos os parâmetros do cmdlet **Set-CASMailbox** na função de administradores do destinatário.

```powershell
Set-ManagementRoleEntry "Recipient Administrators\Set-CASMailbox" -Parameters $Null 
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd351162\(v=exchg.150\)).

## Usar o Shell para aplicar um conjunto específico de parâmetros

Se você quiser apenas um conjunto específico de parâmetros a serem incluídos em uma entrada de função, especifique somente o parâmetro *Parameters* . Não inclua os parâmetros *AddParameter* ou *RemoveParameter* . Quando você especificar apenas o parâmetro *Parameters* , somente os parâmetros especificados no comando estão incluídos na entrada da função. Todos os outros parâmetros são removidos.

Para especificar um conjunto específico de parâmetros, use a sintaxe a seguir.

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>
```

Este exemplo inclui apenas o *Identity*, *DisplayName*, *MissedCallNotificationEnabled*e *PersonalAuthAttendantEnabled* parâmetros do cmdlet **Set-UMMailbox** na função destinatários de email de Seattle.

```powershell
Set-ManagementRoleEntry "Seattle Mail Recipients\Set-UMMailbox" -Parameters Identity, DisplayName, MissedCallNotificationEnabled, PersonalAutoAttendantEnabled
```

Para obter informações detalhadas de sintaxe e parâmetro, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/pt-br/library/dd351162\(v=exchg.150\)).