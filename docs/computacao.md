# Computação

## Elastic Compute Cloud (Amazon EC2)

- Ambientes de computação virtual, conhecidos como instâncias.
- Disponibiliza modelos pré-configurados para suas instâncias, conhecidos como Imagens de máquina da Amazon (_AMIs - Amazon Machine Image_).

### Tipos de instâncias

Os tipos de instância do Amazon EC2 são otimizados para diferentes tarefas.

- **General purpose**:
    - Instâncias de uso geral que fornecem um equilíbrio de recursos de computação, memória e rede.
    - Você pode usá-los para uma variedade de cargas de trabalho, como:
        - Servidores de aplicativos;
        - Servidores de jogos;
        - Servidores back-end para aplicativos corporativos;
        - Bancos de dados de pequeno e médio porte.
- **Compute optimized**:
    - Instâncias otimizadas para computação são ideais para aplicativos vinculados a computação que se beneficiam de processadores de alto desempenho.
    - Você pode usá-los para uma variedade de cargas de trabalho, como:
        - Servidores Web de alto desempenho;
        - Servidores de aplicativos de computação intensiva;
        - Servidores de jogos dedicados;
        - Computação para cargas de trabalho de processamento em lote;
- **Memory optimized**:
    - Instâncias otimizadas para memória são projetadas para fornecer desempenho rápido para cargas de trabalho que processam grandes conjuntos de dados na memória.
    - Você pode usá-los para uma variedade de cargas de trabalho, como:
        - Processamento em tempo real de uma grande quantidade de dados não estruturados.
- **Accelerated computing**:
    - Instâncias de computação acelerada usam aceleradores de hardware, ou coprocessadores, para executar algumas funções com mais eficiência do que é possível em softwares executados em CPUs.
    - Você pode usá-los para uma variedade de cargas de trabalho, como:
        - Cálculos de números de ponto flutuante;
        - Processamento de gráficos;
        - Correspondência de padrões de dados.
        - Aplicativos gráficos;
        - Streaming de jogos.
- **Storage optimized**:
    - Instâncias otimizadas para armazenamento são projetadas para cargas de trabalho que exigem alto acesso sequencial de leitura e gravação a grandes conjuntos de dados no armazenamento local.
    - Você pode usá-los para uma variedade de cargas de trabalho, como:
        - Sistemas de arquivos distribuídos;
        - Aplicativos de armazenamento de dados;
        - Sistemas de processamento de transações online de alta frequência (OLTP).
        - Aplicativo que tenha um alto requisito de entrada/saída por segundo (IOPS).

### Preços

Você paga apenas pelo tempo de computação usado.

O Amazon EC2 oferece uma variedade de opções de preços para diferentes casos de uso:

- **On-Demand**:
    - As instâncias sob demanda são ideais para cargas de trabalho irregulares de curto prazo que não podem ser interrompidas.
    - Não se aplicam custos iniciais ou contratos mínimos.
    - As instâncias são executadas continuamente até que você as interrompa e você paga apenas pelo tempo de computação usado.
    - As instâncias sob demanda não são recomendadas para cargas de trabalho que duram um ano ou mais, devido o custo.
- **Amazon EC2 Savings Plans**:
    - Possui planos de pacotes de horas por ano.
    - Contratos por um período de **1 ou 3 anos**.
    - Planos:
        - **Compute S.P.**:
            - Produtos: Fargate, Lambda, EC2.
            - Pode alterar região, família, tamanho e SO.
            - Economias de até 66% em relação aos custos _On-Demand_.
        - **EC2 S.P.**:
            - Produtos: EC2.
            - Pode alterar somente tamanho e SO.
            - Economias de até 72% em relação aos custos _On-Demand_.
