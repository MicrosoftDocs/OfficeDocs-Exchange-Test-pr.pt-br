---
title: 'Reverter uma migração de pasta pública do Exchange 2013 para o Exchange Online'
TOCTitle: Reverter uma migração de pasta pública do Exchange 2013 para o Exchange Online
ms:assetid: bcd54aa0-aa45-4c68-b504-1475842d4b96
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt798259(v=EXCHG.150)
ms:contentKeyID: 74432747
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Reverter uma migração de pasta pública do Exchange 2013 para o Exchange Online

 

_**Tópico modificado em:** 2017-03-20_

**Resumo:**  siga estas etapas para retornar sua infraestrutura de pasta pública ao seu estado de pré-migração em sua organização do Exchange 2013 local.

Se você encontrar problemas com sua migração de pastas públicas para o Exchange Online, ou por outra necessidade motivo reativar suas pastas públicas do Exchange 2013, siga as etapas abaixo.

## Reverter a migração

Observe que, se você reverter a migração, você perderá qualquer conteúdo que foi adicionado a pastas públicas no Exchange Online pós-migração, através de clientes ou através de emails para pastas públicas habilitadas para email. Para salvar esse conteúdo, você pode exportar o conteúdo de pasta pública de pós-migração para um arquivo. pst, que, em seguida, pode ser importado para as pastas públicas do local quando a reversão é concluída.

1.  Em seu ambiente do Exchange local, execute o seguinte comando para desbloquear suas pastas públicas do Exchange 2013 (Observe que o desbloqueio pode levar várias horas):
    
        Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false -PublicFoldersEnabled Local 

2.  Em seu ambiente do Exchange local, reverta o `ExternalEmailAddress` de qualquer pasta pública habilitada para email que foi atualizada por SetMailPublicFolderExternalAddress.ps1 (o script usado na *etapa 8: testar e desbloquear a pastas públicas no Exchange Online* de [Usar a migração de lote para migrar pastas públicas do Exchange 2013 para o Exchange Online](https://docs.microsoft.com/pt-br/exchange/collaboration-exo/public-folders/batch-migration-of-exchange-2013-public-folders)). Você pode consultar o arquivo de resumo criado pelo script para identificar aqueles que foram modificados ou use o arquivo OnPrem\_MEPF.xml arquivo gerado anteriormente no mesmo processo migriont lote para obter as propriedades originais de todas as pastas públicas habilitadas para email.

3.  No PowerShell do Exchange Online, execute os seguintes comandos para remover todas as pastas públicas do Exchange Online e caixas de correio:
    
        Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
        Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true

4.  Execute o seguinte comando em seu ambiente Exchange Online para redirecionar o tráfego de pasta pública volta para o local (Exchange 2013):
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote

5.  Consulte [Configurar pastas públicas do Exchange 2013 para uma implantação híbrida](https://docs.microsoft.com/pt-br/exchange/collaboration-exo/public-folders/set-up-modern-hybrid-public-folders) para obter instruções sobre reconfiguração acesso às suas pastas públicas no local, para que os usuários do Exchange Online possam acessá-los.

