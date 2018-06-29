---
title: 'Present_FirstSGFilesExist de arquivos de banco de dados mais antigos: Exchange 2013 Help'
TOCTitle: Present_FirstSGFilesExist de arquivos de banco de dados mais antigos
ms:assetid: 907faeb8-1c6d-49fc-95a1-417f415a9d79
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.firstsgfilesexist(v=EXCHG.150)
ms:contentKeyID: 50486173
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Present\_FirstSGFilesExist de arquivos de banco de dados mais antigos

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft® Exchange Server 2007 não pode continuar porque detectou arquivos de banco de dados do Microsoft Exchange existentes no caminho de instalação de destino.

Instalação do Exchange 2007 requer que o caminho de instalação de destino estar vazio dos arquivos de banco de dados do Microsoft Exchange.

Para resolver esse problema, remova todos os arquivos existentes caminhos de instalação de destino e, em seguida, execute novamente a instalação.

Para excluir os arquivos de banco de dados existentes do Exchange Server do caminho de instalação de destino

1.  Em Meu computador ou no Windows Explorer, localize o caminho de instalação de destino.
    

    > [!TIP]
    > Por padrão, os arquivos de banco de dados estão localizados em:<BR>&lt; unidade_do_sistema &gt;: \Program Server\Mailbox\First grupo de armazenamento.



2.  Os arquivos a serem removidas do mouse em e selecione **Excluir**.

3.  Na caixa de diálogo **Confirmar exclusão de arquivo**, clique em **Sim**.

4.  Repita as etapas 2 e 3 para todos os arquivos nos caminhos de instalação de destino.

