```mermaid
stateDiagram-v2
    direction LR

    [*] --> FazerLogin
    [*] --> CriarConta

    CriarConta --> Cliente
    CriarConta --> Motorista

    FazerLogin --> Conta
    Conta --> Cliente
    Conta --> Motorista

    Cliente --> SolicitarServico
    Motorista --> IniciarServico

    SolicitarServico --> Pagamento

    Pagamento --> Credito
    Pagamento --> Debito
    Pagamento --> Dinheiro
    Pagamento --> Pix

    Credito --> Negado
    Debito --> Negado
    Dinheiro --> Negado
    Pix --> Negado

    Credito --> Aprovado
    Debito --> Aprovado
    Dinheiro --> Aprovado
    Pix --> Aprovado

    Negado --> SolicitarServico : tentar outro\nmetodo de pagamento

    Aprovado --> EsperandoMotorista
    EsperandoMotorista --> ClienteEmEspera : notificar cliente
    IniciarServico --> ClienteEmEspera : motorista pronto

    ClienteEmEspera --> CorridaEmAndamento
    CorridaEmAndamento --> FinalizarCorrida
    FinalizarCorrida --> Cliente : fim da viagem

    Cliente --> AvaliacaoDaCorrida
    AvaliacaoDaCorrida --> [*]
