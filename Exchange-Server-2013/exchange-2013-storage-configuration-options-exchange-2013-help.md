---
title: 'Opções de configuração de armazenamento do Exchange 2013: Exchange 2013 Help'
TOCTitle: Opções de configuração de armazenamento do Exchange 2013
ms:assetid: 37cdeacf-74f9-4399-9860-4d1dbec12bb1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee832792(v=EXCHG.150)
ms:contentKeyID: 50485373
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Opções de configuração de armazenamento do Exchange 2013

 

_**Aplica-se a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Noções básicas sobre opções de armazenamento e requisitos para a função de servidor de Caixa de Correio do Microsoft Exchange Server 2013 é uma parte importante de sua solução de projeto de armazenamento de servidor de Caixa de Correio.

**Sumário**

Storage architectures

Physical disk types

Best practices for supported storage configurations

## Arquiteturas de armazenamento

A tabela a seguir descreve as arquiteturas de armazenamento suportadas, além de fornecer orientações de práticas recomendadas para cada tipo de arquitetura de armazenamento onde for necessário.

### Arquiteturas de armazenamento suportadas

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Arquitetura de armazenamento</th>
<th>Descrição</th>
<th>Práticas recomendadas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DAS (Armazenamento anexado diretamente)</p></td>
<td><p>O DAS é um sistema de armazenamento digital anexado diretamente a um servidor ou estação de trabalho, sem que haja uma rede de armazenamento entre eles. Por exemplo, os transportes DAS incluem SAS (Serial Attached SCSI) e ATA (Serial Attached Advanced Technology Attachment).</p></td>
<td><p>Não disponível.</p></td>
</tr>
<tr class="even">
<td><p>SAN (Redes de área de armazenamento): Internet Small Computer System Interface (iSCSI)</p></td>
<td><p>SAN é uma arquitetura para anexar dispositivos de armazenamento de um computador remoto (como matrizes de disco e bibliotecas de fita) a servidores de tal maneira que os dispositivos apareçam como anexados localmente ao sistema operacional (por exemplo, armazenamento de bloco). SANs de iSCSI (Internet Small Computer System Interface) encapsulam comandos SCSI em pacotes IP e usam a infraestrutura de rede padrão como o transporte de armazenamento (por exemplo, Ethernet).</p></td>
<td><p>Não compartilhe com outros aplicativos os discos físicos que são o backup de dados do Exchange.</p>
<p>Use redes de armazenamento dedicadas.</p>
<p>Use caminhos múltiplos de rede para configurações autônomas.</p></td>
</tr>
<tr class="odd">
<td><p>SAN: Fibre Channel</p></td>
<td><p>SANs de Fibre Channel encapsulam os comandos SCSI em pacotes Fibre Channel e geralmente utilizam redes de Fibre Channel especializadas como o transporte de armazenamento.</p></td>
<td><p>Não compartilhe com outros aplicativos os discos físicos que são o backup de dados do Exchange.</p>
<p>Use caminhos múltiplos de rede Fibre Channel para configurações autônomas.</p>
<p>Siga as práticas recomendadas do fornecedor de armazenamento a fim de ajustar os HBAs (Adaptadores de barramento de host) de Fibre Channel, por exemplo, Profundidade da fila e Destino da fila.</p></td>
</tr>
</tbody>
</table>


Uma unidade NAS (Armazenamento anexado na rede) é um computador independente que está conectado a uma rede, com o único propósito de fornecer serviços de armazenamento de dados baseados em arquivo para outros dispositivos na rede. O sistema operacional e outros softwares na unidade NAS proporcionam a funcionalidade de armazenamento de dados, sistemas de arquivos e acesso a arquivos, além do gerenciamento dessas funcionalidades (por exemplo, armazenamento de arquivos).

Todo o armazenamento usado pelo Exchange para armazenar dados do Exchange deve ser um armazenamento no nível de bloco, pois o Exchange 2013 não dá suporte ao uso de volumes NAS, a não ser no cenário SMB 3.0 descrito no tópico [Virtualização do Exchange 2013](exchange-2013-virtualization-exchange-2013-help.md). Além disso, em um ambiente virtualizado, não há suporte para o armazenamento NAS que é apresentado ao convidado como armazenamento no nível de bloco via hipervisor.

Não é recomendável usar os níveis de armazenamento, como ele pode prejudicar o desempenho do sistema. Por esse motivo, não permita o controlador de armazenamento mover automaticamente os arquivos acessados mais para armazenamento "mais rápido".

Voltar ao início

## Tipos de disco físico

A tabela a seguir fornece uma lista de tipos de disco físico suportados, além de fornecer orientações de práticas recomendadas para cada tipo de disco físico onde for necessário.

