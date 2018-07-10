---
title: 'Roteamento de email entre sites do Active Directory: Exchange 2013 Help'
TOCTitle: Roteamento de email entre sites do Active Directory
ms:assetid: 86b423e3-7bec-4430-9a5a-4f84ce9d82ea
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ916681(v=EXCHG.150)
ms:contentKeyID: 52058853
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Roteamento de email entre sites do Active Directory

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Um site do Active Directory é um componente de configuração lógica baseado nos aspectos físicos da rede. O principal objetivo para criar um site do Active Directory é definir quais sub-redes da rede estão conectadas de uma forma que otimiza o controle do tráfego de replicação do Active Directory. A Microsoft Exchange Server 2013 reconhece ambos os grupos de disponibilidade de banco de dados (DAGs) e sites do Active Directory como limite de roteamento, e Exchange 2013 servidores que tomem decisões de roteamento com base na topologia do site do Active Directory.

Por padrão, uma floresta do Active Directory contém apenas um site do Active Directory. O nome padrão para esse site do Active Directory é `Default-First-Site-Name`. Se não forem criados outros sites do Active Directory, todos os computadores membros do domínio na floresta são membros de `Default-First-Site-Name`. Não é necessário configurar uma associação de sub-rede para site. Se forem criados mais sites do Active Directory, você deverá especificar as sub-redes atribuídas a esse site do Active Directory.

**Sumário**

Determining site membership

IP site links

Controlling IP site link costs

Implementing hub sites

Topology discovery

## Determinando a associação do site

Cada site do Active Directory é associado a uma ou mais sub-redes IP. Um administrador atribui associação ao site do Active Directory a computadores configurados como controladores de domínio e servidores de catálogo global. Outros computadores membros do domínio, como servidores Exchange, têm a associação ao site do Active Directory atribuída automaticamente quando configurados para usar um endereço IP que esteja em uma sub-rede IP associada a um site do Active Directory. Computadores com a mesma associação ao site do Active Directory presumivelmente possuem boa conectividade de rede. O servidor é sempre membro de um único site do Active Directory.

Quando um aplicativo pode determinar a associação de site do Active Directory do computador onde está instalado e de outros computadores da floresta, e usar essas informações para controlar o fluxo de comunicação, ele é um aplicativo que reconhece sites. Quando aplicativos que reconhecem sites precisam usar os serviços de outro servidor, como um controlador de domínio ou um servidor de catálogo global, é dada prioridade aos servidores com a mesma associação de site do Active Directory que o computador que está solicitando os serviços.

O Exchange 2013 é um aplicativo que reconhece sites e usa a topologia do Active Directory para roteamento de mensagens e para se comunicar com os serviços que estão sendo executados em computadores com outras funções de servidor do Exchange 2013 instaladas. O site do Active Directory não é apenas o limite de roteamento. Ele também é o limite de descoberta do serviço.

Determinar a associação de site de um computador membro do domínio depende de uma série de consultas de DNS para comparar os endereços IP locais com sub-redes definidas e, em seguida, determinar a associação de site adequada. Para reduzir a sobrecarga associada a consultas de DNS, as as adições de esquema do Active Directory Exchange 2013 incluem o atributo **msExchServerSite** para o objeto de servidor Exchange. O valor desse atributo é o nome diferenciado do site do Active Directory de um servidor Exchange. Esse atributo é uma propriedade de cada objeto de servidor do Exchange. Quando a afinidade de associação de site é armazenada como um atributo do objeto de servidor, a topologia atual pode ser lida diretamente do Active Directory em vez de depender de consultas de DNS, e uma associação de site é habilitada para um computador que não é de domínio, como um servidor de Transporte de Borda inscrito.

