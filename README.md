# juegocar
#es un juego de competencia  de 2
import pygame , random


class enemigos:
    def acelerar1(self,cuanto=0)-> None:
        self.velocidad += 10 + cuanto
    def frenar1(self,cuanto=0)-> None:
        self.velocidad -= 10 + cuanto
    def avanzar1(self):
        self.lat += (self.velocidad/100)+5
        pass
    def retroceder1(self):
        self.lat -= (self.velocidad/100)+5
        pass
    def __init__(self,velocidad=0,lat=0.0,lon=300.0,modelo="",ppu="",color="") -> None:
        self.velocidad = velocidad
        self.lat = lat
        self.lon = lon
        self.modelo = modelo
        self.ppu = ppu
        self.color= color
    def __str__(self)->str:
        return (f'El vehiculo {self.modelo} patente {self.ppu} color {self.color} va a {self.velocidad} km/h')
class Vehiculo:
    def acelerar(self,cuanto=0)-> None:
        self.velocidad += 10 + cuanto
    def frenar(self,cuanto=0)-> None:
        self.velocidad -= 10 + cuanto
    def avanzar(self):
        self.lat += (self.velocidad/100)+5
        pass
    def retroceder(self):
        self.lat -= (self.velocidad/100)+5
        pass
    def __init__(self,velocidad=0,lat=0.0,lon=450.0,modelo="",ppu="",color="") -> None:
        self.velocidad = velocidad
        self.lat = lat
        self.lon = lon
        self.modelo = modelo
        self.ppu = ppu
        self.color= color
    def __str__(self)->str:
        return (f'El vehiculo {self.modelo} patente {self.ppu} color {self.color} va a {self.velocidad} km/h')
class Carretera: 
    ejex = 0.0
    ejey = 0.0
carretera = Carretera()
objeto = Vehiculo()
objeto2= enemigos()




pygame.init()
ventana = pygame.display.set_mode((1024,900))
enemigo= pygame.image.load('./carr.png').convert_alpha()
autito = pygame.image.load('./auto.png').convert_alpha()
fondo = pygame.image.load('./fondo.png').convert_alpha()



while(True):
    for event in pygame.event.get():
        if(event.type== pygame.KEYDOWN and event.key == pygame.K_d):
            objeto.acelerar()
            objeto.avanzar()
            print(objeto)    
        if(event.type== pygame.KEYDOWN and event.key == pygame.K_a):
            objeto.frenar()
            objeto.retroceder() 
            print(objeto)  
        if(event.type== pygame.KEYDOWN and event.key == pygame.K_w):
            objeto.lon -= 10
            pass
        if(event.type== pygame.KEYDOWN and event.key == pygame.K_s):
            objeto.lon += 10
            pass
        if(event.type== pygame.KEYDOWN and event.key == pygame.K_RIGHT):
            objeto2.acelerar1()
            objeto2.avanzar1()
            print(objeto2)
        if(event.type== pygame.KEYDOWN and event.key == pygame.K_LEFT):
            objeto2.frenar1()
            objeto2.retroceder1()
            print(objeto2)  
        if(event.type== pygame.KEYDOWN and event.key == pygame.K_DOWN):
            objeto2.lon +=10
            pass
        if(event.type== pygame.KEYDOWN and event.key == pygame.K_UP):
            objeto2.lon -= 10
            pass
        if(event.type == pygame.QUIT):
            pygame.quit()
            exit()
        if(event.type== pygame.KEYDOWN and event.key == pygame.K_ESCAPE):
            pygame.quit()
            quit()
        elif(objeto.lat >= objeto2.lat and objeto.lat <= objeto2.lat + 100 and objeto.lon >= objeto2.lon and objeto.lon <= objeto2.lon + 100):
            print("colision")
            pygame.quit()
            quit()
        
        if(objeto.lat >= 700):
            objeto.lat = 0
        if(objeto.lat <= 0):
            objeto.lat = 100
        if(objeto.lon >= 500):
            objeto.lon = 0
        if(objeto.lon <= 0):
            objeto.lon = 500    
        if(objeto2.lat >= 700):
            objeto2.lat = 0
        if(objeto2.lat <= 0):
            objeto2.lat = 100
        if(objeto2.lon >= 500):
            objeto2.lon = 0
        if(objeto2.lon <= 0):
            objeto2.lon = 500 
        
            
    carretera.ejex -= objeto.velocidad/100
    carretera.ejex -= objeto2.velocidad/100
    if(carretera.ejex<-500):
        carretera.ejex = 0
    ventana.blit(fondo,(carretera.ejex,carretera.ejey))
    ventana.blit(autito,(objeto.lat,objeto.lon))
    ventana.blit(enemigo,(objeto2.lat,objeto2.lon))
    
    
    pygame.display.update() 
