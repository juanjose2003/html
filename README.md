<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mapa Mental - Componentes del Back-End</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
        }

        h1 {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 30px;
            font-size: 2.5em;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }

        .mindmap {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 30px;
            margin-top: 20px;
        }

        .central-node {
            background: linear-gradient(45deg, #ff6b6b, #ee5a24);
            color: white;
            padding: 25px;
            border-radius: 50%;
            text-align: center;
            font-size: 1.8em;
            font-weight: bold;
            width: 200px;
            height: 200px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 10px 30px rgba(238, 90, 36, 0.4);
            transform: scale(1);
            transition: all 0.3s ease;
            position: relative;
            z-index: 10;
        }

        .central-node:hover {
            transform: scale(1.1);
            box-shadow: 0 15px 40px rgba(238, 90, 36, 0.6);
        }

        .branch {
            background: white;
            border-radius: 15px;
            padding: 20px;
            min-width: 280px;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
            cursor: pointer;
            border-left: 5px solid;
        }

        .branch:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 35px rgba(0, 0, 0, 0.15);
        }

        .branch.servers { border-left-color: #3498db; }
        .branch.databases { border-left-color: #e74c3c; }
        .branch.languages { border-left-color: #f39c12; }
        .branch.frameworks { border-left-color: #2ecc71; }
        .branch.apis { border-left-color: #9b59b6; }
        .branch.auth { border-left-color: #e67e22; }
        .branch.sessions { border-left-color: #1abc9c; }

        .branch-title {
            font-size: 1.4em;
            font-weight: bold;
            margin-bottom: 15px;
            color: #2c3e50;
        }

        .branch-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease;
        }

        .branch.active .branch-content {
            max-height: 500px;
        }

        .sub-item {
            background: #f8f9fa;
            margin: 8px 0;
            padding: 12px;
            border-radius: 8px;
            border-left: 3px solid;
            transition: all 0.3s ease;
        }

        .sub-item:hover {
            background: #e9ecef;
            transform: translateX(5px);
        }

        .sub-item.popular {
            background: linear-gradient(45deg, #ffeaa7, #fdcb6e);
            font-weight: bold;
        }

        .sub-item h4 {
            color: #2c3e50;
            margin-bottom: 5px;
            font-size: 1.1em;
        }

        .sub-item p {
            color: #636e72;
            font-size: 0.9em;
            line-height: 1.4;
        }

        .servers .sub-item { border-left-color: #3498db; }
        .databases .sub-item { border-left-color: #e74c3c; }
        .languages .sub-item { border-left-color: #f39c12; }
        .frameworks .sub-item { border-left-color: #2ecc71; }
        .apis .sub-item { border-left-color: #9b59b6; }
        .auth .sub-item { border-left-color: #e67e22; }
        .sessions .sub-item { border-left-color: #1abc9c; }

        .toggle-btn {
            background: #74b9ff;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 20px;
            cursor: pointer;
            font-size: 0.9em;
            margin-top: 10px;
            transition: background 0.3s ease;
        }

        .toggle-btn:hover {
            background: #0984e3;
        }

        .info-panel {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 20px;
            border-radius: 15px;
            margin-top: 30px;
            text-align: center;
        }

        .highlight {
            background: linear-gradient(45deg, #fdcb6e, #e17055);
            color: white;
            padding: 3px 8px;
            border-radius: 15px;
            font-weight: bold;
            font-size: 0.9em;
        }

        @media (max-width: 768px) {
            .mindmap {
                flex-direction: column;
                align-items: center;
            }
            
            .central-node {
                width: 150px;
                height: 150px;
                font-size: 1.4em;
            }
            
            .branch {
                min-width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🔧 Componentes del Back-End</h1>
        
        <div class="mindmap">
            <div class="central-node">
                BACK-END<br>
                <small style="font-size: 0.6em;">Arquitectura del Servidor</small>
            </div>
            
            <div class="branch servers" onclick="toggleBranch(this)">
                <div class="branch-title">🌐 Servidores Web</div>
                <button class="toggle-btn">Ver Detalles</button>
                <div class="branch-content">
                    <div class="sub-item popular">
                        <h4>Apache HTTP Server</h4>
                        <p>Servidor web más popular mundialmente. Arquitectura basada en procesos/hilos. Excelente compatibilidad y flexibilidad con módulos.</p>
                    </div>
                    <div class="sub-item popular">
                        <h4>Nginx</h4>
                        <p>Servidor web de alto rendimiento. Arquitectura orientada a eventos. Ideal para sitios con alto tráfico y como proxy reverso.</p>
                    </div>
                    <div class="sub-item">
                        <h4>Microsoft IIS</h4>
                        <p>Servidor web de Microsoft para Windows. Integración nativa con tecnologías .NET y Active Directory.</p>
                    </div>
                    <div class="sub-item">
                        <h4>LiteSpeed</h4>
                        <p>Servidor web comercial de alto rendimiento. Compatible con Apache pero más eficiente en recursos.</p>
                    </div>
                </div>
            </div>

            <div class="branch databases" onclick="toggleBranch(this)">
                <div class="branch-title">🗄️ Bases de Datos</div>
                <button class="toggle-btn">Ver Detalles</button>
                <div class="branch-content">
                    <div class="sub-item">
                        <h4><span class="highlight">Relacionales (SQL)</span></h4>
                        <p>Estructura tabular con relaciones definidas</p>
                    </div>
                    <div class="sub-item popular">
                        <h4>MySQL</h4>
                        <p>Base de datos relacional más popular. Open source, rápida y confiable para aplicaciones web.</p>
                    </div>
                    <div class="sub-item popular">
                        <h4>PostgreSQL</h4>
                        <p>Base de datos objeto-relacional avanzada. Soporte para JSON, arrays y funciones complejas.</p>
                    </div>
                    <div class="sub-item">
                        <h4>SQL Server</h4>
                        <p>Base de datos empresarial de Microsoft. Herramientas avanzadas de análisis y reporting.</p>
                    </div>
                    <div class="sub-item">
                        <h4><span class="highlight">No Relacionales (NoSQL)</span></h4>
                        <p>Estructura flexible para datos no estructurados</p>
                    </div>
                    <div class="sub-item popular">
                        <h4>MongoDB</h4>
                        <p>Base de datos de documentos. Almacena datos en formato JSON/BSON. Escalabilidad horizontal.</p>
                    </div>
                    <div class="sub-item">
                        <h4>Redis</h4>
                        <p>Base de datos en memoria. Ideal para caché, sesiones y aplicaciones en tiempo real.</p>
                    </div>
                </div>
            </div>

            <div class="branch languages" onclick="toggleBranch(this)">
                <div class="branch-title">💻 Lenguajes Back-End</div>
                <button class="toggle-btn">Ver Detalles</button>
                <div class="branch-content">
                    <div class="sub-item popular">
                        <h4>JavaScript (Node.js)</h4>
                        <p>Lenguaje unificado front-end y back-end. Event-driven, ideal para aplicaciones en tiempo real.</p>
                    </div>
                    <div class="sub-item popular">
                        <h4>Python</h4>
                        <p>Lenguaje versátil y legible. Excelente para desarrollo web, IA y análisis de datos.</p>
                    </div>
                    <div class="sub-item popular">
                        <h4>PHP</h4>
                        <p>Lenguaje especializado en desarrollo web. Fácil integración con HTML y bases de datos.</p>
                    </div>
                    <div class="sub-item">
                        <h4>Java</h4>
                        <p>Lenguaje robusto y multiplataforma. Ideal para aplicaciones empresariales escalables.</p>
                    </div>
                    <div class="sub-item">
                        <h4>C#</h4>
                        <p>Lenguaje de Microsoft para el ecosistema .NET. Fuertemente tipado y orientado a objetos.</p>
                    </div>
                    <div class="sub-item">
                        <h4>Ruby</h4>
                        <p>Lenguaje elegante y expresivo. Filosofía de "programador feliz" con sintaxis intuitiva.</p>
                    </div>
                </div>
            </div>

            <div class="branch frameworks" onclick="toggleBranch(this)">
                <div class="branch-title">🚀 Frameworks</div>
                <button class="toggle-btn">Ver Detalles</button>
                <div class="branch-content">
                    <div class="sub-item popular">
                        <h4>Laravel (PHP)</h4>
                        <p>Framework elegante con sintaxis expresiva. ORM Eloquent, sistema de plantillas Blade.</p>
                    </div>
                    <div class="sub-item popular">
                        <h4>Django (Python)</h4>
                        <p>Framework "batteries included". Admin panel automático, ORM potente y seguridad integrada.</p>
                    </div>
                    <div class="sub-item popular">
                        <h4>Express.js (Node.js)</h4>
                        <p>Framework minimalista y flexible. Perfecto para APIs REST y aplicaciones web ligeras.</p>
                    </div>
                    <div class="sub-item">
                        <h4>Ruby on Rails (Ruby)</h4>
                        <p>Framework con convenciones sobre configuración. Desarrollo rápido siguiendo principios DRY.</p>
                    </div>
                    <div class="sub-item">
                        <h4>Spring Boot (Java)</h4>
                        <p>Framework empresarial con configuración automática. Microservicios y aplicaciones robustas.</p>
                    </div>
                    <div class="sub-item">
                        <h4>ASP.NET Core (C#)</h4>
                        <p>Framework moderno de Microsoft. Multiplataforma, alto rendimiento y arquitectura modular.</p>
                    </div>
                </div>
            </div>

            <div class="branch apis" onclick="toggleBranch(this)">
                <div class="branch-title">🔌 APIs</div>
                <button class="toggle-btn">Ver Detalles</button>
                <div class="branch-content">
                    <div class="sub-item popular">
                        <h4>REST API</h4>
                        <p>Arquitectura basada en HTTP. Métodos GET, POST, PUT, DELETE. Stateless y cacheable.</p>
                    </div>
                    <div class="sub-item">
                        <h4>GraphQL</h4>
                        <p>Lenguaje de consulta para APIs. Cliente especifica exactamente qué datos necesita.</p>
                    </div>
                    <div class="sub-item">
                        <h4>SOAP</h4>
                        <p>Protocolo basado en XML. Más formal y estructurado, ideal para servicios empresariales.</p>
                    </div>
                    <div class="sub-item">
                        <h4>gRPC</h4>
                        <p>Framework RPC de alto rendimiento de Google. Usa Protocol Buffers y HTTP/2.</p>
                    </div>
                    <div class="sub-item">
                        <h4>WebSockets</h4>
                        <p>Comunicación bidireccional en tiempo real. Ideal para chat, gaming y aplicaciones colaborativas.</p>
                    </div>
                </div>
            </div>

            <div class="branch auth" onclick="toggleBranch(this)">
                <div class="branch-title">🔐 Autenticación/Autorización</div>
                <button class="toggle-btn">Ver Detalles</button>
                <div class="branch-content">
                    <div class="sub-item">
                        <h4>Autenticación</h4>
                        <p>Verificación de identidad del usuario (¿quién eres?)</p>
                    </div>
                    <div class="sub-item">
                        <h4>Autorización</h4>
                        <p>Control de permisos y acceso (¿qué puedes hacer?)</p>
                    </div>
                    <div class="sub-item popular">
                        <h4>JWT (JSON Web Tokens)</h4>
                        <p>Tokens stateless para autenticación. Contiene información codificada y firmada digitalmente.</p>
                    </div>
                    <div class="sub-item">
                        <h4>OAuth 2.0</h4>
                        <p>Protocolo de autorización. Permite acceso limitado sin compartir credenciales.</p>
                    </div>
                    <div class="sub-item">
                        <h4>SAML</h4>
                        <p>Estándar para intercambio de datos de autenticación. Usado en Single Sign-On (SSO).</p>
                    </div>
                    <div class="sub-item">
                        <h4>Multi-Factor Authentication</h4>
                        <p>Seguridad adicional con múltiples factores de verificación (2FA/MFA).</p>
                    </div>
                </div>
            </div>

            <div class="branch sessions" onclick="toggleBranch(this)">
                <div class="branch-title">🍪 Sesiones y Cookies</div>
                <button class="toggle-btn">Ver Detalles</button>
                <div class="branch-content">
                    <div class="sub-item">
                        <h4><span class="highlight">Sesiones</span></h4>
                        <p>Almacenamiento temporal de datos del usuario en el servidor</p>
                    </div>
                    <div class="sub-item">
                        <h4>Session Storage</h4>
                        <p>Datos almacenados en memoria del servidor. Se pierden al cerrar sesión o expirar.</p>
                    </div>
                    <div class="sub-item">
                        <h4>Session ID</h4>
                        <p>Identificador único que conecta cliente con datos de sesión en servidor.</p>
                    </div>
                    <div class="sub-item">
                        <h4><span class="highlight">Cookies</span></h4>
                        <p>Pequeños archivos almacenados en el navegador del usuario</p>
                    </div>
                    <div class="sub-item">
                        <h4>HTTP Cookies</h4>
                        <p>Datos enviados entre cliente y servidor en cada petición HTTP.</p>
                    </div>
                    <div class="sub-item">
                        <h4>Secure Cookies</h4>
                        <p>Cookies con flags de seguridad: HttpOnly, Secure, SameSite para prevenir ataques.</p>
                    </div>
                    <div class="sub-item">
                        <h4>Cookie Expiration</h4>
                        <p>Control de tiempo de vida: session cookies vs persistent cookies.</p>
                    </div>
                </div>
            </div>
        </div>

        <div class="info-panel">
            <h3>💡 Información Adicional</h3>
            <p>Este mapa mental presenta los componentes esenciales del Back-End en 2025. <strong>Haz clic en cada sección</strong> para explorar los detalles de cada componente. Los elementos marcados como "populares" representan las tecnologías más utilizadas actualmente en la industria.</p>
        </div>
    </div>

    <script>
        function toggleBranch(branch) {
            // Cerrar todas las otras ramas
            const allBranches = document.querySelectorAll('.branch');
            allBranches.forEach(b => {
                if (b !== branch) {
                    b.classList.remove('active');
                }
            });
            
            // Toggle la rama actual
            branch.classList.toggle('active');
            
            // Actualizar texto del botón
            const btn = branch.querySelector('.toggle-btn');
            if (branch.classList.contains('active')) {
                btn.textContent = 'Ocultar Detalles';
            } else {
                btn.textContent = 'Ver Detalles';
            }
        }

        // Animación inicial
        window.addEventListener('load', function() {
            const branches = document.querySelectorAll('.branch');
            branches.forEach((branch, index) => {
                setTimeout(() => {
                    branch.style.opacity = '0';
                    branch.style.transform = 'translateY(20px)';
                    setTimeout(() => {
                        branch.style.transition = 'all 0.5s ease';
                        branch.style.opacity = '1';
                        branch.style.transform = 'translateY(0)';
                    }, 50);
                }, index * 100);
            });
        });

        // Efecto de hover en sub-items
        document.querySelectorAll('.sub-item').forEach(item => {
            item.addEventListener('mouseenter', function() {
                this.style.transform = 'translateX(5px) scale(1.02)';
            });
            
            item.addEventListener('mouseleave', function() {
                this.style.transform = 'translateX(0) scale(1)';
            });
        });
    </script>
</body>
</html>
