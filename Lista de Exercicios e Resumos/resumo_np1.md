Este resumo abrange os principais tópicos de Endereçamento de Rede, Fundamentos, Camada de Aplicação e Camada de Transporte, bem como conceitos de Roteamento, conforme detalhado nas fontes fornecidas.

---

## Resumo para a Primeira Prova de Redes de Dados

### 1. Endereçamento de Rede (Físico e Lógico)

#### Sistemas de Numeração
O endereçamento de rede utiliza o **Sistema de Numeração Binário** (Ex: $10110_2 = 22$) e o **Sistema de Numeração Hexadecimal** (Ex: 2001:0DB8:...). A **Função lógica "AND"** é fundamental no cálculo de endereços de rede (1 AND X = X; 0 AND X = 0).

#### Endereçamento Físico (Camada 2)
O Endereço Físico é também conhecido como endereço **MAC**, endereço de enlace, ou endereço de LAN.
*   É fixo e associado ao adaptador de rede (interface física), **independente da rede** em que se encontra.
*   É constituído por **48 bits**, representados no formato hexadecimal (12 dígitos).
*   É dividido em 24 bits para o **OUI** (Organizationally Unique Identifier) e 24 bits para o serial.

#### Endereçamento Lógico (Camada 3)
O endereço lógico, ou **endereço IP**, é atribuído pelo administrador da rede.

1.  **IPv4 (IP versão 4):**
    *   Constituído por **32 bits**.
    *   Representado no formato **decimal com ponto** (Ex: 192.168.15.180).
    *   É formado por duas partes: **Identificação da rede (Net-Id)** e **Identificação do host (Host-Id)**, sendo um endereçamento hierárquico.
2.  **IPv6 (IP versão 6):**
    *   Constituído por **128 bits**.
    *   Representado no formato **hexadecimal** (Ex: fe80::c23d:d9ff:fe76:5f70).

#### Máscara de Rede IPv4
*   Também é formada por 32 bits, representada em decimal com ponto ou formato barra (/n).
*   Permite identificar os campos Net-Id (bits 'um') e Host-Id (bits 'zero') no endereço IPv4.
*   Exemplo: **/24** equivale a **255.255.255.0**.

#### Endereços Especiais
Os endereços de rede e de *broadcast* **não podem ser atribuídos a dispositivos**.
*   **Endereço de Rede:** Identifica o bloco de endereços, com o campo **host\_id formado por bits 0**. O endereço de rede é obtido pela operação lógica AND entre o endereço IP e a Máscara de rede.
*   **Endereço de Broadcast:** Permite o envio de pacotes para todos os hosts da rede, com o campo **host\_id formado por bits 1**.

#### Endereços IP Privados e Públicos
*   **Endereços Públicos:** Endereços globais e padronizados, utilizados na Internet, sendo exclusivos.
*   **Endereços Privados:** Reservados (RFC 1918) para uso interno e privado. **Não podem ser roteados pela Internet** e exigem NAT (*Network Address Translation*) para conexão externa.
    *   Faixas privadas reservadas: **10.0.0.0/8**, **172.16.0.0 a 172.31.255.255 /12**, e **192.168.0.0 a 192.168.255.255 /16**.

#### Endereçamento Estático e Dinâmico
*   **Estático:** Endereços IP atribuídos manualmente pelo administrador (recomendado para dispositivos que precisam ser "vistos" global ou localmente, como servidores).
*   **Dinâmico:** Endereços IP atribuídos automaticamente por servidores de configuração, como o **DHCP** (*Dynamic Host Configuration Protocol*).

#### Sub-redes e VLSM
*   **Cálculo de Sub-redes IPv4:** Permite dividir blocos de endereços em segmentos menores, tomando bits do campo Host-Id e designando-os para o campo Net-Id da sub-rede. Para hosts válidos, é necessário deixar pelo menos **2 bits** para o campo Host\_id.
*   **VLSM** (*Variable Length Subnet Mask*): Permite o uso de **diferentes máscaras de sub-rede** dentro do mesmo bloco de endereços, aumentando a eficiência na distribuição e economizando endereços IP.

---

### 2. Fundamentos de Redes e Modelos

