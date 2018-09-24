---
title: 'Habilitar/desabilitar caixa de correio do log de auditoria de caixa de correio'
TOCTitle: Habilitar ou desabilitar uma caixa de correio do log de auditoria de caixa de correio
ms:assetid: c4bbfd52-6196-49c7-8c31-777fbbee11f2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff461937(v=EXCHG.150)
ms:contentKeyID: 50486600
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar uma caixa de correio do log de auditoria de caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-09-30_

Log de auditoria com caixa de correio, você pode rastrear logons de uma caixa de correio, bem como quais ações são executadas enquanto o usuário está conectado. Quando você habilita a auditoria de caixa de correio de registro em log para uma caixa de correio, algumas ações executadas pelos administradores e representantes são registrados por padrão. Nenhuma das ações executadas pelo proprietário da caixa de correio são registradas. Para saber que mais sobre a caixa de correio do log de auditoria, consulte [Registro em log de auditoria da caixa de correio](mailbox-audit-logging-exchange-2013-help.md).


> [!CAUTION]
> Auditoria de ações de proprietário da caixa de correio pode gerar um grande número de entradas de log de auditoria de caixa de correio e, portanto, está desabilitada por padrão. Recomendamos que você habilite apenas a auditoria de ações de proprietário específicas necessárias para atender aos requisitos de negócios ou segurança.



Para tarefas adicionais relacionadas à caixa de correio do log de auditoria, consulte [Procedimentos de registro em log de auditoria de caixa de correio](mailbox-audit-logging-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Log de auditoria de caixas de correio" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Você não pode usar o Centro de administração do Exchange (EAC) para habilitar ou desabilitar a caixa de correio do log de auditoria. Você deve usar o Shell.

  - Um administrador que recebeu a permissão de Acesso Completo à caixa de correio de um usuário é considerado um usuário representante.

  - Caixas de correio são consideradas como ser acessado por um administrador apenas nos seguintes cenários:
    
      - A In-Place eDiscovery é usada para pesquisar uma caixa de correio.
    
      - O cmdlet **New-MailboxExportRequest** é usado para exportar uma caixa de correio.
    
      - Editor de MAPI do Microsoft Exchange Server é usado para acessar a caixa de correio.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para habilitar ou desabilitar a caixa de correio do log de auditoria

Você pode usar o Shell para habilitar ou desabilitar uma caixa de correio do log de auditoria de caixa de correio. Isso habilita ou desabilita o registro em log de todas as operações especificado para o proprietário da caixa de correio, representantes e administrador.

Este exemplo habilita a caixa de correio Ben Smith do log de auditoria de caixa de correio.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditEnabled $true
```

Este exemplo desabilita a caixa de correio Ben Smith do log de auditoria de caixa de correio.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditEnabled $false
```

Para informações detalhadas sobre sintaxes e parâmetros, consulte [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Usar o Shell para configurar definições de log de auditoria de caixa de correio para acesso de administrador, representante e proprietário

Quando a auditoria de caixa de correio log está habilitado para uma caixa de correio, somente os administrador delegado e proprietário ações especificadas na configuração do log de auditoria da caixa de correio são registradas.

Este exemplo especifica que serão registradas as ações de `SendAs` ou `SendOnBehalf` realizadas pelos usuários do representante de caixa de correio Ben Smith.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditDelegate SendAs,SendOnBehalf -AuditEnabled $true
```

Este exemplo especifica que as ações `MessageBind` e `FolderBind` executadas pelos administradores serão registradas para caixa de correio Ben Smith.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditAdmin MessageBind,FolderBind -AuditEnabled $true
```

Este exemplo especifica que a ação de `HardDelete` executada pelo proprietário da caixa de correio será registrada para caixa de correio Ben Smith.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditOwner HardDelete -AuditEnabled $true
```

Para informações detalhadas sobre sintaxes e parâmetros, consulte [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar que você com êxito habilitada para uma caixa de correio do log de auditoria de caixa de correio e especificar as configurações de registro em log correto para acesso de proprietário, delegado ou administrador, use o cmdlet [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)) para recuperar as configurações de registro em log de auditoria de caixa de correio para essa caixa de correio.

Este exemplo recupera as configurações de caixa de correio Ben Smith e canaliza as configurações de auditoria especificado, incluindo o limite de idade de log de auditoria, para o cmdlet **Format-List** .

    Get-Mailbox "Ben Smith" | Format-List *audit*

