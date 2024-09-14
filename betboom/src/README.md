README - Projeto Surebet Calculator
Índice

    Introdução
    Arquitetura do Projeto
        src/
            odds_provider.py
            surebet_calculator.py
            providers/
        tests/
            test_surebet_calculator.py
            test_providers/
    Como Executar o Projeto
    Como Executar os Testes
    Como Adicionar um Novo Provedor de Odds
    Contribuições
    Licença

Introdução

Este projeto implementa um Surebet Calculator para garantir lucros em apostas esportivas utilizando o conceito de arbitragem. O projeto é desenvolvido seguindo os princípios SOLID de design de software, proporcionando uma arquitetura modular, flexível, robusta e escalável. Ele permite calcular investimentos proporcionais em diferentes mercados de apostas para garantir um lucro, independentemente do resultado.
Arquitetura do Projeto

A estrutura de pastas do projeto é organizada da seguinte forma:

markdown

meu_projeto/
│
├── src/
│   ├── __init__.py
│   ├── odds_provider.py
│   ├── surebet_calculator.py
│   └── providers/
│       ├── __init__.py
│       └── betboom_provider.py
│
├── tests/
│   ├── __init__.py
│   ├── test_surebet_calculator.py
│   └── test_providers/
│       ├── __init__.py
│       └── test_mock_provider.py
│
├── requirements.txt
└── README.md

src/

Esta pasta contém o código-fonte principal do projeto.

    odds_provider.py:
    Este módulo define a interface OddsProvider, que é uma abstração para qualquer classe que forneça odds (cotações de apostas). A interface OddsProvider segue o Princípio da Segregação de Interface (ISP), garantindo que apenas métodos relevantes sejam definidos para os provedores de odds.

    surebet_calculator.py:
    Este módulo contém a classe SurebetCalculator, responsável pelo cálculo de investimentos necessários para garantir lucro em apostas. O SurebetCalculator depende apenas da interface OddsProvider, seguindo o Princípio da Inversão de Dependência (DIP) e o Princípio da Responsabilidade Única (SRP), pois sua única responsabilidade é calcular os investimentos.

    providers/:
    Esta subpasta contém implementações específicas de provedores de odds.
        betboom_provider.py:
        Esta classe implementa o OddsProvider para buscar odds reais da API BetBoom. A implementação segue o Princípio Aberto/Fechado (OCP), permitindo a extensão para suportar novos provedores sem modificar o código existente.

tests/

Esta pasta contém todos os testes unitários e de integração do projeto.

    test_surebet_calculator.py:
    Este módulo contém testes unitários para a classe SurebetCalculator. Ele utiliza mocks para fornecer odds fixas, garantindo que o cálculo dos investimentos funcione corretamente. Segue o Princípio da Substituição de Liskov (LSP) ao usar MockOddsProvider para testar sem dependências reais.

    test_providers/:
    Subpasta para testes relacionados a provedores de odds.
        test_mock_provider.py:
        Contém testes unitários que utilizam mocks para validar o comportamento dos provedores de odds e garantir que a integração com a API BetBoom (ou outros provedores) funcione corretamente.

Como Executar o Projeto

    Clone o repositório:

    bash

git clone https://github.com/seu-usuario/meu_projeto.git
cd meu_projeto

Instale as dependências:

Certifique-se de ter o Python instalado e execute:

bash

pip install -r requirements.txt

Execute o projeto:

O projeto pode ser executado diretamente usando a classe SurebetCalculator:

bash

    python src/surebet_calculator.py

Como Executar os Testes

Para executar todos os testes, utilize o framework unittest:

bash

python -m unittest discover -s tests/

Isso irá executar todos os testes na pasta tests/ e gerar um relatório detalhado de quaisquer falhas.
Como Adicionar um Novo Provedor de Odds

Para adicionar um novo provedor de odds ao projeto, siga os seguintes passos:

    Crie uma nova classe na pasta src/providers/:
        Nomeie o arquivo com o nome do provedor, por exemplo, novo_provider.py.
        Implemente a classe para fornecer odds, garantindo que ela implemente a interface OddsProvider.

    Implemente o método get_odds:
        O método get_odds deve retornar um dicionário com as odds para cada time ou opção de aposta.

    python

    from odds_provider import OddsProvider

    class NovoProvider(OddsProvider):
        def get_odds(self) -> Dict[str, float]:
            # Implementação para buscar odds do novo provedor
            odds = {
                "Time X": 12,
                "Time Y": 0.25
            }
            return odds

    Adicione testes para o novo provedor:
        Crie um novo arquivo de teste em tests/test_providers/ para testar a implementação do novo provedor. Use mocks para simular respostas da API, garantindo que seu código esteja isolado de dependências externas.

Contribuições

Contribuições são bem-vindas! Para contribuir com este projeto:

    Faça um fork do repositório.
    Crie uma branch com a sua feature ou correção de bug (git checkout -b feature/nova-feature).
    Commit suas mudanças (git commit -m 'Adiciona nova feature').
    Envie para a branch (git push origin feature/nova-feature).
    Abra um Pull Request.

Licença

Este projeto é licenciado sob a Licença MIT. Veja o arquivo LICENSE para mais detalhes.