#### Modelo OSI (*Open System Interconnection*)
Lançado em 1984 pela ISO, é um modelo de referência de 7 camadas que define funcionalidades agrupadas, garantindo compatibilidade e interoperabilidade.

| Camada | Funcionalidade Principal |
| :--- | :--- |
| **Aplicação** | Serviços de rede para as aplicações. |
| **Apresentação** | Formatação e sintaxe dos dados, criptografia e compressão. |
| **Sessão** | Gerência de diálogos entre aplicativos. |
| **Transporte** | Gerência de conexões **fim-a-fim** (confiabilidade, controle de fluxo, circuitos virtuais). |
| **Rede** | Conectividade e seleção de caminhos (**roteamento**), endereçamento lógico. Protocolo **IP** atua aqui. |
| **Enlace** | Controle de erros ponto a ponto, controle de acesso ao meio, **endereço físico** (MAC). Switches operam predominantemente aqui. |
| **Física** | Interfaces, sinalização, meios de transmissão, **transmissão de bits**. |

#### Pilha TCP/IP
Tornou-se o padrão da Internet, padronizado em 1981.
*   A **Camada de Internet** é equivalente à Camada de Rede do OSI.
*   A **Camada de Transporte** é responsável por iniciar, manter e encerrar conexões lógicas entre aplicações.
*   A **Camada de Aplicação** corresponde às camadas de Aplicação, Apresentação e Sessão do OSI.
*   A **Camada de Acesso à Rede** é equivalente às camadas Física e Enlace do OSI.

#### Comunicação entre Processos
A comunicação ocorre entre processos de aplicações que trocam mensagens por meio de uma interface de software chamada **socket**. O socket é a interface entre as camadas de aplicação e transporte.
*   Para identificar o processo receptor, são necessários o **endereço IP do hospedeiro** e um **identificador de porta** (número de porta).
*   **Identificadores de Portas (16 bits):**
    *   **Portas Bem Conhecidas (0 a 1023):** Reservadas para serviços e aplicações.
    *   Portas Registradas (1024 a 49151).
    *   Portas Dinâmicas ou Privadas (49152 a 65535): Atribuídas dinamicamente pelo SO do cliente.

---

### 3. Camada de Aplicação (DNS e HTTP)

#### DNS (*Domain Name System*)
*   Função principal: **Traduzir nomes de domínio em endereços IP**.
*   Utiliza o protocolo **UDP na porta 53**.
*   É implementado como um banco de dados distribuído em uma hierarquia de servidores (Raiz, TLD, Autoritativos).

#### HTTP (*HyperText Transfer Protocol*)
*   Protocolo padrão para comunicação Web, que define como as páginas são requisitadas e enviadas.
*   Utiliza o **TCP como protocolo de transporte**.
*   Trabalha no modo **cliente/servidor**.
*   **Conexões não persistentes (HTTP/1.0):** Cada par de requisição/resposta é enviado por uma conexão TCP distinta, e no máximo um objeto é enviado por conexão.
*   **Conexões persistentes (HTTP/1.1 e HTTP/2):** Múltiplos objetos são enviados por uma mesma conexão TCP.
*   **Porta Padrão:** **TCP 80**.
*   **HTTPS** (*HyperText Transfer Protocol Secure*) é a versão segura, que usa **autenticação e criptografia** (via TLS/SSL) para proteger os dados. Usa a **porta 443 do TCP**.

---

### 4. Camada de Transporte (TCP e UDP)

A camada de Transporte fornece comunicação lógica entre processos de aplicações (fim-a-fim). A identificação de serviços nessa camada é feita pelo **Número da Porta**.

| Característica | TCP (*Transmission Control Protocol*) | UDP (*User Datagram Protocol*) |
| :--- | :--- | :--- |
| **Orientação à Conexão** | **Orientado à conexão**. Requer *3-way handshake* (troca de informações de controle) antes do fluxo de dados. | **Não orientado à conexão**. Nenhuma troca de informações ocorre antes da comunicação. |
| **Confiabilidade** | **Confiável**. Garante entrega dos dados sem erro e na ordem correta. | **Não confiável**. Não oferece garantias de entrega; mensagens podem chegar fora de ordem ou serem perdidas. |
| **Controle de Fluxo** | Inclui mecanismo de controle de fluxo (*sliding-window protocol*). | Não inclui. |
| **Controle de Congestionamento**| Inclui mecanismo para limitar a taxa de transmissão quando a rede está congestionada. | Não inclui. |
| **Overhead** | Maior *overhead* (mais complexo). | Baixo *overhead* (simplificado, cabeçalho de 8 bytes). |
| **Uso Comum** | Serviços Web (HTTP), Transferência de arquivos. | Aplicações em tempo real (VoIP), DNS. |

