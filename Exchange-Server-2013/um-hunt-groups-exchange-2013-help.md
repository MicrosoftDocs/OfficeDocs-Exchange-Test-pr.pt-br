---
title: 'Grupos de busca de Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Grupos de busca de Unificação de mensagens
ms:assetid: 026129a1-b0b5-410a-bed6-2d49f85205b3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa995918(v=EXCHG.150)
ms:contentKeyID: 50556133
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Grupos de busca de Unificação de mensagens

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-18_

Um grupo de busca de telefonia fornece uma maneira de distribuir chamadas telefônicas a partir de um único número para diversos ramais ou números de telefone. Na Unificação de Mensagens (UM), um grupo de busca de UM é uma representação lógica de um grupo de busca de telefonia e vincula um gateway IP de UM a um plano de discagem de UM.

Procurando tarefas de gerenciamento relacionadas aos grupos de busca da Unificação de Mensagens? Consulte [Procedimentos de grupo de busca de Unificação de mensagens](um-hunt-group-procedures-exchange-2013-help.md).

**Sumário**

What is a hunt group

What is a pilot number

What is a UM hunt group

## O que é um grupo de busca?

*Grupo de busca* é um termo usado para descrever um grupo de números de ramais de PBX (central privada de comutação telefônica) ou PBX IP compartilhados por usuários. Os grupos de busca são usados para distribuir chamadas com eficiência para/de uma unidade comercial específica. A criação e a definição de um grupo de busca minimiza as chances de um chamador receber o sinal de ocupado quando a chamada é recebida.

Grupos de busca são usados para localizar uma linha, ramal, ou canal aberto quando uma chamada é recebida. As chamadas são "acumuladas" para a próxima linha disponível quando uma linha telefônica primária estiver ocupada ou não atender. A pessoa que estiver ligando recebe um sinal de ocupado ou é direcionada para a caixa postal apenas se não houver ramal no grupo aberto. Por exemplo, um PBX ou PBX IP pode ser configurado para ter 10 ramais destinados ao departamento de vendas. Esses 10 ramais devem ser configurados como um grupo de busca.

As configurações para um grupo de busca simples incluem um nome, um número de ramal, uma lista de membros de grupo disponíveis e um método de seleção de grupo de busca. O método de seleção de grupo de busca determina a ordem em que as chamadas de entrada são apresentadas aos membros do grupo de busca.

Há diversos algoritmos ou métodos que um PBX ou PBX IP podem usar para localizar uma linha, ramal ou canal aberto. Entre as quais:

  - **Grupo de busca ou tocar todos os ramais**    Quando uma chamada é recebida no número de ramal do grupo de busca, o PBX ou PBX IP faz tocar todos os números de ramais no grupo.

  - **Iniciar com o menor número ou busca linear**   Essa é a configuração padrão na maioria dos PBXs e PBXs IP. Com esse método, as chamadas são roteadas para a primeira linha ociosa na ordem sequencial, iniciando com a primeira linha no grupo. Essa configuração é mais frequentemente encontrada em telefones multilinhas em pequenas empresas.

  - **Round robin ou busca circular**   Com esse método, as chamadas são roteadas para a primeira linha ociosa, iniciando com a linha seguinte à que atendeu por último uma chamada. Quando as chamadas são distribuídas usando o método "round robin", se uma chamada for entregue para a linha 1, a próxima chamada vai para a linha 2, depois para a linha 3 e assim por diante. Esse processo continua mesmo que uma das linhas anteriores se torne livre. Quando o fim do grupo de busca é alcançado, a busca começa novamente pela primeira linha. As linhas são ignoradas apenas se ainda estiverem ocupadas em uma chamada anterior. A busca circular ou round robin separa a distribuição de chamadas igualmente entre todas as chamadas, minimizando a possibilidade de uma grande interrupção no serviço;

  - **Busca por mais ocioso e distribuição uniforme**    Com esse método, a chamada é roteada para a primeira linha disponível no grupo que esteve ociosa por mais tempo. Esse método usa o período que a pessoa que atende a chamada esteve ocupada em vez de se a linha está disponível. Esse método é normalmente usado em grandes call centers em que as chamadas de entrada são atendidas por pessoas e a carga é distribuída igualmente entre o grupo de números de ramais.

Você pode configurar um ou mais grupos de busca. Cada grupo de busca deve incluir um mínimo de duas linhas. Se um número já estiver sendo usado no grupo de busca, ele não estará disponível em outro.

A seguir estão exemplos de grupos de busca de telefonia simples e como eles funcionam.

**Exemplo 1**

O ramal 300 (número piloto) está programado para que, quando uma chamada seja recebida, ela toque no ramal 301, depois 302, em seguida, 303 e 304.

1.  O ramal 301 está ocupado.

2.  O ramal 302 toca e não é atendido.

3.  O ramal 303 atende a chamada.

4.  O ramal 304 está livre e à espera de uma chamada recebida.

**Exemplo 2**

O ramal 1000 (número piloto) está programado para que, quando uma chamada seja recebida, ela toque em todos os ramais de 2000 até 2003 ao mesmo tempo.

1.  O ramal 2000 está livre.

2.  O ramal 2001 está livre.

