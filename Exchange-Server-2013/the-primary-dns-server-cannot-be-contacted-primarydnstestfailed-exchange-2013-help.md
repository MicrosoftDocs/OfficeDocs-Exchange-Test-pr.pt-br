---
title: 'O servidor DNS primário não pode ser contatado: Exchange 2013 Help'
TOCTitle: O servidor DNS primário não pode ser contacted_PrimaryDNSTestFailed
ms:assetid: 5b39cb64-c8f1-4fd3-843b-ecd23f99fe3a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.primarydnstestfailed(v=EXCHG.150)
ms:contentKeyID: 50485676
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O servidor DNS primário não pode ser contacted\_PrimaryDNSTestFailed

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

A instalação do Microsoft® Exchange Server 2007 não pode continuar porque não é possível estabelecer comunicação com o servidor primário do sistema de nome de domínio (DNS).

A instalação do Exchange 2007 requer que o computador local se comunicar com o banco de dados do DNS autoritativo para o domínio.

Microsoft Exchange depende de DNS para resolver o endereço IP, seu próximo interno ou externo do servidor de destino.

Comunicação com o servidor DNS primário pode falhar pelos seguintes motivos:

  - A configuração de TCP/IP local não aponta para o servidor DNS correto.

  - O servidor DNS está inoperante ou inacessível devido a uma falha de rede ou por outros motivos.

Para resolver esse problema:

  - Verifique se a configuração de TCP/IP local aponta para o servidor DNS correto.

Para verificar a configuração de TCP/IP local

1.  Revise a configuração de TCP/IP local:
    
    Para obter mais informações, consulte "Configurar o TCP/IP para usar o DNS" ([https://go.microsoft.com/fwlink/?LinkId=68094](https://go.microsoft.com/fwlink/?linkid=68094)).

<!-- end list -->

  - Verifique se o servidor DNS está sendo executado e pode ser contatado.

Para verificar se o servidor DNS está sendo executado e pode ser contatado

1.  Verifique se que o servidor DNS está sendo executado, seguindo um ou mais dos seguintes verificações:
    
      - Examinar o status do servidor DNS do programa de administração do DNS no servidor DNS.
    
      - Reinicie o servidor DNS.
        
        Para obter mais informações, consulte "Iniciar, parar, pausar ou reiniciar um servidor DNS" ([https://go.microsoft.com/fwlink/?LinkId=62999](https://go.microsoft.com/fwlink/?linkid=62999)).
    
      - Verifique se a capacidade de resposta do servidor DNS usando o comando **nslookup**.
        
        Para obter mais informações, consulte as instruções em "Verificar a capacidade de resposta do servidor DNS usando o comando nslookup" ([https://go.microsoft.com/fwlink/?LinkId=63000](https://go.microsoft.com/fwlink/?linkid=63000)).

