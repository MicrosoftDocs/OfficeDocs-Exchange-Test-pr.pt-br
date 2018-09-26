---
title: 'Switchovers do Datacenter: Exchange 2013 Help'
TOCTitle: Switchovers do Datacenter
ms:assetid: ac208c12-04d0-4809-bacd-72478ff14983
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351049(v=EXCHG.150)
ms:contentKeyID: 62523819
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Switchovers do Datacenter

 

_**Aplica-se a:** Exchange Server 2013 SP1_

_**Tópico modificado em:** 2016-03-17_

Em uma configuração resiliente do site, a recuperação automática como resposta a uma falha no nível do site pode ocorrer dentro de um DAG, o que permite que o sistema de mensagens permaneça em um estado funcional. Essa configuração exige pelo menos três locais, devido ao fato de exigir a implantação dos membros DAG em dois locais e do servidor testemunha do DAG em um terceiro local.

Se você não tiver três locais, ou mesmo se tiver três locais mas não quiser controlar as ações de recuperação no nível do datacenter, é possível configurar o DAG para recuperação manual, caso haja uma falha de nível de site. Nesse caso, você executaria um processo chamado *alternância de datacenter*. Assim como em muitos cenários de recuperação de desastres, o planejamento e a preparação antecipada para uma alternância de datacenter podem simplificar o processo de recuperação e reduzir o tempo de interrupção.

Há quatro etapas básicas que devem ser concluídas para a realização de uma alternância de datacenter após a decisão inicial de ativar o segundo datacenter:

1.  **Encerrar um datacenter em execução parcial**   Esta etapa envolve encerrar os serviços do Exchange no datacenter principal, se quaisquer serviços ainda estiverem em execução. Isso é particularmente importante para a função de servidor Caixa de Correio, pois utiliza um modelo de alta disponibilidade ativo/passivo. Se os serviços de um datacenter com falha parcial não forem interrompidos, é possível que o datacenter com falha parcial afete de maneira negativa os serviços durante uma alternância de volta ao datacenter primário.
    

    > [!IMPORTANT]
    > Se a rede ou a confiabilidade da infraestrutura do Active Directory&nbsp;forem comprometidas como resultado da falha no datacenter&nbsp;primário,&nbsp;recomendamos que todos os serviços de mensagem sejam desativados até que essas dependências sejam restauradas para executar serviços íntegros.



2.  **Validar e confirmar os pré-requisitos para um segundo datacenter**   Esta etapa pode ser realizada simultaneamente com a etapa 1 porque a validação da integridade das dependências da infraestrutura no segundo datacenter é amplamente independente dos primeiros serviços do datacenter. Cada organização normalmente requer seu próprio método para realizar esta etapa. Por exemplo, você pode decidir concluir esta etapa analisando as informações de integridade coletadas e filtradas por um aplicativo de monitoramento de infraestrutura ou usando uma ferramenta que seja exclusiva para a infraestrutura de sua organização. Essa etapa é fundamental, pois ativar o segundo datacenter quando sua infraestrutura apresenta instabilidade e falta de integridade provavelmente gerará resultados insatisfatórios.

3.  **Ativar os servidores de Caixa de Correio**   Esta etapa inicia o processo de ativação do segundo datacenter. Esta etapa pode ser realizada simultaneamente com a etapa 4, pois os serviços do Microsoft Exchange podem lidar com interrupções de bancos de dados e com a recuperação. Ativar os servidores de Caixa de Correio envolve o processo de marcar os servidores com falha do datacenter primário como indisponíveis e, em seguida, ativar os servidores do segundo datacenter. O processo de recuperação dos servidores de Caixa de Correio dependem de se o DAG está em modo DAC (coordenação de ativação de datacenter). Para obter mais informações sobre o modo coordenação de ativação do banco de dados, consulte [Modo coordenação de ativação de Datacenter](datacenter-activation-coordination-mode-exchange-2013-help.md).
    
    Se o DAG estiver em modo DAC, é possível usar os cmdlets de resiliência de site do Exchange para encerrar um datacenter parcialmente com falha (se necessário) e ativar os servidores de Caixa de Correio. Por exemplo, no modo DAC, esta etapa é executada usando o cmdlet do [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd335133\(v=exchg.150\)). Em alguns casos, os servidores precisam ser marcados como indisponíveis duas vezes (uma vez em cada datacenter). Em seguida, o cmdlet [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd351169\(v=exchg.150\)) é executado para restaurar os membros restantes do grupo de disponibilidade do banco de dados (DAG) no segundo datacenter, ao reduzir os membros do DAG até que fiquem apenas aqueles que ainda estão em operação e, com isso, restabelecer o quorum. Se o DAG não estiver em modo DAC, você deve usar as ferramentas do cluster de failover do Windows para ativar os servidores de Caixa de Correio. Após a conclusão do processo, as cópias do banco de dados que foram previamente passivas no segundo datacenter podem se tornar ativas e serem montadas. Neste ponto, a recuperação de servidores de caixa de correio está completa.

