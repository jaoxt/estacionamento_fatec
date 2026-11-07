# Parkly – Requisitos do App de Estacionamento (Protótipo)

Integrantes: Alex Victor Nunes do Nascimento e João Henrique de Oliveira Ribeiro

Registro consolidado em 06/11/2026: requisitos originais, sugestões incorporadas e decisões da equipe.

## Como executar o protótipo

Abra o arquivo `index.html` em qualquer navegador (computador ou celular). Não precisa de instalação nem de internet. Os dados ficam só em memória e somem ao recarregar a página.

Contas de demonstração (senha `123`): `cliente@demo.com`, `func@demo.com`, `admin@demo.com`.
O botão "Avançar 15 min" na coluna lateral adianta o relógio simulado, para testar expiração de reserva e tolerância.

## 1. Requisitos originais enviados

1. Registro das placas dos carros.
2. Identidade do condutor.
3. Quantidade de vagas disponíveis.
4. Registro automático de placa via câmera, com vínculo à vaga numerada.
5. Registro do tempo de locação da vaga no app para os clientes.
6. Registro do tempo de locação da vaga no app para cálculo de custo.
7. Duas interfaces: usuário e funcionário.
8. Reservar vagas de acordo com a placa, antes de chegar ao local.
9. Pagar pelo aplicativo antecipadamente, com 20 minutos de tolerância.
10. O usuário pode visualizar a sua vaga no app.
11. O usuário pode fazer login e criar conta.
12. Relatório diário e mensal para os administradores.
13. Cores do app em tons de vermelho (substituído depois, ver seção 6).

## 2. Decisões da equipe

| Tema | Decisão |
|---|---|
| Cancelamento | O usuário recebe mensagem informando o motivo e a situação do reembolso. |
| Taxa de reserva | 10% do valor. |
| Reembolso da taxa de reserva | Não é reembolsável. |
| Base de cálculo dos 10% | A decidir. No protótipo é configurável pelo admin (1 hora, diária ou tempo estimado). Padrão: 1 hora. |
| Cancela | Simulada, sem hardware físico. |
| Câmeras | Não haverá no começo; apenas registro manual pelo funcionário. |
| Após os 20 min de tolerância | Cobrança do tempo excedente. |
| Quantidade de vagas | 50. |
| Cobrança mínima | 1 hora. |
| Número de locais | Pendente (um ou vários). |

## 3. Requisitos funcionais

### Autenticação e perfis
| ID | Requisito | Situação |
|---|---|---|
| RF01 | Criar conta e fazer login (e-mail/senha). | Mantido |
| RF02 | Duas interfaces: usuário (cliente) e funcionário. | Mantido |
| RF03 | Perfil Administrador com acesso a relatórios e configurações. | Mantido |
| RF04 | Recuperação de senha por e-mail ou SMS. | Mantido (não implementado no protótipo) |
| RF05 | Login social (Google/Apple). | Adiado (fase 2) |

### Condutor e veículo
| ID | Requisito | Situação |
|---|---|---|
| RF06 | Registro das placas dos veículos do cliente. | Mantido |
| RF07 | Registro da identidade do condutor (nome, CPF, documento). | Mantido |
| RF08 | Vários veículos por usuário, com um padrão. | Mantido |
| RF09 | Validação do formato de placa (padrão antigo e Mercosul). | Mantido |
| RF10 | O funcionário registra manualmente entrada e saída de placa, com vínculo à vaga. | Essencial (fluxo principal) |
| RF48 | Na reserva, o cliente escolhe qual placa cadastrada usar. | Novo |

### Vagas e monitoramento
| ID | Requisito | Situação |
|---|---|---|
| RF11 | Exibir a quantidade de vagas disponíveis em tempo real. | Mantido |
| RF12 | Registro automático da placa via câmera (OCR/LPR), vinculado a vaga numerada. | Adiado (fase 2) |
| RF13 | O usuário visualiza no app a vaga do seu carro (número e localização). | Mantido |
| RF14 | Mapa do estacionamento com status das vagas (livre, ocupada, reservada). | Mantido |
| RF15 | Status bloqueada/manutenção, definido pelo funcionário. | Mantido |
| RF16 | Alerta ao funcionário por divergência (ex.: vaga reservada ocupada por outra placa), com base em dados manuais. | Adaptado |
| RF17 | Vagas especiais (PCD, idosos, elétricos, motos). | Mantido |

