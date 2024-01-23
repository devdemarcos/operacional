# Operacional
## Projeto para automação de pedido

import sqlite3

conexao = sqlite3.connect('meu_banco_de_dados.db')
cursor = conexao.cursor()


cursor.execute('''
    CREATE TABLE IF NOT EXISTS atendimentos (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        nome TEXT NOT NULL,
        numero TEXT NOT NULL
    )
''')

nome = input('Diga o nome do paciente: ')
numero = input('Numero do atendimento: ')
cursor.execute('''
    INSERT INTO atendimentos (nome, numero)
    VALUES (?, ?)
''', (nome, numero))

conexao.commit()

cursor.execute('''SELECT * FROM atendimentos''')
atendimentos = cursor.fetchall()
for atendimento in atendimentos:
    print(f'ID: {atendimento[0]}, Nome: {atendimento[1]}, Número: {atendimento[2]}')

# Fechar a conexão com o banco de dados
conexao.close()