4.  **Ativar os servidores de Acesso para Cliente**   Envolve o uso das informações de mapeamento de URL e a metodologia de alteração do Sistema de Nomes de Domínio (DNS) para efetuar todas as atualizações de DNS necessárias. As informações de mapeamento descrevem quais alterações no DNS devem ser executadas. O tempo exigido para concluir a atualização depende da metodologia usada e das configurações de Vida Útil (TTL) do registro DNS (e se a infraestrutura da implantação honra a TTL).

Os usuários devem começar a ter acesso aos serviços de mensagem a qualquer momento após a conclusão das etapas 3 e 4. As etapas 3 e 4 serão descritas com mais detalhes adiante neste tópico.

**Sumário**

Terminating a Partially Failed Datacenter

Activating Mailbox Servers

Activating Other Server Roles

Restoring Service to the Primary Datacenter

Reestablishing Site Resilience

## Encerrando um datacenter com falha parcial

Se quaisquer membros DAG com falha ainda estiverem em execução, será preciso encerrá-los.

Quando o DAG estiver em modo DAC, as ativações específicas para encerrar quaisquer membros DAG sobreviventes no datacenter principal são as seguintes:

1.  Os membros do DAG no datacenter primário devem ser marcados como interrompidos no datacenter primário. *Interrompido* é um estado do Gerenciador Ativo que evita que os bancos de dados sejam montados e o Gerenciador Ativo de cada servidor no datacenter com falha é colocado nesse estado usando o cmdlet [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd335133\(v=exchg.150\)). O parâmetro *ActiveDirectorySite* desse cmdlet pode ser usado para marcar, com um único comando, todos os servidores no datacenter primário como interrompidos. Esta etapa pode não ser possível, dependendo da falha. Esta etapa deve ser seguida se o estado do datacenter permitir. O cmdlet **Stop-DatabaseAvailabilityGroup** deve ser executado em todos os servidores no datacenter primário. Se o servidor de Caixa de Correio estiver indisponível, mas o Active Directory estiver operando no datacenter primário, o comando **Stop-DatabaseAvailabilityGroup** com o parâmetro *ConfigurationOnly* deve ser executado em todos os servidores do datacenter primário nesse estado ou o servidor de Caixa de Correio deve ser desativado. Uma falha na desativação dos servidores de Caixa de Correio do datacenter com falha ou na execução bem-sucedida do comando **Stop-DatabaseAvailabilityGroup** nos servidores criará a probabilidade de ocorrência da síndrome do cérebro dividido nos dois datacenters. Talvez seja necessário desligar individualmente os computadores por meio de dispositivos de gerenciamento de energia, a fim de satisfazer esse requerimento.

2.  O segundo datacenter deve ser agora atualizado para representar quais servidores do datacenter primário estão interrompidos. Isso é feito ao se executar o mesmo comando **Stop-DatabaseAvailabilityGroup** com o parâmetro *ConfigurationOnly*, usando o mesmo parâmetro *ActiveDirectorySite* e especificando o nome do site do Active Directory no datacenter primário com falha. A finalidade desta etapa é informar, aos servidores no segundo datacenter, quais servidores de caixa de correio estão disponíveis para uso na restauração do serviço.

Quando o DAG não estiver em modo DAC, as ativações específicas para encerrar quaisquer membros DAG sobreviventes no datacenter principal são as seguintes:

1.  Os membros DAG no datacenter principal devem ser forçados do cluster subjacente do DAG executando os seguintes comandos em cada membro:
    
    ```powershell
        net stop clussvc
        cluster <DAGName> node <DAGMemberName> /forcecleanup
    ```

