---
title: 'Criar uma caixa de correio de pasta pública: Exchange 2013 Help'
TOCTitle: Criar uma caixa de correio de pasta pública
ms:assetid: 64437ffd-231b-4c10-84df-232ccbe9538f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ552410(v=EXCHG.150)
ms:contentKeyID: 50485851
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma caixa de correio de pasta pública

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2014-10-23_

Antes de criar uma pasta pública, você deve criar uma caixa de correio de pasta pública. As caixas de correio de pasta pública contém as informações de hierarquia mais o conteúdo para as pastas públics. A primeira caixa de correio de pasta pública que você cria será a caixa de correio principal da hierarquia, que contém a única cópia editável da hierarquia. Qualquer caixa de correio de pasta pública adicional que você criar será um caixa de correio secundária, que terá apenas uma cópia somente de leitura da hierarquia.


> [!TIP]
> Para saber mais sobre as cotas de armazenamento e limites para pastas públicas, consulte os seguintes tópicos: 
> <UL>
> <LI>
> <P>Para pastas públicas no Office 365, confira <A href="https://go.microsoft.com/fwlink/?linkid=391188">Limites do Exchange Online</A>.</P>
> <LI>
> <P>Para pastas públicas no Exchange Server 2013 local, consulte <A href="limits-for-public-folders-exchange-2013-help.md">Limites para pastas públicas</A>.</P></LI></UL>



Para conhecer tarefas de gerenciamento adicionais relacionadas a pastas públicas no Exchange 2013, consulte [Procedimentos de pasta pública](public-folder-procedures-exchange-2013-help.md).

Para conhecer tarefas de gerenciamento adicionais relacionadas a pastas públicas no Exchange Online, consulte [Procedimentos de pasta pública no Office 365 e Exchange Online](https://technet.microsoft.com/pt-br/library/jj966272\(v=exchg.150\)).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: menos de 5 minutos.

  - Pastas públicas do Exchange 2013 e pastas públicas em servidores Exchange herdados não podem existir na mesma organização. Se você tentar criar uma caixa de correio de pasta pública quando você ainda tiver pastas públicas herdadas, você receberá o erro **uma pasta pública existente implantação foi detectada. Para migrar dados de pasta pública existentes, criar a nova caixa de correio de pasta pública usando a opção - HoldForMigration.**
    
    Antes de criar pastas públicas no Exchange 2013, será preciso migrar suas pastas públicas herdadas para o Exchange 2013. Para fazer isso, siga as etapas descritas em [Use serial migração para migrar pastas públicas para o Exchange 2013 de versões anteriores](https://technet.microsoft.com/pt-br/library/jj150486\(v=exchg.150\)). Estas etapas mostram como criar uma caixa de correio de pasta pública que pode ser usada para armazenar suas pastas públicas migradas.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Pastas públicas" no tópico [Permissões de compartilhamento e colaboração](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## O que você deseja fazer?

## Usar o EAC para criar uma caixa de correio de pasta pública

1.  Navegue até **Pastas públicas** \> **Caixas de correio de pastas públicas** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na página **Caixa de Correio de Pasta Pública**, insira um nome para a caixa de correio de pasta pública.

3.  Clique em **Salvar**.

## Use o Shell para criar uma caixa de correio de pasta pública

Este exemplo cria uma caixa de correio de pasta pública principal.

    New-Mailbox -PublicFolder -Name MasterHierarchy

Este exemplo cria uma caixa de correio de pasta pública secundária. A única diferença entre criar a caixa de correio principal da hierarquia e um caixa de correio secundária da hierarquia é a caixa de correio principal é a primeira que foi criada para a organização. Você ode criar caixas de correio de pasta pública adicionais para balanceamento de carga.

    New-Mailbox -PublicFolder -Name Istanbul 

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-Mailbox](https://technet.microsoft.com/pt-br/library/aa997663\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou com sucesso a caixa de correio da pasta pública principal, execute o seguinte comando no Shell:

    Get-OrganizationConfig | Format-List RootPublicFolderMailbox

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997571\(v=exchg.150\)).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

