# SIRIEMA
class PerfilLitologico:
    def __init__(self, tipo_aquifero):
        self.tipo_aquifero = tipo_aquifero
        self.perfil = []

    def adicionar_litologia(self, litologia, limite_inferior):
        self.perfil.append({"Litologia": litologia, "Limite Inferior (m)": limite_inferior})

    def __str__(self):
        perfil_str = f"Tipo de Aquífero: {self.tipo_aquifero}\n"
        for item in self.perfil:
            perfil_str += f"  {item['Litologia']}: {item['Limite Inferior (m)']} m\n"
        return perfil_str


class PerfilConstrutivo:
    def __init__(self, profundidade_injecao, espessura_laje, area_laje, altura_tubulacao, cota_terreno, metodo_perfuracao):
        self.profundidade_injecao = profundidade_injecao
        self.espessura_laje = espessura_laje
        self.area_laje = area_laje
        self.altura_tubulacao = altura_tubulacao
        self.cota_terreno = cota_terreno
        self.metodo_perfuracao = metodo_perfuracao
        self.diametros_perfuracao = []
        self.selo_sanitario = None
        self.tubulacao = None

    def adicionar_diametro_perfuracao(self, diametro, limite_inferior):
        self.diametros_perfuracao.append({"Diâmetro (pol)": diametro, "Limite Inferior (m)": limite_inferior})

    def adicionar_selo_sanitario(self, material, limite_inferior):
        self.selo_sanitario = {"Material": material, "Limite Inferior (m)": limite_inferior}

    def adicionar_tubulacao(self, material, tipo, diametro, limite_inferior, instalou_prefiltro):
        self.tubulacao = {
            "Material da Tubulação": material,
            "Tipo": tipo,
            "Diâmetro (pol)": diametro,
            "Limite Inferior (m)": limite_inferior,
            "Instalou pré-filtro": instalou_prefiltro
        }

    def __str__(self):
        perfil_str = (
            f"Profundidade do ponto de injeção: {self.profundidade_injecao} m\n"
            f"Espessura da laje de proteção sanitária: {self.espessura_laje} cm\n"
            f"Área da laje de proteção sanitária: {self.area_laje} m²\n"
            f"Altura da boca da tubulação: {self.altura_tubulacao} cm\n"
            f"Cota do terreno: {self.cota_terreno} m\n"
            f"Método de Perfuração do Poço: {self.metodo_perfuracao}\n"
        )
        perfil_str += "Diâmetros da Perfuração:\n"
        for diametro in self.diametros_perfuracao:
            perfil_str += f"  {diametro['Diâmetro (pol)']} pol: {diametro['Limite Inferior (m)']} m\n"
        
        perfil_str += "Selo Sanitário:\n"
        if self.selo_sanitario:
            perfil_str += f"  Material: {self.selo_sanitario['Material']}\n"
            perfil_str += f"  Limite Inferior (m): {self.selo_sanitario['Limite Inferior (m)']} m\n"
        
        perfil_str += "Tubulação:\n"
        if self.tubulacao:
            perfil_str += f"  Material da Tubulação: {self.tubulacao['Material da Tubulação']}\n"
            perfil_str += f"  Tipo: {self.tubulacao['Tipo']}\n"
            perfil_str += f"  Diâmetro (pol): {self.tubulacao['Diâmetro (pol)']}\n"
            perfil_str += f"  Limite Inferior (m): {self.tubulacao['Limite Inferior (m)']} m\n"
            perfil_str += f"  Foi instalado pré-filtro? {'Sim' if self.tubulacao['Instalou pré-filtro'] else 'Não'}\n"

        return perfil_str


# Exemplo de uso:
perfil_litologico = PerfilLitologico("Poroso Livre")
perfil_litologico.adicionar_litologia("Solo", 0)
perfil_litologico.adicionar_litologia("Basalto não desmoronável", 12)

perfil_construtivo = PerfilConstrutivo(20.3, 5, 100, 0.5, 49, "Ro-topneumático")
perfil_construtivo.adicionar_diametro_perfuracao(20, 0)
perfil_construtivo.adicionar_selo_sanitario("Calda de cimento", 20)
perfil_construtivo.adicionar_tubulacao("Aço galvanizado", "Revestimento", 8, 100, True)

# Impressão dos perfis
print("Perfil Litológico:")
print(perfil_litologico)

print("\nPerfil Construtivo:")
print(perfil_construtivo)
