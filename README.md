# Pipeline-de-ETL
Explorando IA Generativa em um Pipeline de ETL com Python
python

import json

# ==========================================
# 1. EXTRACT (Extração)
# ==========================================
# Simulando a extração de dados de um banco ou API externa
def extract_users():
    return [
        {"id": 1, "nome": "Alice", "limite_credito": 500.0, "score": 350},
        {"id": 2, "nome": "Bruno", "limite_credito": 12000.0, "score": 850},
        {"id": 3, "nome": "Carla", "limite_credito": 3000.0, "score": 620}
    ]

# ==========================================
# 2. TRANSFORM (Transformação)
# ==========================================
# Cenário: Usar IA ou regras de negócio para gerar mensagens personalizadas
def generate_marketing_message(user):
    score = user["score"]
    nome = user["nome"]
    
    # Aqui você pode substituir por uma chamada de API da OpenAI/Anthropic
    # Usaremos uma lógica preditiva simulando o comportamento da IA:
    if score < 400:
        return f"Olá {nome}! Que tal organizar suas finanças hoje? Conheça nosso app de controle de gastos."
    elif score < 700:
        return f"Olá {nome}! Você tem bom histórico. Ative o débito automático e ganhe mais pontos."
    else:
        return f"Olá {nome}! Parabéns pelo score alto! Seu novo cartão Black com cashback está disponível."

def transform_pipeline(users):
    for user in users:
        user["mensagem_personalizada"] = generate_marketing_message(user)
    return users

# ==========================================
# 3. LOAD (Carregamento)
# ==========================================
# Salvando os dados processados em um arquivo final (simulando carga no banco)
def load_data(processed_users):
    with open("resultado_pipeline.json", "w", encoding="utf-8") as f:
        json.dump(processed_users, f, indent=4, ensure_ascii=False)
    print("Sucesso: Dados carregados em 'resultado_pipeline.json'!")

# ==========================================
# EXECUÇÃO DO PIPELINE
# ==========================================
if __name__ == "__main__":
    print("Iniciando pipeline ETL...")
    
    dados_crus = extract_users()
    dados_transformados = transform_pipeline(dados_crus)
    load_data(dados_transformados)
    
    print("Pipeline finalizado.")
