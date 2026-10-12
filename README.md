# VanBora API — backend do app de transporte escolar

> **Sobre este repositório:** esta é uma cópia, com o histórico completo de commits, do
> repositório original [CintiaAngelo/vanbora-api](https://github.com/CintiaAngelo/vanbora-api), onde o
> projeto foi desenvolvido **em dupla** por mim e pela [Cintia Angelo](https://github.com/CintiaAngelo).
> O trabalho original continua lá; aqui ele fica disponível no meu perfil como portfólio.
> Veja a divisão do trabalho em [Autoria](#autoria).

API REST do **VanBora**, plataforma que conecta pais e responsáveis a transportadores
escolares. Atende o [app mobile](https://github.com/GuilhermeBussolan/vanbora-app) e os
painéis web.

Projeto de conclusão de curso (Sistemas de Informação — FIAP), selecionado entre os
**30 melhores de 420 equipes no Startup One 2026**.

## O que a API cobre

- **Contas e acesso:** cadastro de responsáveis, transportadores, monitores e escolas,
  com validação de CPF, CNH, placa, telefone e e-mail; login com JWT e login social (Auth0).
- **Contratação:** busca de transportadores por escola e bairro, proposta e contraproposta,
  contrato assinável e cancelamento por dependente.
- **Dia a dia:** presença e avisos de falta, rotas e percursos (a rota se ajusta quando um
  aluno falta), avisos do motorista e chat em tempo real por WebSocket.
- **Financeiro:** cronograma de mensalidades, pagamentos, receitas e despesas do
  transportador e relatórios.
- **Segurança da criança:** checklist ao fim do percurso, com foto e prazo de retenção
  automático.
- **Avaliações:** nota do transportador recalculada a cada avaliação.

## Segurança e LGPD

- Senhas com hash, JWT com revogação no logout e limite de tentativas de login.
- Segredos só por variáveis de ambiente, com checagens na inicialização que impedem subir
  em produção com valores de desenvolvimento.
- Regras de acesso por perfil e por vínculo: cada responsável vê só os próprios dependentes.
- Consentimento e revogação de dados pessoais (LGPD).

## Tecnologias

- **Java 21** e **Spring Boot 3.3**: Web, WebSocket, Data JPA, Validation e Security
- **MySQL 8** (H2 nos testes) e **JJWT**
- **springdoc-openapi** (documentação Swagger da API)
- Rotinas agendadas (expiração de propostas e retenção de fotos)

## Arquitetura

Organizada por funcionalidade (`modules/`: auth, hire, trip, route, finance, payment,
chat, notice, school, monitor…), cada uma com controller, serviço, repositório, domínio e DTOs.
Configuração e segurança ficam em `config/` e `security/`.

## Como rodar

Pré-requisitos: JDK 21 e MySQL 8.

```bash
cp .env.example .env    # preencha DB_PASSWORD e VANBORA_JWT_SECRET
./mvnw spring-boot:run
```

Passo a passo do banco, variáveis e dados de demonstração em [docs/SETUP.md](docs/SETUP.md).

## Autoria

Projeto desenvolvido **em dupla** por **Guilherme Bussolan Loureiro** e
**[Cintia Angelo](https://github.com/CintiaAngelo)**. O trabalho original foi feito no
repositório [CintiaAngelo/vanbora-api](https://github.com/CintiaAngelo/vanbora-api), do qual este foi
clonado com todo o histórico. Os commits de cada um aparecem com o respectivo autor.

- **Guilherme:** implementação das funcionalidades da plataforma — contratação e
  contraproposta, presença, pagamentos, avaliações, multi-dependente, catálogo de escolas,
  avisos, LGPD, rotas dinâmicas, financeiro, perfil MONITOR com checklist de segurança e
  chat em grupo, além do limite de tentativas de login e checagens de segurança na
  inicialização.
- **Cintia:** configuração inicial do projeto, login social com Auth0, segredos fora do
  repositório e revogação de token, registro de erros e dados de demonstração.
