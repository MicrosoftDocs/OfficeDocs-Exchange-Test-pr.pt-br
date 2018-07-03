---
title: 'Planos de discagem secundário: Exchange 2013 Help'
TOCTitle: Planos de discagem secundário
ms:assetid: ecf474c2-042d-4aaf-9f5b-d5138c56ef39
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff629383(v=EXCHG.150)
ms:contentKeyID: 54913447
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Planos de discagem secundário

 

_**Aplica-se a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2015-03-09_

Quando você habilita um usuário para Unificação de mensagens (UM), é necessário que você atribua um número de ramal e o plano de discagem de uma política de caixa de correio de Unificação de mensagens que irá vincular o usuário a uma Unificação de mensagens. Depois que o usuário está habilitado para Unificação de mensagens, você pode atribuir números de ramal adicionais para o usuário no mesmo plano de discagem, mas os números de ramal no plano de discagem que devem ser exclusivos. Em alguns casos, talvez seja necessário ter o mesmo número de ramal nos dois planos de discagem separados um usuário. Se este for o caso, você pode vincular o usuário a um plano de discagem de UM secundário. Isso pode ser útil, por exemplo, se o usuário tem dois telefones físicos ou percorrem entre locais.

**Conteúdo**

Visão geral

Use of secondary extensions

UM features that operate differently for secondary dial plans

## Visão geral

Quando você habilita um usuário para Unificação de mensagens, você deve definir um número de ramal e uma política de caixa de correio de Unificação de mensagens que vincula o usuário a um único plano de discagem de UM. Quando você habilitar o usuário para Unificação de mensagens e estejam vinculados a uma política de caixa de correio de Unificação de mensagens que esteja vinculada a um URI do SIP ou plano de discagem e. 164, você também deve fornecer um endereço SIP ou o número e. 164 com o número de ramal do usuário. Unificação de mensagens usa o plano de discagem e extensão, juntamente com o endereço SIP ou o número e. 164, para localizar o usuário quando uma mensagem de voz é enviada à caixa de correio do usuário.

Se você estiver usando planos de discagem de ramal de telefone e precisa fornecer o mesmo número de ramal de um usuário, você precisará criar um plano de discagem secundário, permitir que o usuário para Unificação de mensagens e fornecer o mesmo número de ramal para o usuário. Isso ocorre porque o número do ramal deve ser exclusivo dentro de um plano de discagem


> [!TIP]
> Não há limite para o número de ramais secundários que você pode adicionar para um usuário habilitado para UM.



Pode haver ocasiões quando um usuário viaja entre locais, tem dois ou mais telefones ou deseja receber a caixa postal em um número de ramal direto DID (discagem) e receber faxes em um número diferente de extensão DID. Para conseguir isso, você deve adicionar uma extensão DID adicional à caixa de correio do usuário e, em alguns casos, adicione um plano de discagem secundário.

Em algumas configurações, depois de adicionar uma extensão de segunda em um plano de discagem principal ou adicionar um números de ramal único ou vários a um plano de discagem secundário, o usuário poderá receber mensagens de voz ou fax usando um ou mais dos números de ramal. Se desejar que a Unificação de mensagens para atender essas chamadas de fax e enviá-los para o segundo número do ramal DID, você deve configurar o equipamento de telefonia em sua organização para encaminhar as chamadas de fax para o segundo número do ramal DID.

À caixa de correio de um usuário habilitado para UM pode ser atribuído o seguinte:

  - Um único ramal, endereço SIP (Session Initiation Protocol) ou endereço E.164 em um único plano de discagem

  - Vários números de ramais em um único plano de discagem

  - Vários números de ramais em dois planos de discagem separados

Quando um usuário está habilitado para Unificação de mensagens, você deve especificar um número de ramal e uma política de caixa de correio de Unificação de mensagens. Unificação de mensagens requer o número de ramal identificar o usuário quando entrarem no Outlook Voice Access para recuperar mensagens. A diretiva de caixa de correio UM contém uma coleção de propriedades de configuração, com valores que UM se aplica a qualquer usuário que seja habilitado sob essa diretiva. A diretiva de caixa de correio de Unificação de mensagens é semelhante de "classe de serviço" encontrado em outros sistemas (por exemplo, caixa postal ou PBX), no sentido de que uma alteração em um valor de diretiva de caixa de correio de Unificação de mensagens pode afetar o comportamento de um grande número de usuários associados.

Uma propriedade em uma diretiva de caixa de correio UM se refere a um plano de discagem de UM. Isso representa um conjunto de extensões capaz de telefonia. Esse conjunto possui um plano de numeração na qual os números de ramal duplicados não são permitidos.