2.  Os membros DAG no segundo datacenter devem agora ser reiniciados e, em seguida, usados para concluir o processo de remoção do segundo datacenter. Pare o serviço de cluster em cada membro DAG no segundo datacenter executando o seguinte comando em cada membro:
    
    ```powershell
        net stop clussvc
    ```

3.  Em um membro DAG no segundo datacenter, force um início de quorum do serviço de Cluster executando o seguinte comando:
    
    ```powershell
        net start clussvc /forcequorum
    ```

4.  Abra a ferramenta de Gerenciamento de Cluster de Failover e conecte-se ao cluster subjacente do DAG. Expanda o cluster e expanda **Nós**. Com o botão direito do mouse, clique em cada modo no datacenter principal e selecione **Mais Ações** e, em seguida, **Remover**. Quando estiver removendo os membros DAG no datacenter principal, feche a ferramenta Gerenciamento de Cluster de Failover.

Voltar ao início

## Ativando servidores de Caixa de Correio

As etapas necessárias para ativar os membros da Caixa de Correio durante uma autenticação do datacenter também dependerão de se o DAG estiver em modo DAC. Antes de ativar os membros DAG em um segundo datacenter, recomendamos que os serviços de infraestrutura no segundo datacenter estejam prontos para ativação do serviço de mensagem.

Quando o DAG estiver em modo DAC, as etapas para a conclusão da ativação dos servidores de caixa de correio no segundo datacenter são as seguintes:

1.  O serviço de Cluster deve ser interrompido em cada membro do DAG do segundo datacenter. É possível usar o cmdlet **Stop-Service** para interromper o serviço (por exemplo, `Stop-Service ClusSvc`) ou usar `net stop clussvc` em um prompt de comando elevado.

2.  Os servidores de Caixa de Correio no datacenter em espera podem então ser ativados usando-se o cmdlet [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd351169\(v=exchg.150\)). O site do Active Directory do datacenter em espera é passado para o cmdlet **Restore-DatabaseAvailabilityGroup** a fim de identificar quais servidores serão usados para restaurar o serviço e configurar o DAG para usar um servidor testemunha alternativo. Se o servidor testemunha alternativo não tiver sido configurado anteriormente, você pode configurá-lo usando os parâmetros *AlternateWitnessServer* e *AlternateWitnessDirectory* do cmdlet e [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd351169\(v=exchg.150\)). Se esse comando for executado com êxito, os critérios do quorum serão reduzidos para os servidores do datacenter em espera. Se o número de servidores nesse datacenter for um número par, o DAG passará a usar o servidor testemunha alternativo conforme identificado pela configuração do objeto do DAG.

3.  Agora, os bancos de dados podem ser ativados. Dependendo da configuração específica usada pela organização, pode ser que esse processo não seja automático. Se os servidores do datacenter em espera tiverem uma configuração de ativação bloqueada, o sistema não efetuará o failover automático do datacenter primário para o datacenter em espera de quaisquer bancos de dados. Se nenhuma restrição de failover estiver presente para qualquer uma das cópias do banco de dados no datacenter em espera, o sistema ativará as cópias no segundo datacenter considerando que estejam íntegras. Se os bancos de dados estiverem com uma configuração de ativação bloqueada que requer uma ação manual explícita, existem duas opções:
    
    1.  Desfazer a configuração que bloqueia a ativação. Isso fará o sistema retornar ao seu comportamento-padrão, que é ativar quaisquer cópias disponíveis.
    
    2.  Manter as configurações inalteradas e usar o cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/pt-br/library/dd298068\(v=exchg.150\)) para concluir a ativação do banco de dado no segundo datacenter. Para concluir essa etapa usando o cmdlet **Move-ActiveMailboxDatabase** quando a ativação bloqueada estiver definida, deve-se identificar explicitamente o destino da mudança.

4.  A última etapa é rever todos os alertas e as mensagens de erro das tarefas. Quaisquer alertas indicados devem ser acompanhados e corrigidos. O modelo de projeto de tarefa para esses comandos é falhar somente se não puderem alcançar o objetivo fundamental de seu projeto. Por exemplo, o cmdlet **Restore-DatabaseAvailabilityGroup** falhará se não puder reduzir o quorum do DAG para permitir que um servidor no segundo datacenter seja reinicializado para executar os serviços sem causar uma interrupção no quorum. Contudo, cada saída de tarefa é também usada para identificar os problemas que requerem o acompanhamento do administrador. É extremamente recomendável salvar todas as saídas de tarefa e revê-las para executar ações de acompanhamento.

