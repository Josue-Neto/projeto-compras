document.addEventListener('DOMContentLoaded', iniciarApp);

function iniciarApp() {
  let listaDeCompras = [];
  const itensIniciais = ['Arroz', 'Feijão', 'Macarrão'];

  const listaElement = document.getElementById('listaDeCompras');
  const botaoAdicionar = document.getElementById('adicionarItemBtn');
  const campoInput = document.getElementById('itemInput');
  const mensagem = document.getElementById('mensagem');

  inicializarLista(itensIniciais);

  botaoAdicionar.addEventListener('click', adicionarMaisItens);

  function inicializarLista(itens) {
    itens.forEach(item => adicionarItem(item));
  }

  function adicionarItem(item) {
    listaDeCompras.push(item);
    adicionarItemNoDOM(item);
  }

  function adicionarItemNoDOM(item) {
    const li = document.createElement('li');
    li.textContent = item;
    listaElement.appendChild(li);
  }

  function adicionarMaisItens() {
    if (listaDeCompras.length >= 5) {
      mostrarMensagem('Sua lista está completa.', true);
      return;
    }

    const novoItem = campoInput.value.trim();

    if (novoItem === '') {
      mostrarMensagem('Digite um item válido.', true);
      return;
    }

    adicionarItem(novoItem);
    mostrarMensagem('Item adicionado com sucesso!', false);

    campoInput.value = '';
    campoInput.focus();

    if (listaDeCompras.length >= 5) {
      mostrarMensagem('Sua lista está completa.', true);
    }
  }

  function mostrarMensagem(texto, erro) {
    mensagem.textContent = texto;
    mensagem.style.color = erro ? 'red' : 'green';
    setTimeout(() => {
      mensagem.textContent = '';
    }, 3000);
  }
}