### Reservas
| ID | Requisito | Situação |
|---|---|---|
| RF18 | Reservar vaga vinculada à placa antes de chegar. | Mantido |
| RF19 | Reserva não utilizada em 20 min é cancelada automaticamente. | Alterado |
| RF20 | O usuário pode cancelar a reserva pelo app. | Mantido |
| RF21 | Notificação de confirmação, lembrete e expiração da reserva. | Mantido |
| RF42 | A reserva gera taxa de 10% sobre a base de cálculo, cobrada no momento da reserva. | Novo |
| RF43 | A taxa de reserva é abatida do valor total quando o usuário usa a vaga. | Novo |

### Tempo, cobrança e pagamento
| ID | Requisito | Situação |
|---|---|---|
| RF22 | Registro de entrada e saída para consulta do cliente. | Mantido |
| RF23 | Registro do tempo de permanência para cálculo do custo. | Mantido |
| RF24 | Pagamento antecipado pelo app, com tolerância de 20 min para sair. | Mantido |
| RF25 | Após a tolerância, cobrança do tempo excedente. | Definido |
| RF26 | O admin configura valor da hora, diária, taxa de reserva (%) e base de cálculo. | Alterado |
| RF27 | Formas de pagamento: Pix, cartão de crédito/débito (simulado no protótipo). | Mantido |
| RF28 | Comprovante/recibo digital. | Mantido |
| RF29 | Histórico de estacionamentos e pagamentos do usuário. | Mantido |
| RF30 | Liberação de saída após pagamento confirmado, simulada. | Alterado |
| RF49 | Cobrança mínima de 1 hora na primeira cobrança da permanência; depois, por fração de 15 min. | Novo |

### Cancelamento e mensagens
| ID | Requisito | Situação |
|---|---|---|
| RF38 | Mensagem de cancelamento (expiração, cancelamento pelo usuário ou funcionário) com o motivo e a situação do reembolso. | Novo |
| RF39 | O usuário cancela pelo app e vê o status do reembolso. | Novo |
| RF40 | Quando houver reembolso, é feito pelo meio de pagamento original. | Novo |
| RF41 | O histórico registra reservas canceladas e reembolsos. | Novo |

### Funcionário
| ID | Requisito | Situação |
|---|---|---|
| RF31 | Painel com veículos no pátio, vagas e reservas. | Mantido |
| RF32 | Busca de veículo por placa. | Mantido |
| RF33 | Registro de ocorrências (pagamento pendente, veículo irregular, divergência de placa). | Mantido (não implementado no protótipo) |
| RF44 | Tela rápida de entrada: placa e vaga numerada (ou vaga reservada sugerida). | Novo |
| RF45 | Tela rápida de saída: tempo, valor e status de pagamento. | Novo |
| RF46 | Validação de placa digitada, com aviso de duplicidade. | Novo |
| RF47 | Registro do funcionário responsável por cada entrada e saída. | Novo |

### Relatórios (administrador)
| ID | Requisito | Situação |
|---|---|---|
| RF34 | Relatório diário. | Mantido |
| RF35 | Relatório mensal. | Mantido |
| RF36 | Conteúdo: faturamento, ocupação, tempo médio de permanência, nº de reservas, no-shows, horários de pico. | Mantido |
| RF37 | Exportação em PDF e CSV/Excel. | Mantido (não implementado no protótipo) |

## 4. Requisitos não funcionais

### Interface e usabilidade
| ID | Requisito | Situação |
|---|---|---|
| RNF01 | Identidade visual em tons de azul e fundo branco, sem emojis (substitui os tons de vermelho). | Alterado |
| RNF02 | Contraste adequado (WCAG AA). | Mantido |
| RNF03 | Status de vaga não depende só de cor: também texto e estilo de borda. | Mantido |
| RNF04 | Interface responsiva e utilizável no celular; fluxos de reserva e pagamento curtos. | Mantido |
| RNF05 | Idioma pt-BR, com preparação para internacionalização. | Mantido |
| RNF26 | Navegação em coluna lateral (no celular, faixa estreita com ícones), com ícones em tons de azul. | Novo |