O valor do atributo **msExchServerSite** é preenchido e mantido atualizado pelo serviço de Topologia do Microsoft Exchange Active Directory. Quando um computador com o Windows é iniciado, o serviço de Logon de Rede determina a associação de site desse computador. O serviço de Logon de Rede usa as informações para localizar os controladores de domínio localizados no mesmo site do Active Directory que o computador local e direciona solicitações de autorização e autenticação a esses servidores. O serviço de Topologia do Microsoft Exchange Active Directory usa a chamada **DsGetSiteName** do API para recuperar o valor de associação de site do serviço de Logon de Rede e grava o nome diferenciado do site do Active Directory para o **msExchServerSite** para o objeto de servidor Exchange para o Active Directory.

A tabela a seguir mostra como uma organização pode definir sites do Active Directory. Neste exemplo, são definidos três sites do Active Directory e cada site do Active Directory é associado a mais de uma sub-rede IP.

**Exemplo de uma associação de site para sub-rede do Active Directory**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do site do Active Directory</th>
<th>Sub-redes IP associadas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Site A</p></td>
<td><p>192.168.1.0/24</p>
<p>192.168.2.0/24</p></td>
</tr>
<tr class="even">
<td><p>Site B</p></td>
<td><p>192.168.3.0/24</p>
<p>192.168.4.0/24</p></td>
</tr>
<tr class="odd">
<td><p>Site C</p></td>
<td><p>192.168.5.0/24</p>
<p>192.168.6.0/24</p></td>
</tr>
</tbody>
</table>


Se um servidor de nome Caixa de Correio01 tem o endereço IP 192.168.1.1, ele é membro do Site A. Mudando o endereço IP de um servidor, você pode mudar sua associação de site. Se você alterar o endereço IP de Caixa de Correio01 para 192.168.2.1, não mudará a associação de site do Active Directory do servidor, porque a sub-rede também está associada ao Site A. Contudo, se você mover o servidor e o endereço IP mudar para 192.168.3.1, o servidor será considerado membro do Site B.

Também pode haver alteração da associação do site se você mudar a associação de sub-redes com sites do Active Directory. Por exemplo, se você remover a sub-rede 192.168.3.0 da associação com o Site B e associá-la ao Site A, a associação de site de um servidor com endereço IP 192.168.3.1 também é alterada para o Site A. Sempre que ocorrer uma alteração na associação do site, o Exchange precisa atualizar seus dados de configuração para que a alteração seja considerada quando o Exchange tomar decisões de roteamento. Ocorre alguma latência entre o momento em que é feita uma alteração na associação de um site do Active Directory e a propagação total da alteração na topologia.

Voltar ao início

## links de site de IP

Links de site são caminhos lógicos entre sites do Active Directory. Um objeto de link de site representa um conjunto de sites que podem se comunicar com custo uniforme. Os links de site não correspondem ao caminho real usado por pacotes de rede na rede física. No entanto, o custo atribuído ao link de site pelo administrador normalmente está relacionado à confiabilidade, velocidade e largura de banda disponível da rede subjacente. Por exemplo, o administrador do Active Directory atribuiria um custo menor a uma conexão de rede com velocidade de 100 megabits por segundo (Mbps) do que a uma conexão de rede com velocidade de 10 Mbps.

Por padrão, todos os links de site são transitivos. Isso significa que, se o Site A tiver um link para o Site B e o Site B tiver um link para o Site C, o Site A estará transitivamente ligado ao Site C. O link transitivo entre o Site A e o Site C também e conhecido com uma *ponte de link de site*.

O Exchange apenas usa IPs de links de sites para determinar a topologia do roteamento do site do Active Directory. O custo atribuído ao link de site de IP será considerado pelo componente de roteamento do Exchange ao calcular uma tabela de roteamento. Esses custos são usados para calcular o caminho de roteamento de menor custo até o destino final de uma mensagem.

Cada site do Active Directory deve estar associado a pelo menos um IP de um link de um site. Há um único link de site de IP padrão chamado `DEFAULTIPSITELINK`. Ao criar um site do Active Directory, você deve associá-lo a um link de site de IP. Você pode criar links de site de IP adicionais para implementar a topologia desejada ou pode associar todos os sites do Active Directory ao `DEFAULTIPSITELINK`. Cada site do Active Directory que faz parte de um link de site de IP pode se comunicar diretamente com todos os outros sites desse link com um custo uniforme.

