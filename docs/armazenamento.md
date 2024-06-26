# Armazenamento

## Instance stores

- Fornece armazenamento temporário em nível de bloco para uma instância do *Amazon EC2*.
- É um armazenamento em disco fisicamente conectado ao computador host para uma instância do *EC2*.
- Tem a mesma vida útil da instância.
    - Quando a instância é encerrada, você perde todos os dados armazenados.

## Amazon Elastic Block Store (Amazon EBS)

- Fornece volumes de armazenamento em nível de bloco para uma instância do *Amazon EC2*.
- HDD ou SSD
- Vida útil não depende da instância.
    - Se você interromper ou encerrar uma instância do *Amazon EC2*, todos os dados no volume do *EBS* anexado **permanecerão** disponíveis.
- Para criar um volume do *EBS*, você define a configuração (como tamanho e tipo de volume) e a provisiona.
    - Depois de criar um volume do *EBS*, ele pode ser anexado a uma instância do *Amazon EC2*.
- Criado em uma **única available zone**.
    - A instância do *Amazon EC2* deve estar na mesma **available zone**.

### Amazon EBS volumes

- Fornece os tipos de volume:
    - **Unidades de estado sólido (SSD)**: otimizadas para workloads de transação envolvendo **operações de leitura/gravação frequentes** com o tamanho pequeno de E/S, onde o atributo dominante de performance é IOPS. Os tipos de volume com suporte de SSD incluem:
        - Volumes SSD de uso geral.
            - Equilibram preço e performance para proporcionar uma ampla variedade de workloads transacionais.
        - Volumes de Provisioned IOPS SSD.
            - Volumes de armazenamento da mais alta performance, criados para workloads essenciais, com uso intenso de IOPS e de throughput que exigem baixa latência.
    - **Unidades de disco rígido (HDD)**: otimizadas para grandes workloads de transmissão em que o atributo de performance dominante é a **throughput**. Os tipos de volume com suporte de HDD incluem:
        - Volumes de HDD otimizado para throughput.
            - Um HDD de baixo custo criado para workloads acessadas com frequência e com alta throughput.
        - HDD frio com throughput.
            - O design de HDD de menor custo para workloads acessadas com menos frequência.
    - **Geração anterior**: unidades de disco rígido que você pode usar para workloads com pequenos conjuntos de dados em que os dados são **acessados raramente** e a performance não é de primordial importância.

