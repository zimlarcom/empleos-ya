import datetime

# Fecha actual
hoy = datetime.datetime.now().strftime("%d/%m/%Y")

# Ofertas organizadas por categorías con enlaces monetizables / afiliados
ofertas = [
    {
        "titulo": "Asistente Virtual Bilingüe",
        "empresa": "Global Remote Inc.",
        "categoria": "remoto",
        "salario": "$1,200 USD / mes",
        "desc": "Soporte administrativo, gestión de agenda y correo en inglés. Horario flexible.",
        "link": "https://telegram.org"  # Aquí irá tu enlace de postulación o afiliado
    },
    {
        "titulo": "Ejecutivo de Atención al Cliente",
        "empresa": "Connect Center",
        "categoria": "atencion",
        "salario": "$850 USD / mes",
        "desc": "Respuesta a tickets y atención vía chat para clientes de habla hispana.",
        "link": "https://telegram.org"
    },
    {
        "titulo": "Desarrollador Web Junior (HTML/CSS)",
        "empresa": "DevStudio",
        "categoria": "tech",
        "salario": "$1,100 USD / mes",
        "desc": "Mantenimiento de páginas web y maquetación básica de sitios corporativos.",
        "link": "https://telegram.org"
    }
]

# Renderizado de empleos en HTML
html_empleos = ""
for op in ofertas:
    cat_badge = "Remoto" if op['categoria'] == 'remoto' else ("Tech" if op['categoria'] == 'tech' else "Atención")
    html_empleos += f"""
    <div class="job-card" data-category="{op['categoria']}">
        <div class="badge">{cat_badge}</div>
        <h3>{op['titulo']}</h3>
        <p class="company"><strong>{op['empresa']}</strong> | <span>{op['salario']}</span></p>
        <p class="desc">{op['desc']}</p>
        <a href="{op['link']}" target="_blank" class="btn-apply">Postularme / Ver Detalles</a>
    </div>
    """

