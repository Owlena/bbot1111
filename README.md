# bbot1111
import discord 
from discord.ext import commands
import os
import random
import requests

print(os.listdir('memes'))

intents = discord.Intents.default()
intents.message_content = True

bot = commands.Bot(command_prefix='^', intents=intents)

def get_fox_image_url():    
    url = 'https://randomfox.ca/floof/'
    res = requests.get(url)
    data = res.json()
    return data['url']

def get_woof_image_url():    
    url = 'https://random.dog/woof.json'
    res = requests.get(url)
    data = res.json()
    return data['url']

def get_duck_image_url():    
    url = 'https://random-d.uk/api/random'
    res = requests.get(url)
    data = res.json()
    return data['url']

@bot.event
async def on_ready():
    print(f'Подключtн {bot.user}')

@bot.command()
async def mem(ctx):
    with open('memes/mem1.jpg', 'rb') as f:
        picture = discord.File(f)
    await ctx.send(file=picture)

@bot.command()
async def mems(ctx):
    img_name = random.choice(os.listdir('memes'))
    with open(f'memes/{img_name}', 'rb') as f:
        picture = discord.File(f)
    await ctx.send(file=picture)

@bot.command('fox')
async def fox(ctx):
    '''По команде duck вызывает функцию get_duck_image_url'''
    image_url = get_fox_image_url()
    await ctx.send(image_url)



@bot.command('duck')
async def duck(ctx):
    image_url = get_duck_image_url()
    await ctx.send(image_url)




@bot.command('woof')
async def woof(ctx):
    image_url = get_woof_image_url()
    await ctx.send(image_url)


bot.run('MTIwODY5MTU5MjYzOTI4MzIwMA.GeW5uI.clY4FZwxJGzTf5GmmHuUHOdEBiu7-HoS7Jr5s8')



