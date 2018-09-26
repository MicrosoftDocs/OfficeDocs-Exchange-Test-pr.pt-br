---
title: 'Modo coordenação de ativação de Datacenter: Exchange 2013 Help'
TOCTitle: Modo coordenação de ativação de Datacenter
ms:assetid: 57e4bf22-eeae-42a5-beb3-d68d06489592
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd979790(v=EXCHG.150)
ms:contentKeyID: 50485644
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modo coordenação de ativação de Datacenter

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-07-14_

Modo coordenação de ativação de Datacenter (DAC) é uma propriedade de um grupo de disponibilidade do banco de dados (DAG). Modo DAC está desabilitado por padrão, mas deve ser habilitado para todos os DAGs com dois ou mais membros que usam replicação contínua. Modo DAC não deve ser habilitado para DAGs que usam o modo de replicação de terceiros, a menos que especificado pelo fornecedor terceirizado.

Modo DAC é usado para controlar a montagem do banco de dados sobre o comportamento de inicialização de um DAG. Esse controle foi projetado para impedir que o split brain que ocorrem no nível do banco de dados durante um switchback de datacenter. Split brain, também conhecidas como situação de inconsistência é uma condição que resulte em um banco de dados copiando seja montado como uma cópia ativa em dois membros do mesmo DAG que não podem se comunicar. Split brain é impedido usando o modo DAC porque requer o modo DAC membros do DAG obter a permissão para montar bancos de dados antes que eles podem ser montados.

Por exemplo, considere um cenário em que um data center principal contém dois membros do DAG e o servidor testemunha e um segundo data center contém dois outros membros do DAG. Neste cenário, o DAG não estiver em modo DAC. Datacenter principal perde energia, portanto você ativar DAG no segundo datacenter. Eventualmente energia para o datacenter primário é restaurada e os membros do DAG no datacenter primário, que tinham quorum antes da falha de energia, serão inicialização e monte seus bancos de dados. Como o datacenter primário foi restaurado sem conectividade de rede para o segundo datacenter, e o DAG não estava em modo DAC, os bancos de dados ativos dentro do DAG inseriu uma condição de cérebro dividido.

## Como funciona o modo DAC

Modo DAC foi projetado para impedir que o split brain ocorram, incluindo um protocolo denominado protocolo de coordenação de ativação de Datacenter (DACP). Quando o modo DAC estiver habilitado, membros DAG automaticamente não montagem bancos de dados, mesmo que eles tenham o quorum. Em vez disso DACP é usado para determinar o estado atual do DAG e se Active Manager deve tentar Monte os bancos de dados.

Você pode considerar modo DAC como um nível de aplicativo de quorum para montar bancos de dados. Para entender a finalidade do DACP e como ele funciona, é importante entender o cenário primário, que ele foi projetado para manipular. Considere o cenário dois-datacenter. Vamos supor que há uma falha completa de energia no datacenter principal. Nesse caso, todos os servidores e WAN estão desativados, para que a organização toma a decisão de ativar o datacenter em espera. Quase todos os nesses cenários de recuperação, quando a alimentação é restaurada para o datacenter primário, conectividade WAN geralmente é não imediatamente restaurada. Isso significa que os membros do DAG no datacenter principal ligará, mas eles não poderão se comunicar com os membros do DAG no datacenter ativado em espera. Datacenter principal sempre deve conter a maioria dos votantes de quorum do DAG, o que significa que, quando a alimentação é restaurada, mesmo na ausência de conectividade WAN com os membros do DAG no datacenter em espera, os membros do DAG no datacenter principal tem uma maioria e, portanto, têm quorum. Este é um problema porque com quorum, esses servidores podem ser capazes de montar seus bancos de dados, que por sua vez causaria divergência em relação as bancos de dados ativos reais que agora são montados no datacenter ativado em espera.

