# Anthorflix
O teste de dev da Anthor.

# Como Rodar
Com Docker Compose V2:

    docker compose up -d

Com Docker Compose V1:

    docker-compose up -d

Acesse o front end em [localhost:3000](localhost:3000). O back-end será exposto em [localhost:4000](localhost:4000).

O front-end estará pronto para acessar após concluir a compilação.

# Repositórios
Back-end: [https://github.com/dannyfranca/anthorflix-api](https://github.com/dannyfranca/anthorflix-api)

Front-end: [https://github.com/dannyfranca/anthorflix-front](https://github.com/dannyfranca/anthorflix-front)

# Bugs Conhecidos
- No front-end as labels dos campos de formulário podem eventualmente sobre por o conteúdo enquanto não clicados.
- Container Front-end utilizando servidor de desenvolvimento para demonstração. Cabe um build estático com Nginx num eventual deploy em produção com docker.

# Planejamento
Considerando o simples objetivo do projeto, decidi utilizar no back-end o framework NestJS, que traz uma filosofia modular, ideal para projetar uma aplicação escalável, além de ter ótimo suporte ao Typescript e ferramentas de teste modulares.

Apesar de escolher o NestJS como framework, o objetivo é não acoplar o sistema ao framework, desenvolvendo o máximo de recursos de forma agnóstica ao NestJS e só então utilizando os recursos do framework para integrar com cada componente.

Como ORM escolhi o Prisma, por tornar extremamente fácil realizar queries e por ter suporte excepcional ao Typescript. Um ponto negativo do Prisma é não ter o melhor suporte para testes, como migrations programáticas. No entanto, eu desenvolvi uma classe que gerencia a criação, migração e exclusão de bancos de dados em produção, utilizando as migrations geradas pelo próprio prisma.

Como não tive uma conversa profunda com um especialista de domínio da aplicação, optei por colocar cada entidade em seu próprio módulo e no decorrer do caminho, caso necessário, criar entidades e repositórios duplicados em módulos distintos, respeitando o DDD e mantendo a separação de contextos.

No front-end, optei por utilizar o create-react-app para ter maior flexibilidade no painel e front-end do usuário. Num projeto real de longo prazo faria sentido utilizar o react puro no painel administrativo, mas o NextJS para a aplicação do usuário final, aproveitando os benefícios do SSG.

# Dificuldades
Não considero qualquer recurso solicitado difícil, provavelmente seria possível implementar tudo rapidamente em uma semana sem testes unitários.

O principal desafio é apenas o curto tempo para projetar e desenvolver com qualidade o projeto completo.

De maneira geral é fácil olhar para cada requisito e enxergar uma maneira simples de chegar ao objetivo.

# Se Tivesse Mais Tempo
- Implementaria um recurso de importação de filmes do TMDB pelo painel.
- Simularia uma sessão de event storming detalhada para:
  - Definir melhor a suposta solução real da aplicação para o mundo
  - Modelar melhor os domínio de acordo com os objetivos
- Um painel administrativo mais elegante
- Utilizaria NextJS para o front-end do usuário final.
