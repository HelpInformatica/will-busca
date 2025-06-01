# will-busca
Assistente virtual que pesquisa na Internet com voz
import wikipedia
import pywhatkit
import pyttsx3

# Configurar voz
voz = pyttsx3.init()
voz.setProperty('rate', 160)  # Velocidade da fala
voz.setProperty('volume', 1.0)  # Volume da fala

def falar(texto):
    print("Will Busca:", texto)
    voz.say(texto)
    voz.runAndWait()

def will_busca():
    falar("Olá! Eu sou o Will Busca. O que você quer que eu pesquise?")

    while True:
        comando = input("Você: ")

        if comando.lower() in ["sair", "exit", "tchau"]:
            falar("Até a próxima! Tchau!")
            break

        if "pesquisa" in comando or "procure" in comando:
            termo = comando.replace("pesquisa", "").replace("procure", "").strip()
            falar(f"Procurando sobre {termo} na Wikipédia.")
            try:
                resultado = wikipedia.summary(termo, sentences=2, auto_suggest=False)
                falar(resultado)
            except:
                falar("Não encontrei na Wikipédia. Vou abrir no Google.")
                pywhatkit.search(termo)
        else:
            falar("Não entendi. Tente dizer 'pesquisa sobre ...' ou 'procure ...'")

# Iniciar o assistente
will_busca()
