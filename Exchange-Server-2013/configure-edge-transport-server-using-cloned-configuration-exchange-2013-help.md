---
title: 'Configurar o servidor de transporte de borda usando configuração clonada: Exchange 2013 Help'
TOCTitle: Configurar o servidor de transporte de borda usando configuração clonada
ms:assetid: 0bbc83e3-e5e8-4480-a8a6-15f035360856
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996008(v=EXCHG.150)
ms:contentKeyID: 61183345
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o servidor de transporte de borda usando configuração clonada

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-04-13_

Você pode usar os scripts do Shell de Gerenciamento do Exchange fornecidos (localizados em %ExchangeInstallPath%Scripts) para duplicar a configuração de um servidor Transporte de Borda. Esse processo é chamado de *configuração clonada*. *Configuração clonada* é a prática de implementar novos servidores de Transporte de Borda com base nas informações de configuração de um servidor de origem configurado anteriormente. As informações de configuração de um servidor de origem configurado anteriormente são copiadas e exportadas para um arquivo XML, que é importado para o servidor de destino. Para ter uma visão geral deste processo, consulte [Configuração clonada do servidor de transporte de borda](edge-transport-server-cloned-configuration-exchange-2013-help.md).

As informações de configuração do servidor de Transporte de Borda são armazenadas nos serviços AD LDS e não são replicadas entre vários servidores de Transporte de Borda. Usando a configuração clonada, você pode garantir que todos os servidores Transporte de Borda implantados em sua rede de perímetro estejam usando a mesma configuração.

Dois scripts do Shell são usados para executar tarefas de configuração clonada:

  - **ExportEdgeConfig.ps1**   Exporta todas as definições configuradas pelo usuário e os dados de um servidor Transporte de Borda e armazena esses dados em um arquivo XML.

  - **ImportEdgeConfig.ps1**   Durante a etapa de validação da configuração, o script ImportEdgeConfig.ps1 examina o arquivo XML para verificar se as configurações de exportação específicas do servidor são válidas para o servidor de destino. Se as configurações precisarem ser modificadas, o script gravará as configurações inválidas em um arquivo de resposta que você modificará para especificar as informações do servidor de destino usadas durante a etapa de importação de configuração. Durante a etapa de importação de configuração, o script importa todos os dados e as configurações definidas pelo usuário armazenados no arquivo XML intermediário criado pelo script ExportEdgeConfig.ps1.

Ambos os scripts estão localizados na pasta %ExchangeInstallPath%Scripts.

## Antes de você começar

  - Tempo estimado para a conclusão da tarefa: 30 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Servidores de Transporte de Borda" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - A configuração clonada não duplica as configurações de Inscrição de Borda de um servidor. Os certificados EdgeSync não são clonados. Você deve executar o processo do EdgeSync separadamente para cada servidor de Transporte de Borda. O EdgeSync sobrescreve todas as configurações que estiverem incluídas em informações de configuração clonada e informações de replicação do EdgeSync.

  - Se algum Conector de envio estiver configurado para usar credenciais, a senha será gravada no arquivo XML intermediário como uma de cadeia de caracteres criptografada. Você pode usar o parâmetro *-key* com os scripts ImportEdgeConfig.ps1 e ExportEdgeConfig.ps1 para especificar a cadeia de caracteres de 32 bytes a ser usada para criptografar e descriptografar senhas. Se você não usar o parâmetro *-key*, uma chave de criptografia padrão será usada.

  - Você só pode usar o Shell para executar esse procedimento. Para saber como abrir o Shell de Gerenciamento do Exchange em sua organização Exchange local, confira [Abra o shell.](https://technet.microsoft.com/pt-br/library/dd638134\(v=exchg.150\)).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Exporte os dados de configuração do servidor de origem para um arquivo no servidor de origem

1.  Copie o script ExportEdgeConfig.ps1 para a pasta raiz do seu perfil de usuário no servidor de origem.

2.  Para exportar os dados de configuração do servidor de origem para um arquivo no servidor de origem, use a sintaxe a seguir.
    
        ./ExportEdgeConfig.ps1 -CloneConfigData:"<configuration file>"
    
    Por exemplo, para exportar os dados de configuração de servidor de origem para o arquivo C:\\CloneConfigData.xml, execute o comando a seguir.
    
        ./ExportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml"

## Como saber se essa etapa funcionou?

Você saberá que exportou com êxito os dados de configuração de origem para um arquivo quando a mensagem de confirmação "Dados de configuração de Borda exportados com êxito para: \<caminho de arquivo de saída\>" aparecer.

## Etapa 2: Validar o arquivo de configuração e criar um arquivo de resposta no servidor de destino

1.  Copie o arquivo de configuração do servidor de origem que você exportou na etapa anterior para o servidor de Transporte de Borda de destino.

2.  Copie o script ImportEdgeConfig.ps1 para a pasta raiz do seu perfil de usuário no servidor de destino.

3.  Para validar o arquivo de configuração e usar os resultados para criar um arquivo de resposta no servidor de destino, use a sintaxe a seguir.
    
        ./ImportEdgeConfig.ps1 -CloneConfigData:"<configuration file>" -IsImport $false -CloneConfigAnswer:"<answer file>"
    
    Por exemplo, para validar o arquivo de configuração C:\\CloneConfigData.xml e criar o arquivo de resposta C:\\CloneConfigAnswer.xml, execute o comando a seguir.
    
        ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $false -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"

4.  Abra o arquivo de resposta e modifique quaisquer configurações que sejam inválidas para o servidor de destino. Se nenhuma modificação for necessária, o arquivo de resposta não terá entradas. Salve suas alterações.

## Como saber se essa etapa funcionou?

Você saberá que validou com êxito o arquivo de configuração e que criou um arquivo de resposta quando a mensagem de confirmação "Arquivo de resposta foi criado com êxito" aparecer.

## Etapa 3: Importar o arquivo de configuração no servidor de destino

Para importar o arquivo de configuração no servidor de destino, use a sintaxe a seguir.

    ./ImportEdgeConfig.ps1 -CloneConfigData:"<Configuration file>" -IsImport $true -CloneConfigAnswer:"<answer file>"

Por exemplo, para validar o arquivo de configuração C:\\CloneConfigData.xml usando o arquivo de resposta C:\\CloneConfigAnswer.xml, execute o comando a seguir.

    ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $true -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"

## Como saber se essa etapa funcionou?

Você saberá que importou com êxito o arquivo de configuração no servidor de destino quando a mensagem de confirmação "A importação das informações de configuração de Borda foi bem-sucedida" aparecer.

