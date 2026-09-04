# Guia de Configuração de Upsell (KashPay)

Este guia ensina como configurar o script de **Auto-Click** (compra automática) e como **alterar o link de destino do botão** nos seus arquivos de Upsell.

---

## 1. Script de Auto-Click (Compra Automática)

Este script aguarda a página carregar completamente e, após o tempo definido (em milissegundos), simula um clique automático no botão de compra do KashPay.

### Código do Script:
```html
<!-- Script de Auto-Click para Upsell -->
<script>
  window.addEventListener('load', function() {
    // Tempo de espera em milissegundos antes de clicar (ex: 2000 = 2 segundos)
    const tempoEspera = 2000; 

    setTimeout(function() {
      // Busca o botão que contém a chamada de aceitar upsell
      var btn = document.querySelector('[onclick*="acceptUpsell"]');
      if (btn) {
        console.log('[Auto-Accept] Iniciando compra automática...');
        btn.click();
      } else {
        console.warn('[Auto-Accept] Botão de upsell não encontrado na página.');
      }
    }, tempoEspera);
  });
</script>
```

### Como usar:
* Cole este código no final do arquivo HTML do seu upsell, logo antes do fechamento da tag `</body>`.
* O botão de compra deve ter o atributo `onclick` chamando `acceptUpsell(...)` para que o script o localize.

---

## 2. Como Alterar o Link do Botão de Compra

Você tem duas formas de alterar o link do botão de upsell do KashPay:

### Método A: Diretamente no HTML (Recomendado e Mais Simples)

Basta abrir o arquivo HTML do seu upsell e alterar a URL que está dentro do atributo `onclick` do botão de compra.

**Exemplo:**
```html
<!-- Mude apenas o link de dentro dos parênteses do acceptUpsell -->
<button onclick="acceptUpsell('https://app.kashpay.com.br/u/COLOQUE_SEU_ID_AQUI')" class="btn-cta">
  Comprar Oferta
</button>
```

---

### Método B: Alteração Dinâmica via JavaScript (Com Auto-Click)

Se você preferir mudar o link dinamicamente por JavaScript e já executar o clique automático em seguida, use o script combinado abaixo. Ele altera o link do botão no momento do clique.

### Código Combinado (Muda Link + Auto-Click):
```html
<script>
  window.addEventListener('load', function() {
    // 1. Defina o novo link do KashPay aqui
    const novoLinkKashpay = 'https://app.kashpay.com.br/u/NOVO_ID_AQUI';
    
    // 2. Tempo de espera em milissegundos (ex: 2000 = 2 segundos)
    const tempoEspera = 2000; 

    setTimeout(function() {
      // Busca o botão de upsell
      var btn = document.querySelector('[onclick*="acceptUpsell"]');
      
      if (btn) {
        // Altera dinamicamente o atributo onclick com a nova URL
        btn.setAttribute('onclick', "acceptUpsell('" + novoLinkKashpay + "')");
        console.log('[Upsell-Manager] Link atualizado para: ' + novoLinkKashpay);
        
        // Dispara o clique automático
        console.log('[Upsell-Manager] Executando clique automático...');
        btn.click();
      } else {
        console.warn('[Upsell-Manager] Botão de upsell não encontrado para alterar o link.');
      }
    }, tempoEspera);
  });
</script>
```

### Como usar o Método B:
1. Cole o código acima no final do seu HTML, antes de `</body>`.
2. Substitua `'https://app.kashpay.com.br/u/NOVO_ID_AQUI'` pela sua URL real de Upsell do KashPay.
