---
title: 'Atualizar o Exchange 2013 para a atualização cumulativa ou pacote de serviço mais recente: Exchange 2013 Help'
TOCTitle: Atualizar o Exchange 2013 para a atualização cumulativa ou pacote de serviço mais recente
ms:assetid: 928a4a0b-0082-4d50-a696-bfaf2782f42d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ983803(v=EXCHG.150)
ms:contentKeyID: 52058856
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Atualizar o Exchange 2013 para a atualização cumulativa ou pacote de serviço mais recente

 

_**Aplica-se a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Tópico modificado em:** 2015-09-04_

Se você tiver o Exchange Server 2013 instalado, é possível atualizá-lo para a atualização cumulativa ou service pack mais recente do Exchange 2013. Você pode usar o assistente de Instalação do Exchange 2013 para atualizar sua versão atual do Exchange 2013. Para obter mais informações sobre a atualização cumulativa ou pacote de serviço do Exchange 2013 mais recente, consulte [Atualizações para o Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md). Para saber mais sobre o Exchange 2013, consulte [Novidades do Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).


> [!WARNING]
> Depois de atualizar o Exchange 2013 para uma atualização cumulativa ou pacote de serviço mais recente, não será possível desinstalar a nova versão para revertê-lo para a versão anterior. Se você desinstalar a nova versão, removerá o Exchange do servidor.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 60 minutos

  - Não deixe de ler as notas de versão antes de instalar o Exchange 2013. Para obter mais informações, consulte [Notas de versão do Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - Verifique se o servidor no qual você planeja instalar a atualização cumulativa ou pacote de serviço atende aos requisitos de sistema e aos pré-requisitos. Para obter mais informações, consulte [Requisitos de sistema do Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md) e [Pré-requisitos do Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).
    

    > [!WARNING]
    > Quaisquer configurações personalizadas em cada servidor feitas nos arquivos de configuração de aplicativo XML do Exchange, por exemplo, os arquivos web.config em servidores de acesso para cliente ou o arquivo EdgeTransport.exe.config em servidores de Caixa de Correio, são substituídos quando você instala uma Atualização Cumulativa do Exchange (CU). Não deixe de salvar essas informações para poder reconfigurar facilmente o servidor após a instalação. Você deve redefinir essas configurações depois de instalar uma Atualização Cumulativa.



  - Após instalar uma atualização cumulativa ou pacote de serviço, você deverá reiniciar o computador para que as alterações no registro e no sistema operacional possam ser feitas.


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Instalar a atualização cumulativa ou service pack do Exchange 2013

Você pode instalar a atualização cumulativa ou o service pack do Exchange 2013 usando o Assistente de Instalação ou o modo autônomo. Para obter instruções específicas, consulte os seguintes tópicos:

  - [Instalar o Exchange 2013 usando o Assistente para Configuração](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

  - [Instalar o Exchange 2013 usando o modo autônomo](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)

Se o computador em que você instalou um service pack ou uma atualização cumulativa em é um membro de um grupo de disponibilidade do banco de dados (DAG), siga as etapas na seção [executando manutenção em membros do DAG](managing-database-availability-groups-exchange-2013-help.md) do tópico [Gerenciando grupos de disponibilidade de banco de dados](managing-database-availability-groups-exchange-2013-help.md) .