# Código completo del HTML
html_contenido = f"""<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Empleos Ya - Portal Oficial</title>
    <style>
        * {{ box-sizing: border-box; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; }}
        body {{ margin: 0; background-color: #f4f6f9; color: #222; }}
        header {{ background: #0d47a1; color: white; padding: 25px 15px; text-align: center; }}
        header h1 {{ margin: 0; font-size: 26px; }}
        header p {{ margin: 5px 0 0; font-size: 14px; opacity: 0.9; }}
        
        .container {{ max-width: 800px; margin: 20px auto; padding: 0 15px; }}
        
        /* Banner Telegram */
        .telegram-banner {{ background: #0088cc; color: white; padding: 15px; border-radius: 10px; text-align: center; margin-bottom: 20px; }}
        .telegram-banner a {{ color: #fff; font-weight: bold; background: rgba(255,255,255,0.2); padding: 8px 15px; border-radius: 5px; text-decoration: none; display: inline-block; margin-top: 8px; }}
        
        /* Filtros */
        .filters {{ display: flex; gap: 8px; overflow-x: auto; padding-bottom: 10px; margin-bottom: 15px; }}
        .filter-btn {{ background: white; border: 1px solid #ccc; padding: 8px 14px; border-radius: 20px; font-size: 13px; font-weight: bold; cursor: pointer; white-space: nowrap; }}
        .filter-btn.active {{ background: #0d47a1; color: white; border-color: #0d47a1; }}
        
        /* Tarjetas de Trabajo */
        .job-card {{ background: white; padding: 18px; border-radius: 10px; margin-bottom: 15px; box-shadow: 0 2px 5px rgba(0,0,0,0.05); position: relative; }}
        .badge {{ position: absolute; top: 15px; right: 15px; background: #e3f2fd; color: #0d47a1; font-size: 11px; font-weight: bold; padding: 4px 8px; border-radius: 4px; }}
        .job-card h3 {{ margin: 0 0 6px 0; font-size: 18px; color: #111; }}
        .company {{ margin: 0 0 10px 0; font-size: 13px; color: #666; }}
        .desc {{ font-size: 14px; color: #444; line-height: 1.4; margin-bottom: 12px; }}
        .btn-apply {{ display: block; text-align: center; background: #2e7d32; color: white; text-decoration: none; padding: 10px; border-radius: 6px; font-weight: bold; font-size: 14px; }}
        
        /* Cursos y Afiliados */
        .courses-section {{ background: #fff3e0; border: 1px solid #ffe0b2; padding: 18px; border-radius: 10px; margin: 25px 0; }}
        .courses-section h3 {{ margin-top: 0; color: #e65100; }}
        .course-item {{ background: white; padding: 12px; border-radius: 6px; margin-top: 10px; display: flex; justify-content: space-between; align-items: center; }}
        .course-item a {{ background: #e65100; color: white; text-decoration: none; padding: 6px 12px; border-radius: 4px; font-size: 12px; font-weight: bold; }}
        
        /* Formulario Captura de Correo */
        .subscribe-box {{ background: #1565c0; color: white; padding: 20px; border-radius: 10px; text-align: center; margin-bottom: 30px; }}
        .subscribe-box input {{ width: 80%; padding: 10px; border-radius: 5px; border: none; margin-top: 10px; font-size: 14px; }}
        .subscribe-box button {{ background: #2e7d32; color: white; border: none; padding: 10px 20px; border-radius: 5px; margin-top: 8px; font-weight: bold; cursor: pointer; }}
        
        footer {{ text-align: center; padding: 20px; font-size: 12px; color: #777; }}
    </style>
</head>
<body>

    <header>
        <h1>Empleos Ya</h1>
        <p>Actualizado hoy: {hoy}</p>
    </header>

    <div class="container">

        <!-- Banner Telegram -->
        <div class="telegram-banner">
            📢 <strong>¡Recibe vacantes al instante en tu celular!</strong>
            <br>
            <a href="https://t.me" target="_blank">Unirme al Canal de Telegram</a>
        </div>

        <!-- Filtros Rápidos -->
        <div class="filters">
            <button class="filter-btn active" onclick="filterJobs('todos')">Todos</button>
            <button class="filter-btn" onclick="filterJobs('remoto')">100% Remoto</button>
            <button class="filter-btn" onclick="filterJobs('atencion')">Atención al Cliente</button>
            <button class="filter-btn" onclick="filterJobs('tech')">Tecnología</button>
        </div>

        <!-- Lista de Empleos -->
        <div id="job-list">
            {html_empleos}
        </div>

        <!-- Sección Monetización por Cursos / Afiliados -->
        <div class="courses-section">
            <h3>🎓 ¿Aumenta tus posibilidades de contratación</h3>
            <p style="font-size: 13px; color: #555;">Mejora tu CV con estos cursos recomendados con certificado:</p>
            
            <div class="course-item">
                <div>
                    <strong>Inglés Intensivo para Trabajos Remotos</strong>
                    <div style="font-size: 11px; color: #777;">Certificado en 30 días</div>
                </div>
                <a href="https://hotmart.com" target="_blank">Ver Curso</a>
            </div>
            
            <div class="course-item">
                <div>
                    <strong>Excel de Cero a Avanzado para Oficinas</strong>
                    <div style="font-size: 11px; color: #777;">Aprende las fórmulas clave</div>
                </div>
                <a href="https://hotmart.com" target="_blank">Ver Curso</a>
            </div>
        </div>

        <!-- Suscripción a Alertas -->
        <div class="subscribe-box">
            <h3>📩 Alertas Diarias en tu Correo</h3>
            <p style="font-size: 13px;">Déjanos tu email y te enviaremos las mejores ofertas de la semana.</p>
            <input type="email" placeholder="Tu correo electrónico aquí...">
            <br>
            <button onclick="alert('¡Gracias! Te has suscrito a las alertas diarias.')">Suscribirme Gratis</button>
        </div>

    </div>

    <footer>
        <p>&copy; {hoy} Empleos Ya - Todos los derechos reservados.</p>
    </footer>

    <script>
        function filterJobs(category) {{
            const cards = document.querySelectorAll('.job-card');
            const buttons = document.querySelectorAll('.filter-btn');
            
            buttons.forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');

            cards.forEach(card => {{
                if (category === 'todos' || card.getAttribute('data-category') === category) {{
                    card.style.display = 'block';
                }} else {{
                    card.style.display = 'none';
                }}
            }});
        }}
    </script>

</body>
</html>
"""

# Guardar index.html
with open("index.html", "w", encoding="utf-8") as f:
    f.write(html_contenido)

print("¡Portal interactivo y monetizable generado exitosamente!")
