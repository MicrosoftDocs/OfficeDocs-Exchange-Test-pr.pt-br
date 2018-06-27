---
title: 'Enable or Disable informações de log de gerenciamento de direitos: Exchange 2013 Help'
TOCTitle: Enable or Disable informações de log de gerenciamento de direitos
ms:assetid: 6933bc65-4d98-4878-9167-0e9eaac68b6b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff686962(v=EXCHG.150)
ms:contentKeyID: 50485764
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Enable or Disable informações de log de gerenciamento de direitos

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-12_

No Exchange Server 2013, é possível usar logs de Gerenciamento de Direitos de Informação (IRM) para monitorar e solucionar problemas em operações IRM. O registro em log do IRM está habilitado por padrão.

Os logs de IRM usam o seguinte conjunto de parâmetros comuns:

  - *IrmLogEnabled*   Habilita ou desabilita o registro em log do IRM. Padrão: `$true`.

  - *IrmLogMaxAge*   Especifica a idade máxima dos arquivos de log do IRM. Os arquivos de log anteriores à idade especificada são excluídos. Padrão: 30 dias.

  - *IrmLogMaxDirectorySize*   Especifica o tamanho máximo do diretório que contém os logs de IRM. Quando o diretório atinge o tamanho máximo de arquivo, o servidor exclui primeiro os arquivos de log mais antigos. Padrão: 250 MB.

  - *IrmLogMaxFileSize*   Especifica o tamanho máximo de cada arquivo de log do IRM. Quando um arquivo de log atinge o tamanho especificado, um novo arquivo de log é criado. Padrão: 10 MB.

  - *IrmLogPath*   Especifica a localização do diretório de log do IRM. Padrão: `%ExchangeInstallPath%Logging\IRMLogs`.

Para tarefas de gerenciamento adicionais relacionadas a IRM, consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 2-5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configurar o registro em log do IRM" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - O Centro de Administração do Exchange (EAC) não pode ser usado para habilitar ou desabilitar o registro em log do IRM em um servidor. É necessário usar o Shell

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para habilitar o log do IRM em um servidor

Este exemplo habilita o log do IRM em um servidor de Caixa de Correio.

    Set-TransportService -Identity EXCH01 -IRMLogEnabled $true

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-TransportService](https://technet.microsoft.com/pt-br/library/jj215682\(v=exchg.150\)).

## Usar o Shell para desabilitar o log do IRM em um servidor

Este exemplo desabilita o registro em log do IRM em um servidor de Caixa de Correio.

    Set-TransportService -Identity EXCH01 -IRMLogEnabled $false

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-TransportService](https://technet.microsoft.com/pt-br/library/jj215682\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou o registro em log do IRM com êxito em um servidor, execute o cmdlet [Get-TransportService](https://technet.microsoft.com/pt-br/library/jj215746\(v=exchg.150\)) para recuperar as configurações de IRM.

Este exemplo recupera todas as propriedades de log do IRM no servidor EXCH01.

    Get-TransportService -Identity EXCH01 | Format-List IRMLog*

