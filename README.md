# 🧾 Projeto To Do Board — React + Tailwind

Este projeto tem como objetivo ensinar o desenvolvimento de uma aplicação web de lista de tarefas utilizando **React**, **Tailwind CSS** e princípios de componentização. Ao final da prática, você será capaz de:

- Criar e utilizar componentes com `props`
- Gerenciar estado com `useState`
- Manipular arrays em React (`push`, `splice`, `spread`, etc.)
- Aplicar estilização com Tailwind
- Entender a estrutura e o fluxo de uma aplicação React moderna

---

## ✅ Pré-requisitos

Antes de começar, você deve ter:

- Node.js instalado
- Familiaridade básica com HTML, CSS e JavaScript
- Conceitos básicos de React (JSX, componentes, props)

---

## 🛠️ Passo a passo de desenvolvimento

### 1. Criação do projeto com Vite

```bash
npm create vite@latest
cd todo-board
npm install
```

### Instalação e configuração do Tailwind CSS

```bash
npm install tailwindcss @tailwindcss/vite
```

No arquivo vite.config.js, configure:

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [
    react(),
    tailwindcss()  
  ],
})

```

No arquivo src/App.css:

```css
@import "tailwindcss";
```

No index.html, adicione:

```html
<link href="/src/App.css" rel="stylesheet">
```

### Estrutura final do projeto

```bash
src/
├── App.jsx
├── main.jsx
├── styles.css
└── components/
    ├── Board.jsx
    └── Input.jsx
public/
└── index.html
```

### Código fonte 

📌 main.jsx — ponto de entrada da aplicação

```jsx
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import App from './App.jsx';

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```
⚙️ Este é o ponto onde o React conecta a aplicação à DOM. O StrictMode ajuda a identificar problemas potenciais.

📌 App.jsx — componente principal da aplicação

```jsx
import { useState } from "react";
import Board from "./components/Board";
import Input from "./components/Input";

// Componente principal da aplicação
function App() {
  const [taskList, setTaskList] = useState([]); // Estado para armazenar a lista de tarefas

  return (
    <div className="flex flex-col items-center justify-center py-8 gap-4">
      {/* Título do aplicativo */}
      <h1 className="text-xl font-semibold">🧾 - To Do Board</h1>
      
      {/* Componente de input para adicionar novas tarefas */}
      <Input taskList={taskList} setTaskList={setTaskList} />
      
      {/* Exibe as tarefas como uma lista de Boards */}
      <div className="flex flex-wrap justify-center gap-4">
        {taskList.map((task, index) => (
          <Board
            key={index} // Chave única para cada item
            index={index} // Índice da tarefa atual
            task={task} // Texto da tarefa
            taskList={taskList} // Lista completa de tarefas
            setTaskList={setTaskList} // Função para atualizar a lista
          />
        ))}
      </div>
    </div>
  );
}

export default App;
```
🔄 Este componente controla o estado global das tarefas e renderiza os componentes Input (para adicionar) e Board (para listar/excluir).

Input.jsx - adiciona novas tarefas

```jsx
import { useState } from "react";

// Componente que contém o input e botão para adicionar novas tarefas
const Input = ({ taskList, setTaskList }) => {
  const [input, setInput] = useState(""); // Estado para armazenar o valor atual do input

  // Função que adiciona uma nova tarefa à lista
  const handleAddTask = (e) => {
    e.preventDefault(); // Evita recarregamento da página
    setTaskList([...taskList, input]); // Adiciona a nova tarefa à lista existente
    setInput(""); // Limpa o campo de input
  };

  return (
    <form className="flex flex-row items-center gap-3">
      {/* Campo de texto para digitar nova tarefa */}
      <input
        type="text"
        className="border rounded-lg px-2.5 py-1.5 text-lg"
        placeholder="Add a new task"
        value={input}
        onChange={(e) => setInput(e.target.value)} // Atualiza o estado conforme digita
      />
      
      {/* Botão para adicionar tarefa */}
      <button
        onClick={handleAddTask}
        className="bg-violet-400 text-white py-2 px-3.5 rounded-lg font-semibold hover:opacity-70"
      >
        Add
      </button>
    </form>
  );
};

export default Input;

```

Board.jsx - card de tarefa com botão de remoção

```jsx
// Componente responsável por exibir uma tarefa individual e um botão para deletá-la
const Board = ({ task, index, taskList, setTaskList }) => {
  // Função que remove a tarefa atual da lista, com base no índice
  const handleDelete = () => {
    const novaLista = [...taskList]; // Cria uma cópia da lista original
    novaLista.splice(index, 1); // Remove a tarefa no índice atual
    setTaskList(novaLista); // Atualiza o estado com a nova lista
  };

  return (
    <div className="max-w-md rounded-xl flex flex-col items-center justify-start border text-center text-lg pt-3 pb-4 px-4 md:px-6">
      {/* Exibe o texto da tarefa */}
      <p>{task}</p>
      
      {/* Botão para deletar a tarefa atual */}
      <button
        className="bg-red-500 text-white rounded-lg py-1 px-2 mt-4"
        onClick={handleDelete}
      >
        Delete
      </button>
    </div>
  );
};

export default Board;
```
🗑️ Este componente exibe a tarefa e um botão para removê-la. O splice() remove a tarefa da cópia da lista, e o estado é atualizado.

### 🎨 Estilização com Tailwind CSS
Tailwind facilita o layout com classes utilitárias. Exemplos:

- flex, gap-4, items-center para alinhamento
- rounded-lg, bg-violet-400, text-white para estilo visual
- max-w-md para limitar a largura dos cards
- hover:opacity-70 para efeito visual no botão

### 🧠 Conceitos abordados

- Estado com useState: controle dinâmico da lista de tarefas
- Componentes reutilizáveis: Input e Board podem ser usados em outras aplicações
- Props: comunicação entre componentes
- Manipulação de arrays em React: spread, splice, map
- Tailwind: estilização rápida e responsiva

### 🧩 Sugestões de melhorias

- Impedir adição de tarefas em branco
- Editar tarefas após adicionadas
- Marcar como "feito"
- Salvar tarefas com localStorage
- Adicionar categorias e filtros
- Usar uuid em vez de índice como chave

### 📚 Para aprofundar

- React Docs
- Tailwind Docs
