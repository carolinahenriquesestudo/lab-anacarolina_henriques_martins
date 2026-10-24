# Memória de Desenvolvimento — Semana 01
**Aluno:** Ana Carolina Henriques Martins 
**Matrícula:** 202421200048 
**Curso:** Sistemas de Informação

---

## 1. Mapeamento da Camada de Transporte
Diagrama Mermaid demonstrando o ciclo de vida da requisição executada no laboratório:

```mermaid
sequenceDiagram
    autonumber
    participant C as Cliente (Netcat)
    participant S as Servidor (example.com)

    C->>S: TCP SYN
    S-->>C: TCP SYN-ACK
    C->>S: TCP ACK
    C->>S: GET / HTTP/1.1\r\nHost: example.com\r\n\r\n
    S-->>C: HTTP/1.1 200 OK
    S->>C: TCP FIN

---

## 2. Captura Bruta e Análise do Protocolo
* **Comando Utilizado:** `nc -C example.com 80`
* **Status Line Retornada:** `HTTP/1.1 200 OK`

### Análise dos Headers Recebidos:
1. **`Content-Type`: Informa o tipo MIME (text/html) e a codificação (UTF-8), permitindo que o parser interprete e renderize o conteúdo corretamente.
2. **`Content-Length`: Indica o tamanho exato do payload em bytes, sendo essencial para o cliente saber exatamente quantos bytes ler do fluxo TCP.
3. **`Connection: close`: Determina o fechamento imediato do socket após o envio da resposta, economizando recursos em comparação ao modo keep-alive, que mantém a conexão aberta.
---

## 3. Conclusão Técnica
A comunicação web opera por meio de fluxos contínuos de bytes TCP estruturados em texto ASCII e delimitados
por sequências CRLF (\r\n). A prática com sockets demonstra que ferramentas de navegação atuam apenas como 
abstrações visuais para requisições e respostas baseadas em protocolos textuais padronizados.