Portanto, o número de ramal de um usuário é exclusivo dentro de UM plano de discagem na qual eles estão habilitados para UM. Na verdade, a UM plano de discagem e par de números de extensão deve ser exclusivo dentro da organização. Esta é uma forma que identifica UM de um usuário habilitado em uma organização. Usar um plano de discagem secundário torna mais fácil manter o número de discagem plano e extensão exclusivo dentro de uma organização. Por exemplo, imagine que uma organização tem dois planos de discagem de UM: um plano de discagem e discagem plano B. Número de ramal de um usuário em um plano de discagem é 55555 e, em B de plano de discagem, ela do 66666. Quando um plano de discagem secundário é usado, o ramal do usuário para o plano de discagem A pode ser 55555 e sua extensão no B de plano de discagem também pode ser 55555. Em ambos os casos, o ramal do usuário no plano de discagem que é usado é exclusivo.

A tabela a seguir define os termos usados ao discutir ramais primários e secundários, números do Outlook Voice Access e planos de discagem de UM.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Termo</th>
<th>Definição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ramal principal</p></td>
<td><p>O número de ramal especificado quando o usuário está habilitado para UM.</p></td>
</tr>
<tr class="even">
<td><p>plano de discagem principal</p></td>
<td><p>O plano de discagem de UM que tenha especificado quando o usuário é UM habilitado. O usuário habilitado para UM está associado com o plano de discagem quando o usuário está vinculado à diretiva de caixa de correio de Unificação de mensagens.</p></td>
</tr>
<tr class="odd">
<td><p>Número primário do Outlook Voice Access</p></td>
<td><p>O número do Outlook Voice Access para o plano de discagem principal do usuário. As chamadas do usuário são encaminhadas para este número se há uma resposta ou sua linha está ocupada. Também é o número que o usuário chama quando eles desejam entrar Outlook Voice Access.</p></td>
</tr>
<tr class="even">
<td><p>ramal secundário</p></td>
<td><p>Um ou mais números de ramal que podem ser adicionados a uma configuração de usuário habilitado para UM.</p></td>
</tr>
<tr class="odd">
<td><p>plano de discagem secundário</p></td>
<td><p>Um plano de discagem de UM diferente do plano de discagem principal no qual um ou mais ramais secundários podem ser configurados.</p></td>
</tr>
<tr class="even">
<td><p>Número secundário do Outlook Voice Access</p></td>
<td><p>O número do Outlook Voice Access do plano de discagem secundário de um usuário. Um usuário pode chamar esse número do seu número de ramal secundário quando eles desejam entrar Outlook Voice Access.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Usar ramais secundários

Na maioria das implantações, apenas uma extensão é configurada por usuário habilitado. No entanto, há algumas implantações mais avançadas que exigem que você adicionar extensões secundárias para os usuários.

Quando Microsoft Lync Server é usado para o Enterprise Voice, a Unificação de mensagens pode fornecer o sistema de caixa postal. No entanto, o plano de discagem de UM usado para o Enterprise Voice deve ser um plano de discagem URI do SIP que é específico para configurações de Unificação de mensagens com o Lync Server. Nessas implantações, o ramal do usuário é fornecido por uma extremidade de comunicação unificada Microsoft, como MicrosoftOffice Communicator, em execução no computador do usuário ou Office Communicator Phone Edition, execução em um dispositivo de telefone IP com suporte. Assim, na maioria dos casos, o plano de discagem principal do usuário deve ser o mesmo plano de discagem URI do SIP usado com o Lync Server. Mas, se o usuário exigir mais números de ramal, você não deve adicionar outra extensão secundário ao plano de discagem principal. Você deve adicionar um plano de discagem secundário e adicione a extensão secundário ou o endereço de proxy EUM ao usuário habilitado para UM.

Para obter mais informações sobre a adição, remoção ou alteração de ramais, consulte o seguinte:

  - [Alterar um número de ramal](change-an-extension-number-exchange-2013-help.md)

  - [Adicionar um número de ramal](add-an-extension-number-exchange-2013-help.md)

  - [Remover um número de ramal](remove-an-extension-number-exchange-2013-help.md)

Se precisar alterar os endereços SIP ou os números E.164 para usuários de UM, consulte:

  - [Adicionar um endereço SIP](add-a-sip-address-exchange-2013-help.md)

  - [Alterar um endereço SIP](change-a-sip-address-exchange-2013-help.md)

  - [Remover um endereço SIP](remove-a-sip-address-exchange-2013-help.md)

  - [Adicionar um número e. 164](add-an-e-164-number-exchange-2013-help.md)

  - [Alterar um número e. 164](change-an-e-164-number-exchange-2013-help.md)

  - [Remover um número e. 164](remove-an-e-164-number-exchange-2013-help.md)

