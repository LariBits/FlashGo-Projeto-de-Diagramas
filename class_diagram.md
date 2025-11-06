classDiagram
    direction LR

    %% Configuração de Estilo (Opcional, mas ajuda na leitura)
    %% Note: mermaid-live-editor usually handles layout, but explicit grouping helps mental model.

    %% Classes de Usuário e Autenticação
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
        +identificarProximoCliente(corridaId)
    }

    %% Classes de Serviço e Transporte
    class Corrida {
        +String idCorrida
        +String origem
        +String destino
        +TipoVeiculo tipoVeiculo  << Enum: Carro, Moto >>
        +String status (Em andamento, Finalizada, Cancelada)
        +Float valorTotal
        +Date horaSolicitacao
        +calcularPreco()
        +finalizar()
    }
    
    class Veiculo {
        +String placa
        +String modelo
        +String cor
        +TipoVeiculo tipo << Enum: Carro, Moto >>
    }

    %% Classes de Feedback e Financeiro
    class Pagamento {
        +String idPagamento
        +MetodoPagamento metodo << Enum: Crédito, Débito, Pix, Dinheiro >>
        +Float valor
        +String statusTransacao (Aprovado, Negado, Pendente)
        +processarPagamento()
    }
    
    class Avaliacao {
        +String idAvaliacao
        +Integer nota (1..5)
        +String comentario
        +registrarAvaliacao()
    }

    %% RELACIONAMENTOS (Formatação UML com Cardinalidade)
    
    %% Herança
    Usuario <|-- Cliente
    Usuario <|-- Motorista
    
    %% Associações Principais (Cliente, Motorista, Corrida)
    Cliente "1" -- "0..*" Corrida : solicita
    Motorista "1" -- "0..*" Corrida : realiza
    
    %% Composição/Agregação (Veículo, Corrida, Pagamento, Avaliação)
    Veiculo "1" -- "0..1" Corrida : usado em
    Motorista "1" -- "1" Veiculo : dirige
    
    Corrida "1" -- "0..1" Avaliacao : resulta em
    Corrida "1" -- "1" Pagamento : inclui
    
    %% Notas e Características
    note for Veiculo "Inclui carros e motocicletas."
    note for Pagamento "Método: Cartão de Crédito, Débito, Pix, ou Dinheiro. Status: Controla aprovação/negação."