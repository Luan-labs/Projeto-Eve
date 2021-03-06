# Projeto-Eve
from Bio.Seq import Seq
from funções import desligar
from funções import aminoácidos
from chatterbot.trainers import ListTrainer
from chatterbot import ChatBot


bot = ChatBot('Eve')

def sequencia():
	frase = str(input('Eve:digite a sequência a ser contada: '))
	palavra = str(input('Eve:nucleotídeo(s) a ser(em) contado(s): '))
	resultado = frase.count(palavra)

def nucleotídeos():
	s = str(input('Eve: digite a sequência de nucleotídeos:'))
	adenina = s.count("A")
	citosina = s.count("C")
	guanina = s.count("G")
	timina = s.count("T")

	print(adenina, citosina, guanina, timina)
	
def transcrição():
	t = str(input('Eve:insira a sequência de DNA:'))
	print (t.replace('T', 'U'))

def complementar():
	s = str(input('Eve:Insira a sequência complementar da fita de DNA:'))
	troca= {"A": "T",
	"T": "A",
	"G": "C",
	"C": "G"}
	s_complementar = [troca[nt] for nt in s]
	
	print(s_complementar)
	
	s_complementar = "".join(reversed(s_complementar))
	print(s_complementar)
	
def tradução():
	s = str(input('Eve: digite a sequência de RNA:'))
	mrna = Seq(s)
	print (mrna.translate())
	
def leitura1():
	arquivo = open('/storage/emulated/0/Download/sequences.csv', 'r')
	unica_string = arquivo.read()
	print(unica_string)
	arquivo.close()

conversa = ['oi', 'olá', 'tudo bem', 'tudo e você?','também', 'tranquilo',  'que bom', 'como se chama', 'nome feio', 'me chamo assim e pronto!', 'Bom dia', 'bom dia!', 'Boa tarde', 'ótimo!', 'Boa noite', 'a noite é uma criança!']
conversa2 = ['Ok', 'certo', 'vamos lá',]

bot.set_trainer(ListTrainer)
bot.train(conversa)
bot.train(conversa2)

name=input("Como você se chama?\n")
print("Eve: Olá %s!" % name)

while True:
	request=input(name+':')
	
	if request=='Bye' or request =='bye':
	       print('Eve: Bye')
	       break
	else:
	       response=bot.get_response(request)
	       print('Eve:',response)
			
	if request == ('desligar'):
		print('Ok, desligando')
		desligar()
	
	if request == ('tradução'):
		tradução()
	
	if request ==('sequência'):
		sequencia()
		
	if request ==('transcrição'):
		transcrição()
		
	if request ==('nucleotídeos'):
		nucleotídeos()
	
	if request ==('DNA complementar'):
		complementar()
		
	if request ==('leitura'):
		leitura1()
	
	if request ==('aminoácidos'):
		aminoácidos()
		
