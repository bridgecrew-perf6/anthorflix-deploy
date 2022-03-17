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

De maneira geral é fácil olhar para cada requisito e enxergar uma maneira simples de chegar ao objetivo.

O que torna o projeto um pouco mais turvo é a ausência de maiores informações sobre os domínios em questão, o que torna o processo de modelagem mais arbitrário por parte do desenvolvedor e e menos para o suposto modelo de negócios em si.

O meu principal desafio foi o curto tempo para projetar e desenvolver com qualidade o projeto completo, considerando as obrigações de trabalho atuais e ocorridos pessoais da semana.

# Se Tivesse Mais Tempo
- Modelaria os domínio pensando na autenticação como um requisito não opcional desde o princípio, no final pude notar que faria mais sentido ter o usuário nos repositórios de avaliação e comentário somente com os campos necessário, enquanto as informações de autenticação ficariam somente no repositório de usuário.
- Faria mais abstrações, especialmente no front-end. Alguns comportamentos podem ser padronizados por meio de hooks para deixar o código menor. No back-end eu faria mais abstrações no teste do controller, deixaria o código menor e quase desacoplado ao NestJS.
- Faria upload de imagem para um bucket no cadastro de filmes, com opção de URL para fazer download e subir para o bucket. Validando o MIME e dimensões da imagem em ambos casos. Para testes automatizados eu utilizaria um serviço como o MINIO para simular o buckets S3 ou o google cloud storage testing
- Criaria mais objetos de valor para maior consistência dos dados (ex: Year, Rating).
- Implementaria um recurso de importação de filmes do TMDB pelo painel.
- Simularia uma sessão de event storming detalhada para:
  - Definir melhor a suposta solução real da aplicação para o mundo
  - Modelar melhor os domínio de acordo com os objetivos
- Um painel administrativo mais elegante
- Utilizaria NextJS para o front-end do usuário final.
- Utilizaria GraphQL no front, facilitaria a buscar somente os dados que preciso em cada tela, tornaria o back-end mais flexível com os field resolvers e poderia ainda passar os campos selecionados como opção para os repositories e otimizar a carga de busca no banco de dados
- Modificaria os repositories para receber as entidades instanciadas, ao invés dos objetos planos das mesmas.
- Implementaria métodos para gerar entidades aleatórias, ao invés de gerar penas os objetos planos
