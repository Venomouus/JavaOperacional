# Melhorias 
<h3>•	Comparação de senha:</h3>
- Considere usar práticas mais segura para armazenar e comparar senhas, tais como uso de algoritmos de hash seguros e práticas de armazenamento seguro de senhas.

<h3>•	Tratamento de Entrada do Usuário:</h3> 
- Considere fazer tratamento de entrada do usuário para verificar se os valores inseridos são válidos. É importante adicionar verificação para evitar exceções e comportamentos inesperados.

<h3>•	Switch-Case sem break:</h3>
- Considere adicionar ‘break’ no final de cada ‘case’ para evitar que o código continua executando os outros ‘cases’ após uma escolha

<h3>•	Comentários e Documentação:</h3> 
- Adicione comentários ao código para explicar partes mais complexas, funções e trechos importantes. Isso ajudará a entender o funcionamento do código e facilitará a manutenção no futuro.

<h3>•	Manipulação de Erros:</h3> 
- Considere adicionar um tratamento adequado de exceções. Como blocos try-catch onde as exceções possam ocorrer para evitar falhas inesperadas, é importante implementar um tratamento de exceções apropriado para oferecer uma experiência melhor ao usuário 

<hr></hr>

# Erros
<h3>•	Valor Comissão:</h3>
- O valor total da venda é adicionado ao saldo da empresa sem considerar a dedução da comissão do sistema, para ajustar esse cálculo, subtraia o valor da comissão do sistema do total da venda antes de atualizar o saldo da empresa.<br></br>

<p>public static Venda criarVenda(List<Produto> carrinho, Empresa empresa, Cliente cliente, List<Venda> vendas) {</p>
   <p>Double total = carrinho.stream().mapToDouble(Produto::getPreco).sum();</p>
   <p>Double comissaoSistema = total * empresa.getTaxa();</p>
   <p>int idVenda = vendas.isEmpty() ? 1 : vendas.get(vendas.size() - 1).getCódigo() + 1;</p>
   <p>Venda venda = new Venda(idVenda, carrinho.stream().toList(), total, comissaoSistema, empresa, cliente);</p>    
   <p>empresa.setSaldo(empresa.getSaldo() + total);  // Erro: Adicionando o total da venda sem dedução da comissão</p>
   <p>vendas.add(venda);</p>
   <p>return venda;</p>
<p>} </p>
  
<h3>•	Falta de proteção de informações:</h3> 
-  Há uma falta de implementação de controles de acesso apropriados para cumprir a regra de negócio que apenas o administrador e a própria empresa podem ver informações detalhadas da empresa, qualquer empresa pode acessar as vendas de outras empresas.  
<img src="/img/Erro(2).png">

 
<h3>•	Verificação Login:</h3>
- Se o cliente logado não for encontrado, a lista resultante estará vazia, e ao tentar acessar o primeiro elemento com ‘get(0)’, ocorre o erro de ‘IndexOutOfBoundsException’.
Para resolver esse problema, você precisa verificar se o cliente logado foi encontrado antes de tentar acessar o primeiro elemento da lista resultante. Uma maneira de fazer isso é verificar se a lista não está vazia antes de chamar ‘get(0)’.<br></br>

<p>List<Cliente> clientesLogados = clientes.stream()</p>
        <p> .filter(x -> x.getUsername().equals(usuarioLogado.getUsername()))</p>
        <p> .collect(Collectors.toList());</p>

<p>if (!clientesLogados.isEmpty()) {</p>
    <p>Cliente clienteLogado = clientesLogados.get(0);</p>
    <p>// .....</p>
<p>} else {</p>
    <p>System.out.println("Cliente não encontrado.");</p>
    <p>// ......</p>
<p>}</p>