Na figura a seguir, quatro sites do Active Directory são configurados na floresta. Todos os sites foram associados ao `DEFAULTIPSITELINK`. Portanto, cada site do Active Directory se comunica diretamente com todos os outros sites usando a mesma métrica de custo. Mais de um caminho de comunicação é indicado, mas apenas um link de site de IP é definido.

**Topologia de malha completa com um único link de site IP**

![Topologia de malha completa com um único link de site IP](images/JJ916681.af38d41d-e768-4221-ab4b-b782aa388b73(EXCHG.150).gif "Topologia de malha completa com um único link de site IP")

Na figura a seguir, quatro sites do Active Directory são configurados na floresta. Nessa topologia, o administrador configurou links de site de IP para criar uma *topologia hub e spoke* de sites do Active Directory. Cada site spoke pode se comunicar diretamente com o site central, e os sites spoke podem se comunicar uns com os outros com os links de site de IP transitivos.

**Topologia hub e spoke de links de site de IP do Active Directory**

![Topologia hub e spoke de links de site IP](images/JJ916681.eca6cd51-8c2e-4996-81ea-070cd9766ef8(EXCHG.150).gif "Topologia hub e spoke de links de site IP")

É importante observar que o Exchange usa links de sites somente quando determina o caminho de menor custo, mas irá sempre tentar entregar as mensagens diretamente o servidor Exchange de destino. Por exemplo, se um usuário no Site B na topologia mostrada na figura anterior enviar uma mensagem para outro usuário no Site C, o servidor de Caixa de Correio no Site B irá se conectar diretamente ao servidor de Caixa de Correio no Site C. Se você quiser forçar as mensagens a ir pelo Site A, você deve habilitar esse site como um site de hub. Para mais informações sobre sites de hub, consulte "Implementando sites de Hub" posteriormente neste tópico.

Um administrador do Active Directory implementa a topologia que melhor representa os requisitos de conectividade e comunicação da floresta. Como a mesma topologia é usada pelo Exchange, você deve certificar-se de que a topologia atual oferece suporte para comunicação eficiente de mensagens.

O custo padrão de um link de site é 100. Um custo de link de site válido pode ser qualquer número de 1 a 99.999. Se você especificar links redundantes, o link de menor custo atribuído será sempre o preferencial. Um administrador da organização do Exchange pode atribuir um custo específico do Exchange a um link de site de IP. Se um custo de Exchange for associado a um link de site de IP, será usado pelo Exchange. Caso contrário, será usado o custo do Active Directory. Para obter mais informações sobre como definir um custo do Exchange em um link de site de IP, consulte "Controlando custos de link de site de IP" posteriormente neste tópico. Um administrador associado ao grupo de Administradores da Empresa pode criar links de site de IP adicionais.

