
class Pais:
    def __init__(self, cod_iso, nome,dimensao_km2,populacao,fronteiras):
        self.cod_iso = cod_iso
        self.nome = nome
        self.dimensao_km2 = dimensao_km2
        self.populacao = populacao
        self.fronteiras = fronteiras

    def get_iso(self):
        return self.cod_iso

    def igualdade_semantica(self, iso2):
        if self.cod_iso == iso2:
            return True
        else:
            return False
        

    def e_limitrofe(self, outro_pais):
        if self.nome in outro_pais:
            return True
        else:
            return False

    def vizinhos_comuns(self, vizinho1,vizinhos2):
        vizinhos_comuns = []
        for i in range(len(vizinho1)):
            if vizinho1[i] in vizinhos2:
                vizinhos_comuns.append(vizinho1[i])
        return vizinhos_comuns
        
    def calcular_dd(self, habitantes, area):
        dd = habitantes/area
        return dd
    def infos(self):
        print(f'[ISO: {self.cod_iso}]')
        print(f'[Nome: {self.nome}]')
        print(f'[População: {self.populacao}]')
        print(f'[Dimensão: {self.dimensao_km2}]')
        print(f'[Paises Vizinhos: {self.fronteiras}]')
brasil = Pais("BRA", "Brasil", 8515767.049, 209288278,["Argentina", "Bolívia", "Paraguai", "Peru", "Venezuela"])
dd_br = brasil.calcular_dd(brasil.populacao, brasil.dimensao_km2)
brasil.infos()
print('Densidade populacional: {:.2f}'.format(dd_br))
print(' ')

#URUGUAI
uruguai = Pais('URY','Uruguai',3426000,176215,['Brasil','Argentina']) 
dd_ury = uruguai.calcular_dd(uruguai.populacao,uruguai.dimensao_km2)
uruguai.infos()
print('Densidade populacional: {:.2f}'.format(dd_ury))
print(' ')

#PARAGUAI
paraguai = Pais('PRY','Paraguai',6704000,406752,['Brasil','Argentina','Bolívia'])
dd_pry = paraguai.calcular_dd(paraguai.populacao, paraguai.dimensao_km2)
paraguai.infos()
print('Densidade populacional: {:.2f}'.format(dd_pry))
vizinhos_c = paraguai.vizinhos_comuns(paraguai.fronteiras, uruguai.fronteiras)
print(vizinhos_c)
print(' ')

#ARGENTINA
argentina = Pais("ARG", "Argentina", 2780400,45195777,["Brasil", "Bolívia", "Chile", "Paraguai", "Uruguai"])
dd_arg = argentina.calcular_dd(argentina.populacao, argentina.dimensao_km2)
argentina.infos()
print('Densidade populacional: {:.2f}'.format(dd_arg))
print(' ')
vl = argentina.e_limitrofe(brasil.fronteiras) #Verificar se um país faz fronteira com outro
if vl == True:
    print(argentina.nome,'é limítrofe com',brasil.nome)
else:
    print('Países não limítrofes')


chile = Pais("CHL", "Chile", 756102, 19107216,["Argentina", "Bolívia", "Peru"])
dd_chl = chile.calcular_dd(chile.populacao, chile.dimensao_km2)
chile.infos()
print('Densidade populacional: {:.2f}'.format(dd_chl))
print(' ')
vl = chile.e_limitrofe(brasil.fronteiras) #Verificar se um país faz fronteira com outro
if vl == True:
    print(chile.nome,'é limítrofe com',brasil.nome)
else:
    print('Países não limítrofes')


#PAISES EUROPEUS
italia = Pais('ITA','Itália',59011000,301230,['França','Áustria','Suiça','Eslovênia',])
franca = Pais('FRA','França',67075000,551695,['Itália','Espanha','Luxemburgo','Bélgica','Alemanha','Mônaco','Andorra'])
luxem = Pais('LUX','Luxemburgo',640064,2586,['Alemanha','França','Bélgica'])
grecia = Pais('GRC','Grécia',10064000,131957,['Macedônia','Turquia','Albânia','Bulgária'])
hol = Pais('NLD','Holanda',17053000,41850,['Bélgica','Alemanha'])