Quando o DAG não estiver em modo DAC, as etapas para a conclusão da ativação dos servidores de caixa de correio no segundo datacenter são as seguintes:

1.  O quorum deve ser modificado com base no número de membros DAG no segundo datacenter.
    
    1.  Se houver um número ímpar de membros DAG, altere o modelo do quorum DAG de um Nó, um Compartilhamento de Arquivo Principais para um quorum de Nó principal executando o seguinte comando:
        
        ```powershell
            cluster <DAGName> /quorum /nodemajority
        ```
    
    2.  Se houver um número par de membros DAG, reconfigure o servidor e o diretório testemunha executando o seguinte comando no Shell de Gerenciamento do Exchange:
        
        ```powershell
            Set-DatabaseAvailabilityGroup <DAGName> -WitnessServer <ServerName>
        ```

2.  Inicie o serviço de Cluster em quaisquer membros DAG remanescentes no segundo datacenter executando o seguinte comando:
    
    ```powershell
        net start clussvc
    ```

3.  Execute alternâncias de servidor para ativar os banco de dados da caixa de correio no DAG executando o seguinte comando para cada membro DAG:
    
    ```powershell
        Move-ActiveMailboxDatabase -Server <DAGMemberinPrimarySite> -ActivateOnServer <DAGMemberinSecondSite>
    ```
    
4.  Monte os banco de dados da caixa de correio em cada membro DAG no segundo site executando o seguinte comando:
    
    ```powershell
        Get-MailboxDatabase <DAGMemberinSecondSite> | Mount-Database
    ```

Voltar ao início

## Ativando servidores de acesso para clientes

Os clientes conectam-se a pontos de extremidade de serviço (por exemplo, Outlook Web App, Descoberta automática, Exchange ActiveSync, Outlook Anywhere, POP3, IMAP4 and a matriz de Acesso para Cliente RPC) para acessar serviços e dados do Exchange. Portanto, a ativação de servidores de Acesso para Cliente requer a alteração do mapeamento dos registros de DNS desses pontos de extremidade de serviço dos endereços IP no datacenter primário para os endereços IP no datacenter secundário, que são configurados como os novos pontos de extremidade de serviço. Dependendo da sua configuração de DNS, os registros de DNS que devem ser modificados podem estar ou não na mesma zona de DNS.

## Ativando servidores de acesso para clientes

Os clientes se conectarão automaticamente aos novos pontos de extremidade de serviço, de duas maneiras:

  - Os clientes continuarão a tentar a conexão e devem se conectar automaticamente após a TTL expirar para a entrada original do DNS e após a entrada expirar do cache DNS do cliente. Os usuários também podem executar o comando `ipconfig /flushdns` a partir de um prompt de comando para limpar manualmente seu cache DNS.

  - Os clientes que estão iniciando ou reiniciando executarão uma pesquisa de DNS na inicialização e obterão o novo endereço IP do ponto de extremidade de serviço, que será um servidor de Acesso para Cliente ou uma matriz no segundo datacenter.

Presumindo que todas as alterações de configuração adequadas foram concluídas para definir e configurar os serviços no segundo datacenter, a fim de que funcionem como se estivessem no datacenter primário, e presumindo que a configuração do DNS estabelecido está correta, não são necessárias mais alterações para ativar os servidores de Acesso para Cliente.

## Ativando os serviços de transporte

Os clientes e outros servidores que enviam mensagens normalmente identificam esses servidores usando o DNS. Ativar os serviços de transporte no segundo datacenter envolve alterar os registros de DNS para apontar para o endereço IP dos servidores de Caixa de Correio no segundo datacenter. Os clientes e os servidores de envio irão se conectar automaticamente aos servidores no segundo datacenter de uma das seguintes maneiras:

  - Os clientes continuarão a tentar a conexão e devem se conectar automaticamente após a TTL expirar para a entrada original do DNS e após a entrada expirar do cache DNS do cliente. Os usuários também podem executar o comando `ipconfig /flushdns` a partir de um prompt de comando para limpar manualmente seu cache DNS.

  - Os clientes que estejam iniciando ou reiniciando executarão uma pesquisa de DNS na inicialização e obterão o novo endereço de IP do ponto de extremidade SMTP, que será um servidor de Caixa de Correio do segundo datacenter.

