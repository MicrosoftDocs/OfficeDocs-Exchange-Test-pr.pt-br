---
title: 'Excluir e recriar a caixa de correio de descoberta padrão no Exchange: Exchange 2013 Help'
TOCTitle: Excluir e recriar a caixa de correio de descoberta padrão no Exchange
ms:assetid: 4bde0b00-bdf7-44b4-ba64-aa062bc10ca2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn750894(v=EXCHG.150)
ms:contentKeyID: 62371338
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Excluir e recriar a caixa de correio de descoberta padrão no Exchange

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-05-04_

Você pode usar o Shell de Gerenciamento do Exchange para excluir a caixa de correio de descoberta padrão, recriá-la e atribuir permissões a ela.

## Por que eu faria isso?

Em Exchange Server 2013 e Exchange Online, o tamanho máximo da caixa de correio de descoberta padrão é 50 GB. Ele é usado para armazenar os resultados da pesquisa de descoberta eletrônica In-loco. Antes do limite de tamanho foi alterado, as organizações podem aumentar a cota de armazenamento para mais de 50 GB. Como resultado, as caixas de correio de descoberta pode aumentar para mais de 50 GB. Existem três problemas com uma caixa de correio de descoberta padrão que é maior do que 50 GB:

  - Não há suporte.

  - Não é possível migrá-las para o Office 365.

  - Se a caixa de correio de descoberta padrão no Exchange Server 2010, ele não pode ser atualizado para Exchange Server 2013.

O modo como você resolve isso depende se você deseja salvar os resultados da pesquisa de uma caixa de correio de descoberta padrão que ultrapassou 50 GB.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Você deseja salvar os resultados da pesquisa?</th>
<th>Faça isto</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Não</p></td>
<td><p>Execute as etapas deste tópico para excluir e recriar a caixa de correio de descoberta padrão.</p></td>
</tr>
<tr class="even">
<td><p>Sim</p></td>
<td><p>Execute as etapas em <a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">Reduzir o tamanho de uma caixa de correio de descoberta no Exchange</a>.</p></td>
</tr>
</tbody>
</table>


## Use o Shell de Gerenciamento do Exchange para excluir e recriar a caixa de correio de descoberta padrão


> [!TIP]
> É possível usar Centro de administração do Exchange (EAC), porque as caixas de correio de descoberta não são exibidas no EAC.



1.  Execute o seguinte comando para excluir a caixa de correio de descoberta padrão.
    
        Remove-Mailbox "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}"

2.  Na mensagem que questiona se você deseja confirmar a exclusão da caixa de correio e do objeto de usuário do Active Directory correspondente, digite **Y** e pressione Enter.
    
    Um novo objeto de usuário é criado no Active Directory quando você cria a caixa de correio de descoberta na próxima etapa.

3.  Execute o seguinte comando para recriar a caixa de correio de descoberta padrão.
    
        New-Mailbox -Name "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -Alias "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -DisplayName "Discovery Search Mailbox" -Discovery

4.  Para atribuir permissões ao grupo de função Gerenciamento de Descoberta para abrir a caixa de correio de descoberta padrão e acessar os resultados da pesquisa, execute o seguinte comando:
    
        Add-MailboxPermission "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User "Discovery Management" -AccessRights FullAccess -InheritanceType all

