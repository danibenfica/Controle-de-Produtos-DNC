![Design sem nome (1)](https://github.com/danibenfica/Mini-projeto-DNC/assets/103818625/33089c82-1b7c-4cf5-acb9-20073e9ae2a6)

[Link do projeto online aqui!](https://controle-de-produtos-dnc.vercel.app/)

# Controle de Produtos

## Visão Geral
O Controle de Produtos é um aplicativo web desenvolvido para facilitar o controle e gerenciamento de produtos. Com ele, é possível adicionar, listar e remover produtos de uma lista.

## Tecnologias Utilizadas
O projeto utiliza as seguintes tecnologias:

- HTML: Para a estruturação e marcação do aplicativo web.
- CSS: Para a estilização e aparência visual do aplicativo.
- JavaScript: Para a implementação da lógica e interatividade do aplicativo.

## Funcionalidades

### Adicionar Produto
A função `Adicionar()` é responsável por adicionar um novo produto à lista de produtos. Ela realiza as seguintes ações:
1. Lê os dados do produto informados pelo usuário.
2. Valida os dados do produto.
3. Se os dados forem válidos, salva o produto na lista de produtos.
4. Atualiza a exibição da lista de produtos.
5. Limpa os campos de entrada de dados.

```javascript
Adicionar() {
   let produto = this.lerDados();
   if (this.Validar(produto) == true) {
      this.Salvar(produto);
   }
   this.Listar();
   this.Cancelar();
}
```

### Ler Dados do Produto
A função `lerDados()` é responsável por ler os dados do produto inseridos pelo usuário e retorná-los em um objeto.
```javascript
lerDados() {
    let produto = {};
    produto.id = this.id;
    produto.nomeProduto = document.getElementById('pdNome').value;
    produto.precoProduto = document.getElementById('pdPreco').value;
    return produto;
}
```

### Validar Produto
A função `Validar(produto)` é responsável por validar os dados do produto. Ela verifica se o nome do produto e o preço foram preenchidos corretamente. Caso haja algum erro, exibe uma mensagem de alerta ao usuário.
```javascript
Validar(produto) {
    let msg = '';
    if (produto.nomeProduto == '') {
        msg += 'Por favor, insira corretamente o nome do produto! \n';
    }
    if (produto.precoProduto == '') {
        msg += 'Por favor, insira corretamente o preço do produto! \n';
    }
    if (msg != '') {
        alert(msg);
        return false;
    }
    return true;
}
```

### Salvar Produto
A função `Salvar(produto)` adiciona o produto à lista de produtos (`arrayProdutos`) e incrementa o ID para o próximo produto a ser adicionado.
```javascript
Salvar(produto) {
    this.arrayProdutos.push(produto);
    this.id++;
}
```

### Listar Produtos
A função `Listar()` exibe a lista de produtos na tabela do HTML. Ela percorre o array de produtos (`arrayProdutos`) e insere cada produto em uma nova linha na tabela.
```javascript
Listar() {
    let tbody = document.getElementById('tbody');
    tbody.innerText = '';

    for (let i = 0; i < this.arrayProdutos.length; i++) {
        let tr = tbody.insertRow();

        let td_id = tr.insertCell();
        let td_nome = tr.insertCell();
        let td_preco = tr.insertCell();
        let td_del = tr.insertCell();

        td_id.innerText = this.arrayProdutos[i].id;
        td_nome.innerText = this.arrayProdutos[i].nomeProduto;
        td_preco.innerText = this.arrayProdutos[i].precoProduto;

        let imagem = document.createElement('img');
        imagem.src = 'delete.png';
        imagem.setAttribute("onclick", "produto.Deletar(" + this.arrayProdutos[i].id + ")");
        td_del.appendChild(imagem);
    }
}
```

### Cancelar
A função `Cancelar()` limpa os campos de entrada de dados, restaurando-os ao estado original.
```javascript
Cancelar() {
    document.getElementById('pdNome').value = '';
    document.getElementById('pdPreco').value = '';
}
```

### Deletar Produto
A função `Deletar(id)` remove um produto da lista de produtos com base no ID fornecido. Ela percorre o array de produtos, localiza o produto com o ID correspondente e o remove tanto do array quanto da tabela exibida no HTML.
```javascript
Deletar(id) {
    let tbody = document.getElementById('tbody');
    for (let i = 0; i < this.arrayProdutos.length; i++) {
        if (this.arrayProdutos[i].id == id) {
            this.arrayProdutos.splice(i, 1);
            tbody.deleteRow(i);
        }
    }
    alert('O item foi apagado com sucesso!');
}
```

## Conclusão
O Controle de Produtos é um projeto simples, mas funcional, que demonstra o uso de JavaScript para adicionar, listar e remover produtos. Com base nas funções mencionadas acima, é possível expandir e aprimorar o projeto adicionando recursos como edição de produtos, armazenamento persistente de dados e integração com um backend.

Qualquer dúvida ou sugestão não hesite em me contatar! :smile: