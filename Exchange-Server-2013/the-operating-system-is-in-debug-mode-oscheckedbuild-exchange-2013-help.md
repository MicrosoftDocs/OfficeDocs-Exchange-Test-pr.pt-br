---
title: 'O sistema operacional está no mode_OSCheckedBuild de depuração: Exchange 2013 Help'
TOCTitle: O sistema operacional está no mode_OSCheckedBuild de depuração
ms:assetid: 93a1380f-1388-494d-8f78-92dfefd069bd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.oscheckedbuild(v=EXCHG.150)
ms:contentKeyID: 50486211
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O sistema operacional está no mode\_OSCheckedBuild de depuração

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2016-12-15_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

O Microsoft® Exchange Server Analyzer Tool consultará a classe do Microsoft Windows® Management Instrumentation (WMI) **Win32\_OperatingSystem** para determinar se um valor for definido para a propriedade de **depuração** . Se o valor para essa chave em um computador com Exchange Server é definido como **True**, um erro será exibido.

Modo de depuração do Windows é alternado adicionando o **parâmetro/depuração** do Boot ini. **Quando/debug** é especificado no arquivo Boot. ini de um computador Windows Server, o depurador do kernel é carregado durante a inicialização e mantido na memória em todas as ocasiões. Isso permite que um profissional de suporte discar para o sistema está sendo depurado e quebrará no depurador, mesmo quando o sistema não está suspenso em uma tela de Kernel PARAR. Ao contrário da opção **/crashdebug** , a **opção/depuração** usa a porta COM se você estiver depurando ou não. Essa opção é usada quando estiver depurando problemas que podem ser reproduzidos regularmente. É provável que o **parâmetro/depuração** foi definido como um meio para solucionar um problema e foi definido acidentalmente para a esquerda.

Por causa dos processos adicionais que estão sendo executados, o desempenho é afetado significativamente. Portanto, não é recomendável executando o Exchange Server em um computador onde o Windows está sendo executado no modo de depuração.

Para eliminar esse erro, edite. ini e remova o **parâmetro/depuração** .

## Para corrigir esse erro

1.  No Windows Explorer, navegue até a partição do sistema. Esta é a partição que contém os arquivos específicos do hardware como Boot. ini e NTLDR.

2.  Se você não conseguir ver. ini, é possível como as **Opções de pasta** estão definidas para **Ocultar arquivos de sistema operacional protegidos**. Se este for o caso, na janela do Windows Explorer, clique em **Ferramentas**, clique em **Opções de pasta**e clique em **Exibir**. Desmarque a caixa de seleção **Ocultar protegidos arquivos de sistema operacional (recomendado)** . Quando solicitado, clique em **Sim**.

3.  Quando o ini estiver visível no Windows Explorer, direito o arquivo, clique em **Abrir com**e selecione **Bloco de notas** , abra o arquivo.

4.  Na seção **\[sistemas operacionais\]** , remova o **parâmetro/depuração** .

5.  Salve e feche o arquivo e reinicie o computador do Exchange Server para que a alteração entre em vigor.

Para obter mais informações sobre os parâmetros que podem ser usados no arquivo Boot. ini, consulte o artigo da Base de Conhecimento Microsoft 833721, "opções de switch disponíveis para o Windows XP e os arquivos de Boot. ini do Windows Server 2003" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=833721](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=833721)).

