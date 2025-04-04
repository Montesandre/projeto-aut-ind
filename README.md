# **Modbus-API: Seu CLP Agora Fala HTTP!** 

**Descrição:**  
Uma API em Flask que faz a ponte entre requisições HTTP e um CLP via **Modbus TCP**, permitindo **ler** e **escrever** registros de forma simples e rápida.  

🔌 **Conecte seu CLP ao mundo web** sem dor de cabeça!  

---

## **📦 Pré-requisitos**  
- **Python 3.8+** (mas roda em versões mais novas também)  
- **Bibliotecas:**  
  ```bash
  pip install flask pyModbusTCP
  ```
- **CLP compatível com Modbus TCP** (testado no **Codesys 3.5**)  
- **Insomnia/Postman** (para testar as requisições)  

---

## **⚙️ Configuração**  

### **1. Conexão Modbus TCP**  
O código já vem configurado para:  
- **Host:** `localhost` (mude para o IP do seu CLP)  
- **Porta:** `502` (padrão do Modbus)  
- **Unit ID:** `1` (se o seu CLP usar outro, ajuste!)  

```python
c = ModbusClient(host="localhost", port=502, unit_id=1, auto_open=True)
```

---

## **🚀 Rotas da API**  

### **📥 `POST /read` – Lê 3 registros a partir do 40001**  
**Exemplo de resposta:**  
```json
{
  "40001": 42,
  "40002": 150,
  "40003": 75
}
```
**O que acontece?**  
1. Abre conexão com o CLP  
2. Lê **3 registros** (40001, 40002, 40003)  
3. Retorna os valores em **JSON**  
4. Fecha a conexão  

---

### **📤 `POST /write` – Escreve em 3 registros a partir do 40004**  
**Exemplo de corpo da requisição:**  
```json
{
  "40004": 100,
  "40005": 200,
  "40006": 300
}
```
**Resposta:**  
- `"escrita OK"` → Se tudo der certo ✅  
- `"write error"` → Se algo der errado ❌  

**O que acontece?**  
1. Recebe um JSON com os valores  
2. Abre conexão com o CLP  
3. Escreve nos registros **40004, 40005, 40006**  
4. Fecha a conexão  

---

## **🔌 Testando no Insomnia**  

1. **Instale o [Insomnia](https://insomnia.rest/)** (ou use Postman)  
2. **Importe as rotas:**  
   - `POST http://localhost:5000/read` (sem corpo)  
   - `POST http://localhost:5000/write` (com JSON no corpo)  

---

## **💡 Por Que Isso É Incrível?**  
✅ **Fácil integração** com sistemas web, mobile ou IoT  
✅ **Padrão industrial (Modbus) + HTTP (REST)** = Combinação poderosa  
✅ **Prototipagem rápida** – Em minutos você já tem uma API funcional!  
✅ **Monitoramento remoto** – Acesse dados do CLP de qualquer lugar  

---

## **⚠️ Cuidados Importantes**  
🔒 **Não exponha essa API direto na internet** (use autenticação se necessário)  
📉 **Evite muitas requisições seguidas** – CLPs não são servidores web!  
🔧 **Trate erros** – Sempre verifique se a conexão foi bem-sucedida  

---

## **🎯 Autor**  
 **André Monteiro** 

---



