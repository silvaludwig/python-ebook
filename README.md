
# Python no Dia a Dia — 10 Automações Práticas para Economizar Horas de Trabalho
**Autor:** Ludwig Silva

---

## 📑 Sumário
1. Renomear Centenas de Arquivos de Uma Vez
2. Ler e Atualizar Planilhas Automaticamente
3. Baixar Imagens de um Site
4. Enviar E-mails Automáticos
5. Gerar Relatórios PDF
6. Monitorar Preço de Produtos
7. Converter CSV para Excel
8. Organizar Arquivos por Tipo e Data
9. Extrair Texto de PDFs
10. Agendar Execução de Scripts

---

## ✨ Introdução
A automação com Python pode transformar horas de trabalho repetitivo em minutos.  
Este e-book reúne 10 scripts práticos para você aplicar hoje mesmo, sem complicação.

---

## 1️⃣ Renomear Centenas de Arquivos de Uma Vez
**O que faz:** renomeia todos os arquivos de uma pasta usando um padrão definido.

```python
import os

pasta = r'C:\\caminho\\para\\pasta'
for i, nome in enumerate(os.listdir(pasta), start=1):
    extensao = os.path.splitext(nome)[1]
    novo_nome = f'arquivo_{i}{extensao}'
    os.rename(os.path.join(pasta, nome), os.path.join(pasta, novo_nome))
```

💡 **Dica extra:** combine com `datetime` para incluir a data no nome do arquivo.

---

## 2️⃣ Ler e Atualizar Planilhas Automaticamente
**O que faz:** lê um Excel, calcula novos valores e salva o resultado.

```python
import pandas as pd

df = pd.read_excel('vendas.xlsx')
df['Total'] = df['Quantidade'] * df['Preço Unitário']
df.to_excel('vendas_atualizado.xlsx', index=False)
```

🔗 **Link útil:** [Documentação do Pandas](https://pandas.pydata.org/)

---

## 3️⃣ Baixar Imagens de um Site
**O que faz:** extrai links de imagens e faz o download.

```python
import requests
from bs4 import BeautifulSoup
import os

url = 'https://exemplo.com'
html = requests.get(url).text
soup = BeautifulSoup(html, 'html.parser')

os.makedirs('imagens', exist_ok=True)
for img in soup.find_all('img'):
    src = img.get('src')
    if src:
        img_data = requests.get(src).content
        nome_arquivo = os.path.join('imagens', os.path.basename(src))
        with open(nome_arquivo, 'wb') as f:
            f.write(img_data)
```

💡 **Dica extra:** use `asyncio` para baixar várias imagens simultaneamente.

---

## 4️⃣ Enviar E-mails Automáticos
**O que faz:** envia e-mails via Gmail sem abrir navegador.

```python
import smtplib
from email.mime.text import MIMEText

msg = MIMEText("Corpo do e-mail")
msg['Subject'] = 'Assunto'
msg['From'] = 'seuemail@gmail.com'
msg['To'] = 'destinatario@gmail.com'

with smtplib.SMTP_SSL('smtp.gmail.com', 465) as server:
    server.login('seuemail@gmail.com', 'SUA_SENHA')
    server.send_message(msg)
```

⚠ **Atenção:** use senhas de app do Google para mais segurança.

---

## 5️⃣ Gerar Relatórios PDF
**O que faz:** cria PDFs com textos e tabelas.

```python
from reportlab.lib.pagesizes import A4
from reportlab.pdfgen import canvas

c = canvas.Canvas("relatorio.pdf", pagesize=A4)
c.drawString(100, 800, "Relatório de Vendas")
c.save()
```

💡 **Dica extra:** combine com Pandas para inserir dados automaticamente.

---

## 6️⃣ Monitorar Preço de Produtos
**O que faz:** coleta preços de páginas de produto.

```python
import requests
from bs4 import BeautifulSoup

url = 'https://exemplo.com/produto'
html = requests.get(url).text
soup = BeautifulSoup(html, 'html.parser')

preco = soup.find(class_='preco').text
print(f"Preço atual: {preco}")
```

---

## 7️⃣ Converter CSV para Excel
**O que faz:** converte `.csv` em `.xlsx`.

```python
import pandas as pd

df = pd.read_csv('dados.csv')
df.to_excel('dados.xlsx', index=False)
```

---

## 8️⃣ Organizar Arquivos por Tipo e Data
**O que faz:** separa arquivos em pastas por extensão.

```python
import os
import shutil

pasta = 'downloads'
for arquivo in os.listdir(pasta):
    extensao = os.path.splitext(arquivo)[1].replace('.', '')
    destino = os.path.join(pasta, extensao)
    os.makedirs(destino, exist_ok=True)
    shutil.move(os.path.join(pasta, arquivo), os.path.join(destino, arquivo))
```

---

## 9️⃣ Extrair Texto de PDFs
**O que faz:** lê PDFs e extrai texto.

```python
import pdfplumber

with pdfplumber.open("documento.pdf") as pdf:
    for pagina in pdf.pages:
        print(pagina.extract_text())
```

---

## 🔟 Agendar Execução de Scripts
**O que faz:** roda scripts em horários definidos.

```python
import schedule
import time

def tarefa():
    print("Executando tarefa!")

schedule.every().day.at("10:00").do(tarefa)

while True:
    schedule.run_pending()
    time.sleep(1)
```

---

## 📌 Conclusão
Com esses 10 exemplos, você já pode automatizar tarefas e economizar muito tempo.  
O próximo passo é **adaptar** cada código à sua necessidade e **escalar** as automações.

💬 **Call to Action:** Me siga no [Instagram](https://instagram.com/eu_ludwig) e [LinkedIn](https://linkedin.com/silvaludwig) para mais conteúdos sobre programação e automação.

---
