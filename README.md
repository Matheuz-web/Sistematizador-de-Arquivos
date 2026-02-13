# Sistematizador-de-Arquivos
Criei um sistematizador de arquivos que cria pastas para a organização de extensões.

# Este script move arquivos de uma pasta para subpastas baseadas na extensão, ex: .jpg para imagens, e por ai vai

# Primeiros vamos usar algumas bibliotecas

import os
# "operating system" linguagem de maquina para listar, separar e criar novas pastas.

import shutil
# "shell utilities" para manipulação de arquivos.

import time
# para o scrip não consumir 100% da cpu

# Abaixo será especificado as extensoes de cada grupo a ser organizado.

def organizar_pasta(caminho):
    diretorios = {
        'imagens': ['.jps', '.png', '.gif'],
        'documentos': ['.pdf', '.docx', '.txt'],
        'executaveis': ['.exe', '.msi'],
    }

    if not os.path.exists(caminho):
        print('Caminho não encontrado!')
        return
# essa linha de codigo impede que o script dê erro e retorna a pedir um novo caminho para organização de arquivos.

    for arquivo in os.listdir(caminho):
        nome, extensao = os.path.splitext(arquivo)
        for pasta, extensoes in diretorios.items():
            if extensao.lower() in extensoes:
                pasta_destino = os.path.join(caminho, pasta)
                os.makedirs(pasta_destino, exist_ok=True)
                shutil.move(os.path.join(caminho, arquivo), os.path.join(pasta_destino, arquivo))

def monitorar(caminho):
    global rodando
    while rodando:
        organizar_pasta(caminho)
        time.sleep(5)
# Verifica a cada 5 segundos a pasta.

if __name__ == '__main__':
    pasta_alvo = input('Digite o caminho da pasta para organizar: ')
    input('Procurando a pasta... pressione ENTER para parar.')
    rodando = False
    print('Busca Interrompida com sucesso!')
    # linha pra tornar a teclada ENTER um catalizador pro script.

# No fim para utilizar o script, basta copiar o caminho de algum arquivo e colar assim que rodar o codigo.