## Atendimento de chamadas

A Unificação de Mensagens oferece o seguinte:

  - **Atendimento de chamadas**   Ocorre quando um usuário não responde a uma chamada e a UM atende.

  - **Outlook Voice Access**   Usado pelos usuários quando ligam para o sistema de correio de voz a fim de acessar suas caixas postais.

Duas configurações são usadas com frequência:

  - Um usuário habilitado para Unificação de mensagens tem dois números de ramal (um primário, outro secundário) no plano de discagem principal. Essas extensões correspondem aos telefones diferentes na equipe de assistência técnica do usuário e estão conectados ao mesmo PBX. Esses números diferentes estão disponíveis para dois audiências separadas. Nesta configuração, o ramal principal é o número de trabalho "general" e a extensão secundária é o número de "tarefas específicas", possivelmente uma linha de assistência técnica ou um número de fax dedicado.

  - Um usuário habilitado gasta um determinado período de tempo, talvez três semanas a cada quatro no escritório de principal da sua empresa e o resto do tempo no office outra em um dos locais remotos da empresa. Os dois escritórios tem diferentes PBXs e os números de extensão são exclusivos de cada PBX. Neste exemplo, o usuário está configurado para ter uma extensão de principal no seu plano de discagem principal no escritório principal PBX e uma extensão de secundária em um plano de discagem secundário no PBX do escritório de.

Em qualquer uma das configurações, as mensagens de voz ou mensagens de notificação de chamadas perdidas geradas por chamadas não respondidas para o ramal serão enviadas para a Caixa de Entrada do usuário.

## Outlook Voice Access

Você talvez prefira usuários habilitados para poder entrar no Outlook Voice Access a partir de qualquer extensão, primário ou secundário. Embora seja possível, pode haver algumas restrições arquiteturais que mantêm isso funcione identicamente de todas as extensões. Para entrar em Outlook Voice Access, usuários habilitados para Unificação de mensagens devem executar as seguintes etapas:

1.  Ligar para um número do Outlook Voice Access.

2.  Digitar o número de ramal, se estiverem chamando de um outro número de telefone.

3.  Inserir seu PIN se não estiverem habilitados para o Enterprise Voice e estiverem ligando de um telefone de Unificação de Comunicações, do Office Communicator ou do Lync Server.

**Cenários de uso**

  - **Extensão único com o Outlook Voice Access**   Se o usuário tiver uma única extensão principal, eles sempre devem chamar o número do Outlook Voice Access para seu plano de discagem de UM principal. Se ligarem do seu número de ramal, eles não serão avisados para inserir o número de ramal e a etapa 2 das etapas anteriores será ignorada.

  - **Duas extensões no primário discagem plano com o Outlook Voice Access**   Se o usuário tem apenas duas extensões, principais e secundárias, e tanto a extensão primária e secundária está no mesmo plano de discagem de Unificação de mensagens, eles sempre devem chamar o número do Outlook Voice Access de plano de discagem. Se ligarem da extensão primário ou secundário, eles não serão avisados para inserir o número de ramal e a etapa 2 das etapas anteriores será ignorada. Outlook Recursos de acesso de voz funcionará da mesma forma, seja qual for o ramal é usado para entrar.

  - **Plano de discagem de extensões no primário e em um secundário de discagem plano com o Outlook Voice Access**   Se o usuário tem apenas duas extensões, principais e secundárias, e as extensões primárias e secundárias constam na discagem de Unificação de mensagens diferentes planos (primários e secundários); eles devem chamar o número do Outlook Voice Access apropriado para seu plano de discagem. Na sua extensão primário, eles devem chamar o número do Outlook Voice Access de plano de discagem principal e de sua extensão secundário, eles devem chamar o número do Outlook Voice Access de plano de discagem secundário. Se eles fazem isso, eles não serão avisados para inserir o número de ramal e a etapa 2 das etapas anteriores será ignorada.
    
    Outlook Recursos de acesso de voz que não envolvem discagem de saída (por exemplo "O remetente da chamada" ou "Chamada do escritório") funcionará da mesma forma, seja qual for o ramal é usado para entrar. No entanto, os recursos de acesso de voz do Outlook que exigem a discagem de saída não funcionarão como esperado quando o usuário entra ao plano de discagem secundário, a menos que as regras de discagem de saída forem exatamente iguais em ambos os planos de discagem. Para o comportamento de discagem de saída para ser exatamente o mesmo, você deve garantir que as seguintes propriedades são configuradas de forma idêntica nos planos de discagem primários e secundários:
    
      - Códigos de discagem (acesso do tronco, nacional/regional e internacional)
    
      - Códigos de discagem local ou regional
    
      - Regras de discagem
    
      - Nomes de grupos de regras de discagem

