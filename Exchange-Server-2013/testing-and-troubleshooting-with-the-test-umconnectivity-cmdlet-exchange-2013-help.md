---
title: 'Testando e Solucionando problemas com o cmdlet Test-UMConnectivity: Exchange 2013 Help'
TOCTitle: Testando e Solucionando problemas com o cmdlet Test-UMConnectivity
ms:assetid: 08e67a99-e37f-4afd-bd58-455b62580af7
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa995978(v=EXCHG.150)
ms:contentKeyID: 56270504
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Testando e Solucionando problemas com o cmdlet Test-UMConnectivity

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-06-25_

Após instalar os servidores da Caixa de Correio e de Acesso do Cliente e configurar a Unificação de Mensagens, você pode usar vários testes de diagnóstico e um aplicativo de telefone baseado em software para testar a conectividade da telefonia e a operação dos serviços de Unificação de Mensagens.

## Test-UMConnectivity

O cmdlet **Test-UMConnectivity** pode ser usado para verificar a conectividade com os servidores de Caixa de Correio e de Acesso do Cliente de várias maneiras, dependendo dos parâmetros usados com o cmdlet. Para testar a funcionalidade de Unificação de Mensagens, é possível usar estes testes:

  - **Local**   O cmdlet **Test-UMConnectivity** verifica a comunicação de Voz sobre IP (VoIP) com os servidores de Caixa de Correio em execução no mesmo computador local.

  - **Local com TUILogon**   O cmdlet **Test-UMConnectivity** tenta estabelecer comunicação VoIP com o servidor de Caixa de Correio que em execução no mesmo computador. Se houver a conexão, ele tentará entrar em uma ou mais caixas de correio habilitadas para UM, enviando o número do ramal e o PIN da caixa de correio. Se o parâmetro *–TUILogon* for dado, os valores de parâmetro a seguir também devem ser fornecidos com as informações adequadas para a caixa de correio de teste:
    
      - *–Phone*   Este parâmetro deve conter o número do ramal da caixa de correio de teste.
    
      - *–PIN*   Este parâmetro deve conter o PIN da caixa de correio habilitada para UM.
    
      - *–UMDialPlan   *Este parâmetro deve conter o plano de discagem ligado à caixa de correio de teste.

  - **Remoto**   O cmdlet **Test-UMConnectivity** tenta conectar-se ao servidor remoto de Acesso do Cliente fazendo uma chamada através de um gateway de VoIP. Após a conexão, são realizadas verificações de conectividade no servidor remoto de Acesso do Cliente e nos caminhos da mídia.
    

    > [!TIP]
    > Se receber a mensagem a seguir, reinicie o serviço de Unificação de Mensagens do MicrosoftExchange porque ele parou ou não está respondendo: "A tarefa Test-UMConnectivity encontrou um erro durante a tentativa de estabelecimento de uma chamada. Detalhes: Não é possível estabelecer uma conexão."


