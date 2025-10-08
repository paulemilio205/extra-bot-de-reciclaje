import discord
from discord.ext import commands
import random
import os

# Emojis para las tragamonedas
emojis = ["🍒", "🍋", "🍉", "⭐", "🍇", "🔔", "💎"]


frases = [
    "💡 Nunca es tarde para empezar de nuevo.",
    "🔥 Si puedes soñarlo, puedes lograrlo.",
    "🚀 El éxito es la suma de pequeños esfuerzos repetidos cada día.",
    "🌟 Cree en ti, incluso cuando nadie más lo haga.",
    "💪 Las grandes cosas toman tiempo, sé paciente.",
    "🌈 Cada día es una nueva oportunidad."
]

datos = [
    "Los pulpos tienen tres corazones.",
    "La miel nunca caduca, se han encontrado tarros de miel de miles de años en buen estado.",
    "Las vacas tienen mejores amigas y se estresan cuando se separan.",
    "Un día en Venus dura más que un año en Venus.",
    "Los flamencos nacen grises, se vuelven rosados por su alimentación.",
    "Los tiburones existen desde antes que los árboles."
]

chistes = [
    "¿Por qué el libro de matemáticas se deprimió? Porque tenía demasiados problemas.",
    "¿Qué le dice una impresora a otra? —¿Esa hoja es tuya o es una impresión mía?",
    "¿Cómo se dice pañuelo en japonés? Saka-moko.",
    "¿Por qué la computadora fue al médico? ¡Porque tenía un virus!",
    "¿Qué hace una abeja en el gimnasio? ¡Zum-ba!",
    "Oye ¿tú estudias derecho? No, yo estudio sentado."
]


def flip_coin():
    flip = random.randint(0, 2)
    if flip == 0:
        return "cara"
    else:
        return "cruz"

intents = discord.Intents.default()
intents.message_content = True

bot = commands.Bot(command_prefix='$', intents=intents)

@bot.event
async def on_ready():
    print(f'We have logged in as {bot.user}')

@bot.command()
async def hola(ctx):
    await ctx.send(f'Hola, soy un bot {bot.user}!')

@bot.command()
async def heh(ctx, count_heh = 5):
    await ctx.send("he" * count_heh)

@bot.command()
async def cara_o_cruz(ctx):
    await ctx.send(flip_coin())

@bot.command()
async def adios(ctx):
    await ctx.send("Adios que te valla bien",)

@bot.command()
async def pilas(ctx):
    await ctx.send("ponlas en un bote rojo",)

@bot.command()
async def plastico(ctx):
    await ctx.send("tiralo en un bote cafe",)

@bot.command()
async def botellas(ctx):
    await ctx.send("depende si es de plastico a el bote blanco si es cristal al bote gris y si es carton o papel a el bote azul",)

@bot.command()
async def metal(ctx):
    await ctx.send("ponlas en un bote amarillo",)

@bot.command()
async def limpieza(ctx):
    await ctx.send("en el bote negro",)

@bot.command()
async def boteazul(ctx):
    await ctx.send("es el bote donde van los plasticos y el carton",)

@bot.command()
async def boteverde(ctx):
    await ctx.send("es el bote donde va el vidrio",)

@bot.command()
async def boteamarillo(ctx):
    await ctx.send("es el bote donde van los metales",)

@bot.command()
async def boteblanco(ctx):
    await ctx.send("es el bote donde van los plasticos",)

@bot.command()
async def botecafe(ctx):
    await ctx.send("donde van las cosas organicas",)

@bot.command()
async def boterojo(ctx):
    await ctx.send("es el bote dende van los residuos peligrosos",)

@bot.command()
async def botenegro(ctx):
    await ctx.send("bote donde van las cosas que no estan mencionadas en los otros botes",)







@bot.command()
async def chiste(ctx):
    await ctx.send(random.choice(chistes))

@bot.command()
async def dato(ctx):
    await ctx.send(random.choice(datos))

    
@bot.command()
async def frase(ctx):
    await ctx.send(random.choice(frases))
 
@bot.command()
async def meme(ctx):
    with open(r'M1L4/foto/meme1.jpg', 'rb') as f:
        picture = discord.File(f)
    
    await ctx.send(file = picture)

@bot.event
async def on_member_join(member):
    # Buscar canal llamado "bienvenida"
    channel = discord.utils.get(member.guild.text_channels, name="bienvenida")
    if channel:
        await channel.send(f"🎉 Bienvenido/a {member.mention} al servidor **{member.guild.name}**!🚀 ")

@bot.command()
async def slots(ctx):
    slot1 = random.choice(emojis)
    slot2 = random.choice(emojis)
    slot3 = random.choice(emojis)

    resultado = f"| {slot1} | {slot2} | {slot3} |"

    if slot1 == slot2 == slot3:
        await ctx.send(f"🎰 {resultado} 🎰\n🎉 ¡Jackpot {ctx.author.mention}! Ganaste 🎉")
    elif slot1 == slot2 or slot2 == slot3 or slot1 == slot3:
        await ctx.send(f"🎰 {resultado} 🎰\n✨ Casi lo logras {ctx.author.mention}, dos iguales ✨")
    else:
        await ctx.send(f"🎰 {resultado} 🎰\n😢 Mala suerte {ctx.author.mention}, inténtalo de nuevo.")




bot.run("tu toke aqui  :)")
