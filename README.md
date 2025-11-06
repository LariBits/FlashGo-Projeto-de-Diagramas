---
config:
  layout: elk
---
stateDiagram
  direction LR
  [*] --> Fazerlogin
  [*] --> Criarconta
  Criarconta --> Usuario
  Criarconta --> Motorista
  Fazerlogin --> Conta
  Conta --> Usuario
  Conta --> Motorista
  Motorista --> IniciarServiço
  Usuario --> SolicitarServiço
  SolicitarServiço --> Pagamento
  Pagamento --> Credito
  Pagamento --> Debito
  Pagamento --> Dinheiro
  Pagamento --> Pix
  Pix --> Negado
  Debito --> Negado
  Credito --> Negado
  Dinheiro --> Negado
  Pix --> Aprovado
  Dinheiro --> Aprovado
  Credito --> Aprovado
  Debito --> Aprovado
  Negado --> SolicitarServiço
  Aprovado --> EsperandoMotorista
  EsperandoMotorista --> ClienteEmEspera
  IniciarServiço --> ClienteEmEspera
  ClienteEmEspera --> CorridaEmAndamento
  CorridaEmAndamento --> FinalizarCorrida
  FinalizarCorrida --> Usuario
  Usuario --> AvaliaoDaCorrida