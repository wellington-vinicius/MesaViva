# Mesa Viva 🌿

Um restaurante de demonstração para aprender **React + Vite + Tailwind CSS**. Interface em português, pensada primeiro para celular e adaptada ao computador. JavaScript puro: sem TypeScript, servidor ou banco de dados para configurar.

## Começar

Instale Node.js **22.12 ou superior** (Node 24 também funciona). Abra esta pasta no VS Code e execute no terminal:

```sh
npm install
npm run dev
```

Abra o endereço mostrado no terminal, normalmente `http://127.0.0.1:5173`.

Em ambientes com restrições de leitura de pastas, o modo de desenvolvimento pode encontrar “Acesso negado” na ferramenta esbuild. Nesse caso, use `npm run build` e `npm run preview` para abrir a aplicação compilada em `http://127.0.0.1:4173`. O projeto também inclui a pasta `dist` já compilada. Os scripts usam o carregamento nativo de configuração do Vite.

```sh
npm test       # verifica as regras de negócio
npm run build # gera a versão final em dist/
npm run preview # abre a versão compilada
```

## O que funciona

- 12 mesas, abertura com cliente e quantidade de pessoas.
- Filtros por ocupação e busca por número ou cliente.
- Tempo da mesa aberta e tempo desde o último pedido não cancelado, atualizado automaticamente.
- Cardápio com categorias, preços, quantidades e observações.
- Envio para a cozinha: na fila → preparando → pronto → entregue.
- Cancelamento de pedidos que ainda estão na fila.
- Consumo da mesa, serviço opcional de 10%, forma de pagamento e liberação da mesa.
- Bloqueio do fechamento enquanto houver pedidos não entregues.
- Histórico detalhado de contas no caixa.
- Persistência no navegador e botão para reiniciar os exemplos.

## Um roteiro de demonstração

1. Na aba **Mesas**, abra a mesa 1 com seu nome.
2. Toque em **Novo pedido**, escolha um burger e uma limonada. Escreva “sem cebola”.
3. Envie para a cozinha e observe o consumo da mesa.
4. Na aba **Cozinha**, comece o preparo e marque como pronto.
5. Confirme a entrega na cozinha ou nos detalhes da mesa.
6. Feche a conta, escolha Pix e confirme o recebimento.
7. Veja o recibo na aba **Caixa** e a mesa livre novamente.
8. Atualize a página: os dados continuam salvos. Use **Reiniciar demo** para uma nova aula.

## Entendendo o código

```text
src/
  main.jsx        Entrada: coloca o React na página
  App.jsx         Telas, eventos e estado da aplicação
  components.jsx  Componentes reutilizáveis: selo e janela
  data.js         Cardápio e dados de exemplo
  helpers.js      Regras e funções de dinheiro, tempo e conta
  styles.css      Tailwind e estilos da identidade visual
tests/
  orders.test.js  Testes das regras de pedidos e fechamento
```

O estado fica no componente `App` para a turma acompanhar o fluxo sem Context, Redux ou roteadores. `useState` guarda as informações; `useEffect` salva no navegador e atualiza o relógio; `map` desenha listas; `filter` escolhe o que aparece. Cada clique atualiza uma cópia do estado anterior.

Os pedidos guardam uma cópia do produto e do preço no momento da compra. Assim, alterar o cardápio depois não muda o valor de pedidos já registrados. Valores são armazenados em centavos: `3200` representa R$ 32,00.

As classes do Tailwind aparecem no JSX, por exemplo `grid grid-cols-2 gap-3 md:grid-cols-3`. As classes com nomes próprios no CSS concentram estilos repetidos e a identidade visual. Não é necessário configurar `tailwind.config.js`: este projeto usa Tailwind 4 com o plugin do Vite.

## Proposta para a turma

| Aula | Conceito               | Atividade                                           |
| ---- | ---------------------- | --------------------------------------------------- |
| 1    | JSX e componentes      | Trocar nome, cores e textos do restaurante          |
| 2    | Arrays e `map`         | Adicionar um produto em `data.js`                   |
| 3    | Estado e eventos       | Entender os botões de quantidade                    |
| 4    | Formulários e filtros  | Validar a abertura de uma mesa e pesquisar clientes |
| 5    | Regras de negócio      | Acompanhar o pedido e calcular a conta              |
| 6    | Efeitos e persistência | Atualizar a página e inspecionar o `localStorage`   |

Desafios: adicionar uma categoria “Entradas”, criar um filtro para mesas com pedido pronto, extrair o cartão de mesa para um componente e adicionar um desconto com limites claros.

## Limites da demonstração

É um protótipo didático local. Salão e cozinha compartilham o mesmo estado na aplicação. Abas do mesmo navegador e endereço recebem atualizações via `localStorage`, mas edições simultâneas podem sobrescrever dados. **Celulares e computadores diferentes não compartilham pedidos**: para isso, uma próxima etapa precisa de servidor/banco e sincronização.

Não há login, pagamento real, emissão fiscal, impressão, estoque ou operação em produção. “Confirmar recebimento” apenas registra a forma de pagamento escolhida. Não insira dados reais de clientes. Limpar os dados do navegador ou reiniciar a demonstração apaga os registros locais.

## Referências

- [Guia oficial do Vite](https://vite.dev/guide/)
- [Tailwind CSS com Vite](https://tailwindcss.com/docs/installation/using-vite)
- [Aprenda React](https://react.dev/learn)