### Tipos de disco físico suportados

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipos de disco físico</th>
<th>Descrição</th>
<th>Com suporte ou prática recomendada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SATA (Serial ATA)</p></td>
<td><p>SATA é uma interface serial para ATA e discos IDE (integrated device electronics). Os discos de SATA estão disponíveis em vários fatores forma, velocidades e capacidades.</p>
<p>Em geral, escolha discos de SATA para o armazenamento de caixas de correio do Exchange 2013 quando você tiver os requisitos de design a seguir:</p>
<ul>
<li><p>Alta capacidade</p></li>
<li><p>Desempenho moderado</p></li>
<li><p>Consumo moderado de energia</p></li>
</ul></td>
<td><p>Suportado:  discos de setor de 512 bytes para Windows Server 2008 e Windows Server 2008 R2. Além disso, discos 512e são suportados para Windows Server 2008 R2 com o seguinte:</p>
<ul>
<li><p>O hotfix descrito no <a href="https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=982018">artigo 982018 da Base de Dados de Conhecimento Microsoft</a>. Uma atualização que aprimora a compatibilidade do Windows 7 e do Windows Server 2008 R2 com discos de formatação avançada, está disponível.</p></li>
<li><p>Windows Server 2008 R2 com Service Pack 1 (SP1) e Exchange Server 2010 SP1.</p></li>
</ul>
<p>O Exchange 2013 e versões posteriores oferecem suporte aos discos de setores de 4 KB e discos 512e. O suporte requer que todas as cópias de bancos de dados residam no mesmo tipo de disco físico. Por exemplo, não há suporte para hospedar uma cópia de determinado banco de dados em um disco de setores de 512 bytes e outra cópia do mesmo banco de dados em um disco 512e ou 4 KB.</p>
<p>Práticas recomendadas: Considere discos SATA de nível empresarial, os quais geralmente têm melhores características de aquecimento, vibração e confiabilidade.</p></td>
</tr>
<tr class="even">
<td><p>Serial Attached SCSI</p></td>
<td><p>Serial Attached SCSI é uma interface serial para discos SCSI. Os discos Serial Attached SCSI estão disponíveis em vários formatos, velocidades e capacidades.</p>
<p>Em geral, escolha discos de Serial Attached SCSI para o armazenamento de caixas de correio do Exchange 2013 quando você tiver os requisitos de design a seguir:</p>
<ul>
<li><p>Capacidade moderada</p></li>
<li><p>Alto desempenho</p></li>
<li><p>Consumo moderado de energia</p></li>
</ul></td>
<td><p>Suportado:  discos de setor de 512 bytes para Windows Server 2008 e Windows Server 2008 R2. Além disso, discos 512e são suportados para Windows Server 2008 R2 com o seguinte:</p>
<ul>
<li><p>O hotfix descrito no <a href="https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=982018">artigo 982018 da Base de Dados de Conhecimento Microsoft</a>. Uma atualização que aprimora a compatibilidade do Windows 7 e do Windows Server 2008 R2 com discos de formatação avançada, está disponível.</p></li>
<li><p>Windows Server 2008 R2 com Service Pack 1 (SP1) e Exchange Server 2010 SP1.</p></li>
</ul>
<p>O Exchange 2013 e versões posteriores oferecem suporte aos discos de setores de 4 KB e discos 512e. O suporte requer que todas as cópias de bancos de dados residam no mesmo tipo de disco físico. Por exemplo, não há suporte para hospedar uma cópia de determinado banco de dados em um disco de setores de 512 bytes e outra cópia do mesmo banco de dados em um disco 512e ou 4 KB.</p>
<p>Práticas recomendadas: O cache de gravação de disco físico deve estar desabilitado quando usado sem um no-break.</p></td>
</tr>
<tr class="odd">
<td><p>Fibre Channel</p></td>
<td><p>Fibre Channel é uma interface elétrica usada para conectar discos a SANs baseadas em Fibre Channel. Os discos Fibre Channel estão disponíveis em várias velocidades e capacidades.</p>
<p>Em geral, escolha discos Fibre Channel para o armazenamento de caixas de correio do Exchange 2013 quando você tiver os requisitos de design a seguir:</p>
<ul>
<li><p>Capacidade moderada</p></li>
<li><p>Alto desempenho</p></li>
<li><p>Conectividade SAN</p></li>
</ul></td>
<td><p>Suportado:  discos de setor de 512 bytes para Windows Server 2008 e Windows Server 2008 R2. Além disso, discos 512e são suportados para Windows Server 2008 R2 com o seguinte:</p>
<ul>
<li><p>O hotfix descrito no <a href="https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=982018">artigo 982018 da Base de Dados de Conhecimento Microsoft</a>. Uma atualização que aprimora a compatibilidade do Windows 7 e do Windows Server 2008 R2 com discos de formatação avançada, está disponível.</p></li>
<li><p>Windows Server 2008 R2 com Service Pack 1 (SP1) e Exchange Server 2010 SP1.</p></li>
</ul>
<p>O Exchange 2013 e versões posteriores oferecem suporte aos discos de setores de 4 KB e discos 512e. O suporte requer que todas as cópias de bancos de dados residam no mesmo tipo de disco físico. Por exemplo, não há suporte para hospedar uma cópia de determinado banco de dados em um disco de setores de 512 bytes e outra cópia do mesmo banco de dados em um disco 512e ou 4 KB.</p>
<p>Práticas recomendadas: O cache de gravação de disco físico deve estar desabilitado quando usado sem um no-break.</p></td>
</tr>
<tr class="even">
<td><p>SSD (unidade de estado sólido) (disco flash)</p></td>
<td><p>Um SSD é um dispositivo de armazenamento de dados que usa memória de estado sólido para armazenar dados persistentes. Um SSD emula a interface de unidade de disco rígido. Discos SSD estão disponíveis em várias velocidades (capacidades de desempenho de E/S diferentes) e capacidades.</p>
<p>Em geral, escolha discos de SSD para o armazenamento de caixas de correio do Exchange 2013 quando você tiver os requisitos de design a seguir:</p>
<ul>
<li><p>Baixa capacidade</p></li>
<li><p>Desempenho extremamente alto</p></li>
</ul></td>
<td><p>Suportado:  discos de setor de 512 bytes para Windows Server 2008 e Windows Server 2008 R2. Além disso, discos 512e são suportados para Windows Server 2008 R2 com o seguinte:</p>
<ul>
<li><p>O hotfix descrito no <a href="https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=982018">artigo 982018 da Base de Dados de Conhecimento Microsoft</a>. Uma atualização que aprimora a compatibilidade do Windows 7 e do Windows Server 2008 R2 com discos de formatação avançada, está disponível.</p></li>
<li><p>Windows Server 2008 R2 com Service Pack 1 (SP1) e Exchange Server 2010 SP1.</p></li>
</ul>
<p>O Exchange 2013 e versões posteriores oferecem suporte aos discos de setores de 4 KB e discos 512e. O suporte requer que todas as cópias de bancos de dados residam no mesmo tipo de disco físico. Por exemplo, não há suporte para hospedar uma cópia de determinado banco de dados em um disco de setores de 512 bytes e outra cópia do mesmo banco de dados em um disco 512e ou 4 KB.</p>
<p>Práticas recomendadas: O cache de gravação de disco físico deve estar desabilitado quando usado sem um no-break.</p>
<p>Em geral, os servidores de Caixa de correio do Exchange 2013 não exigem as características de desempenho do armazenamento SSD.</p></td>
</tr>
</tbody>
</table>


## Fatores para considerar na escolha de tipos de disco

Há uma série de fatores que devem ser considerados na escolha dos tipos de disco para armazenamento do Exchange 2013. O disco correto é aquele que equilibra desempenho (tanto sequencial quanto aleatório) com capacidade, confiabilidade, consumo de energia e custo de capital. A tabela de tipos de disco físico suportados a seguir fornece informações que o auxiliarão na consideração desses fatores.

A partir de um desempenho perspectiva, usando discos grandes, mais lentos para armazenamento do Exchange é tudo bem, fornecidos os discos podem manter uma média de leitura e gravação de latência de 20 ms ou menos sob carga.

### Fatores na escolha do tipo de disco

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Velocidade do disco (RPM)</th>
<th>Fator forma do disco</th>
<th>Interface ou transporte</th>
<th>Capacidade</th>
<th>Desempenho de E/S aleatório</th>
<th>Desempenho de E/S sequencial</th>
<th>Consumo de energia</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5,400</p></td>
<td><p>2.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>Média</p></td>
<td><p>Ruim</p></td>
<td><p>Ruim</p></td>
<td><p>Excelente</p></td>
</tr>
<tr class="even">
<td><p>5,400</p></td>
<td><p>3.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>Excelente</p></td>
<td><p>Ruim</p></td>
<td><p>Ruim</p></td>
<td><p>Acima da média</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>2.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>Média</p></td>
<td><p>Média</p></td>
<td><p>Média</p></td>
<td><p>Excelente</p></td>
</tr>
<tr class="even">
<td><p>7,200</p></td>
<td><p>2.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Média</p></td>
<td><p>Média</p></td>
<td><p>Acima da média</p></td>
<td><p>Excelente</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>3.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>Excelente</p></td>
<td><p>Média</p></td>
<td><p>Acima da média</p></td>
<td><p>Acima da média</p></td>
</tr>
<tr class="even">
<td><p>7,200</p></td>
<td><p>3.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Excelente</p></td>
<td><p>Média</p></td>
<td><p>Acima da média</p></td>
<td><p>Acima da média</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>3.5-inch</p></td>
<td><p>Fibre Channel</p></td>
<td><p>Excelente</p></td>
<td><p>Média</p></td>
<td><p>Acima da média</p></td>
<td><p>Média</p></td>
</tr>
<tr class="even">
<td><p>10,000</p></td>
<td><p>2.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Abaixo da média</p></td>
<td><p>Excelente</p></td>
<td><p>Acima da média</p></td>
<td><p>Acima da média</p></td>
</tr>
<tr class="odd">
<td><p>10,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>Média</p></td>
<td><p>Média</p></td>
<td><p>Acima da média</p></td>
<td><p>Acima da média</p></td>
</tr>
<tr class="even">
<td><p>10,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Média</p></td>
<td><p>Acima da média</p></td>
<td><p>Acima da média</p></td>
<td><p>Abaixo da média</p></td>
</tr>
<tr class="odd">
<td><p>10,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>Fibre Channel</p></td>
<td><p>Média</p></td>
<td><p>Acima da média</p></td>
<td><p>Acima da média</p></td>
<td><p>Abaixo da média</p></td>
</tr>
<tr class="even">
<td><p>15,000</p></td>
<td><p>2.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Ruim</p></td>
<td><p>Excelente</p></td>
<td><p>Excelente</p></td>
<td><p>Média</p></td>
</tr>
<tr class="odd">
<td><p>15,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>Média</p></td>
<td><p>Excelente</p></td>
<td><p>Excelente</p></td>
<td><p>Abaixo da média</p></td>
</tr>
<tr class="even">
<td><p>15,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>Fibre Channel</p></td>
<td><p>Média</p></td>
<td><p>Excelente</p></td>
<td><p>Excelente</p></td>
<td><p>Ruim</p></td>
</tr>
<tr class="odd">
<td><p>SSD: classe empresarial</p></td>
<td><p>Não aplicável</p></td>
<td><p>SATA, Serial Attached SCSI, Fibre Channel</p></td>
<td><p>Ruim</p></td>
<td><p>Excelente</p></td>
<td><p>Excelente</p></td>
<td><p>Excelente</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Práticas recomendadas para configurações de armazenamento suportadas