3.  O ramal 2002 está livre.

4.  O ramal 2003 atende a chamada de entrada.

Voltar ao início

## O que é um número piloto?

Em uma rede telefônica, um PBX ou um PBX IP pode ser configurado para ter um único ou vários grupos de busca. Cada grupo de busca criado em um PBX ou PBX IP precisa ter um *número piloto* associado. O uso de um número piloto ajuda a eliminar os sinais de ocupado e a rotear as chamadas de entrada para os números de ramal disponíveis. O PBX ou PBX IP usa o número piloto para localizar o grupo de busca e localizar o ramal do telefone em que a chamada de entrada foi recebida e os ramais que estão atribuídos ao grupo de busca. Sem um número piloto definido, o PBX ou PBX IP não pode localizar onde a chamada de entrada foi recebida.

Um número piloto é um endereço, ramal ou local do grupo de busca dentro do PBX ou PBX IP. Geralmente é um ramal vazio ou um número de ramal dentre um grupo de busca de ramais ao qual não há uma pessoa ou um telefone associado. Por exemplo, um grupo de busca pode ser configurado em um PBX ou PBX IP para conter os ramais 4100, 4101, 4102, 4103, 4104 e 4105. O número piloto do grupo de busca está configurado como o ramal 4100. Quando uma chamada é recebida pelo ramal 4100, o PBX ou PBX IP procura o próximo ramal disponível para determinar onde a chamada dever ser atendida. Nesse exemplo, o PBX ou PBX IP usará seu algoritmo de busca programada para buscar em números de ramal 4101, 4102, 4103, 4104 e 4105.

O uso de um número piloto ajuda a eliminar os sinais de ocupado e a rotear as chamadas de entrada para os números de ramal disponíveis. Na Unificação de Mensagens, o número piloto de PBX ou PBX IP é usado como o destino. Se nenhum número de ramal no grupo de busca atender uma chamada de entrada, a chamada será roteada para um servidor de Caixa de Correio que executa o serviço de Unificação de Mensagens do Microsoft Exchange.

Voltar ao início

## O que é um grupo de busca de UM?

Os grupos de busca de Unificação de Mensagens são essenciais para a operação do sistema de UM. Um grupo de busca de UM é uma representação lógica de um grupo de busca existente para PBX ou PBX IP. É usado para vincular um gateway IP de UM a um plano de discagem de UM. Um único grupo de busca de UM também pode vincular diversos gateways IP de UM a um plano de discagem de UM. Por padrão, quando você cria um gateway IP de UM e o associa a um plano de discagem de UM, um grupo de busca de UM é criado e você também pode criar outros grupos de busca. Você deve criar pelo menos um grupo de busca de UM.

Os grupos de busca de UM são usados para localizar o grupo de busca do PBX ou PBX IP de onde a chamada de entrada foi recebida. Um número piloto, definido para um grupo de busca no PBX ou PBX IP, também deve estar definido para um grupo de busca de UM. O número piloto é usado para fazer a correspondência entre as informações apresentadas pelas chamadas de entrada, usando as informações de sinalização do SIP (Protocolo de Iniciação da Sessão) na mensagem de voz. O número piloto permite que os servidores do Exchange interpretem a chamada junto com o plano de discagem adequado para que ela possa ser roteada corretamente. A ausência de um grupo de busca impede que os servidores do Exchange reconheçam a localização da chamada de entrada. O reconhecimento da localização das chamadas de entrada permite que os servidores do Exchange aceitem as informações de cabeçalho das chamadas que passaram do gateway VoIP, PBX IP, ou PBX habilitado por SIP. É muito importante configurar os grupos de busca de UM corretamente, porque as chamadas de entrada que não corresponderem corretamente ao número piloto definido no grupo de busca de UM não serão atendidas e o roteamento da chamada de entrada falhará.

Em implantações locais e híbirdas, quando você cria um grupo de busca de UM, você habilita todos os servidores de Acesso para Cliente e de Caixa de Correio, independentemente de você ter adicionado eles ou não a um plano de discagem de UM para se comunicarem com um gateway VoIP, PBX IP ou PBX habilitado por SIP. Isso ocorre porque todos os servidores de Acesso para Cliente e de Caixa de Correio atendem chamadas de entrada para todos os planos de discagem, em vez de atender para um plano de discagem de UM específico como o servidor de UM fazia em versões anteriores do Exchange. Se você excluir um grupo de busca de UM, o gateway IP da UM associado não poderá atender chamadas de entrada de um gateway VoIP, PBX IP ou PBX habilitado por SIP nem realizar chamadas de saída por meio de gateway IP, PBX IP ou PBX habilitado por SIP usando o número piloto especificado.

No entanto, para implantações locais e híbridas, se você estiver integrando a UM com Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server, é necessário adicionar todos os servidores de Acesso para Cliente e de Caixa de Correio a todos os planos de discagem URI SIP que foram criados para trabalhar com o Communications Server 2007 R2 ou Lync Server. Isso permite que o roteamento de chamadas e discagem externa funcionem corretamente.

Para obter mais informações sobre gateways IP da UM, consulte [Gateways IP de UM](um-ip-gateways-exchange-2013-help.md).

