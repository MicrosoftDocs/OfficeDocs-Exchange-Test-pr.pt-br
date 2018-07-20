---
title: 'Recomendações de configuração e dimensionamento do Exchange 2013: Exchange 2013 Help'
TOCTitle: Recomendações de configuração e dimensionamento do Exchange 2013
ms:assetid: 4c4ba2fc-014a-46fb-949a-2dabba92c4a5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn879075(v=EXCHG.150)
ms:contentKeyID: 63763722
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Recomendações de configuração e dimensionamento do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-03-27_

O Exchange 2013 exige mais recursos do sistema do que as versões anteriores do Exchange. Dimensionando corretamente sua infraestrutura do Exchange 2013 e fazendo algumas configurações recomendadas nos componentes relacionados ao Exchange dentro dessa infraestrutura, você pode preparar a base para uma implantação com desempenho ideal.

## Dimensionar o Exchange 2013

O dimensionamento correto do Exchange 2013 é uma das maneiras mais eficazes de evitar problemas de desempenho. A Calculadora de Requisitos de Função de Servidor do Exchange 2013 está [disponível aqui](http://go.microsoft.com/fwlink/p/?linkid=523844). A versão mais recente é a 6.6, mas recomendamos verificar se há novas atualizações periodicamente. Para usar essa calculadora corretamente, consulte as orientações nas postagens [Calculadora de Requisitos de Função de Servidor do Exchange 2013](http://go.microsoft.com/fwlink/p/?linkid=386677) e [Dimensionamento de implantações do Exchange 2013](http://go.microsoft.com/fwlink/p/?linkid=301990) do blog.

É importante começar com a calculadora antes de comprar e implantar o hardware; primeiro você deve determinar os requisitos gerais de recursos com base nos resultados da calculadora. Você pode usar a calculadora para inserir as demandas de sua organização e usar os resultados para se orientar sobre como dimensionar seu hardware. A calculadora não informa quantos servidores usar, mas permite que você estime o impacto de uma carga de trabalho do Exchange em um determinado conjunto de servidores. Você deve experimentar diferentes configurações para ver como elas afetam o desempenho, a fim de atender às necessidades de hardware e comerciais específicas para seu ambiente.

Para simplificar as implantações e obter o melhor uso do hardware, o grupo de produtos do Exchange recomenda servidores com várias funções. Usar servidores com várias funções oferece melhor disponibilidade na camada de servidor de acesso para cliente (CAS), já que há mais servidores de acesso para cliente disponíveis para lidar com solicitações durante um cenário de falha. A principal consideração sobre design do Exchange 2013 é utilizar servidores básicos "menores" (distribuição ao invés de dimensionamento). O projeto e o teste foram feitos com computadores com dois soquetes que contêm até 20 núcleos de processador, com até 96 gigabytes (GB) de RAM. Se o hardware for maior do que isso, você deve considerar outras opções, como usar esse hardware para outras necessidades e adquirir servidores menores para seu ambiente do Exchange 2013, ou usar a virtualização.

É preferível para criar mais servidores (distribuição) do que adicionar recursos aos servidores existentes e maiores (dimensionamento). A distribuição permite que seu ambiente aproveite os recursos internos de alta disponibilidade do Exchange 2013. Para compreender por que essa configuração é recomendada, revise detalhadamente as postagens [A arquitetura preferida](http://go.microsoft.com/fwlink/p/?linkid=523782) e [Impacto da resistência sobre a disponibilidade do site](http://go.microsoft.com/fwlink/p/?linkid=523845).

A calculadora não considera produtos de terceiros em execução nos servidores Exchange, nem produtos que interagem com o Exchange (incluindo aplicativos desenvolvidos internamente), o que significa que você deve ter certeza ao considerá-los durante seu dimensionamento. O Lync Server, por exemplo, e aplicativos dos Serviços Web do Exchange (EWS) e dispositivos ActiveSync de terceiros podem aumentar significativamente os requisitos de CPU por usuário. Você pode consultar a documentação de produtos de terceiros para obter informações sobre como eles afetarão o Exchange. É recomendável criar uma linha de base de desempenho para o Exchange antes da implementação de soluções de terceiros.

## Configurações de desempenho recomendadas

As otimizações de desempenho a seguir são recomendadas para seu ambiente do Exchange 2013.

## Energia

Defina a BIOS para permitir que o sistema operacional gerencie a energia.

No sistema operacional, ative o plano de energia de Alto Desempenho.

## Processamento

Desative o hyper-threading em servidores Exchange físicos. Se estiver usando a virtualização, o hyper-threading pode estar habilitado no servidor físico, mas cada servidor virtual só deve ter a quantidade necessária de CPUs virtuais alocada (não reserve CPUs virtuais demais) e apenas utiliza a contagem de núcleo de processador físico para cálculos de dimensionamento.

No Exchange Server 2013 Service Pack 1 ou posterior é possível habilitar a descarga de SSL para ajudar a reduzir o consumo de CPU por servidores de acesso para cliente, mas a configuração complexa da descarga de SSL talvez não valha o benefício.

## .NET Framework


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Versão do Exchange</th>
<th>.NET Framework 4.7.1</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU19</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU16 - CU18</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


Se não for possível instalar o .net 4.5.2, veja o artigo 2995145, "[Problemas de desempenho ou atrasos quando você se conecta ao Exchange Server 2013 em execução no Windows Server](http://go.microsoft.com/fwlink/p/?linkid=524159)", da Base de Dados de Conhecimento Microsoft. As correções neste artigo foram desenvolvidas com base em descobertas internas sobre a utilização de memória do Processo de trabalho do repositório. Aplicando essas correções, você reduz o consumo de memória geral de todos os processos gerenciados (inclusive o processo de trabalho do repositório) e reduz o tempo total da CPU gasto na coleta de lixo do .NET.

## Hotfixes

A equipe de desempenho do Exchange recomenda instalar todas as seguintes hot fixes relacionadas ao desempenho.

  - [A atualização que aprimora a resiliência do cluster no Windows Server 2012 está disponível](http://go.microsoft.com/fwlink/p/?linkid=524088)

  - [Hotfixes e atualizações recomendados para clusters de failover baseados no Windows Server 2012](http://go.microsoft.com/fwlink/p/?linkid=524089)

  - [Hotfixes e atualizações recomendados para clusters de failover baseados no Windows Server 2012 R2](https://go.microsoft.com/fwlink/p/?linkid=524090)

  - [Atribuição incorreta de processador RSS em um computador baseado em Windows 8 ou Windows Server 2012 com processadores de vários núcleos](http://go.microsoft.com/fwlink/p/?linkid=324140)

  - [Problemas de desempenho ou atrasos quando você se conecta ao Exchange Server 2013 em execução no Windows Server](http://go.microsoft.com/fwlink/p/?linkid=312962)

  - [Problemas de conectividade com o Outlook se SSLOffloading for "Verdadeiro" no Exchange 2013](http://go.microsoft.com/fwlink/p/?linkid=524091)

  - [Longo período de conexão do servidor para o Outlook após o failover de um banco de dados no Exchange Server 2013](http://go.microsoft.com/fwlink/p/?linkid=524092)

  - [Desempenho lento no Outlook Web App quando o Lync está integrado ao Exchange Server 2013](http://go.microsoft.com/fwlink/p/?linkid=524093)

  - [Os EMS demoram muito tempo para executar o primeiro comando em um ambiente da atualização cumulativa 5 do Exchange Server 2013](http://go.microsoft.com/fwlink/p/?linkid=524094)

  - [Latência de roteamento de mensagens se o IPv6 for habilitado no Exchange Server 2013](http://go.microsoft.com/fwlink/p/?linkid=524095)

  - [Alto uso da CPU por um aplicativo que depende de um cliente LDAP da Microsoft no Windows Server 2008 R2 SP1](http://go.microsoft.com/fwlink/p/?linkid=530287)

  - [O uso da CPU está alto quando você usa a RPC ao invés do protocolo HTTP no Windows 8.1 ou no Windows Server 2012 R2](http://go.microsoft.com/fwlink/p/?linkid=619127)

## Sistema de rede

Com o Exchange 2013, um único adaptador de rede é recomendável, pois não é mais necessário dividir redes MAPI e de replicação. Para saber mais, consulte [Network requirements](planning-for-high-availability-and-site-resilience-exchange-2013-help.md).

Use as configurações de descarga de SNP padrão quando disponíveis e certifique-se de que o RSS esteja ativado (a configuração padrão no Windows Server 2012 e versões posteriores). O RSS ajudará a dimensionar a utilização da CPU, especialmente em 10 GbE.

Verifique se o sistema operacional não está desativando o cartão de rede para economizar energia.

Mantenha os drivers de NIC atualizados. Verifique com seu fornecedor mensalmente para obter atualizações de driver relevantes.

## Serviços de Informações da Internet (IIS)

Durante a instalação, o Exchange modifica alguns limites de conexão para IIS. Nenhum outro ajuste do IIS é recomendado.

Evite personalizações sempre que possível. Qualquer alteração às chaves do registro ou a web.config pode ser substituída por atualizações cumulativas do Exchange ou atualizações do Windows.

## Armazenamento

Diretrizes para o armazenamento do Exchange 2013 estão disponíveis em [Opções de configuração de armazenamento do Exchange 2013](exchange-2013-storage-configuration-options-exchange-2013-help.md).

## Virtualização

Consulte [Requisitos para virtualização de hardware](exchange-2013-virtualization-exchange-2013-help.md). Além disso, observe que o Exchange reconhece o acesso não uniforme à memória (NUMA). Portanto, recomenda-se usar as configurações padrão do fabricante para o hardware.

## Active Directory

Monitore o desempenho do servidor de diretórios, pois consultas do Active Directory têm impacto direto em sua implantação do Exchange.

O tempo de pesquisa do LDAP é um contador essencial para medir a integridade do Active Directory. Monitore a CPU em seus controladores de domínio. Problemas de CPU nos controladores de domínio serão processados como um impacto de desempenho nos servidores do Exchange.

Execute o “Diagnóstico do Active Directory” no Controlador de Domínio em Monitor de Desempenho, localizado sob “Conjunto de Coletores de Dados” para ajudar a isolar a causa dos problemas de desempenho do controlador de domínio.

Separe RAM suficiente nos Controladores de Domínio para poder armazenar em cache todo o arquivo de banco de dados do AD.

Recomenda-se implantar um núcleo de catálogo global do Active Directory para cada oito núcleos de caixa de correio que lidam com cargas ativas (com base em núcleos de catálogo globais de 64 bits).

## Balanceamento de carga

Todos os Servidores de Acesso para Cliente devem receber aproximadamente a mesma quantidade de conexões de entrada.

O Exchange 2013 não exige afinidade de sessão entre um determinado servidor de acesso para cliente e o balanceador de carga para nenhum dos protocolos.

Um balanceador de carga de hardware ou software deve ser usado para gerenciar todo o tráfego de entrada em servidores de acesso para cliente. A seleção do servidor de destino pode ser feita de várias formas, como “round robin”, em que cada conexão de entrada passa para o próximo servidor de destino em uma lista circular, ou “menos conexões”, em que o balanceador de carga envia cada nova conexão ao servidor que tem menos conexões estabelecidas naquele momento. Esses métodos são mais detalhados em [Balanceamento de carga](load-balancing-exchange-2013-help.md). Você também deve considerar o seguinte:

  - Round-robin tem o problema de convergência lenta com conexões de vida longa (como RPC/HTTP). Conforme novos computadores são colocados online, o equilíbrio de conexões fornecidas entre os computadores de destino leva muito tempo para convergir.

  - Com o método “menos conexões” você deve estar ciente de que é possível para um servidor de acesso para cliente se tornar sobrecarregado e parar de responder durante uma falha do servidor de acesso para cliente ou durante uma manutenção para correção. No contexto de desempenho do Exchange, a autenticação é uma operação cara.

Devido a vária limitações com o Balanceamento de Carga de Rede (NLB) do Windows em um ambiente do Exchange 2013, detalhadas em [Balanceamento de carga](load-balancing-exchange-2013-help.md), não recomendamos usar o Windows NLB.

## Distribuição de usuários e de banco de dados

Mantenha uma distribuição bem equilibrada de usuários por banco de dados e de bancos de dados ativos por servidor. Distribua o consumo do espaço em disco do banco de dados uniformemente e equilibre os usuários entre todos os bancos de dados.

Você deve analisar o perfil de sua base de usuários para entender como eles interagem com o Exchange (dispositivos, Outlook e OWA) e o impacto que essas interações causam de um ponto de vista do desempenho. Consulte as postagens sobre a Calculadora da seção 2 para obter uma compreensão melhor de como analisar o uso do Exchange de acordo com os usuários.

Configure as preferências de ativação de cópia de banco de dados e as configurações de "MaximumPreferredActiveDatabases" (por servidor) para manter o equilíbrio durante um failover ou uma migração.

O script RedistributeActiveDatabases.ps1 equilibra novamente as cópias de bancos de dados ativas nos nós do DAG.

Considere impor limites rígidos de contagem de itens que correspondam ao Office 365. Para fazer isso, use o cmdlet Set-Mailbox e as informações fornecidas no tópico [Limites de pasta de caixas de correio](http://go.microsoft.com/fwlink/p/?linkid=398779).

## Arquivo de paginação

Defina um tamanho máximo para o arquivo de paginação de 32778 MB se estiver usando mais de 32 GB de RAM.

O arquivo de paginação não deve ser hospedado na mesma unidade que arquivos de bancos de dados do Exchange ou arquivos de log de banco de dados.

É fundamental que você use um arquivo de paginação de tamanho fixo e não permita que o Windows gerencie o tamanho. Um arquivo de paginação com tamanho crescente pode ser uma tarefa que afetam muito o desempenho e pode causar problemas quando o Exchange estiver sobrecarregado.

Caso precise obter um arquivo de despejo de kernel completo, use o artigo 969028, [Como gerar um arquivo de despejo de memória ou de kernel completo no Windows Server 2008 e no Windows Server 2008 R2](http://go.microsoft.com/fwlink/p/?linkid=524044), da Base de Dados de Conhecimento da Microsoft para obter um arquivo de despejo dedicado.

## Modo do Outlook

Recomendamos o Modo em Cache. Para compreender os benefícios de usar o Modo em Cache, confira [Escolher entre o Modo em Cache do Exchange e o Modo Online do Outlook 2013](http://go.microsoft.com/fwlink/p/?linkid=524045).

É importante observar que o desempenho pode ser afetado por suplementos do servidor e suplementos de terceiros para o Outlook. Ao usar o modo online, os clientes podem esperar alguns problemas de desempenho com suplementos de terceiros, contagens de itens de alta, modos de exibição restritos, quantidade de usuários acessando a caixa de correio, entre outros fatores. Os clientes herdados podem sofrer maior impacto com a contagem de itens alta e o desempenho do que o Outlook 2013.

Se a principal razão de uma organização ter configurado o Outlook no modo online for por questões de segurança, considere usar o BitLocker.

O Outlook 2013 oferece um novo recurso de "Controle Deslizante de Sincronização" para reduzir o tempo de download e o tamanho do arquivo OST. Confira o artigo [Configurar o Modo em Cache do Exchange no Outlook 2013](http://go.microsoft.com/fwlink/p/?linkid=390456) para saber mais.

Verifique mensalmente se há atualizações para clientes do Outlook que são compatíveis com o seu ambiente.

## Software de terceiros

Como prática recomendada, desinstale ou desabilite o software de terceiros durante a solução de problemas de desempenho do Exchange. A lista a seguir contém os tipos de softwares de terceiros que a equipe de suporte da Microsoft tem visto afetar com mais frequência o desempenho do Exchange 2013.

  - Soluções antivírus

  - Software de prevenção de invasão

  - Software de backup

  - Software de auditoria, para usuários e arquivos

  - Soluções de arquivamento

