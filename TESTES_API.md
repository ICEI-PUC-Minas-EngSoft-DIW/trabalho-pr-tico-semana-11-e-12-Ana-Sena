# Guia de Testes da API - JSON Server

Este documento contém exemplos de testes para a entidade principal **espetaculos** usando requisições HTTP.

## URL Base
```
http://localhost:3000
```

## Endpoints Disponíveis

### Espetáculos
- `GET /espetaculos` - Lista todos os espetáculos
- `GET /espetaculos/:id` - Busca um espetáculo por ID
- `POST /espetaculos` - Cria um novo espetáculo
- `PUT /espetaculos/:id` - Atualiza um espetáculo completo
- `PATCH /espetaculos/:id` - Atualiza parcialmente um espetáculo
- `DELETE /espetaculos/:id` - Remove um espetáculo

---

## 1. TESTE GET - Listar Todos os Espetáculos

**Método:** `GET`  
**URL:** `http://localhost:3000/espetaculos`  
**Headers:** Não necessário

**Resultado Esperado:**
- Status: `200 OK`
- Body: Array com todos os espetáculos cadastrados

---

## 2. TESTE GET - Buscar Espetáculo por ID

**Método:** `GET`  
**URL:** `http://localhost:3000/espetaculos/1`  
**Headers:** Não necessário

**Resultado Esperado:**
- Status: `200 OK`
- Body: Objeto com os dados do espetáculo de ID 1

---

## 3. TESTE POST - Criar Novo Espetáculo

**Método:** `POST`  
**URL:** `http://localhost:3000/espetaculos`  
**Headers:** 
```
Content-Type: application/json
```

**Body (JSON):**
```json
{
  "nome": "Romeu e Julieta",
  "titulo": "Romeu e Julieta: A Tragédia de Shakespeare em Ballet",
  "resumo": "O ballet Romeu e Julieta é uma adaptação da famosa tragédia de William Shakespeare, com música de Sergei Prokofiev e coreografia de diversos coreógrafos ao longo dos anos.",
  "origens": "O ballet foi criado em 1935, com música composta por Sergei Prokofiev especialmente para a obra.",
  "trama": "A história narra o amor proibido entre Romeu e Julieta, membros de famílias rivais em Verona.",
  "coreografia": "A coreografia varia conforme a produção, mas geralmente mantém a essência dramática da obra original.",
  "legado": "Romeu e Julieta é um dos ballets mais populares e frequentemente apresentados no mundo.",
  "imagem": "assets/Img/romeu_julieta.jpeg",
  "mais_imagens": [
    {
      "id": 1,
      "imagem": "assets/Img/romeu-julieta/rj1.jpg"
    },
    {
      "id": 2,
      "imagem": "assets/Img/romeu-julieta/rj2.jpg"
    }
  ]
}
```

**Resultado Esperado:**
- Status: `201 Created`
- Body: Objeto criado com ID gerado automaticamente

---

## 4. TESTE PUT - Atualizar Espetáculo Completo

**Método:** `PUT`  
**URL:** `http://localhost:3000/espetaculos/1`  
**Headers:** 
```
Content-Type: application/json
```

**Body (JSON):**
```json
{
  "id": 1,
  "nome": "O Lago dos Cisnes - Edição Especial",
  "titulo": "O Lago dos Cisnes: conheça um dos ballets de repertório mais famosos do mundo",
  "resumo": "Em 4 de março de 1877, um novo balé estreou no Teatro Bolshoi em Moscou – O Lago dos Cisnes. Esta foi a primeira grande partitura de balé composta por Piotr Ilitch Tchaikovsky.",
  "origens": "Na verdade, não há evidências de onde surgiu a ideia do enredo de O Lago dos Cisnes, ou o que inspirou seu escritor.",
  "trama": "Como muitas histórias de amor poderosas, o balé mágico O Lago dos Cisnes tem uma narrativa clássica de amor trágico.",
  "coreografia": "O Lago dos Cisnes tem algumas das coreografias mais exclusivas e icônicas da história do balé.",
  "legado": "Muitas interpretações de O Lago dos Cisnes foram feitas. É hoje o balé mais apresentado no mundo.",
  "imagem": "assets/Img/swan_lake.jpeg",
  "mais_imagens": [
    {
      "id": 1,
      "imagem": "assets/Img/swan-lake/swanL1.jpg"
    }
  ]
}
```

**Resultado Esperado:**
- Status: `200 OK`
- Body: Objeto atualizado

---

## 5. TESTE DELETE - Remover Espetáculo

**Método:** `DELETE`  
**URL:** `http://localhost:3000/espetaculos/3`  
**Headers:** Não necessário

**Resultado Esperado:**
- Status: `200 OK`
- Body: Objeto vazio `{}`

**Nota:** Após deletar, ao fazer um GET no mesmo ID, deve retornar `404 Not Found`.

---

## Como Executar os Testes

### Opção 1: Postman
1. Instale o Postman: https://www.postman.com/downloads/
2. Abra o Postman
3. Crie uma nova requisição
4. Selecione o método HTTP (GET, POST, PUT, DELETE)
5. Digite a URL completa
6. Para POST e PUT, vá em "Body" > "raw" > selecione "JSON" e cole o JSON
7. Clique em "Send"
8. Tire um print da resposta

### Opção 2: Thunder Client (VS Code)
1. Instale a extensão "Thunder Client" no VS Code
2. Abra o Thunder Client no VS Code
3. Crie uma nova requisição
4. Selecione o método HTTP
5. Digite a URL
6. Para POST e PUT, vá em "Body" > "JSON" e cole o JSON
7. Clique em "Send"
8. Tire um print da resposta

### Opção 3: Insomnia
1. Instale o Insomnia: https://insomnia.rest/download
2. Abra o Insomnia
3. Crie uma nova requisição
4. Selecione o método HTTP
5. Digite a URL
6. Para POST e PUT, vá em "Body" > "JSON" e cole o JSON
7. Clique em "Send"
8. Tire um print da resposta

---

## Ordem Recomendada de Testes

1. **GET /espetaculos** - Verificar os dados iniciais
2. **GET /espetaculos/1** - Buscar um espetáculo específico
3. **POST /espetaculos** - Criar um novo espetáculo
4. **GET /espetaculos** - Verificar se o novo espetáculo foi adicionado
5. **PUT /espetaculos/1** - Atualizar um espetáculo
6. **GET /espetaculos/1** - Verificar se a atualização funcionou
7. **DELETE /espetaculos/3** - Deletar um espetáculo
8. **GET /espetaculos/3** - Verificar se foi deletado (deve retornar 404)

---

## Observações Importantes

- O JSON Server gera automaticamente IDs numéricos sequenciais para novos registros
- Ao fazer PUT, é necessário enviar TODOS os campos do objeto
- Ao fazer DELETE, o registro é removido permanentemente do arquivo db.json
- O servidor precisa estar rodando para os testes funcionarem
- Use o comando `npm start` para iniciar o servidor