Para obter mais informações sobre a configuração de site do Active Directory, consulte [Projetando a topologia de Site](https://go.microsoft.com/fwlink/p/?linkid=33551).

Voltar ao início

## Controlando os custos do link de site de IP

Os custos dos links do site de IP do Active Directory são baseados na velocidade de rede relativa comparada a todas as conexões de rede na WAN e são projetados para produzir uma topologia de replicação confiável e eficiente. Entretanto, em muitos casos, os custos do link do site de IP devem funcionar bem para o roteamento de mensagens do Exchange. No entanto, se, depois de documentar o site do Active Directory existente e a topologia de link de site de IP, você verificar que os custos de link de site de IP do Active Directory e os padrões de fluxo de tráfego não são ideais para o Exchange, você poderá fazer ajustes nos custos avaliados pelo Exchange. Alterar o custo atribuído ao link do site de IP, usando as ferramentas do Active Directory causaria impactos a todo o ambiente. Em vez disso, você pode usar o cmdlet **Set-AdSiteLink** no Exchange Management Shell para atribuir um custo específico do Exchange ao link do site IP. Por exemplo, para configurar um valor de custo de 25 específico do Exchange non link de site de IP chamado SITELINKAB, corra o seguinte comando no Shell: `Set-AdSiteLink SITELINKAB -ExchangeCost 25`.

Quando um custo específico do Exchange é atribuído a um link de site IP, o custo do Exchange substitui com eficácia o custo do Active Directory apenas para roteamento de mensagens, e o roteamento apenas considera o custo do Exchange quando avalia o caminho de roteamento de menor custo.

Ajustar os custos do link de site IP pode ser útil quando a mensagem de topologia de roteamento tem de divergir da topologia de replicação do Active Directory. Os custos do Exchange podem ser usados para forçar todos os roteamentos de mensagens a usar um site de hub. Os custos do Exchange também podem ser usados para controlar onde as mensagens são colocads em fila quando a comunicação com um site do Active Directory falha. A figura a seguir mostra uma topologia de Active Directory com quatro sites.

**Topologia com os custos configurados do Exchange em links de site IP**

![Topologia com os custos do Exchange em links de site IP](images/JJ916681.56ac2bab-99de-4ddf-b968-80cd34ab8c21(EXCHG.150).gif "Topologia com os custos do Exchange em links de site IP")

Na figura anterior, a conexão de rede entre o Site C e o Site D é uma conexão de baixa largura de banda, usada apenas para replicação do Active Directory, e não deve ser usada para roteamento de mensagens. No entanto, os custos de link de site de IP do Active Directory fazem com que esse link seja incluído no caminho de menor custo de roteamento de qualquer outro site do Active Directory até o Site D. Portanto, as mensagens são entregues à fila do Site D no Site C. O administrador do Exchange prefere que o caminho de roteamento de menor custo inclua o Site B em vez disso, de modo que, se o Site D estiver indisponível, as mensagens sejam colocadas em fila no Site B. A configuração de um alto custo do Exchange para o link de site de IP entre o Site C e o Site D impede que esse link de site de IP seja incluído no caminho de roteamento de menor custo até o Site D.

O Exchange fornece suporte para a configuração de um limite máximo de tamanho de mensagem em um link de site IP do Active Directory. Por padrão, o Exchange não impõe um limite máximo de tamanho para as mensagens que são retransmitidas entre os servidores de Exchange, em sites diversos do Active Directory. Se você utilizar o cmdlet **Set-AdSiteLink** para configurar o tamanho máximo da mensagem em um link de site de IP do Active Directory, o roteamento criará um relatório de falha na entrega (NDR) para as mensagens que possuam um tamanho superior ao limite estipulado no link de site do Active Directory no caminho de roteamento de menor custo. Essa configuração é útil para restringir o tamanho das mensagens enviadas aos sites remotos do Active Directory, que precisam se comunicar com conexões de largura de banda baixa. Para mais informações, consulte [Limites de tamanhos de mensagens](message-size-limits-exchange-2013-help.md).

Voltar ao início

## Implementando sites de hub

Em sua organização do Exchange, você pode forçar todas as entregas de mensagens através de um sites do Active Directory específico. Você pode usar o Shell para designar um site do Active Directory como um site de hub. Ao fazer isso, você causa sobrecarga geral adicional, pois mais servidores estão envolvidos na entrega de mensagens. Por exemplo, considere uma mensagem enviada do Site A para o Site E. Se o caminho de roteamento de menor custo for Site A-Site B-Site C-Site D-Site E, e você designar o Site C como um site de hub, a mensagem será retransmitida do Site A para o Site C e, em seguida, retransmitida do Site C para o Site E.

Você usa o cmdlet **Set-AdSite** para especificar um site do Active Directory como um site de hub. Sempre que houver um site de hub ao longo do caminho de roteamento de menor custo para entrega da mensagem, as mensagens serão colocadas em fila e processadas pelo serviço de Transporte nos servidores Caixa de Correio no site de hub antes de serem retransmitidas para o destino final.

Depois que o caminho de roteamento de menor custo é escolhido, o roteamento determina se há um site de hub nesse caminho de roteamento. Se um site de hub estiver configurado, as mensagens pararão em um servidor de Caixa de Correio no site de hub antes de serem retransmitidas para o destino. Se houver mais de um site de hub no caminho de roteamento de menor custo, as mensagens pararão em todos os sites de hub do caminho de roteamento.

Você deve compreender que essa variação do roteamento de retransmissão direta só funciona quando o site de hub está localizado no caminho de roteamento de menor custo. A figura a seguir mostra o uso correto de um site de hub. Neste diagrama, o Site B está configurado como um site de hub. Mensagens retransmitidas do Site A para o Site D são retransmitidas ao Site B antes de serem entregues ao Site D.

**Entrega de mensagens com um site de hub**

![Entrega de mensagens com um site de hub](images/JJ916681.93238bcb-6bbc-4a48-aeb0-09342a421b5b(EXCHG.150).gif "Entrega de mensagens com um site de hub")

A figura a seguir mostra como os custos de link de site de IP afetam o roteamento para um site de hub. Neste cenário, o Site B foi designado como um site de hub. Contudo, o Site B não existe no caminho de roteamento de menor custo entre quaisquer outros sites. Portanto, mensagens retransmitidas do Site A para o Site D nunca são retransmitidas ao Site B. Um site Active Directory nunca é usado como site de hub se ele não estiver no caminho de roteamento de menor custo entre dois outros sites.

**Site de hub configurado incorretamente**

![Site de hub configurado incorretamente](images/JJ916681.c010d4d8-5cd3-4b79-b7db-0367ba3cc287(EXCHG.150).gif "Site de hub configurado incorretamente")

Você pode configurar qualquer site do Active Directory como um site de hub. Entretanto, para que essa configuração funcione corretamente, você deve ter implantado pelo menos um servidor de Caixa de Correio nesse site de hub.

Voltar ao início

## Descoberta de topologia

A topologia do Active Directory é fornecida para o Exchange pelos seguintes elementos obrigatórios:

  - Serviço de topologia do Active Directory do Microsoft Exchange.

  - O módulo de descoberta de topologia dentro do serviço de Transporte do Microsoft Exchange.

O serviço de Topologia do Microsoft Exchange Active Directory corre em todos os servidores Exchange 2013 Acesso para Cliente e Caixa de Correio. Esses servidores do serviço de topologia do Active Directory do Microsoft Exchange usam o para descobrir os controladores de domínio e servidores de catálogo global que podem ser usados pelos servidores Exchange para ler e gravar dados do Active Directory. O Exchange 2013 é ligado aos servidores de diretório identificados sempre que o precisar ler ou gravar no Active Directory.

O módulo de descoberta de topologia é parte do serviço de Transporte do  Exchange e fornece informações sobre a topologia do Active Directory para servidores Exchange. Esta API descobre os servidores e funções do Exchange na organização e determina seu relacionamento com os objetos de configuração do Active Directory. Os dados de configuração são recuperados do Active Directory e, em seguida, armazenados em cache para poderem ser acessados pelos serviços do Exchange em execução nesse computador.

O módulo de descoberta de topologia executa as etapas a seguir para gerar uma topologia de roteamento do Exchange:

1.  Dados lidos do Active Directory. Todos os objetos a seguir são recuperados:
    
      - Sites do Active Directory.
    
      - Links de site de IP.
    
      - Todos os servidores Exchange.

2.  Os dados recuperados na etapa 1 são usados para criar a topologia inicial e começar a vincular e mapear os objetos de configuração relacionados.

3.  A correspondência de servidores Exchange com sites do Active Directory é feita recuperando o valor de atributo do site do objeto de servidor do Exchange armazenado no Active Directory.

4.  As tabelas de roteamento são atualizadas com as informações recuperadas.

Esse processo faz com que todo servidor do Exchange 2013 da organização e a proximidade entre os servidores do Exchange.

Voltar ao início