Esta seção fornece informações e práticas recomendadas sobre as configurações de disco e de controlador de matriz suportados.

RAID (redundant array of independent disks) geralmente é usada para aprimorar as características de desempenho de discos individuais (distribuindo dados em vários discos) e para oferecer proteção contra falhas de disco individuais. Com os avanços na alta disponibilidade do Exchange 2013, RAID não é mais um componente exigido para o design de armazenamento do Exchange 2013. Entretanto, RAID ainda é um componente essencial do design de armazenamento do Exchange 2013 para servidores independentes, assim como soluções que requerem tolerância a falhas de armazenamento.

**Volume de sistema operacional, sistema ou arquivo de paginação**

A configuração recomendada para um volume de sistema operacional, sistema ou arquivo de paginação é utilizar tecnologia RAID para proteger esse tipo de dados. A configuração RAID recomendada é RAID-1 ou RAID-1/0, no entanto, todos os tipos RAID são suportados.

**Volumes separados de banco de dados de caixa de correio e log**

Se você estiver implantando uma arquitetura de função de servidor de Caixa de Correio autônoma, a tecnologia RAID é requerida para os volumes de banco de dados de caixa de correio e log. A configuração RAID recomendada para volumes de caixa de correio é RAID-1/0 (especialmente se você estiver usando discos de 5,4 K ou 7,2 K); no entanto, todos os tipos RAID são suportados. Para volumes de log, RAID-1 ou RAID-1/0 é a configuração RAID recomendada.

Ao usar configurações RAID-5 ou RAID-6 para os volumes de sistema operacional, arquivo de paginação ou Exchange dados, observe o seguinte:

  - Configurações RAID-5, incluindo variações como RAID-50 e RAID-51, não devem ter mais de 7 discos por grupo de matriz e verificação de superfície e varredura de alta prioridade para controlador de matriz habilitadas.

  - Configurações RAID-6 devem ter verificação de superfície e varredura de alta prioridade para controlador de matriz habilitadas.

Embora JBOD seja suportado em arquiteturas de alta disponibilidade que tenham 3 ou mais cópias de banco de dados altamente disponíveis, como os volumes de log e de banco de dados de caixa de correio são separados, JBOD não é recomendado.

**Colocalização de volume de banco de dados de caixa de correio e log**

A colocalização de volume de banco de dados de caixa de correio e log não é recomendada em arquiteturas autônomas. Em arquiteturas de alta disponibilidade, há duas possibilidades para esse cenário:

1.  Banco de dados único por volume

2.  Vários bancos de dados por volume

**Banco de dados único por volume**

A partir de uma perspectiva do Exchange, JBOD significa ter o banco de dados e seus logs associados armazenados em um único disco. Para implantar em JBOD, é preciso implantar no mínimo três cópias de banco de dados com disponibilidade alta. A utilização de um único disco é um ponto de falha único, porque, quando o disco falha, a cópia de banco de dados que reside nesse disco é perdida. Ter um mínimo de três cópias de banco de dados garante tolerância a falhas, basta ter duas cópias adicionais caso essa cópia (ou um disco) falhe. Entretanto, o uso de três cópias de banco de dados com disponibilidade alta, bem como o uso de cópias de banco de dados com retardamento, pode afetar o projeto de armazenamento. A tabela a seguir mostra diretrizes para considerações de RAID e JBOD.

### Considerações de RAID ou JBOD

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Servidores de datacenter</th>
<th>Duas cópias com disponibilidade alta (total)</th>
<th>Três cópias com disponibilidade alta (total)</th>
<th>Duas ou mais cópias com disponibilidade alta por datacenter</th>
<th>Uma cópia com retardamento</th>
<th>Duas ou mais cópias com atraso por datacenter</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores de datacenter principal</p></td>
<td><p>RAID</p></td>
<td><p>RAID ou JBOD (2 cópias)</p></td>
<td><p>RAID ou JBOD</p></td>
<td><p>RAID</p></td>
<td><p>RAID ou JBOD</p></td>
</tr>
<tr class="even">
<td><p>Servidores de datacenter secundário</p></td>
<td><p>RAID</p></td>
<td><p>RAID (1 cópia)</p></td>
<td><p>RAID ou JBOD</p></td>
<td><p>RAID</p></td>
<td><p>RAID ou JBOD</p></td>
</tr>
</tbody>
</table>


Para implantar em JBOD com os servidores de datacenter principais, você precisa de três ou mais cópias de banco de dados com disponibilidade alta no DAG. Caso ocorra a mistura de cópias com retardamento no mesmo servidor que hospeda cópias de banco de dados com disponibilidade alta (por exemplo, sem o uso de servidores de cópia de banco de dados com retardamento dedicados), você precisará de pelos menos duas cópias de banco de dados com retardamento.

Para que os servidores de datacenter secundários usem JBOD, você deverá ter pelo menos duas cópias de banco de dados com disponibilidade alta no datacenter secundário. A perda de uma cópia no datacenter secundário não resultará na solicitação de nova propagação pela WAN ou na necessidade de ter um único ponto de falha caso o datacenter secundário seja ativado. Caso ocorra a mistura de cópias de banco de dados com retardamento no mesmo servidor que hospeda cópias de banco de dados com disponibilidade alta (por exemplo, sem o uso de servidores de cópia de banco de dados com retardamento dedicados), você precisará de pelos menos duas cópias de banco de dados com retardamento.

Para servidores de cópia de banco de dados com retardamento dedicados, você deverá ter pelo menos duas cópias de banco de dados com retardamento em um datacenter para usar JBOD. Caso contrário, a perda de disco resultará na perda de cópia de banco de dados com retardamento, bem como na perda do mecanismo de proteção.

**Vários bancos de dados por volume**

Vários bancos de dados por volume é um novo cenário de JBOD disponível no Exchange 2013, que permite que cópias ativas e passivas (incluindo cópias com atraso) sejam misturadas em um único disco, possibilitando melhor utilização de disco. No entanto, para implantar cópias com atraso dessa maneira, o descarte automático do arquivo de log de cópia com atraso deve ser habilitado. A tabela seguinte mostra diretrizes para considerações sobre o JBOD para vários bancos de dados por volume.

### Considerações sobre o JBOD

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Servidores de datacenter</th>
<th>3 ou mais cópias (total)</th>
<th>Duas ou mais cópias por datacenter</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores de datacenter principal</p></td>
<td><p>JBOD</p></td>
<td><p>JBOD</p></td>
</tr>
<tr class="even">
<td><p>Servidores de datacenter secundário</p></td>
<td><p>N/D</p></td>
<td><p>JBOD</p></td>
</tr>
</tbody>
</table>


A tabela a seguir fornece orientações sobre as configurações de matriz de armazenamento do Exchange 2013.

### Tipos de RAID suportados para a função de servidor de Caixa de correio do Exchange 2013

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de RAID</th>
<th>Descrição</th>
<th>Com suporte ou prática recomendada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tamanho da faixa de RAID na matriz de disco (KB)</p></td>
<td><p>O tamanho da faixa é a unidade por disco de distribuição de dados em um conjunto RAID. O tamanho da faixa é também conhecido como <em>tamanho de bloco</em>.</p></td>
<td><p>Práticas recomendadas: 256 KB ou mais. Seguir as práticas recomendadas do fornecedor de armazenamento.</p></td>
</tr>
<tr class="even">
<td><p>Configurações de cache da matriz de armazenamento</p></td>
<td><p>As configurações de cache são fornecidas por um controlador de matriz em cache com suporte de bateria.</p></td>
<td><p>Práticas recomendadas: 100 por cento cache de gravação (bateria ou cache alimentado flash) para controladores de armazenamento em um uma configuração de RAID ou JBOD. 75% de gravação cache, cache (bateria ou cache alimentado flash) de leitura de 25 por cento para outros tipos de soluções de armazenamento, como SAN. Se o seu fornecedor de SAN tem diferentes práticas recomendadas para configuração de cache em sua plataforma, siga as orientações de seu fornecedor de SAN.</p></td>
</tr>
<tr class="odd">
<td><p>Cache de gravação de disco físico</p></td>
<td><p>As configurações para o cache estão em cada disco individual.</p></td>
<td><p>Com suporte: O cache de gravação de disco físico deve estar desabilitado quando usado sem um no-break.</p></td>
</tr>
</tbody>
</table>


A tabela a seguir fornece orientações sobre escolha de arquivos de log e de banco de dados.