- [Veja mais sobre os tipos de volumes](https://aws.amazon.com/pt/ebs/volume-types/)

### Amazon EBS snapshots

- Como os volumes do *EBS* são para dados que precisam persistir, é importante fazer backup dos dados.
- Você pode fazer backups incrementais de volumes do *EBS* criando snapshots do *Amazon EBS*.
- Um *snapshots* do EBS é um backup incremental. Isso significa que o primeiro backup feito de um volume copia todos os dados. Para backups subsequentes, apenas os blocos de dados que foram alterados desde o *snapshots* mais recente são salvos.
- Durante o processo de *snapshot* o volume EBS pode ser usando normalmente.

## Amazon Simple Storage Service (Amazon S3)

- Armazena dados como **objetos** em *buckets*.
- Aceita upload de qualquer tipo de arquivo.
- Oferece espaço de armazenamento ilimitado.
- Global, não é definida por região.
- O tamanho máximo de arquivo para um objeto no Amazon S3 é **5 TB**.
- Para cada arquivo é possível definir permissões para controlar a visibilidade e o acesso a ele.
- Possui recurso de versão para rastrear alterações em seus objetos ao longo do tempo.
- Você paga apenas pelo que usa.

### Otimizar a performance do Amazon S3

- O Amazon S3 **escala automaticamente** para taxas de solicitações elevadas.
    - Sua aplicação pode atingir pelo menos **3,5 mil** solicitações PUT/COPY/POST/DELETE ou **5,5 mil** solicitações GET/HEAD por segundo **por prefixo particionado**.
    - Você pode melhorar a performance de leitura ou gravação usando paralelização por prefixos.
        - Por exemplo, se você criar 10 prefixos em um bucket do Amazon S3 para paralelizar leituras, poderá escalar a performance de leitura para 55.000 solicitações de leitura por segundo.
            - Da mesma forma, você pode dimensionar as operações de gravação gravando em vários prefixos.

### Organizar objetos usando prefixos

- Um prefixo é uma string no início do nome da chave do objeto.
- Forma de organizar seus dados de forma semelhante aos diretórios (mas não é diretório)
- Não há limite para o número de prefixos em um bucket.
- É possível definir qual será o delimitador dos prefixos, mas o mais comum é "/", exemplos:
    - `photos/2006/January/sample.jpg`
    - `photos/2006/February/sample3.jpg`

### Amazon S3 storage classes

- Ao selecionar uma classe de armazenamento do Amazon S3, considere estes dois fatores:
    - Com que frequência você planeja recuperar seus dados
    - Quão disponíveis você precisa que seus dados estejam

#### S3 Standard

- Armazenamento de uso geral para dados acessados com frequência.
- Armazena dados em no mínimo **três available zones** de disponibilidade.
- Oferece alta disponibilidade para objetos.
    - Usado para sites, distribuição de conteúdo e análise de dados.
- Custo mais alto.
- Não há cobrança mínima de tempo.
- Não há cobrança por GB recuperado.
- 99,999999999% de durabilidade e 99,99% de disponibilidade.

#### Reduced Redundancy Storage (RRS)

- Redundância reduzida: foi criada para dados reproduzíveis não críticos que podem ser armazenados em níveis de redundância menores do que a classe S3 Standard.
- 99,99% de durabilidade e 99,99% de disponibilidade.
- **Não mais recomendada, AWS indica a Standard pelo custo benefício**

#### S3 Standard-Infrequent Access (S3 Standard-IA)

- Dados acessados com pouca frequência que precisam de acesso em milissegundos.
- Semelhante ao S3 Standard, mas tem um preço de armazenamento mais baixo e um preço de recuperação mais alto.
- Ideal para dados acessados ​​com pouca frequência, mas requer alta disponibilidade quando necessário.
- Armazena dados em no mínimo **três available zones** de disponibilidade.
- Custo 40% menor em relação ao *S3 Standard*
- Cobrança mínima de 30 dias.
- Há cobrança por GB recuperado.

#### S3 One Zone-Infrequent Access (S3 One Zone-IA)

- Dados recriáveis acessados com pouca frequência.
- Armazena dados em uma **única available zone** de disponibilidade.
- Tem um preço de armazenamento menor que o *S3 Standard-IA*.
- Ideal para economizar custos de armazenamento, mas os dados podem ser recuperados em caso de falha.
- Custo 20% menor em relação ao *S3 Standard-Infrequent Access*
- Cobrança mínima de 30 dias.
- Há cobrança por GB recuperado.

#### S3 Express One Zone

- Armazenamento de alta performance para seus dados acessados com mais frequência.
- Armazena dados em uma **única available zone** de disponibilidade.
- Latência de solicitação consistente de um dígito em milissegundos.
- Otimizado para grandes conjuntos de dados com muitos objetos pequenos.
- Custo 50% menor em relação ao *S3 Standard*
- Cobrança mínima de 1h.
- Não há cobrança por GB recuperado.

#### S3 Intelligent-Tiering

- Economia automática de custos para dados com padrões de acesso desconhecidos ou variáveis.
- Requer uma pequena taxa mensal de monitoramento e automação por objeto.
- Os padrões de acesso dos objetos são monitorados.
    - Se o objeto não tiver acesso por **30 dias consecutivos**, será movido para *S3 Standard-IA*.
    - Se o objeto não tiver acesso por **90 dias consecutivos**, será movido para *Archive Instant Access*.
    - Se o objeto que estava em *S3 Standard-IA* for acessado, será movido para *S3 Standard*.
- Objetos menores que **128 KB** podem ser armazenados na *S3 Intelligent-Tiering*, mas sempre serão cobrados pelas taxas de camadas de acesso frequente, sem cobrança de monitoramento e automação.
- A movimentação de objetos entre as classes entra na cobrança de transferências de objetos.
- Não há cobrança mínima de tempo.
- Não há cobrança por GB recuperado.

#### S3 Glacier Instant Retrieval

- Dados de longa duração que são acessados algumas vezes por ano com recuperações instantâneas e baixo custo.
- Recupera objetos em milissegundos com a mesma performance do *S3 Standard*.
- Custo 68% menor em relação ao *S3 Standard-Infrequent Access*
- Cobrança mínima de 90 dias.
- Há cobrança por GB recuperado.

#### S3 Glacier Flexible Retrieval

- Backup e arquivamento de dados que raramente são acessados e baixo custo.
- Dados de arquivo que são acessados 1 a 2 vezes por ano.
- Recupera objetos dentro de alguns **minutos a horas**.
- Custo 10% menor em relação ao *S3 Glacier Instant Retrieval*
- Cobrança mínima de 90 dias.
- Há cobrança por GB recuperado.

#### S3 Glacier Deep Archive

- Arquivamento de dados que são raramente acessados e custo **muito** baixo.
- Recupera objetos dentro de **12 horas**.
- Cobrança mínima de 180 dias.
- Há cobrança por GB recuperado.

#### S3 Outposts

- Oferece armazenamento de objetos para seu ambiente de AWS Outposts on-premises.

### S3 Transfer Acceleration

- É um recurso em nível de bucket que possibilita transferências de arquivos rápidas, fáceis e seguras em longas distâncias entre o seu cliente e um bucket do S3.
- Foi projetado para otimizar as velocidades de transferência de todo o mundo para buckets do S3.
- O Transfer Acceleration tira proveito dos pontos de presença distribuídos globalmente no Amazon CloudFront.
    - Conforme os dados chegam em um ponto de presença, eles são roteados para o Amazon S3 por um **caminho de rede otimizado**.
- Você pode usar o Transfer Acceleration em um bucket por vários motivos:
    - Seus clientes fazem upload em um bucket centralizado do mundo todo.
    - Você transfere gigabytes a terabytes de dados regularmente entre continentes.
    - Não é possível utilizar toda a largura de banda disponível via Internet ao fazer upload para o Amazon S3.
- Veja o que é necessário ao usar o Transfer Acceleration em um bucket do S3:
    - O nome do bucket usado para o Transfer Acceleration deve ser compatível com DNS e não deve conter pontos (".").
    - O Transfer Acceleration deve estar ativado no bucket.

### Transferência de dados

Você paga por toda a largura de banda para dentro e para fora do Amazon S3, **exceto** pelo seguinte:

    - Dados transferidos para a Internet nos primeiros 100 GB por mês, agregados em todos os produtos e regiões da AWS.
    - Dados transferidos da Internet.
    - Dados transferidos entre buckets do S3 na mesma região da AWS. 
    - Dados transferidos de um bucket do Amazon S3 para qualquer serviço da AWS dentro da mesma região AWS que o bucket do S3 (incluindo para uma conta diferente na mesma região da AWS).
    - Dados transferidos para fora para o Amazon CloudFront (CloudFront).

## Amazon Elastic File System (Amazon EFS)

- Armazenas dados como **arquivos**.
- É um sistema de arquivos escalável, **serverless**, usado com serviços da Nuvem AWS e recursos locais.
- Ideal para casos de uso em que um grande número de serviços e recursos precisam acessar os mesmos dados ao mesmo tempo.
- À medida que você adiciona e remove arquivos, o *Amazon EFS* cresce e diminui automaticamente.
- Pode ser dimensionado sob demanda para **petabytes** sem interromper os aplicativos.
- Armazenado em várias **available zones** da região.
- Servidores locais podem acessar o *Amazon EFS* usando o AWS *Direct Connect*.

### Amazon EFS x Amazon EBS

- O EFS pode ser usado quando você precisar de uma opção de armazenamento de arquivos compartilhados para várias **instâncias do EC2** com **dimensionamento automático de alto desempenho**. Isso o torna um ótimo candidato para armazenamento de arquivos para sistemas de gerenciamento de conteúdo; para operações de elevação e deslocamento, pois seu potencial de escalonamento automático significa que você não precisa rearquitetar; para o desenvolvimento de aplicativos, pois o armazenamento de arquivos compartilháveis do EFS é ideal para armazenar códigos e arquivos de mídia.

## AWS Storage Gateway

O AWS Storage Gateway é um conjunto de serviços de armazenamento na nuvem híbrida que oferece acesso on-premises a armazenamento virtual na nuvem praticamente ilimitado.

![Diagrama - Fonte: https://aws.amazon.com/pt/storagegateway](assets/storage-gateway-diagram.png)

## Referências

- <https://explore.skillbuilder.aws/learn/course/134/play/31418/aws-cloud-practitioner-essentials-all-modules>