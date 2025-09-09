código 

<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Mini Loja</title>
  <style>
    .produtos, .carrinho {
      border: solid 1px lightgray;
      padding: 10px;
      margin-bottom: 20px;
    }

    .produto {
      
      border: solid 1px lightgray;
      display: inline-block;
      margin: 10px;
      padding: 10px;
    }

    .produto li {
      list-style: none;
    }

    .item-carrinho {
      border: solid 1px lightgray;
      padding: 10px;
      margin: 10px 0;
    }

    .quantidade-control {
      display: flex;
      align-items: center;
      gap: 10px;
      margin-top: 5px;
    }

    button {
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Mini Loja</h1>
  <main>
    <div class="produtos">
      <div class="produto" data-id="produto-1" data-nome="Produto" data-preco="50">
        <ul>
          <li>Produto</li>
          <li>R$50</li>
          <button class="btn-adicionar">adicionar</button>
        </ul>
      </div>
    </div>

    <div class="carrinho">
      <h1>Carrinho</h1>
      <!-- Produtos adicionados vão aqui -->
    </div>
  </main>

  <script>
    const botaoAdicionar = document.querySelector('.btn-adicionar');
    const produto = document.querySelector('.produto');
    const carrinho = document.querySelector('.carrinho');

    botaoAdicionar.addEventListener('click', () => {
      const produtoId = produto.getAttribute('data-id');
      const nome = produto.getAttribute('data-nome');
      const preco = parseFloat(produto.getAttribute('data-preco'));

      // Verifica se já está no carrinho
      const jaAdicionado = carrinho.querySelector(`[data-id="${produtoId}"]`);

      if (!jaAdicionado) {
        // Cria o item no carrinho
        const item = document.createElement('div');
        item.classList.add('item-carrinho');
        item.setAttribute('data-id', produtoId);

        let quantidade = 1;
        let total = preco;

        item.innerHTML = `
          <strong>${nome}</strong><br>
          <div class="quantidade-control">
            <button class="diminuir">-</button>
            <span class="quantidade">${quantidade}</span>
            <button class="aumentar">+</button>
          </div>
          <div>Total: R$<span class="total">${total.toFixed(2)}</span></div>
        `;

        // Adiciona ao carrinho
        carrinho.appendChild(item);

        // Botões de controle
        const btnAumentar = item.querySelector('.aumentar');
        const btnDiminuir = item.querySelector('.diminuir');
        const spanQuantidade = item.querySelector('.quantidade');
        const spanTotal = item.querySelector('.total');

        btnAumentar.addEventListener('click', () => {
          quantidade++;
          spanQuantidade.textContent = quantidade;
          spanTotal.textContent = (quantidade * preco).toFixed(2);
        });

        btnDiminuir.addEventListener('click', () => {
          if (quantidade > 1) {
            quantidade--;
            spanQuantidade.textContent = quantidade;
            spanTotal.textContent = (quantidade * preco).toFixed(2);
          }
        });
      }
    });
  </script>
</body>
</html>