### Escolhas de arquivo de log e de banco de dados para a função de servidor de Caixa de correio do Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Opções de arquivo de log e de banco de dados</th>
<th>Descrição</th>
<th>Autônomo: com suporte ou prática recomendada</th>
<th>Alta disponibilidade: com suporte ou prática recomendada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Localização do arquivo: banco de dados por isolamento de log</p></td>
<td><p>Isolamento de banco de dados por log se refere à colocação de arquivos e logs de banco de dados do mesmo banco de dados de caixa de correio em diferentes volumes com suporte de discos físicos diferentes.</p></td>
<td><p>Práticas recomendadas: Para recuperação, mova os logs e arquivos de banco de dados (.edb) do mesmo banco de dados para diferentes volumes com suporte de discos físicos diferentes.</p></td>
<td><p>Com suporte: A isolação de logs e de bancos de dados não é exigida.</p></td>
</tr>
<tr class="even">
<td><p>Localização do arquivo: arquivos de banco de dados por volume</p></td>
<td><p>Arquivos de banco de dados por volume se refere a como você distribui os arquivos de banco de dados nos ou pelos volumes de disco.</p></td>
<td><p>Práticas recomendadas: Com base em sua metodologia de backup.</p></td>
<td><p>Com suporte: Ao usar o JBOD, crie um volume único com diretórios separados para bancos de dados e para arquivos de log.</p></td>
</tr>
<tr class="odd">
<td><p>Localização do arquivo: fluxos de log por volume</p></td>
<td><p>Fluxos de log por volume se refere a como você distribui os arquivos de log de banco de dados nos ou pelos volumes de disco.</p></td>
<td><p>Práticas recomendadas: Com base em sua metodologia de backup.</p></td>
<td><p>Com suporte: Ao usar o JBOD, crie um volume único com diretórios separados para bancos de dados e para arquivos de log.</p>
<p>Práticas recomendadas: Ao usar o JBOD, use vários bancos de dados por volume.</p></td>
</tr>
<tr class="even">
<td><p>Tamanho do banco de dados</p></td>
<td><p>Tamanho do banco de dados se refere ao tamanho do arquivo de banco de dados (.edb) no disco.</p></td>
<td><p>Com suporte: Aproximadamente 16 terabytes.</p>
<p>Práticas recomendadas:</p>
<ul>
<li><p>200 gigabytes (GB) ou menos.</p></li>
<li><p>Provisionar para 120% do tamanho máximo calculado do banco de dados.</p></li>
</ul></td>
<td><p>Com suporte: Aproximadamente 16 terabytes.</p>
<p>Práticas recomendadas:</p>
<ul>
<li><p>2 terabytes ou menos.</p></li>
<li><p>Provisionar para 120% do tamanho máximo calculado do banco de dados.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Método de truncamento de log</p></td>
<td><p>Método de truncamento de log é o processo de truncamento e exclusão dos arquivos antigos de log de banco de dados. Há dois mecanismos:</p>
<ul>
<li><p>Log circular, no qual o Exchange exclui os logs.</p></li>
<li><p>Truncamento de log, que ocorre após um backup completo ou incremental de VSS (Serviço de cópias de sombra de volume) com êxito.</p></li>
</ul></td>
<td><p>Práticas recomendadas:</p>
<ul>
<li><p>Use backups para truncamento de log (por exemplo, log circular desabilitado).</p></li>
<li><p>Provisionamento para três dias de capacidade de geração de log.</p></li>
</ul></td>
<td><p>Práticas recomendadas:</p>
<ul>
<li><p>Habilite o log circular para implantações que usem os recursos de proteção de dados nativos do Exchange.</p></li>
<li><p>Provisionamento para três dias além da configuração de retardo de repetição da capacidade de geração de log.</p></li>
</ul></td>
</tr>
</tbody>
</table>


A tabela a seguir fornece orientações sobre os tipos de disco do Windows.

### Tipos de disco do Windows para a função de servidor de Caixa de correio do Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de disco do Windows</th>
<th>Descrição</th>
<th>Autônomo: com suporte ou prática recomendada</th>
<th>Alta disponibilidade: com suporte ou prática recomendada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Disco básico</p></td>
<td><p>Um disco inicializado para armazenamento básico é chamado de disco básico. Um disco básico contém volumes básicos, como partições primárias, partições estendidas e unidades lógicas.</p></td>
<td><p>Com suporte.</p>
<p>Práticas recomendadas: Use discos básicos.</p></td>
<td><p>Com suporte.</p>
<p>Práticas recomendadas: Use discos básicos.</p></td>
</tr>
<tr class="even">
<td><p>Disco dinâmico</p></td>
<td><p>Um disco inicializado para armazenamento dinâmico é chamado de disco dinâmico. Um disco dinâmico contém volumes dinâmicos, como volumes simples, volumes estendidos, volumes distribuídos, volumes espelhados e volumes RAID-5.</p></td>
<td><p>Com suporte.</p></td>
<td><p>Com suporte.</p></td>
</tr>
</tbody>
</table>


A tabela a seguir fornece orientações sobre as configurações de volume.