Um usuário habilitado para Unificação de mensagens é associado a uma política de caixa de correio de Unificação de mensagens e essa diretiva de caixa de correio de Unificação de mensagens está vinculada ao plano de discagem principal do usuário. As configurações de diretiva de caixa de correio de Unificação de mensagens que estão associadas ao plano de discagem principal do usuário habilitado para UM serão aplicadas ao usuário. Se um usuário estiver associado um plano de discagem secundário com um segundo número do ramal no plano de discagem secundário, as configurações de diretiva de caixa de correio de Unificação de mensagens associadas ao plano de discagem principal ainda serão aplicadas. No Outlook Voice Access, a mesma política de caixa de correio de Unificação de mensagens associadas ao plano de discagem principal de configurações são aplicadas se o usuário faz uma chamada para o principal plano de discagem ou plano de discagem para um secundário.

As propriedades **AllowedInCountryOrRegionGroups** e **AllowedInternationalGroups** na diretiva de caixa de correio de Unificação de mensagens contêm os nomes dos grupos de regras de discagem configurados na **ConfiguredInCountryOrRegionGroups** e **ConfiguredInternationalGroups** propriedades de um UM plano de discagem. Quando um usuário habilitado chama Outlook Voice Access, as regras de chamada de saída da diretiva de caixa de correio de UM associados com o principal ou plano de discagem secundário se aplicará às chamadas feitas pelo usuário, dependendo se o usuário habilitado chamou em ao primário ou secundário de discagem número do Outlook Voice Access do plano.

Por exemplo, se um plano de discagem principal chamado "plano de discagem de Contoso 1" tem uma regra de discagem chamada "EUA e Canadá" em sua propriedade **ConfiguredInCountryOrRegionGroups** , a diretiva de caixa de correio de Unificação de mensagens "Contoso UM Policy 1" também pode ter "EUA e Canadá" em sua propriedade **AllowedInCountryOrRegionGroups** . Se você deseja adicionar uma extensão secundária no "plano de discagem de Contoso 2" para um usuário em "política de Unificação de mensagens do Contoso 2", você teria que garantir que a propriedade **ConfiguredInCountryOrRegionGroups** de "plano de discagem de Contoso 2" também contém uma regra chamada "EUA e Canadá". Caso contrário, se o usuário entra no Outlook Voice Access a partir de sua extensão secundário, Unificação de mensagens não será capaz de encontrar uma regra no plano de discagem de secundário chamado "EUA e Canadá". Se isso acontecer, UM permitirá que apenas o usuário chamar números são permitidos para qualquer chamador ao plano de discagem secundário, o que poderia ser mais restritivo.

Voltar ao início

## Recursos de UM que funcionam de forma diferente em planos de discagem secundários

Há um conjunto de recursos de Unificação de mensagens que pode usar os planos de discagem secundário, mas pode não funcionar corretamente em determinadas situações. É importante compreender como cada um desses recursos é afetado quando você configurar usuários habilitados para usar um plano de discagem secundário.

## Tocar no Telefone

Em Outlook Web App, tocar no telefone usa o gateway de VoIP que está associado ao plano de discagem principal do usuário para fazer a chamada de saída. Ele aplica regras de discagem do plano de discagem principal e a diretiva de caixa de correio de Unificação de mensagens que está associado a caixa de correio do usuário.

## Pesquisa de diretório (Outlook Voice Access)

Uma pesquisa do diretório de um usuário que foi autenticado seguirá estas regras:

  - A capacidade de pesquisar por um usuário e deixar uma mensagem de voz ou ligue para um usuário estará disponível somente se o usuário realizando a pesquisa é UM habilitada e tem uma extensão primária no mesmo plano de discagem do usuário que está sendo chamado. Nesse caso, uma pesquisa por nome, o alias e o ramal principal serão localizar o usuário. No entanto, a pesquisa usando a extensão secundária não localizar o usuário.

  - Se o usuário que está sendo procurado for UM habilitada e tem uma extensão secundária no plano de discagem chamado, e depois que uma pesquisa pelo nome, o alias e a extensão secundário encontrará o usuário. No entanto, embora receberá opções para deixar uma mensagem de voz e chamá-lo, a opção de visita de chamada não bem-sucedidas. Nesse caso, uma pesquisa com a extensão principal não localizar o usuário.

  - Para localizar e ser capaz de chamada ou deixar uma mensagem de voz para o usuário está procurando, o usuário habilitado deve usar Outlook Voice Access por meio do número do Outlook Voice Access e pesquisar por nome, o alias ou o ramal principal de seu plano de discagem principal. Se o usuário pesquisada para for chamado usando o número do Outlook Voice Access do plano de discagem secundário, o usuário só será localizado se a pesquisa é feita pelo nome, alias ou extensão secundário. Se o ramal principal for usado, a única opção estará disponível se é para o usuário deixar uma caixa postal.

