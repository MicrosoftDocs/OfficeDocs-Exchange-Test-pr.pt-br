---
title: 'Configurar propriedades de cópia de banco de dados de caixa de correio'
TOCTitle: Configurar propriedades de cópia de banco de dados de caixa de correio
ms:assetid: cf186561-ab2c-45c0-90f5-8d3ecfabeeac
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351151(v=EXCHG.150)
ms:contentKeyID: 50486673
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar propriedades de cópia de banco de dados de caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-01_

Cada cópia do banco de dados de caixa de correio tem suas próprias propriedades que podem ser definidas. Incluem a quantidade de tempo, se houver, para o número de preferência de ativação e de retardo de truncamento e de retardo de repetição. Para obter mais informações sobre o número de preferência de ativação, de retardo de truncamento e de retardo de repetição, consulte [Gerenciando cópias de banco de dados de caixa de correio](managing-mailbox-database-copies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte oEntrada "Cópias de banco de dados da caixa de correio" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar propriedades de cópia de banco de dados de caixa de correio

1.  Na EAC, vá até **Servidores** \> **Bancos de dados**.

2.  Selecione o banco de dados que você deseja configurar.

3.  No painel de detalhes, em **Cópias de banco de dados**, clique em **Exibir detalhes** para a cópia do banco de dados desejado e, em seguida, exibir ou configurar o seguinte:
    
      - **Banco de dados**    Exibe o nome do banco de dados selecionado.
    
      - **Servidor de caixa de correio**    Exibe o nome do servidor de caixa de correio que hospeda a cópia do banco de dados selecionado.
    
      - **Estado do índice de conteúdo**    Exibe o estado atual do índice de conteúdo para a cópia do banco de dados selecionado.
    
      - **Status**    Exibe o status atual da cópia do banco de dados selecionado.
    
      - **Copie o comprimento da fila**    Indica o número de arquivos de log aguardando para serem copiados para a cópia do banco de dados selecionado. Este campo é relevante apenas para cópias passivas do banco de dados.
    
      - **Comprimento da fila de repetição**    Indica o número de arquivos de log aguardando para ser copiado para a cópia do banco de dados selecionado. Este campo é relevante apenas para cópias passivas do banco de dados.
    
      - **Mensagens de erro**    Exibe todas as mensagens de erro para cópias de banco de dados que têm um status de `Failed` ou `Failed and Suspended`.
    
      - **Última hora de log disponíveis**    Exibe o carimbo de data e hora do arquivo de log gerado mais recentemente na cópia ativa do banco de dados. Este campo é relevante apenas para cópias passivas do banco de dados. Em cópias de banco de dados ativo (replicadas e autônomas), esse campo exibirá **nunca**.
    
      - **Horário da última inspecionados log**    Exibe o carimbo de data e hora do último arquivo de log foi inspecionado pelo LogInspector na cópia do banco de dados selecionado. Este campo é relevante apenas para cópias passivas do banco de dados. Em cópias de banco de dados ativo (replicadas e autônomas), esse campo exibirá **nunca**.
    
      - **Hora do último log copiado**    Exibe o carimbo de data e hora do último arquivo de log que foi copiado com o LogCopier na cópia do banco de dados selecionado. Este campo é relevante apenas para cópias passivas do banco de dados. Em cópias de banco de dados ativo (replicadas e autônomas), esse campo exibirá **nunca**.
    
      - **Hora da última repetição do log**    Exibe o carimbo de data e hora do último arquivo de log que foi copiado pelo LogReplayer para a cópia do banco de dados selecionado. Este campo é relevante apenas para cópias passivas do banco de dados. Em cópias de banco de dados ativo (replicadas e autônomas), esse campo exibirá **nunca**.
    
      - **Número de preferência de ativação**    Exibe o número de preferência de ativação. Isso é usado como parte do processo de seleção de melhor cópia do Gerenciador ativo e para balancear o DAG através da redistribuição bancos de dados de caixa de correio ativas em todo o DAG usando o script Redistributeactivedatabases ps1. O valor de preferência de ativação é um número igual ou maior que 1, onde 1 é na parte superior da ordem de preferência. O número não pode ser maior que o número de cópias do banco de dados de caixa de correio.
    
      - **Retardo de repetição tempo (dias)**    Exibe a quantidade de tempo que o serviço Microsoft Exchange Information Store deve aguardar antes de repetir arquivos de log que foram copiados pelo serviço de replicação do Microsoft Exchange para a cópia passiva do banco de dados. A definição deste parâmetro como um valor maior do que 0 cria uma cópia do banco de dados com atraso. A configuração padrão para este valor é 0 dias. O valor máximo permitido para essa configuração é 14 dias. O valor mínimo permitido é 0 dias e a definição desse valor como 0 desabilita o atraso de repetição.

## Use o Shell para configurar propriedades de cópia de banco de dados de caixa de correio

Este exemplo configura uma cópia do banco de dados de caixa de correio com um número de preferência de ativação de 3.

```powershell
Set-MailboxDatabaseCopy -Identity DB3\EX3 -ActivationPreference 3
```

Este exemplo configura uma cópia do banco de dados DB1 hospedado no servidor1 com um tempo de retardo de repetição e tempo de retardo de truncamento de 1 dia e um número de preferência de ativação de 2.

    Set-MailboxDatabaseCopy -Identity DB1\Server1 -ReplayLagTime 1.0:0:0 -TruncationLagTime 1.0:0:0 -ActivationPreference 2

## Como saber se funcionou?

Para verificar se você configurou com êxito uma cópia do banco de dados de caixa de correio, siga um destes procedimentos:

  - No EAC, navegue até **Servidores** \> **Bancos de dados**. Selecione o banco de dados apropriado e, no painel Detalhes, clique em **Exibir detalhes**, para exibir as propriedades de cópia do banco de dados.

  - No Shell, execute o seguinte comando para exibir informações de configuração de uma cópia do banco de dados.
    
    ```powershell
Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List
```

## Para saber mais

[Set-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd298104\(v=exchg.150\))

[Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/pt-br/library/dd298044\(v=exchg.150\))

[Get-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb124924\(v=exchg.150\))

