from datetime import datetime

# Fecha actual para mantener el portal fresco cada día
hoy = datetime.now().strftime("%d de %B de %Y")

# Lista de vacantes dinámicas (aquí puedes programar el script para que 
# en el futuro busque en APIs de empleo gratuitas o bases de datos)
ofertas = [
    {
        "titulo": "Asistente Virtual Bilingüe (Remoto)",
        "empresa": "Global Solutions",
        "modalidad": "Remoto",
        "salario": "$1,200 - $1,500 USD",
        "desc": "Soporte administrativo diario, manejo de agendas y atención a clientes internacionales en inglés."
    },
    {
        "titulo": "Analista de Datos Junior",
        "empresa": "TechCorp Latam",
        "modalidad": "Híbrido",
        "salario": "Competitivo",
        "desc": "Manejo de bases de datos en la nube, limpieza de información y reportes operativos diarios."
    },
    {
        "titulo": "Redactor de Contenidos SEO",
        "empresa": "Digital Media Group",
        "modalidad": "100% Remoto",
        "salario": "Por proyecto",
        "desc": "Creación de artículos optimizados para buscadores y gestión de publicaciones semanales."
    }
]

# Construir el listado de empleos de forma automática en HTML
html_empleos = ""
for empleo in ofertas:
    html_empleos += f"""
        <div class="job">
            <h3>{empleo['titulo']}</h3>
            <p><strong>Empresa:</strong> {empleo['empresa']} | <strong>Modalidad:</strong> {empleo['modalidad']} | <strong>Salario:</strong> {empleo['salario']}</p>
            <p>{empleo['desc']}</p>
            <a href="#" class="btn">Postularme ahora</a>
        </div>
    """

# Estructura completa de la página web
html_contenido = f"""
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Empleos Ya - Ofertas Diarias</title>
    <style>
        body {{ font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; margin: 0; padding: 20px; background: #f4f4f9; color: #333; }}
        .container {{ max-width: 800px; margin: auto; background: white; padding: 25px; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.05); }}
        h1 {{ color: #0066cc; font-size: 26px; margin-bottom: 5px; }}
        .subtitle {{ color: #666; font-size: 14px; margin-bottom: 20px; }}
        .job {{ border-bottom: 1px solid #eaeaea; padding: 20px 0; }}
        .job:last-child {{ border-bottom: none; }}
        .job h3 {{ margin: 0 0 8px 0; color: #111; }}
        .job p {{ margin: 6px 0; font-size: 14px; color: #555; }}
        .btn {{ background: #28a745; color: white; padding: 10px 18px; text-decoration: none; border-radius: 6px; display: inline-block; margin-top: 10px; font-weight: bold; font-size: 14px; }}
        .btn:hover {{ background: #218838; }}
    </style>
</head>
<body>
    <div class="container">
        <h1>Empleos Ya - Oportunidades Diarias</h1>
        <div class="subtitle">Portal actualizado automáticamente el: <strong>{hoy}</strong></div>
        <hr style="border:0; border-top: 1px solid #eee;">
        
        {html_empleos}
        
    </div>
</body>
</html>
"""

# Sobrescribir el archivo index.html automáticamente
with open("index.html", "w", encoding="utf-8") as f:
    f.write(html_contenido)

print("¡Portal de empleos actualizado y generado con éxito!")

No pierdas la oportunidad de mejorar tu vida,no importa que tan lento vayas, llegarás lejos
