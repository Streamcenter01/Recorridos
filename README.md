<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>SegurApp Recorridos</title>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <style>
        :root {
            --bg-principal: #000000;
            --bg-tarjeta: #121212;
            --bg-input: #1a1a1a;
            --neon-verde: #ff1e27; /* Rojo deportivo principal */
            --neon-cian: #ffffff;    /* Blanco puro para contraste de realces */
            --neon-rosa: #e50914;    /* Rojo secundario/alerta oscuro */
            --texto-principal: #ffffff;
            --texto-secundario: #a0a0a0; /* Gris plata */
            --borde-sutil: rgba(255, 255, 255, 0.1);
            --fuente: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            -webkit-tap-highlight-color: transparent;
            font-family: var(--fuente);
        }

        body {
            background-color: var(--bg-principal);
            color: var(--texto-principal);
            overflow-x: hidden;
            position: relative;
        }

        /* Fondo temático limpio sin overlays pesados */
        body::before {
            content: '';
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(180deg, rgba(0, 0, 0, 0.9) 0%, rgba(18, 18, 18, 0.98) 100%),
                        url('https://imgs.search.brave.com/4EBMHUrFzUMmziphOMTPiPrRGPM74GSSptcyBcla7gU/rs:fit:860:0:0:0/g:ce/aHR0cHM6Ly9kZWxj/YXIuY29tLnV5L3dw/LWNvbnRlbnQvdXBs/b2Fkcy8yMDIzLzEw/L1JBSURFUi03LXNj/YWxlZC5qcGc') no-repeat center center;
            background-size: cover;
            z-index: -1;
            transform: translateZ(0);
        }

        /* Contenedor de Pantallas */
        .pantalla {
            display: none;
            min-height: 100vh;
            padding: 24px;
            padding-bottom: 110px;
            opacity: 0;
            transform: translateY(8px);
            transition: opacity 0.35s ease, transform 0.35s ease;
            will-change: transform, opacity;
        }

        .pantalla.activa {
            display: flex;
            flex-direction: column;
            opacity: 1;
            transform: translateY(0);
        }

        /* Animaciones */
        @keyframes pulsoLogo {
            0%, 100% { border-color: rgba(255, 30, 39, 0.4); box-shadow: 0 0 10px rgba(255, 30, 39, 0.1); }
            50% { border-color: var(--neon-verde); box-shadow: 0 0 20px rgba(255, 30, 39, 0.4); }
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        @keyframes barridoMetalico {
            0% { left: -150%; }
            50% { left: -150%; }
            100% { left: 150%; }
        }

        /* Logo Estilo Técnico Minimalista */
        .logo-contenedor {
            width: 110px;
            height: 110px;
            border-radius: 50%;
            background: rgba(26, 26, 26, 0.6);
            border: 2px solid rgba(255, 30, 39, 0.4);
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 30px auto 15px auto;
            position: relative;
            animation: pulsoLogo 4s infinite ease-in-out;
            backdrop-filter: blur(8px);
        }

        .logo-contenedor .material-icons {
            font-size: 50px;
            color: #fff;
            z-index: 2;
        }

        /* Encabezados */
        .titulo-app {
            text-align: center;
            font-size: 2rem;
            font-weight: 800;
            text-transform: uppercase;
            letter-spacing: 2px;
            color: #fff;
        }

        .subtitulo-app {
            text-align: center;
            font-size: 0.8rem;
            color: var(--texto-secundario);
            margin-bottom: 30px;
            line-height: 1.4;
            max-width: 320px;
            margin-left: auto;
            margin-right: auto;
        }

        #pantalla-home .subtitulo-app {
            color: var(--neon-verde);
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 12px;
        }

        /* Tarjetas */
        .tarjeta-cyber {
            background: var(--bg-tarjeta);
            border: 1px solid var(--borde-sutil);
            border-radius: 24px;
            padding: 24px;
            margin-bottom: 20px;
            position: relative;
            overflow: hidden;
            transition: border-color 0.25s ease;
        }

        .tarjeta-cyber::after {
            content: '';
            position: absolute;
            top: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(
                90deg,
                rgba(255, 255, 255, 0) 0%,
                rgba(255, 255, 255, 0.03) 20%,
                rgba(255, 255, 255, 0.12) 50%,
                rgba(255, 255, 255, 0.03) 80%,
                rgba(255, 255, 255, 0) 100%
            );
            transform: skewX(-25deg);
            animation: barridoMetalico 6s infinite ease-in-out;
            pointer-events: none;
        }

        .tarjeta-cyber:focus-within {
            border-color: rgba(255, 30, 39, 0.4);
        }

        .grupo-input {
            margin-bottom: 20px;
        }

        .grupo-input label {
            display: block;
            font-size: 0.7rem;
            text-transform: uppercase;
            color: var(--texto-secundario);
            margin-bottom: 8px;
            letter-spacing: 1px;
            font-weight: 600;
        }

        /* Inputs */
        .input-cyber {
            width: 100%;
            background: var(--bg-input);
            border: 1px solid transparent;
            border-radius: 14px;
            padding: 16px;
            color: #fff;
            font-size: 0.95rem;
            transition: all 0.2s ease;
        }

        .input-cyber:focus {
            outline: none;
            border-color: rgba(255, 30, 39, 0.5);
            background: #222222;
        }

        /* Avatares */
        .contenedor-foto {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-bottom: 25px;
        }

        .avatar-contenedor-efecto {
            position: relative;
            width: 100px;
            height: 100px;
            border-radius: 50%;
            border: 2px solid var(--neon-rosa);
            box-shadow: 0 0 15px rgba(229, 9, 20, 0.5);
            background: var(--bg-input);
            margin-bottom: 12px;
            overflow: hidden;
        }

        .avatar-contenedor-efecto::after {
            content: '';
            position: absolute;
            top: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(
                90deg,
                rgba(255, 255, 255, 0) 0%,
                rgba(255, 255, 255, 0.05) 20%,
                rgba(255, 255, 255, 0.25) 50%,
                rgba(255, 255, 255, 0.05) 80%,
                rgba(255, 255, 255, 0) 100%
            );
            transform: skewX(-25deg);
            animation: barridoMetalico 4s infinite ease-in-out;
            pointer-events: none;
        }

        .avatar-preview {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.25s ease;
        }

        .btn-archivo {
            background: rgba(229, 9, 20, 0.08);
            color: var(--neon-rosa);
            border: 1px solid rgba(229, 9, 20, 0.2);
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 0.75rem;
            text-transform: uppercase;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.2s ease;
        }

        .btn-archivo:active {
            background: rgba(229, 9, 20, 0.2);
        }

        /* Botones */
        .btn-neon {
            width: 100%;
            background: var(--neon-verde);
            color: #ffffff;
            border: none;
            padding: 16px;
            border-radius: 14px;
            font-size: 0.95rem;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            transition: transform 0.1s ease, background-color 0.2s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .btn-neon::after {
            content: '';
            position: absolute;
            top: 0;
            width: 120%;
            height: 100%;
            background: linear-gradient(
                90deg,
                rgba(255, 255, 255, 0) 0%,
                rgba(255, 255, 255, 0.1) 20%,
                rgba(255, 255, 255, 0.3) 50%,
                rgba(255, 255, 255, 0.1) 80%,
                rgba(255, 255, 255, 0) 100%
            );
            transform: skewX(-20deg);
            animation: barridoMetalico 4.5s infinite ease-in-out;
            pointer-events: none;
        }

        .btn-neon:active {
            transform: scale(0.97);
            background: #cc0007;
        }

        #pantalla-home .btn-neon {
            background: #ffffff;
            color: #000000;
        }
        #pantalla-home .btn-neon:active {
            background: #e0e0e0;
        }

        /* Botón Solicitar Home */
        @keyframes motorRalenti {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.02); }
        }

        @keyframes pulsoMagnetico {
            0% {
                box-shadow: 0 0 0 0 rgba(255, 30, 39, 0.7), 
                            0 0 0 0 rgba(255, 30, 39, 0.4);
            }
            70% {
                box-shadow: 0 0 0 12px rgba(255, 30, 39, 0), 
                            0 0 0 24px rgba(255, 30, 39, 0);
            }
            100% {
                box-shadow: 0 0 0 0 rgba(255, 30, 39, 0), 
                            0 0 0 0 rgba(255, 30, 39, 0);
            }
        }

        @keyframes destelloCritico {
            0% { left: -150%; }
            30% { left: 150%; }
            100% { left: 150%; }
        }

        #pantalla-home .btn-neon-solicitar {
            background: linear-gradient(135deg, #ff1e27 0%, #e50914 100%) !important;
            color: #ffffff !important;
            font-size: 1.05rem !important;
            letter-spacing: 1px !important;
            box-shadow: 0 4px 20px rgba(255, 30, 39, 0.4);
            border: 1px solid rgba(255, 255, 255, 0.2) !important;
            animation: motorRalenti 1.8s infinite ease-in-out, 
                       pulsoMagnetico 2s infinite ease-in-out !important;
            transition: all 0.2s ease-in-out !important;
        }

        #pantalla-home .btn-neon-solicitar::after {
            background: linear-gradient(
                90deg,
                rgba(255, 255, 255, 0) 0%,
                rgba(255, 255, 255, 0.2) 20%,
                rgba(255, 255, 255, 0.6) 50%,
                rgba(255, 255, 255, 0.2) 80%,
                rgba(255, 255, 255, 0) 100%
            ) !important;
            animation: destelloCritico 3.5s infinite ease-in-out !important;
        }

        #pantalla-home .btn-neon-solicitar:hover {
            transform: scale(1.04);
            filter: brightness(1.1);
        }

        #pantalla-home .btn-neon-solicitar:active {
            transform: scale(0.96) !important;
            background: #990005 !important;
            box-shadow: 0 2px 10px rgba(255, 30, 39, 0.2);
        }

        #pantalla-home .btn-neon-solicitar .material-icons {
            font-size: 24px;
            filter: drop-shadow(0 0 2px rgba(255,255,255,0.6));
        }

        .btn-secundario {
            width: 100%;
            background: transparent;
            border: none;
            color: var(--texto-secundario);
            padding: 12px;
            text-align: center;
            font-size: 0.8rem;
            cursor: pointer;
            margin-top: 10px;
            transition: color 0.2s ease;
        }
        .btn-secundario:active {
            color: #fff;
        }

        /* Perfil */
        .perfil-resumen {
            display: flex;
            align-items: center;
            gap: 15px;
            background: var(--bg-tarjeta);
            border-radius: 20px;
            padding: 16px;
            border: 1px solid var(--borde-sutil);
            margin-bottom: 20px;
        }

        .foto-resumen-contenedor {
            position: relative;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            border: 2px solid var(--neon-verde);
            box-shadow: 0 0 12px rgba(255, 30, 39, 0.4);
            overflow: hidden;
        }

        .foto-resumen-contenedor::after {
            content: '';
            position: absolute;
            top: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(
                90deg,
                rgba(255, 255, 255, 0) 0%,
                rgba(255, 255, 255, 0.05) 20%,
                rgba(255, 255, 255, 0.25) 50%,
                rgba(255, 255, 255, 0.05) 80%,
                rgba(255, 255, 255, 0) 100%
            );
            transform: skewX(-25deg);
            animation: barridoMetalico 4s infinite ease-in-out;
            pointer-events: none;
        }

        .perfil-resumen img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .perfil-resumen h4 {
            font-size: 0.95rem;
            font-weight: 600;
        }

        .perfil-resumen p {
            font-size: 0.8rem;
            color: var(--texto-secundario);
            margin-top: 2px;
        }

        /* Barra de contacto flotante */
        .barra-contacto {
            position: fixed;
            bottom: 24px; left: 24px; right: 24px;
            display: flex;
            gap: 12px;
            z-index: 100;
        }

        .btn-flotante {
            flex: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            padding: 16px;
            border-radius: 16px;
            font-weight: 700;
            text-transform: uppercase;
            font-size: 0.8rem;
            text-decoration: none;
            transition: transform 0.1s ease;
        }

        .btn-flotante:active {
            transform: scale(0.96);
        }

        .btn-llamada {
            background: #1a1a1a;
            color: var(--neon-verde);
            border: 1px solid rgba(255, 30, 39, 0.2);
        }

        .btn-config {
            background: #121212;
            color: #fff;
            border: 1px solid var(--borde-sutil);
        }

        .status-ubicacion {
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.8rem;
            margin-top: 5px;
            color: var(--neon-rosa);
        }
        .status-ubicacion.listo {
            color: #ffffff;
        }
        
        .status-ubicacion .material-icons {
            animation: spin 2s infinite linear;
        }

        /* Modal Alertas */
        .modal-alerta-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.85);
            backdrop-filter: blur(4px);
            z-index: 1000;
            display: none;
            align-items: center;
            justify-content: center;
            padding: 24px;
        }
        
        .modal-alerta-caja {
            background: #121212;
            border: 2px solid var(--neon-verde);
            border-radius: 20px;
            width: 100%;
            max-width: 340px;
            padding: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.8);
            transform: scale(0.9);
            transition: transform 0.2s ease;
        }

        .modal-alerta-header {
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--neon-verde);
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 1.5px;
            font-weight: bold;
            margin-bottom: 12px;
            border-bottom: 1px solid rgba(255,255,255,0.06);
            padding-bottom: 8px;
        }

        .modal-alerta-cuerpo {
            font-size: 0.95rem;
            line-height: 1.4;
            color: #fff;
            margin-bottom: 20px;
        }

        .modal-alerta-btn {
            width: 100%;
            background: transparent;
            border: 1px solid var(--neon-verde);
            color: var(--neon-verde);
            padding: 12px;
            border-radius: 10px;
            font-weight: bold;
            text-transform: uppercase;
            font-size: 0.8rem;
            cursor: pointer;
            transition: all 0.1s ease;
        }
        .modal-alerta-btn:active {
            background: var(--neon-verde);
            color: #000;
        }

        .copyright {
            text-align: center;
            font-size: 0.7rem;
            color: var(--texto-secundario);
            margin-top: auto;
            padding-top: 30px;
            line-height: 1.5;
        }
        .copyright span {
            color: #fff;
            font-weight: 600;
        }

        .info-recorridos {
            margin-bottom: 20px;
            font-size: 0.9rem;
            line-height: 1.4;
        }
        .info-recorridos p {
            margin-bottom: 12px;
            color: var(--texto-principal);
        }
        .info-recorridos h5 {
            color: var(--neon-verde);
            font-size: 0.85rem;
            text-transform: uppercase;
            margin-bottom: 10px;
            letter-spacing: 0.5px;
        }
        .info-recorridos ul {
            list-style: none;
            padding-left: 0;
        }
        .info-recorridos li {
            margin-bottom: 8px;
            display: flex;
            align-items: flex-start;
            gap: 8px;
            color: var(--texto-secundario);
        }
        .info-recorridos li span {
            color: var(--texto-principal);
        }
    </style>