- **Reserved Instances**:
    - AWS recomenda **EC2 Savings Plans** pelo custo benefício.
    - Desconto de cobrança aplicado ao uso de instâncias _On-Demand_ em sua conta.
    - Contratos por um período de **1 ou 3 anos**.
    - Planos:
        - **Standard Reserved**: pode mudar somente AZ, tamanho e tipo de rede.
        - **Convertible Reserved**: pode mudar de AZ, tamanho, tipo de rede, família de instancia, OS.
        - **Scheduled Reserved**:
            - Lançamento dentro da janela de tempo reservada (fração do dia, semana ou mês).
            - Instâncias reservadas agendadas por um período de 1 ano.
    - Ao final de um período de instância reservada, a instância permanece sem interrupção sendo cobradas taxas _On-Demand_ até que você faça um dos seguintes:
        - Encerre a instância.
        - Compre uma nova instância reservada que corresponda aos atributos da instância (tipo de instância, região, locação e plataforma).
- **Spot Instances**:
    - As instâncias spot são ideais para cargas de trabalho com horários de início e término flexíveis ou que podem suportar interrupções.
    - Usam a capacidade de computação não utilizada do Amazon EC2 e oferecem economia de custos de até 90% dos preços sob _On-Demand_.
    - Se a capacidade do Amazon EC2 estiver indisponível, o lançamento aguardará em segundo plano até a disponibilidade.
    - Numa instância spot em execução, se a capacidade não estiver mais disponível ou a demanda por instâncias spot aumentar, sua instância poderá ser interrompida.
- **Dedicated Instance**:
    - Continua usando uma instancia (VM)
    - Mas o hardware não é compartilhado com outras instâncias.
    - Geralmente usado por instituições que prezam pela máxima segurança de dados.
- **Dedicated Hosts**:
    - Usando **servidores físicos** totalmente dedicados ao seu uso.
    - Você pode usar suas licenças de software existentes por soquete, por núcleo ou por VM para ajudar a manter a conformidade com as licenças.
    - Opção mais cara.

## AWS Lambda

- O termo "_serverless_" significa que seu código é executado em servidores, mas você não precisa provisionar ou gerenciar esses servidores.
- Dimensiona aplicativos sem servidor automaticamente.
- Pague apenas pelo tempo de computação que você consumir.
- Uma instância em execução terá no máximo 15 minutos para executar seu trabalho.
- Um código em um AWS Lambda é executado ao ser acionado por um evento configurado.

## AWS Elastic Beanstalk

- Com o Elastic Beanstalk, é possível implantar e gerenciar rapidamente aplicações na Nuvem AWS sem se preocupar com a infraestrutura que as executa.
- Basta fazer upload da aplicação e o Elastic Beanstalk automaticamente gerencia os detalhes de provisão de capacidade, balanceamento de carga, escalabilidade e monitoramento do status da aplicação.
- Compatível com aplicações desenvolvidas em Go, Java, .NET, Node.js, PHP, Python e Ruby.
- Constrói a versão da plataforma suportada selecionada e provisiona um ou mais recursos da AWS, como instâncias do Amazon EC2, para executar a aplicação.
- Não há custo adicional para o Elastic Beanstalk. Você paga apenas pelos recursos subjacentes da AWS consumidos pela aplicação.

## Placement Groups (Grupo de posicionamento)

- **Cluster**: agrupa as instâncias em uma zona de disponibilidade. Essa estratégia permite que as workloads atinjam a performance de rede de baixa latência necessária para a comunicação de nó a nó totalmente acoplada que é típica das aplicações de computação de alta performance (HPC).
- **Partition**: distribui as instâncias entre partições lógicas, de tal modo que as instâncias em uma partição não compartilhem o hardware subjacente com os grupos de instâncias em outras partições. Essa estratégia é normalmente usada por grandes workloads distribuídas e replicadas, como Hadoop, Cassandra e Kafka.
- **Spread**: posiciona estritamente um pequeno grupo de instâncias no hardware subjacente distinto a fim de reduzir as falhas correlacionadas.

## Referências

- <https://aws.amazon.com/pt/ec2>