Presumindo que todas as alterações de configuração adequadas para definir e configurar os serviços no segundo datacenter de modo a que funcionem como se estivessem no datacenter primário tenham sido concluídas, e presumindo que a configuração de DNS estabelecida esteja correta, não deverão ser necessárias mais alterações para ativar os servidores de transporte.

## Ativando serviços de Unificação de Mensagens

Os serviços de Unificação de Mensagens (UM) conectam-se a um sistema de PABX e às linhas telefônicas de uma organização. A conexão lógica entre o sistema de PABX e o serviço de Unificação de Mensagens é fornecida por um gateway de IP. Os gateways de IP incluem funcionalidade de alta disponibilidade e são capazes de alternar entre vários serviços de Unificação de Mensagens quando uma falha é detectada.

Se existirem serviços de Unificação de Mensagens no segundo datacenter que tenham estado em um estado desativado porque estavam dedicados à solução de resiliências do site, é possível habilitá-los usando o cmdlet [Enable-UMService](https://technet.microsoft.com/pt-br/library/jj552411\(v=exchg.150\)) (por exemplo, `Enable-UMService EX4`).

Presumindo que os gateways de IP estejam associados aos serviços de Unificação de Mensagens por meio de servidores de DNS, a ativação dos serviços de Unificação de Mensagens envolverá, portanto, alterar os registros de DNS para apontar para os novos endereços IP que serão configurados para os serviços de Unificação de Mensagens no segundo datacenter. Presumindo que todas as alterações de configuração adequadas para definir e configurar os serviços no segundo datacenter de modo que funcionem como se estivessem no datacenter primário tenham sido concluídas, e presumindo que a configuração de DNS estabelecida esteja correta, não deverão ser necessárias mais alterações para ativar os serviços de Unificação de Mensagens.

Se o gateway de IP em uso não oferecer suporte ao uso de nomes de DNS para resolver os serviços de Unificação de Mensagens, serão necessárias etapas de configuração adicionais para apontar manualmente o gateway de IP para os endereços IP dos serviços de Unificação de Mensagens no segundo datacenter.

## Ativando servidores de Transporte de Borda

As etapas para ativar a função do servidor de Transporte de Borda variarão dependendo da configuração específica. Os servidores de Transporte de Borda em dois datacenters podem ser configurados como ativo/passivo ou ativo/ativo. Na configuração ativo/passivo, o servidor de Transporte de Borda do segundo datacenter fica ocioso até que o segundo datacenter seja ativado. Na configuração ativo/ativo, os servidores de Transporte de Borda nos dois datacenters fazem entregas contínuas de mensagens.

Na configuração ativo/ativo, nenhuma etapa é necessária para ativar os servidores de Transporte de Borda do segundo datacenter porque eles já estão em execução. Na configuração ativo/passivo, o registro de recurso MX do DNS para cada domínio SMTP precisa ser atualizado como parte da alternância do datacenter primário para o datacenter em espera. Embora a configuração ativo/ativo forneça uma solução de alternância de datacenter simples, ela carrega a desvantagem de requerer um monitoramento de carga cuidadoso para garantir que, após a alternância do datacenter, os servidores de Transporte de Borda no segundo datacenter ofereçam capacidade suficiente para dar suporte à carga aumentada que flui através deles, como resultado da indisponibilidade dos servidores de Transporte de Borda no datacenter primário.

Até mesmo com uma configuração ativo/ativo, é adequado atualizar os registros de recurso MX dos servidores de Transporte de Borda durante uma alternância de datacenter. Permitir que o registro de recurso MX do datacenter com falha continue a apontar para o datacenter com falha significa que, quando o datacenter iniciar a recuperação, ele pode começar a fazer tentativas de conexão com seus servidores de Transporte de Borda. Isso pode acontecer enquanto os serviços de Transporte de Borda estão em um estado instável (por exemplo, porque serviços dependentes estão sendo restaurados no datacenter).

Presumindo que os registros DNS estão sob o controle da organização, ativar os servidores de Transporte de Borda envolve atualizar o registro de recurso MX de cada domínio SMTP hospedado pelo servidor.


> [!TIP]
> Se o registro de recurso MX utilizado por sua organização não estiver hospedado por um servidor DNS sob o controle de sua organização, deve-se considerar a consulta a um registro CNAME no registro de recurso MX e o uso de um registro CNAME sob o controle da organização, que pode, então, ser atualizado.



As atualizações do DNS permitem o tráfego de entrada, e o tráfego de saída é manipulado pela ativação dos bancos de dados de caixa de correio em um site que tem servidores de Transporte de Borda funcionais:

  - Quando as conexões SMTP de entrada são iniciadas usando as informações atualizadas de resolução de nome, os clientes SMTP se conectarão aos servidores de Transporte de Borda no segundo datacenter. O tráfego será roteado adequadamente pelo servidor de Transporte de Borda, e não serão requeridas alterações adicionais.

  - Quando conexões SMTP de saída são iniciadas, elas tentam o servidor de Transporte de Borda localmente disponível, e essas mensagens são enfileiradas ou enviadas imediatamente de acordo com o status do servidor de recebimento.

Voltar ao início

## Restaurando o serviço para o datacenter primário

Geralmente, as falhas dos datacenters são temporárias ou permanentes. Quando há uma falha permanente, como um evento que causou a destruição permanente de um datacenter primário, não se espera que o datacenter primário seja ativado. Contudo, quando há uma falha temporária (por exemplo, uma perda de energia prolongada ou danos prolongados, porém reparáveis), há uma expectativa de que o datacenter primário acabe sendo restaurado para o funcionamento normal.

O processo de restauração de serviço de um datacenter com falha prévia é denominado *switchback*. As etapas utilizadas na realização do switchback de um datacenter são similares às etapas para a realização da alternância de um datacenter. Uma distinção significativa é que os switchbacks dos datacenters são programados e a duração da interrupção costuma ser muito menor.

É importante que o switchback não seja realizado até que as dependências da infraestrutura do Exchange sejam reativadas, estejam em funcionamento e estáveis e tenham sido validadas. Se essas dependências não estiverem disponíveis ou íntegras, é provável que o processo de switchback cause uma interrupção com duração maior do que a necessária ou falhe totalmente.

## Switchback de Função de Servidor Caixa de Correio

A função de servidor Caixa de Correio deve ser a primeira função a ser restaurada no datacenter primário. As seguintes etapas detalham o processo de switchback da função de servidor Caixa de Correio:

1.  Como parte do processo de alternância de datacenter, os servidores de Caixa de Correio no datacenter primário foram colocados no estado interrompido. Quando o ambiente (como o datacenter primário, as dependências do Exchange e a conectividade WAN (rede de longa distância)) está pronto, o primeiro passo é colocar os servidores de Caixa de Correio do datacenter primário restaurado em um estado iniciado e incorporá-los ao DAG. O modo no qual ele é feito depende de se o DAG está em modo DAC.
    
    1.  Se o DAG estiver em modo DAC, é possível reincorporar os membros do DAG no site principal usando o cmdlet do [Start-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd335076\(v=exchg.150\)). Em seguida, para certificar-se de que o modelo de quorum adequado está sendo usado pelo DAG, execute o cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd297934\(v=exchg.150\)) contra o DAG sem especificar nenhum parâmetro.
    
    2.  Se o DAG não estiver em modo DAC, é possível reincorporar os membros do DAG usando o cmdlet do [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/pt-br/library/dd298049\(v=exchg.150\)).

