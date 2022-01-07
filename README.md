#bibliotecaas
from random import randrange

def apresentacao():
    print("~" * 32)
    print("SEJA BEM VINDO AO JOGO DA FORCA!")
    print("~" * 32)

def definindo_nivel():
    print("(1) Fácil (2) Médio (3) Difícil")
    nivel = int(input("Em qual dificuldade deseja jogar? "))
    return nivel

def definindo_tema():
    temas = ["animais.txt", "frutas.txt", "verbos.txt", "adjetivos.txt"]
    anuncio_tema = ["ANIMAIS", "FRUTAS", "VERBOS", "ADJETIVOS"]
    n1 = randrange(0, 4)
    tema = temas[n1]
    print(f"###### TEMA:> {anuncio_tema[n1]} ######")
    return tema

def separando_palavras_por_nivel():
    palavras_facil = []
    palavras_medio = []
    palavras_dificil = []
    with open(tema) as arquivo:
        for palavra in arquivo:
            if len(palavra.strip()) <= 4:
                palavras_facil.append(palavra.strip().upper())
            elif len(palavra.strip()) >= 9:
                palavras_dificil.append(palavra.strip().upper())
            else:
                palavras_medio.append(palavra.strip().upper())
    return palavras_facil, palavras_medio, palavras_dificil

def escolhendo_palavra_por_dificuldade(nivel,palavras_facil,palavras_medio,palavras_dificil):
    if nivel == 1:
        n2 = randrange(0, len(palavras_facil))
        palavra_secreta = palavras_facil[n2]
    elif nivel == 2:
        n3 = randrange(0, len(palavras_medio))
        palavra_secreta = palavras_medio[n3]
    elif nivel == 3:
        n4 = randrange(0, len(palavras_dificil))
        palavra_secreta = palavras_dificil[n4]
    return palavra_secreta

def gerando_underlines(palavra_secreta):
    underlines_da_palavra = []
    contador1 = 0
    # se for uma palavra composta
    if "-" in palavra_secreta:
        for cada_letra in palavra_secreta:
            if cada_letra == "-":
                letras_da_palavra.append("-")
            else:
                letras_da_palavra.append("_")
            contador1 += 1
    # palavra normal
    else:
        letras_da_palavra = ["_" for cada_letra in palavra_secreta]
    print("~" * 50)
    print(letras_da_palavra)
    return letras_da_palavra

def chutes(palavra_secreta, underlines_da_palavra):
    ganhou = False
    perdeu = False
    erros = 0
    while not ganhou and not perdeu:
        chute = input("Digite uma letra: ").strip().upper()
        print("~" * 50)
        if chute in palavra_secreta:
            contador = 0
            for letra in palavra_secreta:
                if letra == chute:
                    underlines_da_palavra[contador] = letra
                contador += 1
            ganhou = '_' not in underlines_da_palavra
        else:
            erros += 1
            print("  _______     ")
            print(" |/      |    ")

            if (erros == 1):
                print(" |      (_)   ")
                print(" |            ")
                print(" |            ")
                print(" |            ")

            if (erros == 2):
                print(" |      (_)   ")
                print(" |      \     ")
                print(" |            ")
                print(" |            ")

            if (erros == 3):
                print(" |      (_)   ")
                print(" |      \|    ")
                print(" |            ")
                print(" |            ")

            if (erros == 4):
                print(" |      (_)   ")
                print(" |      \|/   ")
                print(" |            ")
                print(" |            ")

            if (erros == 5):
                print(" |      (_)   ")
                print(" |      \|/   ")
                print(" |       |    ")
                print(" |            ")

            if (erros == 6):
                print(" |      (_)   ")
                print(" |      \|/   ")
                print(" |       |    ")
                print(" |      /     ")

            if (erros == 7):
                print(" |      (_)   ")
                print(" |      \|/   ")
                print(" |       |    ")
                print(" |      / \   ")

            print(" |            ")
            print("_|___         ")
            print()
            print(f"Voce errou! Ainda tem {7 - erros} tentativas")
            perdeu = erros == 7

        print(underlines_da_palavra)
    return ganhou, perdeu

def vitoria():
    print("Parabéns, você ganhou!")
    print("       ___________      ")
    print("      '._==_==_=_.'     ")
    print("      .-\\:      /-.    ")
    print("     | (|:.     |) |    ")
    print("      '-|:.     |-'     ")
    print("        \\::.    /      ")
    print("         '::. .'        ")
    print("           ) (          ")
    print("         _.' '._        ")
    print("        '-------'       ")

def derrota(palavra_secreta):
    print("Puxa, você foi enforcado!")
    print("A palavra era {}".format(palavra_secreta))
    print("    _______________         ")
    print("   /               \       ")
    print("  /                 \      ")
    print("//                   \/\  ")
    print("\|   XXXX     XXXX   | /   ")
    print(" |   XXXX     XXXX   |/     ")
    print(" |   XXX       XXX   |      ")
    print(" |                   |      ")
    print(" \__      XXX      __/     ")
    print("   |\     XXX     /|       ")
    print("   | |           | |        ")
    print("   | I I I I I I I |        ")
    print("   |  I I I I I I  |        ")
    print("   \_             _/       ")
    print("     \_         _/         ")
    print("       \_______/           ")


#apresentacao
apresentacao()

#definindo nivel
nivel = definindo_nivel()

#sorteando palavra
#1 -
tema = definindo_tema()

#2 - separando palavras por nivel
palavras_facil, palavras_medio, palavras_dificil = separando_palavras_por_nivel()

# 3 - escolhendo lista de palavras por dificuldade
palavra_secreta = escolhendo_palavra_por_dificuldade(nivel,palavras_facil,palavras_medio,palavras_dificil)

#gerando underlines para usuario
underlines_da_palavra = gerando_underlines(palavra_secreta)

#chute do usuario
ganhou, perdeu = chutes(palavra_secreta, underlines_da_palavra)

if ganhou:
    vitoria()
elif perdeu:
    derrota(palavra_secreta)
