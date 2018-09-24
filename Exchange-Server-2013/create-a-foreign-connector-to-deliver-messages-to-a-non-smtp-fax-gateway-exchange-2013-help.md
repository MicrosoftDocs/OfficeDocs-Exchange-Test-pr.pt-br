---
title: 'Criar conector estrangeiro para entregar mensagens a gateway de fax não SMTP'
TOCTitle: Criar um conector estrangeiro para entregar mensagens a um gateway de fax não SMTP
ms:assetid: 589db487-3c4c-409a-92e3-c78dd8f639b6
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ710163(v=EXCHG.150)
ms:contentKeyID: 50485656
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um conector estrangeiro para entregar mensagens a um gateway de fax não SMTP

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-17_

Você pode ter uma situação na qual deseja enviar e receber mensagens de um servidor de gateway de fax que não use SMTP como mecanismo principal de transporte. Siga as etapas descritas neste procedimento para criar um conector estrangeiro que entregue mensagens para sistemas estrangeiros e receba mensagens deles.


> [!TIP]
> Na maioria dos casos onde você deve fornecer mensagens de saída a um sistema que não é SMTP, recomendamos conectores de Agente de Entrega, porque eles permitem o gerenciamento de filas de mensagens, as mensagens não precisam ser gravadas no sistema de arquivos, além de outros benefícios. O tópico <A href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">Agentes de entrega e conectores de agentes de entrega</A> fornece mais detalhes.



Interessado em cenários em que esse procedimento é usado? Consulte os seguintes tópicos:

  - [Planejamento e implantação](planning-and-deployment-for-exchange-2013-installation-instructions.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 30 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectores estrangeiros" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Usar o Shell para criar um conector estrangeiro que envie mensagens para um servidor de gateway não SMTP

1.  Execute o seguinte comando para criar o conector estrangeiro:
    
        New-ForeignConnector -Name "Contoso Foreign Connector" -AddressSpaces "X400:c=US;a=Fabrikam;P=Contoso;5" -SourceTransportServers Hub01,Hub02
    
    Neste exemplo, Hub01 e Hub02 são servidores de origem em sua organização que você designa para enviar mensagens ao sistema estrangeiro. O uso de mais de um servidor de origem oferece tolerância a falhas.

Depois de criar o conector estrangeiro, você pode configurar os diretórios de Recebimento, Retirada e Repetição, dependendo dos requisitos de sua organização.

## Como saber se essa etapa funcionou?

Para confirmar se o conector estrangeiro foi criado com êxito, execute este comando:

```powershell
Get-ForeignConnector | Format-List Name
```

Verifique se o nome do conector estrangeiro que você criou aparece.

## Etapa 2: Usar o Shell para configurar o diretório de recebimento de um servidor de Caixa de Correio executando o serviço Transporte

O diretório de recebimento de um servidor de Caixa de Correio executando o serviço Transporte é usado para entregar mensagens de saída de seu conector estrangeiro.

Você cria um diretório para usar como diretório de recebimento em seu sistema de arquivos local. Você também pode usar um diretório em um compartilhamento de arquivo de rede.

1.  Execute o seguinte script para especificar o diretório de recebimento de seu conector estrangeiro (mude o valor do parâmetro *DropDirectory* para um caminho apropriado ao seu ambiente):
    
    ```powershell
Set-ForeignConnector "Contoso Foreign Connector" -DropDirectory "C:\Drop Directory"
```

## Como saber se essa etapa funcionou?

Para confirmar se você configurou o diretório de recebimento corretamente, execute este script de cmdlet para confirmar o valor do parâmetro *DropDirectory*:

```powershell
Get-ForeignConnector "Contoso Foreign Connector" | Format-List
```

Depois de criar seu conector estrangeiro e especificar o diretório de recebimento, você pode enviar uma mensagem usando o servidor de Caixa de Correio no qual você criou o conector estrangeiro e confirmar se um arquivo é entregue ao diretório de recebimento.

## Etapa 3: Usar o Shell para configurar o diretório de retirada do serviço Transporte em um servidor de Caixa de Correio

O diretório de retirada do serviço Transporte em um servidor de Caixa de Correio é usado para coletar mensagens geradas por sistemas não SMTP. Use esse procedimento quando quiser coletar novas mensagens geradas por um sistema não SMTP, como um servidor de gateway de fax, por meio da transferência de arquivos.

Para obter instruções detalhadas para configurar o diretório de recebimento, consulte [Configurar o diretório de retirada e o diretório de repetição](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md).

## Como saber se essa etapa funcionou?

Para confirmar se você configurou o diretório de retirada corretamente, execute este comando para confirmar o valor do parâmetro *PickupDirectoryPath*:

```powershell
Get-TransportService | Format-List PickupDirectoryPath
```

## Etapa 4: Usar o Shell para configurar o diretório de repetição do serviço Transporte em um servidor de Caixa de Correio

O diretório de repetição do serviço Transporte em um servidor de Caixa de Correio é usado para coletar mensagens geradas por sistemas não SMTP. Use este procedimento para configurar o diretório de repetição quando quiser reenviar mensagens de email, geralmente a partir de um servidor de gateway estrangeiro não SMTP, geradas em seu ambiente do Exchange e exportadas do transporte do Exchange.

Para obter instruções detalhadas para configurar o diretório de recebimento, consulte [Configurar o diretório de retirada e o diretório de repetição](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md).

## Como saber se essa etapa funcionou?

Para confirmar se você configurou o diretório de repetição corretamente, execute este comando para confirmar o valor do parâmetro *ReplayDirectoryPath*:

```powershell
Get-TransportService | Format-List ReplayDirectoryPath
```

## Para obter mais informações

[Conectores externos](foreign-connectors-exchange-2013-help.md)

[Agentes de entrega e conectores de agentes de entrega](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

