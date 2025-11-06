---
config:
  layout: elk
---
stateDiagram direction LR
  [*] --> Fazerlogin
  [*] --> Criarconta
  Criarconta --> Cliente: Cliente/Usuário
  Criarconta --> Motorista: Motorista/Usuário
  Fazerlogin --> Conta
  Conta --> Cliente
  Conta --> Motorista
  Motorista --> IniciarServiço
  Cliente --> SolicitarServiço
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
  Negado --> SolicitarServiço: Tentar outro pagamento
  Aprovado --> EsperandoMotorista
  EsperandoMotorista --> ClienteEmEspera: Notificação ao Cliente
  IniciarServiço --> ClienteEmEspera: Motorista pronto
  ClienteEmEspera --> CorridaEmAndamento
  CorridaEmAndamento --> FinalizarCorrida
  FinalizarCorrida --> Cliente: Fim da Viagem
  Cliente --> AvaliaoDaCorrida
  AvaliaoDaCorrida --> [*]