### Desempenho
| ID | Requisito | Situação |
|---|---|---|
| RNF06 | Disponibilidade de vagas atualizada em até 5 s. | Mantido |
| RNF07 | Reconhecimento de placa em até 3 s, com 95% de acerto. | Adiado (fase 2) |
| RNF08 | Telas principais em até 3 s em rede 4G. | Mantido |
| RNF09 | Suportar N usuários simultâneos (definir N). | Mantido |
| RNF25 | Lançar uma entrada manual em menos de 10 s. | Novo |

### Segurança e privacidade
| ID | Requisito | Situação |
|---|---|---|
| RNF10 | Conformidade com a LGPD. | Mantido |
| RNF11 | Criptografia em trânsito (HTTPS/TLS) e senhas com hash (bcrypt/argon2). | Mantido |
| RNF12 | Pagamentos via gateway certificado (PCI-DSS); o app não guarda dados de cartão. | Mantido |
| RNF13 | Controle de acesso por perfil (usuário, funcionário, admin). | Mantido |
| RNF14 | Retenção de imagens das câmeras. | Adiado (fase 2) |
| RNF15 | Log de auditoria de ações de funcionários e administradores. | Mantido |

### Disponibilidade e confiabilidade
| ID | Requisito | Situação |
|---|---|---|
| RNF16 | Disponibilidade mínima de 99% (meta do protótipo). | Mantido |
| RNF17 | Operação manual como fluxo principal (sem câmeras). | Revisado |
| RNF18 | Backup diário. | Mantido |
| RNF19 | Servidor como fonte única de tempo, para evitar erros de cobrança. | Mantido |

### Compatibilidade e arquitetura
| ID | Requisito | Situação |
|---|---|---|
| RNF20 | Compatível com Android e iOS (ou PWA/multiplataforma no protótipo). | Mantido |
| RNF21 | Interface de integração com cancela (simulada no protótipo) e com gateway de pagamento via API; integração com câmeras na fase 2. | Alterado |
| RNF22 | Arquitetura modular, com API separada do front-end. | Mantido |
| RNF23 | Código versionado e documentado. | Mantido |
| RNF24 | Registro de placa desacoplado da origem (manual ou câmera), para plugar o OCR depois. | Novo |

## 5. Regras de negócio

- **RN01:** Uma placa só pode estar vinculada a uma vaga ativa por vez.
- **RN02:** Uma vaga reservada só pode ser ocupada pela placa da reserva.
- **RN03:** A tolerância de 20 min começa a contar a partir da confirmação do pagamento.
- **RN04:** Reserva não utilizada em 20 min é cancelada, com mensagem ao usuário.
- **RN05:** A taxa de reserva é de 10% e é abatida do valor final se a vaga for usada.
- **RN06:** Todo cancelamento gera mensagem ao usuário e registro, com a situação do reembolso.
- **RN07:** No protótipo, a liberação de saída é apenas simulada.
- **RN08:** A taxa de reserva não é reembolsável (cancelamento ou expiração resultam em reembolso de R$ 0,00).
- **RN09:** Após os 20 min de tolerância, o tempo excedente é cobrado.
- **RN10:** A primeira cobrança da permanência tem valor mínimo equivalente a 1 hora.

## 6. Mudanças pedidas durante o protótipo

1. Correção do seletor de placa na reserva, que não permitia trocar de veículo quando havia mais de uma placa cadastrada.
2. Cobrança mínima de 1 hora.
3. Tema azul e branco, com visual mais profissional e uso no celular.
4. Fundo branco, paleta definida pelo time de design e remoção dos emojis.
5. Barra superior substituída por coluna lateral, com mais tons de azul em botões e ícones.

## 7. Escopo do protótipo e pendências

**Entra no protótipo:** login e cadastro, cadastro de placa e condutor, mapa e contagem de 50 vagas, reserva com taxa de 10%, pagamento antecipado com tolerância, registro manual de entrada e saída, painel do funcionário, cancelamento com mensagem, cancela simulada, relatórios diário e mensal, configuração de preços.

**Fase 2:** câmeras e OCR, retenção de imagens, cancela física, login social, recuperação de senha, ocorrências, exportação de relatórios, persistência de dados.

**Em aberto:**

1. Base de cálculo dos 10% da reserva (1 hora, diária ou tempo estimado).
2. Um ou vários locais (multiunidade).
3. Valores definitivos da tabela de preços (hora, diária, tarifa noturna).
4. Número N de usuários simultâneos.