2.  Após os servidores de Caixa de Correio do datacenter primário serem incorporados ao DAG, eles precisam de um tempo para sincronizar suas cópias do banco de dados. Dependendo da natureza da falha, da extensão da interrupção e das decisões tomadas pelo administrador durante a interrupção, pode ser necessário reenviar as cópias do banco de dados. Por exemplo, se durante a interrupção, você remover as cópias do banco de dados do datacenter primário com falha para permitir o truncamento do arquivo de log para as cópias ativas restantes no segundo datacenter, será necessária uma nova propagação. Cada banco de dados pode prosseguir individualmente deste ponto em diante. Depois que uma cópia replicada do banco de dados no datacenter primário estiver íntegra, é possível prosseguir para a próxima etapa.
    

    > [!TIP]
    > Esse processo não requer que todos os bancos de dados sejam removidos ao mesmo tempo. É recomendável mover a maior parte dos bancos de dados de sua organização de uma só vez, porém alguns bancos de dados podem se demorar no segundo datacenter, se houver problemas associados às cópias do banco de dados no datacenter primário.



3.  Depois que a maior parte dos bancos de dados estiver em um estado íntegro no datacenter primário, a interrupção do switchback poderá ser programada. Quando a hora agendada chegar, estas instruções devem ser seguidas:
    
    1.  Durante o processo de alternância do datacenter, o DAG foi configurado para usar um servidor testemunha alternativo. O DAG deve ser reconfigurado para usar um servidor testemunha no datacenter primário. Se você estiver usando o mesmo servidor testemunha e o diretório testemunha que foi usado antes da interrupção do datacenter primário, é possível executar o comando `Set-DatabaseAvailabilityGroup -Identity DAGName`. Se você pretende usar um servidor testemunha ou um diretório testemunha diferente do servidor ou diretório testemunha original, use o comando [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd297934\(v=exchg.150\)) para configurar os parâmetros do servidor testemunha e do diretório testemunha com os valores apropriados.
    
    2.  Os bancos de dados que são reativados no datacenter primário devem ser desmontados do segundo datacenter. Você pode usar o cmdlet [Dismount-Database](https://technet.microsoft.com/pt-br/library/bb124936\(v=exchg.150\)) para desmontar os bancos de dados.
    
    3.  Depois que os bancos de dados forem desmontados, os URLs do servidor de Acesso para Cliente devem ser movidos do segundo datacenter para o datacenter primário. Isso é conseguido alterando-se o registro DNS dos URLs para apontar para o servidor de Acesso para Cliente ou matriz no datacenter primário. Isso fará o sistema agir, ainda que um failover do banco de dados tenha ocorrido em cada banco de dados que estava sendo movido.
        

        > [!IMPORTANT]
        > Não passe para a próxima etapa até que os URLs do servidor de Acesso para Cliente tenham sido movidos e a TTL do DNS e das entradas de cache tenham expirado. Ativar os bancos de dados no datacenter primário antes de mover os URLs do servidor de Acesso para Cliente para o datacenter primário resultará em uma configuração inválida (por exemplo, um banco de dados montado que não tem servidores de Acesso para Clientes em seu site do Active Directory).

    
    4.  Como cada banco de dados do datacenter primário está em um estado íntegro, é permitida a sua ativação no datacenter primário ao realizar as alternâncias do banco de dados. Isso é obtido usando-se o cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/pt-br/library/dd298068\(v=exchg.150\)) para cada banco de dados que será ativado.
    
    5.  Depois que cada banco de dados tiver sido movido para o datacenter primário, eles podem ser montados usando-se o cmdlet [Mount-Database](https://technet.microsoft.com/pt-br/library/aa998871\(v=exchg.150\)).

Depois que um ou mais bancos de dados estiverem ativos e montados no datacenter primário, os procedimentos de switchback para os outros servidores poderão ser realizados.

## Switchback de servidor de Acesso para Cliente

Como parte do processo de alternância, os registros de DNS internos e externos usados por clientes, outros servidores e gateways de IP para resolver os pontos de extremidade de serviço para servidores de Acesso para Cliente, serviços de Transporte e Unificação de Mensagens e servidores de Transporte de Borda foram modificados para apontar para os pontos de extremidade correspondentes no segundo datacenter. O processo de switchback para outras funções de servidor envolve modificar esses registros para apontar para os pontos de extremidade de serviço restaurados no datacenter primário.

Assim como nas alterações de DNS que foram feitas durante a alternância para o segundo datacenter, os clientes, servidores e gateways IP continuarão a tentar a conexão e deverão conectar-se automaticamente após a TTL expirar para a entrada original do DNS, e após a expiração da entrada do cache DNS.

Voltar ao início

## Restabelecendo a resiliência do site

Após a conclusão bem-sucedida do switchback do datacenter primário, é possível restabelecer a resiliência do site para o datacenter primário ao verificar a integridade e o status de cada cópia do banco de dados de caixa de correio no segundo datacenter. Além disso, se quaisquer cópias de banco de dados no segundo datacenter estiverem originalmente bloqueadas para ativação, é possível reconfigurar essas configurações, nesse momento.

Voltar ao início

