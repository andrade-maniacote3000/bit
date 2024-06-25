from urllib import request
import discord
from discord.ext import commands
import random 
import os
import requests

intents = discord.Intents.default()
intents.message_content = True

bot = commands.Bot(command_prefix='$', intents=intents)

@bot.event
async def on_ready():
    print(f'We have logged in as {bot.user}')

@bot.command()
async def hello(ctx):
    await ctx.send(f'Hola, soy un bot {bot.user}!')

@bot.command()
async def heh(ctx, count_heh = 5):
    await ctx.send("he" * count_heh)

@bot.command()
async def elefantes(ctx, num1:int, num2:int ):
    resultado = num1 - num2
    await ctx.send(resultado)

@bot.command()
async def moneda(ctx):
    caras=["cara",
           "sello"]
    await ctx.send(random.choice(caras))


@bot.command()
async def repeat(ctx, times:int, content='repeating...'):
    """Repeats a menssage multiple times."""
    for i in range(times):
        await ctx.send(content)

@bot.command()
async def mem(ctx):
    img_name=random.choice(os.listdir('LA GRANDE'))
    with open(f'LA GRANDE/{img_name}', 'rb') as f:
        picture = discord.File(f)
    await ctx.send(file=picture)

def get_dog_image_url():    
    url = 'https://random.dog/woof.json'
    res = requests.get(url)
    data = res.json()
    return data['url']


@bot.command('dog')
async def dog(ctx):
    image_url = get_dog_image_url()
    await ctx.send(image_url)


@bot.command()
async def chimbumpapas(ctx, otra):
    chim=["piedra", "papel", "tijera"]
    await ctx.send(random.choice(chim))

@bot.command()
async def manualidades(ctx):
    usos=["ladrillos ecologicos",
           "usar botellas como macetas",
           "reciclar los plasticos de las botelllas triturandolos para usarlos como rastrillos de escoba"
           ]
    await ctx.send(random.choice(usos))

@bot.command()
async def clasificacion(ctx,*,item:str):
    reciclables=["botella de plastico", "papel", "lata", "desechos toxicos"]
    no_reciclable=["pañales","comida", "metal", "desechos fecales"]
    if item.lower() in reciclables:
        await ctx.send("reciclable.")
    elif item.lower() in no_reciclable:
        await ctx.send("no reciclable.")
    else:
        await ctx.send("hasta allí no llego.")

bot.run("")