## Pesquisa de diretório (Outlook Voice Access)

Uma pesquisa do diretório de um usuário que não foi autenticado seguirá estas regras:

  - O usuário que está sendo procurado será encontrado e a opção de deixar uma mensagem de voz ou uma chamada, que o usuário será oferecido apenas se o usuário é UM habilitada e tem uma extensão principal no plano de discagem chamado. Nesse caso, uma pesquisa por nome, o alias e o ramal principal encontrará o usuário. No entanto, uma pesquisa com a extensão secundário não localizar o usuário.

  - Se o usuário que está sendo procurado for habilitada de Unificação de mensagens, tem uma extensão secundária no plano de discagem chamado e a opção de **transferência e pesquisa** \> **Permitir que chamadores** \> **deixar mensagens de voz, sem precisar ligar o telefone de um usuário** for selecionado no plano de discagem chamado, uma pesquisa por nome, o alias e a extensão secundário encontrará-los. No entanto, a opção de deixar a caixa postal será oferecida ao chamador, e não haverá nenhuma opção para telefonar para ele.

  - Para localizar e ser capaz de chamada ou deixar uma mensagem de voz para um usuário, o chamador deve chamar o número do Outlook Voice Access do plano de discagem principal do usuário e pesquisa pelo nome, alias ou o ramal do usuário secundário. Se o número do usuário secundário Outlook Voice Access for chamado, eles só serão localizados se a opção de **Permitir que os chamadores para pesquisar por nome do alias** é definida como **em toda a organização**. Nesse caso, apenas a opção deixar uma mensagem de voz será fornecida.

## Ligar para o remetente (Outlook Voice Access)

Quando um usuário chama Outlook Voice Access e escolhe a opção de chamar o remetente, eles podem enviar uma mensagem de email ou uma mensagem de voz a um usuário habilitado para UM. As opções disponíveis dependem se o chamador está associado com o mesmo plano de discagem como o remetente eles estiver chamando. Chamadas para um usuário habilitado para Unificação de mensagens quando o chamador disca para um número do Outlook Voice Access e o chamador é autenticado seguirá estas regras:

  - **Mensagens de email**   Se o remetente da mensagem de email é um usuário habilitado para Unificação de mensagens, escolhendo a opção de chamar o remetente resultará em uma chamada para o ramal de principal do remetente que está configurado no plano de discagem principal do usuário. No caso onde o ramal de principal do remetente é em um plano de discagem que seja diferente do que o chamador, o aviso para "Chamar o remetente" receberá apenas se houver comercial, residencial, ou celular configurado para o emissor e as regras de discagem são configuradas para permitir que a chamada.

  - **Mensagens de caixa postal**   Se o chamador é um usuário habilitado, a opção de chamar o remetente sempre resultará em uma chamada para a extensão que o remetente usa para deixar sua mensagem de voz. Se essa extensão tem um número de dígitos diferentes de chamada plano de discagem, o prompt para chamar o remetente não fornecido, a menos que existem em regras de discagem in-loco que permita a chamada. Por exemplo:
    
      - A opção \&quot;Ligar para o remetente\&quot; será oferecida se o remetente usa um remal no plano de discagem usado para enviar a mensagem de voz.
    
      - A opção "O remetente chamada" será reproduzida se o remetente usa uma extensão de um plano de discagem diferentes que o plano de discagem que é usado com Outlook Voice Access para enviar a mensagem de voz e ambos os planos de discagem tenham o mesmo número de dígitos. O sucesso da chamada dependerá se a infra-estrutura de PBX e o gateway VoIP permitem a transferência de chamada.
    
      - A opção \&quot;Ligar para o remetente\&quot; não será tocada se o remetente usa um ramal de um plano de discagem diferente do plano de discagem usado com o Outlook Voice Access para enviar a mensagem de voz, os planos de discagem tem um número de digitos diferente e não há regras de discagem de saída que corresponda ao ramal do remetente.

Voltar ao início