</head>
<body>

    <!-- Alerta Custom -->
    <div id="mi-alerta-custom" class="modal-alerta-overlay">
        <div class="modal-alerta-caja" id="mi-alerta-caja">
            <div class="modal-alerta-header">
                <span class="material-icons" style="font-size: 18px;">build_circle</span>
                <span>SISTEMA CHECK // SEGURAPP</span>
            </div>
            
            <div class="modal-alerta-cuerpo" id="mi-alerta-texto">
                Mensaje de diagnóstico de motor.
            </div>
            <button type="button" class="modal-alerta-btn" onclick="cerrarAlertaCustom()">
                Entendido / Aceptar
            </button>
        </div>
    </div>

    <!-- PANTALLA LOGIN -->
    <div id="pantalla-login" class="pantalla activa">
        <div class="logo-contenedor">
            <span class="material-icons">sports_motorsports</span>
        </div>

        <div class="titulo-app">SegurApp</div>
        <div class="subtitulo-app">Recorridos en la ciudad de Neiva</div>
        
        <div class="tarjeta-cyber info-recorridos">
            <p>Si buscas un servicio de transporte rápido, seguro y totalmente confiable, <strong>Recorridos</strong> es tu mejor opción. 📍</p>
            <p>Nos encargamos de que llegues a tiempo a tus citas, trabajo, compromisos o de regreso a casa, con la comodidad y la tranquilidad que te mereces.</p>
            
            <h5>¿Por qué elegirnos?</h5>
            <ul>
                <li>⏱️ <span><strong>Puntualidad garantizada:</strong> Respetamos tu tiempo.</span></li>
                <li>🔒 <span><strong>Viajes seguros:</strong> Conductores de confianza y rutas optimizadas.</span></li>
                <li>💬 <span><strong>Fácil de solicitar:</strong> Sin enredos ni esperas largas.</span></li>
            </ul>
            <p style="margin-top: 12px; margin-bottom: 0; font-weight: bold; color: var(--neon-verde);">¡Olvídate del estrés del tráfico! Déjanos el volante a nosotros.</p>
        </div>
        
        <div class="tarjeta-cyber" style="margin-top: auto; margin-bottom: auto;">
            <div class="grupo-input">
                <label>Número de Teléfono</label>
                <input type="tel" id="login-telefono" class="input-cyber" placeholder="Ej. 3189882787">
            </div>

            <button type="button" class="btn-neon" onclick="procesarLogin()">
                <span class="material-icons">flash_on</span> Ingreso Inmediato
            </button>

            <button type="button" class="btn-secundario" onclick="navegarA('pantalla-registro')">
                ¿No tienes cuenta? Registra tu Piloto
            </button>
        </div>

        <footer class="copyright">
            © 2026 SegurApp Recorridos. Todos los derechos reservados.<br>
            Desarrollado por <span>Sergio Chala</span>
        </footer>
    </div>

    <!-- PANTALLA REGISTRO -->
    <div id="pantalla-registro" class="pantalla">
        <div class="titulo-app" id="registro-titulo">Registro</div>
        <div class="subtitulo-app">Información del Usuario</div>

        <div class="tarjeta-cyber">
            <div class="contenedor-foto">
                <div class="avatar-contenedor-efecto">
                    <img src="" id="registro-preview" class="avatar-preview" alt="Avatar">
                </div>
                <input type="file" id="registro-foto" accept="image/*" style="display: none;" onchange="manejarCargaFoto(event)">
                <button type="button" class="btn-archivo" onclick="document.getElementById('registro-foto').click()">
                    <span class="material-icons" style="font-size: 14px; vertical-align: middle;">camera_alt</span> Cargar Foto
                </button>
            </div>

            <div class="grupo-input">
                <label>Nombre de Usuario</label>
                <input type="text" id="registro-nombre" class="input-cyber" placeholder="Nombre o Apodo">
            </div>

            <div class="grupo-input">
                <label>Número de Teléfono</label>
                <input type="tel" id="registro-telefono" class="input-cyber" placeholder="Ej. 3189882787">
            </div>

            <button type="button" class="btn-neon" id="btn-guardar-perfil" onclick="guardarPerfil()">
                <span class="material-icons">save</span> Guardar Perfil
            </button>

            <button type="button" class="btn-secundario" id="btn-cancelar-registro" onclick="navegarA('pantalla-login')">
                Volver
            </button>
        </div>

        <footer class="copyright">
            © 2026 SegurApp Recorridos. Todos los derechos reservados.<br>
            Desarrollado por <span>Sergio Chala</span>
        </footer>
    </div>

    <!-- PANTALLA HOME -->
    <div id="pantalla-home" class="pantalla">
        <div class="titulo-app">SegurApp</div>
        
        <div class="perfil-resumen">
            <div class="foto-resumen-contenedor">
                <img src="" id="home-user-foto" alt="Usuario">
            </div>
            <div class="info">
                <h4 id="home-user-nombre">Usuario Anónimo</h4>
                <p id="home-user-telefono">Teléfono: --</p>
            </div>
        </div>

        <div class="tarjeta-cyber">
            <div class="grupo-input">
                <span style="color:#ff0000; font-size: 13px; display:inline-block; margin-top:5px;">⏳¡Reserva con 10 minutos de anticipación!</span>
                <label>Notas de Ruta (Opcional)</label>
                <input type="text" id="reserva-notes" class="input-cyber" placeholder="Ej: Llevar casco extra, maleta pesada...">
            </div>

            <div class="status-ubicacion" id="geo-status">
                <span class="material-icons" style="font-size: 18px;">share_location</span>
                <span id="geo-texto">Sincronizando radar GPS...</span>
            </div>
            
            <div style="margin-top: 25px;">
                <button type="button" class="btn-neon btn-neon-solicitar" onclick="enviarReserva()">
                    <span class="material-icons">motorcycle</span> Solicitar Servicio Ahora
                </button>
            </div>
        </div>

        <div class="barra-contacto">
            <button type="button" class="btn-flotante btn-config" onclick="abrirConfiguracion()">
                <span class="material-icons">tune</span> Mi Perfil
            </button>
            <a href="tel:3189882787" class="btn-flotante btn-llamada">
                <span class="material-icons">phone_in_talk</span> Soporte
            </a>
        </div>

        <footer class="copyright">
            © 2026 SegurApp Recorridos. Todos los derechos reservados.<br>
            Desarrollado por <span>Sergio Chala</span>
        </footer>
    </div>

    <!-- INTEGRACIÓN FIREBASE -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getDatabase, ref, set, get, child } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";
        import { getStorage, ref as storageRef, uploadString, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-storage.js";

        const firebaseConfig = {
            apiKey: "AIzaSyDTNh_JZfAPDdW1PDuhse3H3kSeuzd3V-4",
            authDomain: "mi-app-a88d7.firebaseapp.com",
            databaseURL: "https://mi-app-a88d7-default-rtdb.firebaseio.com",
            projectId: "mi-app-a88d7",
            storageBucket: "mi-app-a88d7.firebasestorage.app",
            messagingSenderId: "372012990915",
            appId: "1:372012990915:web:552c23fa6d01351a92fd76"
        };

        const app = initializeApp(firebaseConfig);
        const database = getDatabase(app);
        const storage = getStorage(app);

        let usuarioBase64Foto = ""; 
        let datosUbicacionActual = "Buscando satélites...";
        const WHATSAPP_DESTINO = "573189882787";
        let callbackDespuesDeAlerta = null;

        window.manejarCargaFoto = manejarCargaFoto;
        window.guardarPerfil = guardarPerfil;
        window.procesarLogin = procesarLogin;
        window.enviarReserva = enviarReserva;
        window.abrirConfiguracion = abrirConfiguracion;
        window.navegarA = navegarA;
        window.cerrarAlertaCustom = cerrarAlertaCustom;

        function mostrarAlertaCustom(mensaje, callback = null) {
            document.getElementById('mi-alerta-texto').innerText = mensaje;
            const overlay = document.getElementById('mi-alerta-custom');
            overlay.style.display = 'flex';
            setTimeout(() => {
                document.getElementById('mi-alerta-caja').style.transform = 'scale(1)';
            }, 50);
            callbackDespuesDeAlerta = callback;
        }

        function cerrarAlertaCustom() {
            document.getElementById('mi-alerta-caja').style.transform = 'scale(0.9)';
            document.getElementById('mi-alerta-custom').style.display = 'none';
            if (callbackDespuesDeAlerta) {
                callbackDespuesDeAlerta();
                callbackDespuesDeAlerta = null;
            }
        }

        document.addEventListener("DOMContentLoaded", () => {
            solicitarGeolocalizacion();
            if(localStorage.getItem("segurapp_usuario")) {
                cargarDatosHome();
                navegarA('pantalla-home');
            }
        });

        function navegarA(idPantalla) {
            const pantallaActivaActual = document.querySelector('.pantalla.activa');
            
            if (pantallaActivaActual) {
                pantallaActivaActual.style.opacity = '0';
                pantallaActivaActual.style.transform = 'translateY(-4px)';
                
                setTimeout(() => {
                    pantallaActivaActual.classList.remove('activa');
                    activarSiguiente(idPantalla);
                }, 200); 
            } else {
                activarSiguiente(idPantalla);
            }
        }

        function activarSiguiente(idPantalla) {
            const siguientePantalla = document.getElementById(idPantalla);
            siguientePantalla.classList.add('activa');
            
            requestAnimationFrame(() => {
                siguientePantalla.style.opacity = '1';
                siguientePantalla.style.transform = 'translateY(0)';
            });
            window.scrollTo(0, 0);
        }

        function manejarCargaFoto(event) {
            const archivo = event.target.files[0];
            if (archivo) {
                const lector = new FileReader();
                lector.onload = function(e) {
                    usuarioBase64Foto = e.target.result;
                    document.getElementById('registro-preview').src = usuarioBase64Foto;
                }
                lector.readAsDataURL(archivo);
            }
        }

        async function guardarPerfil() {
            const nombre = document.getElementById('registro-nombre').value.trim();
            const telefono = document.getElementById('registro-telefono').value.trim();

            if(!nombre || !telefono) {
                mostrarAlertaCustom("⚠️ Falla de encendido: Completa tu Nombre y tu Teléfono para encender motores.");
                return;
            }

            mostrarAlertaCustom("⚡ Guardando datos... Por favor, espera.");

            let fotoURL = "https://via.placeholder.com/150";

            try {
                if (usuarioBase64Foto && usuarioBase64Foto.startsWith("data:image")) {
                    const picRef = storageRef(storage, `avatar_${telefono}.jpg`);
                    const uploadResult = await uploadString(picRef, usuarioBase64Foto, 'data_url');
                    fotoURL = await getDownloadURL(uploadResult.ref);
                } else if (usuarioBase64Foto) {
                    fotoURL = usuarioBase64Foto;
                }

                const objetoUsuario = {
                    nombre: nombre,
                    telefono: telefono,
                    foto: fotoURL
                };

                await set(ref(database, 'usuarios/' + telefono), objetoUsuario);
                localStorage.setItem("segurapp_usuario", JSON.stringify(objetoUsuario));
                
                mostrarAlertaCustom("⚡ ¡Perfil guardado correctamente en la nube!", () => {
                    cargarDatosHome();
                    navegarA('pantalla-home');
                });

            } catch (error) {
                console.error(error);
                mostrarAlertaCustom("❌ Error de Conexión: No se pudo subir el perfil a Firebase.");
            }
        }

        async function procesarLogin() {
            const telefonoLogin = document.getElementById('login-telefono').value.trim();

            if(!telefonoLogin) {
                mostrarAlertaCustom("❌ Error: Por favor ingresa tu número telefónico.");
                return;
            }

            mostrarAlertaCustom("🔍 Buscando piloto en el radar Firebase...");

            try {
                const dbRef = ref(database);
                const snapshot = await get(child(dbRef, `usuarios/${telefonoLogin}`));

                if (snapshot.exists()) {
                    const user = snapshot.val();
                    localStorage.setItem("segurapp_usuario", JSON.stringify(user));
                    
                    mostrarAlertaCustom("⚡ ¡Ingreso exitoso! Perfil sincronizado.", () => {
                        cargarDatosHome();
                        navegarA('pantalla-home');
                    });
                } else {
                    mostrarAlertaCustom("⚙️ Piloto no registrado. Regístrate ahora mismo.", () => {
                        document.getElementById('registro-telefono').value = telefonoLogin;
                        navegarA('pantalla-registro');
                    });
                }
            } catch (error) {
                console.error(error);
                const localData = localStorage.getItem("segurapp_usuario");
                if (localData) {
                    const user = JSON.parse(localData);
                    if (user.telefono === telefonoLogin) {
                        mostrarAlertaCustom("⚠️ Modo Offline: Accediendo con datos locales.", () => {
                            cargarDatosHome();
                            navegarA('pantalla-home');
                        });
                        return;
                    }
                }
                mostrarAlertaCustom("❌ Error de Red: Asegúrate de tener conexión a internet.");
            }
        }

        function cargarDatosHome() {
            const localData = localStorage.getItem("segurapp_usuario");
            if(localData) {
                const user = JSON.parse(localData);
                document.getElementById('home-user-nombre').innerText = user.nombre;
                document.getElementById('home-user-telefono').innerText = "Usuario Cel: " + user.telefono;
                document.getElementById('home-user-foto').src = user.foto;
            }
        }

        function abrirConfiguracion() {
            const localData = localStorage.getItem("segurapp_usuario");
            if(localData) {
                const user = JSON.parse(localData);
                document.getElementById('registro-nombre').value = user.nombre;
                document.getElementById('registro-telefono').value = user.telefono;
                document.getElementById('registro-preview').src = user.foto;
                usuarioBase64Foto = user.foto;
                
                document.getElementById('registro-titulo').innerText = "Modificar Usuario";
                document.getElementById('btn-guardar-perfil').innerHTML = '<span class="material-icons">sync</span> Guardar Cambios';
                document.getElementById('btn-cancelar-registro').onclick = () => navegarA('pantalla-home');
                
                navegarA('pantalla-registro');
            }
        }

        function solicitarGeolocalizacion() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(
                    (position) => {
                        const lat = position.coords.latitude;
                        const lon = position.coords.longitude;
                        datosUbicacionActual = `https://www.google.com/maps?q=${lat},${lon}`;
                        
                        const geoStatus = document.getElementById('geo-status');
                        geoStatus.classList.add('listo');
                        document.getElementById('geo-texto').innerText = "Ubicación de partida fijada por GPS.";
                        geoStatus.querySelector('.material-icons').style.animation = 'none';
                    },
                    (error) => {
                        document.getElementById('geo-texto').innerText = "Ubicación manual o imprecisa.";
                        datosUbicacionActual = "GPS Local (Verificar mapa al contactar)";
                        document.getElementById('geo-status').querySelector('.material-icons').style.animation = 'none';
                    },
                    { enableHighAccuracy: true, timeout: 10000 }
                );
            } else {
                document.getElementById('geo-texto').innerText = "GPS no soportado.";
            }
        }

        async function enviarReserva() {
            const destino = "Origen fijado por GPS";
            const notas = document.getElementById('reserva-notes').value.trim();
            const userData = JSON.parse(localStorage.getItem("segurapp_usuario"));
            
            if(!userData) {
                mostrarAlertaCustom("❌ Acceso denegado: Por favor regístrate primero.");
                return;
            }

            const timestampId = Date.now();

            try {
                const servicioInfo = {
                    usuarioNombre: userData.nombre,
                    usuarioTelefono: userData.telefono,
                    origenGPS: datosUbicacionActual,
                    destino: destino,
                    detalles: notas || "Sin especificaciones",
                    fechaYHora: new Date().toISOString(),
                    estado: "Solicitado"
                };

                await set(ref(database, `servicios/${userData.telefono}_${timestampId}`), servicioInfo);

            } catch (error) {
                console.error("Error al registrar respaldo de viaje en la nube: ", error);
            }

            let mensaje = `*SOLICITUD DE RECORRIDO INMEDIATO* \n`;
            mensaje += `───────────────────────\n\n`;
            mensaje += ` *Usuario:* ${userData.nombre}\n`;
            mensaje += ` *Teléfono Cel:* ${userData.telefono}\n\n`;
            mensaje += ` *Origen:* _Fijado automáticamente por GPS_ \n`;
            mensaje += ` *Destino:* ${destino}\n`;
            
            if(notas) {
                mensaje += ` *Detalles:* ${notas}\n`;
            }
            
            mensaje += `\n *Coordenadas de Origen en Tiempo Real:* \n${datosUbicacionActual}\n\n`;
            mensaje += `───────────────────────\n\n`;
            mensaje += ` *Tiempo estimado de respuesta 5min*`;

            window.open(`https://wa.me/${WHATSAPP_DESTINO}?text=${encodeURIComponent(mensaje)}`, '_blank');
        }
    </script>
</body>
</html>
