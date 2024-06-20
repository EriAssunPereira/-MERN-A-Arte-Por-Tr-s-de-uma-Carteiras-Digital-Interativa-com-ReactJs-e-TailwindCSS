# MERN-A-Arte-Por-Trás-de-uma-Carteiras-Digital-Interativa-com-ReactJs-e-TailwindCSS

Para criar uma Carteira Digital Interativa utilizando ReactJS e TailwindCSS, vamos seguir uma abordagem modular, detalhando cada passo necessário para construir uma interface amigável e esteticamente cativante para gerenciar finanças de forma intuitiva.

### Descrição do Projeto:
Desenvolver uma Carteira Digital utilizando ReactJS e TailwindCSS, focando na interatividade e usabilidade para gerenciar finanças pessoais de maneira intuitiva.

### Passos para Implementação:

#### Passo 1: Configuração do Ambiente
Certifique-se de ter o ambiente de desenvolvimento configurado com Node.js e npm (Node Package Manager).

#### Passo 2: Criação do Projeto React
Crie um novo projeto React utilizando Create React App.

```bash
npx create-react-app carteira-digital-react
cd carteira-digital-react
```

#### Passo 3: Instalação do TailwindCSS
Instale o TailwindCSS para estilização da aplicação.

```bash
npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
```

#### Passo 4: Configuração do TailwindCSS
Crie e configure o TailwindCSS seguindo a documentação oficial para criar o arquivo de configuração e configurar os estilos globais.

```bash
npx tailwindcss init -p
```

#### Passo 5: Estrutura do Projeto e Componentes
Organize a estrutura do projeto e crie os componentes principais para a carteira digital.

1. **Componente de Layout Principal:**
   - Crie um layout principal utilizando TailwindCSS para estruturação básica.

```jsx
// src/components/Layout.js
import React from 'react';

const Layout = ({ children }) => {
    return (
        <div className="flex flex-col min-h-screen bg-gray-100">
            <header className="bg-blue-500 text-white p-4">
                <h1 className="text-2xl font-bold">Minha Carteira Digital</h1>
            </header>
            <main className="flex-grow container mx-auto p-4">
                {children}
            </main>
            <footer className="bg-blue-500 text-white p-4 text-center">
                &copy; 2024 Minha Carteira Digital. Todos os direitos reservados.
            </footer>
        </div>
    );
};

export default Layout;
```

2. **Componente de Lista de Transações:**
   - Crie um componente para exibir a lista de transações.

```jsx
// src/components/TransactionList.js
import React from 'react';

const TransactionList = ({ transactions }) => {
    return (
        <div className="mt-4">
            <h2 className="text-xl font-semibold mb-2">Últimas Transações</h2>
            <ul className="divide-y divide-gray-200">
                {transactions.map(transaction => (
                    <li key={transaction.id} className="py-2">
                        <div className="flex justify-between items-center">
                            <span className="font-semibold">{transaction.title}</span>
                            <span className={`${transaction.type === 'expense' ? 'text-red-500' : 'text-green-500'}`}>
                                {transaction.type === 'expense' ? '-' : '+'} R$ {transaction.amount.toFixed(2)}
                            </span>
                        </div>
                        <span className="text-sm text-gray-500">{transaction.date}</span>
                    </li>
                ))}
            </ul>
        </div>
    );
};

export default TransactionList;
```

3. **Componente de Formulário para Adicionar Transação:**
   - Crie um componente para adicionar novas transações.

```jsx
// src/components/AddTransactionForm.js
import React, { useState } from 'react';

const AddTransactionForm = ({ onAddTransaction }) => {
    const [title, setTitle] = useState('');
    const [amount, setAmount] = useState(0);
    const [type, setType] = useState('income'); // 'income' or 'expense'

    const handleSubmit = (e) => {
        e.preventDefault();
        const newTransaction = {
            id: Math.random().toString(),
            title,
            amount: +amount,
            type,
            date: new Date().toLocaleDateString()
        };
        onAddTransaction(newTransaction);
        setTitle('');
        setAmount(0);
        setType('income');
    };

    return (
        <div className="mt-4">
            <h2 className="text-xl font-semibold mb-2">Adicionar Transação</h2>
            <form onSubmit={handleSubmit} className="space-y-4">
                <input type="text" value={title} onChange={(e) => setTitle(e.target.value)} placeholder="Título da Transação" className="block w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:border-blue-500" required />
                <input type="number" value={amount} onChange={(e) => setAmount(e.target.value)} placeholder="Valor" className="block w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:border-blue-500" required />
                <select value={type} onChange={(e) => setType(e.target.value)} className="block w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:border-blue-500">
                    <option value="income">Receita</option>
                    <option value="expense">Despesa</option>
                </select>
                <button type="submit" className="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-md">Adicionar</button>
            </form>
        </div>
    );
};

export default AddTransactionForm;
```

#### Passo 6: Integração dos Componentes no Layout Principal
Integre os componentes criados (`Layout`, `TransactionList`, `AddTransactionForm`) na aplicação principal.

```jsx
// src/App.js
import React, { useState } from 'react';
import Layout from './components/Layout';
import TransactionList from './components/TransactionList';
import AddTransactionForm from './components/AddTransactionForm';

const App = () => {
    const [transactions, setTransactions] = useState([]);

    const addTransaction = (newTransaction) => {
        setTransactions([newTransaction, ...transactions]);
    };

    return (
        <Layout>
            <TransactionList transactions={transactions} />
            <AddTransactionForm onAddTransaction={addTransaction} />
        </Layout>
    );
};

export default App;
```

#### Passo 7: Executando a Aplicação
Execute a aplicação React para testar a carteira digital.

```bash
npm start
```

### Considerações Finais:
Este projeto prático oferece uma introdução completa ao desenvolvimento de uma carteira digital interativa utilizando ReactJS e TailwindCSS. Podemos expandir este projeto adicionando mais funcionalidades, como gráficos de análise de despesas, autenticação de usuário, integração com APIs externas para sincronização de dados financeiros, entre outros recursos avançados para proporcionar uma experiência completa de gerenciamento financeiro.
