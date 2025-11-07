```mermaid
classDiagram
    direction LR

    class Usuario {
        +String idUsuario
        +String nome
        +String email
        -String senhaHash
        +String status
        +criarConta()
    }

    class Cliente {
        +String formaPagamentoPreferida
        +solicitarCorrida(origem, destino, tipoVeiculo)
        +avaliarMotorista(corridaId, nota)
    }
    
    class Motorista {
        +String cnh
        +String statusDisponibilidade
        +Float scoreAvaliacao
        +aceitarCorrida(corridaId)
        +iniciarGPS(destino)
        +identificarProximoCliente()
    }

    class Corrida {
        +String idCorrida
        +String origem
        +String destino
        +TipoVeiculo tipoVeiculo
        +String status
        +Float valorTotal
        +Date horaSolicitacao
        +calcularPreco()
        +finalizar()
    }

    class Veiculo {
        +String placa
        +String modelo
        +String cor
        +TipoVeiculo tipo
    }

    class Pagamento {
        +String idPagamento
        +MetodoPagamento metodo
        +Float valor
        +String statusTransacao
        +processarPagamento()
    }
    
    class Avaliacao {
        +String idAvaliacao
        +Integer nota
        +String comentario
        +registrarAvaliacao()
    }

    Usuario <|-- Cliente
    Usuario <|-- Motorista
    
    Cliente "1" -- "0..*" Corrida : solicita
    Motorista "1" -- "0..*" Corrida : realiza

    Motorista "1" -- "1" Veiculo : dirige
    Veiculo "1" -- "0..1" Corrida : utilizado em

    Corrida "1" -- "1" Pagamento : inclui
    Corrida "1" -- "0..1" Avaliacao : gera
