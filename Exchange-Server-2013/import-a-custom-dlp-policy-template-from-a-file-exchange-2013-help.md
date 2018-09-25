---
title: 'Importar um modelo de política DLP personalizado de um arquivo'
TOCTitle: Importar um modelo de política DLP personalizado de um arquivo
ms:assetid: 83f49dbd-f9b1-498e-b548-1529c5e1ccdb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150531(v=EXCHG.150)
ms:contentKeyID: 50484746
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importar um modelo de política DLP personalizado de um arquivo

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-08-09_

Você pode gerenciar informações confidenciais por meio de políticas DLP importando um arquivo que contém as configurações de política de informações. Modelos de política DLP podem ser desenvolvidos independente do Exchange como arquivos XML. No entanto, eles devem atender os requisitos de formato específico para funcionar corretamente. Como alternativa, a políticas que são exportadas de uma versão anterior do Exchange podem ser importadas para o Microsoft Exchange Server 2013.


> [!CAUTION]
> Você deve habilitar as políticas de DLP no modo de teste antes de executá-las no seu ambiente de produção. Durante esses testes, recomenda-se que você configure caixas de correio de usuários de amostra e envie mensagens de teste que invoquem as políticas de teste para confirmar os resultados.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada \&quot;Prevenção de perda de dados (DLP)\&quot; no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para importar um modelo de política DLP personalizado de um arquivo

Use o procedimento a seguir para importar um modelo de política DLP personalizado de um arquivo. Para evitar a confusão, forneça um nome exclusivo para cada parte da sua política ou regra quando você tem a opção para fornecer o seu próprio nome.

1.  No EAC, navegue até **gerenciamento de conformidade** \> **prevenção de perda de dados**.

2.  Clique na seta ao lado do ícone de![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar")**AdicionarImportar diretiva**.

3.  Na página **Importar diretiva**, preencha os seguintes campos:
    
    1.  **Selecione o arquivo a ser importado**    Adicione o nome do arquivo de diretiva que você deseja instalar.
    
    2.  **Nome**   Adicionar um nome que irá distinguir essa política das outras.
    
    3.  **Descrição**    Opcionalmente, adicione uma descrição que resuma esta política.
    
    4.  **Mais opções**    Selecione o modo ou estado para esta diretiva. A nova diretiva não está habilitada totalmente até que você especifique o que deve ser. O modo de padrão para uma diretiva é teste sem notificações.
    
    5.  Clique em **próximo** para validar e importar a diretiva.

## Usar o Shell para importar um modelo de política DLP personalizado de um arquivo

Este exemplo importa um arquivo de modelo de política DLP personalizado no arquivo C:\\My Documents\\DLP backup. Importando um conjunto de política DLP a partir de um arquivo XML, remove ou substitui todas as políticas de DLP pré-existente que foram definidas em sua organização. Verifique se você tem um backup do seu conjunto atual de política DLP antes de importar e substituir as políticas de DLP atuais.

```powershell
Import-DlpPolicyCollection -FileData ([Byte[]]$(Get-Content -Path " C:\My Documents\DLP Backup.xml " -Encoding Byte -ReadCount 0))
```

## Para obter mais informações

[Prevenção de perda de dados](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