### Configurações de volume para a função de servidor de Caixa de correio do Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuração de volume</th>
<th>Descrição</th>
<th>Autônomo: com suporte ou prática recomendada</th>
<th>Alta disponibilidade: com suporte ou prática recomendada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GPT (tabela de partição da GUID)</p></td>
<td><p>GPT é uma arquitetura de disco que se expande no esquema de particionamento do MBR (registro mestre de inicialização) mais antigo. O tamanho máximo de partição formatada NTFS é de 256 terabytes.</p></td>
<td><p>Com suporte.</p>
<p>Práticas recomendadas: Use as partições GPT.</p></td>
<td><p>Com suporte.</p>
<p>Práticas recomendadas: Use as partições GPT.</p></td>
</tr>
<tr class="even">
<td><p>MBR</p></td>
<td><p>Um MBR, ou setor de partição, é o setor de inicialização de 512 bytes que é o primeiro setor (LBA Sector 0) de um dispositivo particionado de armazenamento de dados, como um disco rígido. O tamanho máximo de partição formatada NTFS é de 2 terabytes.</p></td>
<td><p>Com suporte.</p></td>
<td><p>Com suporte.</p></td>
</tr>
<tr class="odd">
<td><p>Alinhamento de partição</p></td>
<td><p>O alinhamento de partição se refere ao alinhamento de partições nos limites do setor para desempenho ideal.</p></td>
<td><p>Com suporte: O padrão para o Windows Server 2008 R2 e o Windows Server 2012 é de 1 megabyte (MB).</p></td>
<td><p>Com suporte: O padrão para o Windows Server 2008 R2 e o Windows Server 2012 é de 1 MB.</p></td>
</tr>
<tr class="even">
<td><p>Caminho do volume</p></td>
<td><p>Caminho do volume se refere a como um volume é acessado.</p></td>
<td><p>Com suporte: Letra da unidade ou ponto de montagem.</p>
<p>Práticas recomendadas: O volume de host do ponto de montagem deve ter RAID habilitado.</p></td>
<td><p>Com suporte: Letra da unidade ou ponto de montagem.</p>
<p>Práticas recomendadas: O volume de host do ponto de montagem deve ter RAID habilitado.</p></td>
</tr>
<tr class="odd">
<td><p>Sistema de arquivos</p></td>
<td><p>O sistema de arquivos é um método de armazenar e organizar arquivos de computador e os dados que eles contêm de forma que seja fácil localizá-los e acessá-los.</p></td>
<td><p>Com suporte: NTFS e ReFS.</p></td>
<td><p>Com suporte: NTFS e ReFS.</p></td>
</tr>
<tr class="even">
<td><p>Desfragmentação NTFS</p></td>
<td><p>A desfragmentação NTFS é um processo que reduz a quantidade de fragmentação em sistemas de arquivo do Windows. Isso é feito com a organização física de conteúdos do disco, a fim de armazenar as partes de cada arquivo de forma bem próxima e contígua.</p></td>
<td><p>Com suporte.</p>
<p>Práticas recomendadas: Não é exigida nem recomendada. No Windows Server 2012, também recomendamos desabilitar a otimização de disco automática e o recurso de desfragmentação.</p></td>
<td><p>Com suporte.</p>
<p>Práticas recomendadas: Não é exigida nem recomendada. No Windows Server 2012, também recomendamos desabilitar a otimização de disco automática e o recurso de desfragmentação.</p></td>
</tr>
<tr class="odd">
<td><p>Tamanho de unidade de alocação NTFS</p></td>
<td><p>O tamanho de unidade de alocação NFTS representa a menor quantidade de espaço em disco que pode ser alocada para manter um arquivo.</p></td>
<td><p>Com suporte: Todos os tamanhos de unidade de alocação.</p>
<p>Práticas recomendadas: 64 KB para volumes de arquivos .edb e de log.</p></td>
<td><p>Com suporte: Todos os tamanhos de unidade de alocação.</p>
<p>Práticas recomendadas: 64 KB para volumes de arquivos .edb e de log.</p></td>
</tr>
<tr class="even">
<td><p>Compressão NTFS</p></td>
<td><p>A compressão NTFS é o processo de redução do tamanho real de um arquivo armazenado em um disco rígido.</p></td>
<td><p>Com suporte: Não suportado para arquivos de log ou banco de dados do Exchange.</p></td>
<td><p>Com suporte: Não suportado para arquivos de log ou banco de dados do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p>Sistema EFS (Encrypting File System) NTFS</p></td>
<td><p>O EFS permite que os usuários criptografem arquivos e pastas individuais, além de unidades de dados inteiras. Uma vez que o EFS oferece criptografia consistente por meio de algoritmos e criptografia por chave pública com o padrão do setor, os arquivos criptografados serão confidenciais mesmo se um invasor driblar a segurança do sistema.</p></td>
<td><p>Com suporte: Não suportado para arquivos de log ou banco de dados do Exchange.</p></td>
<td><p>Não suportado para arquivos de log ou banco de dados do Exchange.</p></td>
</tr>
<tr class="even">
<td><p>Windows BitLocker (criptografia de volume)</p></td>
<td><p>Windows BitLocker é um recurso de proteção de dados no Windows Server 2008. O BitLocker protege contra roubo de dados ou exposição em computadores que são perdidos ou roubados e oferece exclusão de dados mais segura quando os computadores são encerrados.</p></td>
<td><p>Com suporte: Todos os arquivos de log e banco de dados do Exchange.</p></td>
<td><p>Com suporte: Todos os arquivos de log e banco de dados do Exchange. Os clusters de failover do Windows exigem o Windows Server 2008 R2 ou o Windows Server 2008 R2 SP1 e o seguinte hotfix: <a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=2446607">Você não poderá habilitar o BitLocker em um volume de disco no Windows Server 2008 R2, se o computador for um nó de cluster de failover</a>. Os volumes do Exchange com o BitLocker habilitado não são suportados em clusters de failover do Windows executando versões anteriores do Windows.</p>
<p>Para obter mais informações sobre a criptografia de disco BitLocker Windows 7, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=220898">criptografia de unidade de disco BitLocker no Windows 7: perguntas frequentes</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Protocolo SMB 3.0</p></td>
<td><p>O protocolo SMB é um protocolo de compartilhamento de rede (em adição ao TCP/IP ou outros protocolos de rede) que permite que os aplicativos em um computador acessem arquivos e recursos em um servidor remoto. Isso também permite que os aplicativos se comuniquem com qualquer programa de servidor que esteja configurado para receber uma solicitação de cliente SMB. O Windows Server 2012 apresenta a nova versão 3.0 do protocolo SMB, com os seguintes recursos:</p>
<ul>
<li><p>Failover transparente para SMB</p></li>
<li><p>Dimensionamento de SMB</p></li>
<li><p>SMB Multicanais</p></li>
<li><p>SMB Direto</p></li>
<li><p>Criptografia SMB</p></li>
<li><p>VSS para compartilhamentos de arquivos SMB</p></li>
<li><p>Leasing de Diretório SMB</p></li>
<li><p>PowerShell SMB</p></li>
</ul></td>
<td><p>Suporte limitado. O cenário com suporte é uma implantação virtualizada de hardware onde os discos são hospedados em VHDs em um compartilhamento SMB 3.0. Esses VHDs são apresentados ao host por meio de um hipervisor. Para obter mais informações, consulte <a href="exchange-2013-virtualization-exchange-2013-help.md">Virtualização do Exchange 2013</a>.</p></td>
<td><p>Suporte Limitado. O cenário com suporte é uma implantação virtualizada de hardware onde os discos são hospedados em VHDs em um compartilhamento SMB 3.0. Esses VHDs são apresentados ao host por meio de um hipervisor. Para obter mais informações, consulte <a href="exchange-2013-virtualization-exchange-2013-help.md">Virtualização do Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Espaços de Armazenamento</p></td>
<td><p>Espaços de armazenamento é uma nova solução de armazenamento que oferece recursos de virtualização do Windows Server 2012. Espaços de armazenamento permitem que você organize discos físicos em pools de armazenamento, que podem ser facilmente expandidos simplesmente adicionando discos. Esses discos podem ser conectados por meio de USB, SATA ou SAS. Ele também utiliza discos virtuais (espaços), se comportam como discos físicos, com recursos poderosos associados como fina de provisionamento, bem como resiliência a falhas de mídia física subjacente. Para obter mais informações sobre os espaços de armazenamento, consulte <a href="https://technet.microsoft.com/en-us/library/hh831739.aspx">Visão geral de espaços de armazenamento</a>.</p></td>
<td><p>Com suporte. As mesmas restrições de tipos de disco físico descritas neste tópico.</p></td>
<td><p>Com suporte. As mesmas restrições de tipos de disco físico descritas neste tópico.</p></td>
</tr>
<tr class="odd">
<td><p>Sistema de Arquivos Resiliente (ReFS)</p></td>
<td><p>ReFS é um sistema de arquivos recentemente engenharia do Windows Server 2012 que se baseia nas bases do NTFS. ReFS mantém alto grau de compatibilidade com NTFS ao mesmo tempo fornecendo as técnicas de verificação e correção automática aprimorada de dados, bem como uma integrada resiliência de ponta a ponta para corrupções, especialmente quando usada em conjunto com o recurso de espaços de armazenamento. Para obter mais informações sobre ReFS, consulte <a href="https://technet.microsoft.com/en-us/library/hh831724.aspx">Visão geral de sistema do arquivo resiliente</a>.</p></td>
<td><p>Suporte para volumes que contêm os arquivos de banco de dados, arquivos de log e arquivos de indexação de conteúdo do Exchange. Se implantar o Windows Server 2012, certifique-se de que os seguintes hotfixes são instalados no Windows Server 2012:</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717874">Windows 8 e Windows Server 2012 pacotes cumulativos de atualizações: abril de 2013</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717877">Serviço de disco virtual ou aplicativos que usam o serviço de disco Virtual de travamento ou congelar no Windows Server 2012</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717879">Computador baseado no Windows Server 2012 ou Windows 8 congela quando você executar o comando 'dir' um volume ReFS</a></p></li>
</ul>
<p>ReFS não é suportado para volumes de sistema operacional.</p>
<p>Práticas recomendadas: recursos de integridade de dados devem ser desabilitados para os arquivos de banco de dados (. edb) do Exchange ou o volume que hospeda esses arquivos.</p></td>
<td><p>Suporte para volumes que contêm os arquivos de banco de dados, arquivos de log e arquivos de indexação de conteúdo do Exchange. Se Implantando o Windows Server 2012, certifique-se de que os seguintes hotfixes são instalados no Windows Server 2012:</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717874">Windows 8 e Windows Server 2012 pacotes cumulativos de atualizações: abril de 2013</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717877">Serviço de disco virtual ou aplicativos que usam o serviço de disco Virtual de travamento ou congelar no Windows Server 2012</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717879">Computador baseado no Windows Server 2012 ou Windows 8 congela quando você executar o comando 'dir' um volume ReFS</a></p></li>
</ul>
<p>ReFS não é suportado para volumes de sistema operacional.</p>
<p>Práticas recomendadas: recursos de integridade de dados devem ser desabilitados para os arquivos de banco de dados (. edb) do Exchange ou o volume que hospeda esses arquivos.</p></td>
</tr>
<tr class="even">
<td><p>Eliminação da duplicação de dados</p></td>
<td><p>A eliminação da duplicação de dados é uma nova técnica para otimizar a utilização de armazenamento para o Windows Server 2012. É um método para localizar e remover a duplicação nos dados sem comprometer sua fidelidade ou integridade. A meta é armazenar mais dados em menos espaço ao segmentar arquivos em pequenas partes de tamanho variado, identificando as partes duplicadas e mantendo uma cópia de cada uma delas. Cópias redundantes da parte são substituídas por uma referência à cópia única, as partes são organizadas em arquivos contêineres e os contêineres são compactados para mais otimização de espaço.</p></td>
<td><p>Sem suporte para arquivos de banco de dados do Exchange. Observação: Pode ser usado para arquivos de banco de dados do Exchange que estejam completamente offline (usado como backups ou arquivos mortos).</p></td>
<td><p>Sem suporte para arquivos de banco de dados do Exchange. Observação: Pode ser usado para arquivos de banco de dados do Exchange que estejam completamente offline (usado como backups ou arquivos mortos).</p></td>
</tr>
</tbody>
</table>


Voltar ao início