---

### 5. Roteamento IP

#### Conceitos de Roteamento
*   **Rota:** Caminho que guia um pacote IP até a rede destino.
*   **Protocolos Roteados:** Fornecem informações para a função de roteamento (Ex: IP).
*   **Protocolos de Roteamento:** Usados para a troca de informações entre roteadores sobre rotas/redes conhecidas (Ex: OSPF, RIP, BGP).

#### Tipos de Rotas
1.  **Rotas Diretas:** Encontradas pelo protocolo de enlace, identificam redes conectadas diretamente ao roteador.
2.  **Rotas Estáticas:** Configuradas **manualmente** pelo administrador. Possuem prioridade sobre o roteamento dinâmico.
3.  **Rotas Dinâmicas:** Descobertas e mantidas através de protocolos de roteamento (Ex: OSPF).

#### Classificação dos Protocolos de Roteamento
*   **IGP (*Interior Gateway Protocol*):** Usados para troca de anúncios **dentro de um mesmo Sistema Autônomo (AS)**. Exemplos: RIP, OSPF, EIGRP.
*   **EGP (*Exterior Gateway Protocol*):** Usados para troca de anúncios **entre dois ASs**. Exemplo: BGP.

#### Protocolos de Roteamento (Operação)
1.  **Vetor de Distância:**
    *   Rotas anunciadas com Distância (custo) e Vetor (direção/próximo salto).
    *   Anúncios ocorrem **periodicamente**.
    *   Os roteadores anunciam apenas para seus vizinhos (não possuem visão de toda a topologia).
    *   Exemplo: **RIPv2** (Classless, utiliza o algoritmo Bellman-Ford, custo baseado em número de saltos, encapsulado em UDP porta 520).
2.  **Estado de Enlace (*Link State*):**
    *   Cada roteador descobre vizinhos (*Hello*), monta pacotes LSP (*link-state packet*) e os envia aos demais roteadores (visão topológica da rede).
    *   Utiliza o **algoritmo SPF** (*Shortest Path First* / Dijkstra) para calcular a árvore de caminho mais curto.
    *   Anúncios ocorrem na inicialização e somente quando há alteração na topologia (não periodicamente).
    *   Exemplo: **OSPF** (*Open Shortest Path First*) (Classless, rápida convergência, escalável por áreas, custo relacionado à largura de banda).

3.  **Vetor de Caminho (*Path Vector*):**
    *   Usado pelo **BGP** (*Border Gateway Protocol*), que é o protocolo EGP padrão para troca de informações entre ASs.
    *   As atualizações são encapsuladas no **TCP, usando a porta 179**.

#### Configuração de Roteamento Estático (Exemplo)
A sintaxe básica para configurar uma rota estática é:
`Router(config)# ip route [endereço IP da rede destino] [máscara de rede] [próximo salto / interface de saída]`.

---

Com certeza. Adicionarei os detalhes sobre os cálculos de sub-rede e VLSM (Máscaras de Sub-rede de Tamanho Variável) à seção de Endereçamento de Rede do seu resumo, conforme o material fornecido.

---

## Adição ao Resumo: Cálculos de Sub-rede e VLSM

### 1. Endereçamento de Rede (Cálculos de Sub-rede IPv4)

O cálculo de sub-redes permite dividir blocos de endereços em segmentos menores (sub-redes), oferecendo maior flexibilidade na administração.

#### Sub-redes com Máscara de Tamanho Fixo (Sub-redes Convencionais)

Para criar um endereço de sub-rede, são tomados bits do campo **Host\_Id** (a partir do bit mais significativo) e designados para o campo **Net\_Id** da sub-rede.

