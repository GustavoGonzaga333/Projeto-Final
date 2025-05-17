# Crud Python SQLITE3🚀
[Projeto DE SISTEMA.pptx](https://github.com/user-attachments/files/20265541/Projeto.DE.SISTEMA.pptx)
[Uploading projetofinal1.py…]()# VAMOS COMPLETAR A INTERFACE GRÁFICA...
import sqlite3 # banco de dados
import tkinter as tk # interface basica
from tkinter import messagebox # caixas de mensagens
from tkinter import ttk # interface grafica tb

def conectar():
    return sqlite3.connect('teste.db')
# criar o banco (connect)

def criar_tabela():
    conn = conectar()
    c= conn.cursor()
    c.execute('''
        CREATE TABLE IF NOT EXISTS usuarios(
        RA INTEGER NOT NULL,
        aluno TEXT NOT NULL,
        email_inst TEXT NOT NULL              
        )       
    ''')
    conn.commit()
    conn.close()
  


# CREATE
def inserir_aluno():
    RA = entry_RA.get()
    aluno = entry_aluno.get()
    email_inst =  entry_email_inst.get()

    if aluno and email_inst:
        conn = conectar()
        c = conn.cursor()
        c.execute('INSERT INTO usuarios(aluno,email_inst,RA) VALUES(?,?,?)', (aluno, email_inst,RA))
        conn.commit()
        conn.close()
        messagebox.showinfo('AVISO', 'ALUNO INSERIDO COM SUCESSO!') 
        mostrar_usuario()
    else:
        messagebox.showerror('ERRO', 'ALGO DEU ERRADO!') 

# READ
def mostrar_aluno():
    for row in tree.get_children():   
        tree.delete(row)
    conn = conectar()
    c = conn.cursor()    
    c.execute('SELECT * FROM usuarios')
    usuarios = c.fetchall()
    for usuario in usuarios:
        tree.insert("", "end", values=(usuario[0], usuario[1],usuario[2]))
    conn.close()    


# DELETE
def delete_aluno():
    dado_del = tree.selection()
    if dado_del:
       user_id = tree.item(dado_del)['values'][0]
       conn = conectar()
       c = conn.cursor()    
       c.execute('DELETE FROM usuarios WHERE RA = ? ',(user_RA,))
       conn.commit()
       conn.close()
       messagebox.showinfo('', 'DADO DELETADO')
       mostrar_usuario()

    else:
       messagebox.showerror('', 'OCORREU UM ERRO')  

# UPDATE 
       
def editar():
     selecao = tree.selection()
     if selecao:
         user_RA = tree.item(selecao)['values'][0]
         novo_aluno = entry_nome.get()
         novo_email_inst = entry_email.get()

         if novo_aluno and novo_email_inst:
            conn = conectar()
            c = conn.cursor()    
            c.execute('UPDATE usuarios SET aluno = ? , email_inst = ? WHERE RA = ? ',(novo_aluno,novo_email_inst,user_RA))
            conn.commit()
            conn.close()  
            messagebox.showinfo('', 'DADOS ATUALIZADOS')
            mostrar_usuario()

         else:
             messagebox.showwarning('', 'PREENCHA TODOS OS CAMPOS')

     else:
            messagebox.showerror('','ALGO DEU ERRADO!')


# VAMOS COMPLETAR A INTERFACE GRÁFICA...
# 1
janela = tk.Tk()
janela.title('PAINEL DE CONTROLE DE ALUNOS')

label_aluno = tk.Label(janela, text='aluno:')
label_aluno.grid(row=0, column=0, padx=10, pady=10)
entry_aluno = tk.Entry(janela)
entry_aluno.grid(row=0, column=1, padx=10, pady=10)

label_email_inst = tk.Label(janela, text='email_inst:')
label_email_inst.grid(row=1, column=0, padx=10, pady=10)
entry_email_inst = tk.Entry(janela)
entry_email_inst.grid(row=1, column=1, padx=10, pady=10)


label_RA = tk.Label(janela, text='RA:')
label_RA.grid(row=2, column=0, padx=10, pady=10)

entry_RA = tk.Entry(janela, text='RA:')
entry_RA.grid(row=2, column=1, padx=10, pady=10)



# botões

btn_salvar = tk.Button(janela, text='SALVAR',command=inserir_aluno)
btn_salvar.grid(row = 3, column=0, padx=10, pady=10  )

btn_deletar = tk.Button(janela, text='DELETAR',command=delete_aluno)
btn_deletar.grid(row = 3, column=1, padx=10, pady=10  )

btn_atualizar = tk.Button(janela, text='ATUALIZAR',command=editar)
btn_atualizar.grid(row = 3, column=2, padx=10, pady=10  )

# arvore
columns = ('RA','aluno', 'email_inst')

tree = ttk.Treeview(janela, columns=columns, show='headings')
tree.grid(row=6, column=0,columnspan=2, padx=10, pady=10 )

for col in columns:
    tree.heading(col, text=col)

criar_tabela()
mostrar_aluno()


janela.mainloop()

Um parágrafo da descrição do projeto vai aqui

# 🔌Como fazer funcionar na sua máquina:

- Instale Python na sua máquina;

# 📋Pré-requisitos do sistema:

> PYTHON 3.13
> 

## 🛠️Tecnologias utilizadas:

> Visual studio code
> Python
Bibliotecas
> TKINTER
> SQLITE 3

## Versões:

> Python 3.13
> 

## Autores:

> Gustavo Gonzaga de Oliveira
>