DACP foi criado para resolver esse problema. O Active Manager armazena um pouco na memória (0 ou 1) que informa o DAG se ele tem permissão para montar bancos de dados locais que são atribuídos como ativo no servidor. Quando um DAG está sendo executado em modo DAC, sempre que o Active Manager é iniciado estará definido o bit é definido como 0, o que significa que ele não é permitido para montar bancos de dados. Porque ele está em modo DAC, o servidor deve tentar se comunicar com todos os outros membros do DAG que ele conhece obter outro membro do DAG dar-lhe uma resposta como para se ele pode montar bancos de dados locais que são atribuídos como ativa a ela. A resposta é fornecido na forma da configuração de bit para outros gerenciadores de ativo no DAG. Se o outro servidor responde que seu bit for definido como 1, significa que servidores têm permissão para montar bancos de dados, para que o servidor Iniciando define seu bit como 1 e monta seus bancos de dados.

Mas quando você recupera uma interrupção de energia de datacenter principal onde os servidores são recuperados, mas não foi restaurada conectividade WAN, todos os membros do DAG no datacenter principal terá um valor DACP bit 0; e, portanto, nenhum dos servidores de início de backup no datacenter principal recuperado será montado bancos de dados, porque nenhum deles podem se comunicar com um membro do DAG que tem um DACP bit valor de 1.

## Modo DAC para DAGs com dois membros

DAGs com dois membros têm limitações inerentes que impedem que o DACP bit sozinho totalmente proteção contra a situação de inconsistência nível de aplicativo. Para DAGs com apenas dois membros, o modo DAC também usa o tempo de inicialização do servidor de testemunha do DAG para determinar se ele pode montar bancos de dados na inicialização. O tempo de inicialização do servidor testemunha é comparado com a hora quando estará definido o bit DACP foi definido como 1.

  - Se o horário em que foi definido o bit DACP for mais antigos que o tempo de inicialização do servidor testemunha, o sistema pressupõe que o servidor de testemunha e o membro do DAG foram reinicializado ao mesmo tempo (talvez por causa de perda de energia no datacenter principal) e membro do DAG não é permitido para @ to bancos de dados do NT.

  - Se a hora em que foi definido o bit DACP for mais recente do que o tempo de inicialização do servidor testemunha, o sistema pressupõe que o membro do DAG foi reinicializado por algum outro motivo (talvez uma interrupção agendada no qual manutenção foi executada ou talvez uma falha no sistema ou power perda iso relacionado ao membro DAG), e membro do DAG tem permissão para montar bancos de dados.


> [!IMPORTANT]
> Como o tempo de inicialização do servidor testemunha é usado para determinar se um membro do DAG pode montar seus bancos de dados ativos na inicialização, você nunca deve reiniciar o servidor testemunha e o único membro do DAG ao mesmo tempo. Isso pode deixar o membro do DAG em um estado onde ele não é possível montar bancos de dados na inicialização. Se isso ocorrer, você deve executar o cmdlet <A href="https://technet.microsoft.com/pt-br/library/dd351169(v=exchg.150)">Restore-DatabaseAvailabilityGroup</A> no DAG. Isso redefine o bit DACP e permite que o membro do DAG para montar bancos de dados.



## Outros benefícios do modo DAC

Além de impedir a situação de inconsistência no nível do aplicativo, o modo DAC também permite que o uso dos cmdlets resiliência site interno usados para realizar alternâncias de datacenter. Isso inclui o seguinte:

  - [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd335133\(v=exchg.150\))

  - [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd351169\(v=exchg.150\))

  - [Start-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd335076\(v=exchg.150\))

Realizar uma alternância de datacenter para DAGs que não estejam em modo DAC envolve o uso de uma combinação de ferramentas de Exchange e ferramentas de gerenciamento do cluster. Para obter mais informações, consulte [Switchovers do Datacenter](datacenter-switchovers-exchange-2013-help.md).

## Habilitando o modo DAC

Modo DAC pode ser habilitado somente por meio de Exchange Management Shell. Especificamente, você pode usar o cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd297934\(v=exchg.150\)) para habilitar o modo DAC, conforme ilustrado no exemplo a seguir.

```powershell
Set-DatabaseAvailabilityGroup -Identity DAG2 -DatacenterActivationMode DagOnly
```

No exemplo anterior, DAG2 é habilitado para o modo DAC.

Para obter mais informações sobre como habilitar o modo DAC, consulte [Configurar as propriedades do grupo de disponibilidade do banco de dados](configure-database-availability-group-properties-exchange-2013-help.md) e [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd297934\(v=exchg.150\)).