1.  **Cálculo da Máscara (Bits Emprestados):**
    *   É necessário determinar quantos bits (**s**) do campo Host\_Id precisam ser emprestados para atender ao número de sub-redes desejado: $2^s \ge \text{Número de sub-redes requisitadas}$.
    *   A nova Máscara de rede será calculada como: **Prefix $\text{Novo} = \text{Prefix Original} + s$**.

2.  **Cálculo de Hosts Válidos:**
    *   A quantidade máxima de bits (**h**) que podem ser emprestados é qualquer valor que deixe **pelo menos 2 bits** para o campo Host\_Id.
    *   O número total de endereços em cada sub-rede é $2^h$.
    *   O número de hosts válidos é $2^h - 2$ (o endereço de rede e o endereço de *broadcast* não podem ser atribuídos a dispositivos).

3.  **Determinação da Máscara:**
    *   A máscara de sub-rede é formada por "1" binário nas posições relativas à rede e sub-rede (Net-Id) e "0" nos bits do Host-Id.

| Exemplo de Bits Emprestados (partindo de /24) | Máscara Decimal | Prefixo | Hosts Válidos (2^h - 2) |
| :--- | :--- | :--- | :--- |
| **1 bit** emprestado (s=1) | 255.255.255.128 | /25 | $2^7 - 2 = 126$ hosts |
| **3 bits** emprestados (s=3) | 255.255.255.224 | /27 | $2^5 - 2 = 30$ hosts |
| **6 bits** emprestados (s=6) | 255.255.255.252 | /30 | $2^2 - 2 = 2$ hosts |

***

### 2. VLSM (Variable Length Subnet Mask)

O **VLSM** é a técnica que permite a **utilização de diferentes máscaras de sub-rede** dentro de um mesmo bloco de endereços, aumentando a eficiência na distribuição e economizando endereços IP.

#### Metodologia VLSM (Baseado em Hosts)

Ao contrário do cálculo de sub-redes de tamanho fixo (que se baseia no número de sub-redes), o VLSM baseia-se no **número de endereços de hosts necessários** para cada segmento.

1.  **Prioridade de Alocação:** Para economizar endereços IP ao máximo, deve-se alocar os prefixos (sub-redes) **começando pela necessidade de maior número de hosts**.

2.  **Cálculo da Máscara por Necessidade de Host:** Para cada sub-rede, define-se a máscara adequada para comportar a quantidade de hosts exigida:
    *   Determine o número de bits de host (**h**) tal que: $2^h - 2 \ge \text{Número de hosts requisitados}$.
    *   O prefixo (/n) será $32 - h$.

3.  **Alocação Sequencial:** O próximo endereço de rede disponível é usado para calcular a próxima sub-rede, sempre respeitando a máscara calculada para aquela necessidade específica.

#### Exemplo de Aplicação VLSM

Dada a necessidade de hosts, o administrador define qual máscara usar:

| Necessidade de Hosts (N) | Bits de Host (h) ($2^h \ge N+2$) | Endereços Totais ($2^h$) | Máscara (/n) (32-h) | Endereços Válidos ($2^h - 2$) |
| :--- | :--- | :--- | :--- | :--- |
| **60 hosts** | 6 bits ($2^6=64$) | 64 | **/26** | 62 hosts |
| **28 hosts** | 5 bits ($2^5=32$) | 32 | **/27** | 30 hosts |
| **12 hosts** | 4 bits ($2^4=16$) | 16 | **/28** | 14 hosts |
| **2 hosts** (enlace WAN) | 2 bits ($2^2=4$) | 4 | **/30** | 2 hosts |

**Exemplo de Alocação de Endereços (Bloco inicial 192.168.10.0/24)**:

| Sub-rede | Requisito | Máscara | Endereço de Rede | Endereço de Broadcast |
| :--- | :--- | :--- | :--- | :--- |
| **LAN 1** | 60 hosts | /26 | **192.168.10.0** | 192.168.10.63 |
| **LAN 4** | 28 hosts | /27 | **192.168.10.64** | 192.168.10.95 |
| **LAN 2** | 12 hosts | /28 | **192.168.10.96** | 192.168.10.111 |
| **WAN 1** | 2 hosts | /30 | **192.168.10.128** | 192.168.10.131 |