class Continente:
    def __init__(self, nome, outros_pais):
        self.nome = nome
        self.outros_pais = outros_pais

    def adicionar_pais(self, outros_pais):
        self.outros_pais = outros_pais
    
    def dimensao_total(self, outros_pais):
        dimen_total = 0
        for i in range(len(outros_pais)):
            dimen_total += outros_pais[i].dimensao_km2
            return dimen_total
    
    def populacao_total(self, outros_pais):
        popu_total = 0
        for i in range(len(outros_pais)):
            popu_total += outros_pais[i].populacao
            return popu_total

    def maior_populacao(self, outros_pais):
        maior_populacao = 0
        maior_pais = str
        for i in range(len(outros_pais)):
            if maior_populacao < outros_pais[i].populacao:
                maior_populacao = outros_pais[i].populacao
                maior_pais = outros_pais[i].nome
            return maior_pais

    def menor_populacao(self, outros_pais):
        menor_populacao = 0
        menor_pais = str
        for i in range(len(outros_pais)):
            if menor_populacao > outros_pais[i].populacao or menor_populacao == 0:
                menor_populacao = outros_pais[i].populacao
                menor_pais = outros_pais[i].nome
            return menor_pais
        
    def maior_dimensao_territorial(self, outros_pais):
        maior_dim = 0
        maior_pais = str
        for i in range(len(outros_pais)):
            if maior_dim < outros_pais[i].dimensao_km2:
                maior_dim = outros_pais[i].dimensao_km2
                maior_pais = outros_pais[i].nome
            return maior_pais

    def menor_dimensao_territorial(self, outros_pais):
        menor_dim = 0
        menor_pais = str
        for i in range(len(outros_pais)):
            if menor_dim < outros_pais[i].dimensao_km2:
                menor_dim = outros_pais[i].dimensao_km2
                menor_pais = outros_pais[i].nome
            return menor_pais
        
    def razao_territorial(self, outros_pais):
        menor_dim = 0
        maior_dim = 0
        for i in range(len(outros_pais)):
            if menor_dim > outros_pais[i].dimensao_km2  or menor_dim == 0:
                menor_dim = outros_pais[i].dimensao_km2
            else:
                maior_dim = outros_pais[i].dimensao_km2

        r_t = maior_dim/menor_dim
        return r_t


#Criando um continente
ameSul = Continente("América do Sul",[])
america_sul = [brasil, uruguai, paraguai, argentina, chile]
ameSul.adicionar_pais(america_sul)

Euro = Continente('Europa',[])
euro = [italia,franca,luxem,grecia,hol]
Euro.adicionar_pais(euro)

print("[AMÉRICA DO SUL]")
maior_populacao = ameSul.maior_populacao(ameSul.outros_pais)
menor_populacao = ameSul.menor_populacao(ameSul.outros_pais)
maior_dimensão = ameSul.maior_dimensao_territorial(ameSul.outros_pais)
menor_dimensão = ameSul.menor_dimensao_territorial(ameSul.outros_pais)
pop_total = ameSul.populacao_total(ameSul.outros_pais)
di_total = ameSul.dimensao_total(ameSul.outros_pais)
razao_ter = ameSul.razao_territorial(ameSul.outros_pais)
print('Dimensão total do continente: ',di_total,'\nPopulação total do continente:',pop_total,'\nPaís com a maior população: ',maior_populacao,'\nPaís com a menor população: ',menor_populacao,'\nPaís com a maior dimensão territorial: ',maior_dimensão,'\nPaís com a menor dimensão territorial: ',menor_dimensão,'\nRazão territorial entre o maior e menor país do continente: {:.2f}'.format(razao_ter))
print(' ')

print('[EUROPA]')
maior_populacao = Euro.maior_populacao(Euro.outros_pais)
menor_populacao = Euro.menor_populacao(Euro.outros_pais)
maior_dimensão = Euro.maior_dimensao_territorial(Euro.outros_pais)
menor_dimensão = Euro.menor_dimensao_territorial(Euro.outros_pais)
pop_total = Euro.populacao_total(Euro.outros_pais)
di_total = Euro.dimensao_total(Euro.outros_pais)
razao_ter = Euro.razao_territorial(Euro.outros_pais)
print('Dimensão total do continente: ',di_total,'\nPopulação total do continente:',pop_total,'\nPaís com a maior população: ',maior_populacao,'\nPaís com a menor população: ',menor_populacao,'\nPaís com a maior dimensão territorial: ',maior_dimensão,'\nPaís com a menor dimensão territorial: ',menor_dimensão,'\nRazão territorial entre o maior e menor país do continente: {:.2f}'.format(razao_ter))
print(' ')

