#Plano de Testes Automatizados - Projeto Raízes do Nordeste

Este documento descreve o roteiro de validação da API do Projeto Raízes do Nordeste, contendo as orientações de ambiente, a ordem de execução lógica e a tabela de mapeamento dos cenários testados através do Postman.

---

##Pré-requisitos e Configuração do Ambiente

Para reproduzir os testes localmente, certifique-se de cumprir os seguintes passos:

1. Executar a API: Abra o terminal na pasta raiz do projeto back-end(https://github.com/Pablo-lara/Projeto-Raizes-do-Nordeste) e inicie o servidor com o seguinte comando:
   dotnet run
2. Identificar a URL Local: Verifique a porta gerada no seu terminal (geralmente http://localhost:5054 ou https://localhost:7123).

3. Importar a Coleção no Postman:

  -Abra o Postman.

  -Clique em Import (superior esquerdo).

  -Selecione o arquivo Projeto Raízes.postman_collection.json localizado na raiz deste repositório.

##Ordem de execução sugerida
Para evitar inconsistências de chaves estrangeiras ou status inválidos no banco de dados, os testes devem seguir estritamente a sequência abaixo:
T01 (Cadastro): Cria o usuário inicial no banco.

T07 e T08 (Erros de Validação): Validam as travas de segurança do cadastro antes de avançar.

T02 (Login): Autentica o usuário recém-criado.

T03 (Cardápio): Retorna os produtos ativos da lanchonete.

T04 (Criar Pedido): Abre um carrinho com base nos produtos do cardápio.

T09 (Erro de Produto): Tenta forçar um pedido inválido para testar o bloqueio da API.

T05 (Status do Pedido): Consulta o estado inicial ("Recebido") do pedido gerado no T04.

T06 (Pagamento): Simula a aprovação financeira e muda o status para "Em Preparação".

T10 (Erro de Pagamento): Tenta pagar novamente o mesmo pedido para validar o bloqueio de duplicidade.

Obs: Indices dos testes segue padrão apresentado na tabela de testes presente na seção de testes no documento final de entrega do trabalho.

##Observações de auditorias e logs
Sistema de Logs/Auditoria Automatizada: Não implementado nesta versão do software.

Justificativa Técnica: O controle e histórico das operações sensíveis são gerenciados e persistidos por meio de uma máquina de estados finitos acoplada diretamente à propriedade estrutural Status na tabela Pedidos,
garantindo a rastreabilidade essencial do negócio sem a introdução de tabelas secundárias de histórico nesta janela de entrega.
