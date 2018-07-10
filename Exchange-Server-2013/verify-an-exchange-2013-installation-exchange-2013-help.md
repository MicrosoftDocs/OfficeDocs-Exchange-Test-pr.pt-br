---
title: 'Verificar uma instalação do Exchange 2013: Exchange 2013 Help'
TOCTitle: Verificar uma instalação do Exchange 2013
ms:assetid: fdd20a2a-c8c1-4d17-b813-3c05d88a4411
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125254(v=EXCHG.150)
ms:contentKeyID: 50487093
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Verificar uma instalação do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Após instalar o Microsoft Exchange Server 2013, recomendamos que você verifique se a instalação executando o cmdlet **Get-ExchangeServer** e examinando o arquivo de log de instalação. Se o processo de instalação falha ou erros ocorrem durante a instalação, você pode usar o arquivo de log de instalação para controlar a origem do problema.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

## Executar Get-ExchangeServer

Para verificar se o Exchange 2013 foi instalado com sucesso, execute o cmdlet **Get-ExchangeServer** no Shell de Gerenciamento do Exchange. É exibida uma lista de todas as funções do servidor Exchange 2013 que são instaladas no servidor especificado quando esse cmdlet é executado.

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ExchangeServer](https://technet.microsoft.com/pt-br/library/bb123873\(v=exchg.150\)).

## Examinar o arquivo de log de instalação

Você também pode saber mais sobre a instalação e a configuração do Exchange 2013 examinando o arquivo de log de instalação criado durante o processo de instalação.

Durante o processo, a Instalação do Exchange registra eventos de log de **Aplicativo** do **Visualizador de Eventos** em computadores que executam o Windows Server 2008 R2 com Service Pack 1 (SP1) e o Windows Server 2012. Examine o log de **Aplicativo** e verifique se não há mensagens de aviso ou erro relacionadas à instalação do Exchange. Esses arquivos de log contêm um histórico de cada ação que o sistema executa durante a instalação do Exchange 2013 e quaisquer erros que possam ter ocorrido. Por padrão, o método de registro em log está definido como `Verbose`. Existem informações disponíveis para cada função de servidor instalada.

O arquivo de log de instalação está disponível em *\<system drive\>*\\ExchangeSetupLogs\\ExchangeSetup.log. A variável *\<system drive\>* representa o diretório raiz da unidade na qual o sistema operacional está instalado.

O arquivo de log de instalação acompanha o progresso de todas as tarefas executadas durante a instalação e a configuração do Exchange 2013. O arquivo contém informações sobre o status das verificações de pré-requisitos e da preparação do sistema, executadas antes do início da instalação, sobre o progresso da instalação do aplicativo e sobre as alterações de configuração feitas no sistema. Verifique esse arquivo de log para saber se as funções de servidor foram instaladas conforme o esperado.

Convém iniciar o exame do arquivo de log de instalação procurando erros. Se encontrar uma entrada que indique a ocorrência de um erro, leia o respectivo texto para determinar a causa do erro.

