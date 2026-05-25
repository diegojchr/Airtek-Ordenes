<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Airtek - Órdenes De Compra</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Outfit:wght@400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <!-- PANTALLA DE LOGIN -->
    <div id="login-screen" class="login-overlay">
        <div class="login-box">
            <div class="login-logo">
                <div class="logo-icon-large">
                    <i class="fa-solid fa-boxes-stacked"></i>
                </div>
                <h2>AIRTEK</h2>
                <p>Órdenes de compra - Gerencia Operativa de Energía</p>
            </div>
            <form id="login-form">
                <div class="form-group">
                    <label>Usuario / Correo</label>
                    <input type="email" id="login-email" placeholder="ejemplo@airtek.com.ve" required>
                </div>
                <div class="form-group">
                    <label>Contraseña</label>
                    <input type="password" id="login-password" placeholder="••••••••" required>
                </div>
                <div id="login-error" style="color: #ef4444; font-size: 12px; margin-bottom: 12px; display: none;"></div>
                <button type="submit" id="btn-login" class="btn-primary btn-block">Ingresar al Sistema</button>
            </form>
        </div>
    </div>

    <div class="app-container" id="app-content" style="display: none;">
        <!-- Sidebar -->
        <aside class="sidebar">
            <div class="sidebar-header" style="align-items: center; text-align: center; padding-top: 36px; padding-bottom: 24px;">
                <div class="logo" style="justify-content: center; margin-bottom: 12px;">
                    <div class="logo-icon">
                        <i class="fa-solid fa-boxes-stacked"></i>
                    </div>
                    <h2 style="font-size: 26px;">AIRTEK</h2>
                </div>
                <span class="sub-logo" style="margin-left: 0; font-size: 11px; text-align: center; line-height: 1.4; color: #60a5fa;">
                    ÓRDENES DE COMPRA<br>GERENCIA OPERATIVA DE ENERGÍA
                </span>
            </div>

            <nav class="sidebar-menu">
                <div class="menu-section">
                    <h3>GESTIÓN DE COMPRAS</h3>
                    <ul>
                        <li class="nav-item active" data-target="view-resumen">
                            <a href="#"><i class="fa-solid fa-chart-pie"></i> Resumen General</a>
                        </li>
                        <li class="nav-item" data-target="view-ordenes">
                            <a href="#"><i class="fa-solid fa-file-invoice"></i> Órdenes de Compra</a>
                        </li>
                        <li class="nav-item" data-target="view-graficas">
                            <a href="#"><i class="fa-solid fa-chart-line"></i> Gráficas y Métricas</a>
                        </li>
                    </ul>
                </div>
                <div class="menu-section">
                    <h3>ADMINISTRACIÓN</h3>
                    <ul>
                        <li class="nav-item" data-target="view-depuracion">
                            <a href="#"><i class="fa-solid fa-broom"></i> Herramientas Depuración</a>
                        </li>
                    </ul>
                </div>
            </nav>

            <div class="sidebar-footer">
                <a href="#" class="logout-btn" id="btn-logout">
                    <i class="fa-solid fa-arrow-right-from-bracket"></i> Cerrar Sesión
                </a>
            </div>
        </aside>

        <!-- Main Content -->
        <main class="main-content">
            <header class="top-header">
                <div class="header-title">
                    <h1 id="page-title">Resumen General</h1>
                </div>
                <div class="header-user">
                    <div class="user-info">
                        <span class="user-name" id="display-user-name">Usuario <span class="badge">ADMIN</span></span>
                        <span class="user-status"><span class="status-dot"></span> En línea</span>
                    </div>
                    <div class="user-avatar">
                        <i class="fa-solid fa-user"></i>
                    </div>
                </div>
            </header>

            <!-- VISTA: RESUMEN -->
            <div id="view-resumen" class="view-section active">
                <section class="filters-section" style="margin-bottom: 24px;">
                    <div class="filter-group">
                        <span class="filter-label"><i class="fa-solid fa-filter"></i> FILTROS</span>
                        <div class="filter-item">
                            <input type="month" class="filter-select" id="filter-resumen-mes" title="Mes">
                        </div>
                        <div class="filter-search" style="margin-left: 5px;">
                            <i class="fa-solid fa-magnifying-glass search-icon"></i>
                            <input type="text" class="filter-input-search" id="filter-resumen-oc" placeholder="N° Orden Compra..." style="width: 150px; padding-left: 35px;">
                        </div>
                        <div class="filter-item">
                            <select class="filter-select" id="filter-resumen-recibo">
                                <option value="todos">Estado de Recepción</option>
                                <option value="recibidos">Ítems Recibidos</option>
                                <option value="pendientes">Ítems Pendientes</option>
                            </select>
                        </div>
                        <div class="filter-item">
                            <select class="filter-select" id="filter-resumen-pago">
                                <option value="todos">Estado de Pago</option>
                                <option value="pagados">Órdenes Pagadas</option>
                                <option value="proceso">Órdenes en Proceso</option>
                            </select>
                        </div>
                    </div>
                    <button class="btn-clear" id="btn-clear-resumen" style="margin-left: auto;"><i class="fa-solid fa-eraser"></i> Limpiar Filtros</button>
                </section>

                <section class="stats-section">
                    <div class="stat-card">
                        <div class="stat-icon icon-blue"><i class="fa-solid fa-file-invoice"></i></div>
                        <div class="stat-info"><span class="stat-title">Total Órdenes</span><h2 class="stat-value" id="stat-total">0</h2></div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon icon-orange"><i class="fa-solid fa-clock-rotate-left"></i></div>
                        <div class="stat-info"><span class="stat-title">Ítems Pendientes</span><h2 class="stat-value" id="stat-pending">0</h2></div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon icon-green"><i class="fa-solid fa-check-to-slot"></i></div>
                        <div class="stat-info"><span class="stat-title">Ítems Recibidos</span><h2 class="stat-value" id="stat-received">0</h2></div>
                    </div>
                </section>

                <div class="dashboard-grid">
                    <section class="table-section" style="flex: 2;">
                        <div class="table-header">
                            <h3>VISUAL: LOS QUE FALTAN (ÍTEMS PENDIENTES)</h3>
                            <span class="badge badge-red">Prioridad de Procura</span>
                        </div>
                        <div class="table-container">
                            <table>
                                <thead>
                                    <tr>
                                        <th>ÍTEM</th>
                                        <th>CANTIDAD FALTANTE</th>
                                        <th>PERSONAL PROCURA</th>
                                        <th>N° ORDEN COMPRA</th>
                                        <th>N° RECIBO DE COMPRA</th>
                                    </tr>
                                </thead>
                                <tbody id="table-body-faltantes"></tbody>
                            </table>
                        </div>
                    </section>
                </div>
            </div>

            <!-- VISTA: ÓRDENES DE COMPRA -->
            <div id="view-ordenes" class="view-section">
                <section class="filters-section">
                    <div class="filter-group" style="width: 100%;">
                        <div class="filter-search">
                            <i class="fa-solid fa-magnifying-glass search-icon"></i>
                            <input type="text" class="filter-input-search" id="filter-ordenes-text" placeholder="N° OC, RC o Ítem..." style="width: 180px;">
                        </div>
                        <div class="filter-item">
                            <input type="month" class="filter-select" id="filter-ordenes-mes" title="Mes">
                        </div>
                        <div class="filter-item">
                            <select class="filter-select" id="filter-ordenes-pago">
                                <option value="todos">Est. Pago (Todos)</option>
                                <option value="pagado">Pagado</option>
                                <option value="parcial">Parcial</option>
                                <option value="nopagado">No Pagado</option>
                            </select>
                        </div>
                        <div class="filter-item">
                            <select class="filter-select" id="filter-ordenes-recibo">
                                <option value="todos">Est. Recibo (Todos)</option>
                                <option value="completo">Recibido</option>
                                <option value="parcial">Parcial</option>
                                <option value="norecibido">No Recibido</option>
                            </select>
                        </div>
                        <button class="btn-clear" id="btn-clear-ordenes" style="margin-left: 10px;"><i class="fa-solid fa-eraser"></i> Limpiar</button>
                        
                        <button class="btn-primary" id="btn-open-modal" style="margin-left: auto;"><i class="fa-solid fa-plus"></i> Nueva Orden</button>
                    </div>
                </section>

                <section class="table-section">
                    <div class="table-header">
                        <h3>DESGLOSE COMPLETO DE ÓRDENES</h3>
                    </div>
                    <div class="table-container">
                        <table style="min-width: 1650px;">
                            <thead>
                                <tr>
                                    <th>N° ORDEN COMPRA</th>
                                    <th>N° RECIBO DE COMPRA</th>
                                    <th>COORDINACIÓN</th>
                                    <th>PERSONAL PROCURA</th>
                                    <th>COMENTARIO SOLICITUD</th>
                                    <th>ÍTEM</th>
                                    <th>CANT.</th>
                                    <th>ESTADO PAGO</th>
                                    <th>ESTADO RECIBO</th>
                                    <th>COMENTARIO RECEPCIÓN</th>
                                    <th>ACCIONES</th>
                                </tr>
                            </thead>
                            <tbody id="table-body-ordenes"></tbody>
                        </table>
                    </div>
                </section>
            </div>

            <!-- VISTA: GRÁFICAS -->
            <div id="view-graficas" class="view-section">
                <div class="charts-grid">
                    <div class="chart-card" style="grid-column: span 2;">
                        <div class="chart-header">
                            <h3>Histórico Mensual (Órdenes vs Productos)</h3>
                        </div>
                        <div class="chart-body">
                            <canvas id="monthlyChart"></canvas>
                        </div>
                    </div>
                    <div class="chart-card">
                        <div class="chart-header">
                            <h3>Estado General de Ítems</h3>
                        </div>
                        <div class="chart-body" style="display: flex; justify-content: center; align-items: center; height: 300px;">
                            <canvas id="statusChart"></canvas>
                        </div>
                    </div>
                </div>
            </div>

            <!-- VISTA: DEPURACIÓN -->
            <div id="view-depuracion" class="view-section">
                <div class="dashboard-grid">
                    <section class="table-section" style="flex: 1; border-color: #fca5a5;">
                        <div class="table-header" style="background-color: #fef2f2; border-bottom-color: #fca5a5;">
                            <h3 style="color: #b91c1c;">ZONA DE PELIGRO: DEPURACIÓN MASIVA</h3>
                            <span class="badge badge-red"><i class="fa-solid fa-triangle-exclamation"></i> Administradores</span>
                        </div>
                        <div style="padding: 24px;">
                            <p style="margin-bottom: 24px; color: var(--text-secondary); line-height: 1.6;">
                                Utiliza estas herramientas para limpiar la base de datos cuando se sature de información. Las acciones realizadas aquí eliminarán los datos permanentemente de Firebase.
                            </p>

                            <!-- Depurar por Mes -->
                            <div style="background: #f8fafc; padding: 20px; border-radius: 12px; border: 1px solid var(--border-color); margin-bottom: 20px;">
                                <h4 style="margin-bottom: 12px; font-family: var(--font-sans); font-size: 14px;">Eliminar por Mes Correspondiente</h4>
                                <div style="display: flex; gap: 12px; align-items: center;">
                                    <input type="month" id="purge-month" class="filter-select">
                                    <button class="btn-danger" id="btn-purge-month"><i class="fa-solid fa-trash"></i> Eliminar todo este mes</button>
                                </div>
                            </div>

                            <!-- Depurar por Orden de Compra -->
                            <div style="background: #f8fafc; padding: 20px; border-radius: 12px; border: 1px solid var(--border-color);">
                                <h4 style="margin-bottom: 12px; font-family: var(--font-sans); font-size: 14px;">Eliminar por N° Orden de Compra</h4>
                                <div style="display: flex; gap: 12px; align-items: center;">
                                    <input type="text" id="purge-oc" class="filter-select" placeholder="Ej: OC-001" style="width: 250px;">
                                    <button class="btn-danger" id="btn-purge-oc"><i class="fa-solid fa-trash"></i> Eliminar toda esta orden</button>
                                </div>
                            </div>
                        </div>
                    </section>
                </div>
            </div>
        </main>
    </div>

    <!-- MODAL NUEVA ORDEN -->
    <div id="modal-nueva-orden" class="modal-overlay" style="display: none;">
        <div class="modal-content" style="width: 1000px; max-width: 95%;">
            <div class="modal-header">
                <h2>Agregar Nueva Orden de Compra</h2>
                <button class="btn-close" id="btn-close-modal"><i class="fa-solid fa-xmark"></i></button>
            </div>
            
            <div class="modal-tabs">
                <div class="modal-tab active" data-tab="tab-individual">Crear Orden (Múltiples Ítems)</div>
                <div class="modal-tab" data-tab="tab-masiva">Subida Masiva desde Excel</div>
            </div>

            <div class="modal-body">
                <div id="tab-individual" class="tab-content active">
                    <div class="form-section-title">Datos Principales de la Orden</div>
                    <div class="form-grid" style="margin-bottom: 24px; grid-template-columns: repeat(5, 1fr);">
                        <div class="form-group">
                            <label>N° de Orden de Compra</label>
                            <input type="text" id="new-orden-compra" placeholder="Ej: OC-00123">
                        </div>
                        <div class="form-group">
                            <label>N° Recibo de Compra</label>
                            <input type="text" id="new-recibo-compra" placeholder="Ej: F-PRO-06675">
                        </div>
                        <div class="form-group">
                            <label>Coordinación</label>
                            <input type="text" id="new-coordinacion" placeholder="Ej: OPERACIONES">
                        </div>
                        <div class="form-group">
                            <label>Personal de Procura</label>
                            <input type="text" id="new-procura" placeholder="Ej: JUAN PEREZ">
                        </div>
                        <div class="form-group">
                            <label>Mes Correspondiente</label>
                            <input type="month" id="new-mes" class="filter-select" style="width:100%; padding: 10px 14px;">
                        </div>
                        <div class="form-group" style="grid-column: span 5;">
                            <label>Comentario del para qué se solicitó</label>
                            <textarea id="new-com-sol" rows="2" placeholder="Motivo general de la orden..."></textarea>
                        </div>
                    </div>

                    <div class="form-section-title" style="display: flex; justify-content: space-between; align-items: center;">
                        <span>Ítems / Materiales a solicitar</span>
                        <button class="btn-secondary btn-small" id="btn-add-item"><i class="fa-solid fa-plus"></i> Agregar otro ítem</button>
                    </div>
                    
                    <div id="dynamic-items-container">
                        <div class="item-row-grid">
                            <div class="form-group">
                                <label>Ítem / Material</label>
                                <input type="text" class="new-item-desc" placeholder="Descripción del producto">
                            </div>
                            <div class="form-group">
                                <label>Cant.</label>
                                <input type="number" class="new-item-cant" placeholder="0" style="min-width: 60px;">
                            </div>
                            <div class="form-group">
                                <label>Est. Pago</label>
                                <select class="new-item-pago">
                                    <option value="pagado">Pagado</option>
                                    <option value="parcial">Parcial</option>
                                    <option value="nopagado">No Pagado</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label>Est. Recibo</label>
                                <select class="new-item-recibo">
                                    <option value="completo">Recibido</option>
                                    <option value="parcial">Parcial</option>
                                    <option value="norecibido">No recibido</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label>Comentario Rec.</label>
                                <input type="text" class="new-item-comrec" placeholder="Detalles...">
                            </div>
                            <div class="form-group" style="justify-content: flex-end;">
                                <button class="btn-remove-item" style="display: none; height: 40px; margin-bottom: 0;"><i class="fa-solid fa-trash"></i></button>
                            </div>
                        </div>
                    </div>

                    <div class="modal-footer">
                        <button class="btn-clear" id="btn-cancel-modal">Cancelar</button>
                        <button class="btn-primary" id="btn-save-order">Guardar Orden de Compra</button>
                    </div>
                </div>

                <div id="tab-masiva" class="tab-content" style="display: none;">
                    <p style="margin-bottom: 16px; color: var(--text-secondary); font-size: 14px;">
                        Pega aquí la lista de materiales separados por la barra vertical " | ". <br>
                        <strong>Estructura requerida por línea:</strong> N° OC | Materiales | Cantidad | N° Recibo | Procura | Mes (YYYY-MM) | Estado pago (pagado/parcial/nopagado) | Estado recibo (completo/parcial/norecibido)
                    </p>
                    <div class="form-group">
                        <textarea id="bulk-text" rows="10" placeholder="OC-001 | ESMERIL | 1 | F-PRO-06651 | JUAN PEREZ | 2026-05 | pagado | norecibido"></textarea>
                    </div>
                    <div class="modal-footer">
                        <button class="btn-clear" id="btn-cancel-bulk">Cancelar</button>
                        <button class="btn-primary" id="btn-save-bulk">Procesar Subida Masiva</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- MODAL EDITAR COMENTARIO (Simplificado) -->
    <div id="modal-editar-orden" class="modal-overlay" style="display: none;">
        <div class="modal-content" style="width: 500px; max-width: 95%;">
            <div class="modal-header">
                <h2>Editar Comentario de Recepción</h2>
                <button class="btn-close" id="btn-close-edit"><i class="fa-solid fa-xmark"></i></button>
            </div>
            
            <div class="modal-body">
                <input type="hidden" id="edit-id">
                <div class="form-group">
                    <label>Comentario Recepción</label>
                    <textarea id="edit-comentario-recibo" rows="4" placeholder="Detalles de la recepción..."></textarea>
                </div>
            </div>
            <div class="modal-footer">
                <button class="btn-clear" id="btn-cancel-edit">Cancelar</button>
                <button class="btn-primary" id="btn-save-edit">Guardar Comentario</button>
            </div>
        </div>
    </div>

    <!-- MODAL ELIMINAR (Único o Múltiple) -->
    <div id="modal-eliminar" class="modal-overlay" style="display: none;">
        <div class="modal-content" style="width: 450px; max-width: 95%;">
            <div class="modal-header">
                <h2>Eliminar Ítem u Orden</h2>
                <button class="btn-close" id="btn-close-delete"><i class="fa-solid fa-xmark"></i></button>
            </div>
            
            <div class="modal-body">
                <input type="hidden" id="delete-id">
                <input type="hidden" id="delete-oc">
                <p style="margin-bottom: 20px; color: var(--text-secondary); line-height: 1.5;">
                    Estás a punto de eliminar un ítem perteneciente a la orden 
                    <strong id="delete-oc-label" style="color: var(--text-primary);"></strong>. 
                    <br><br>¿Deseas eliminar solo este ítem o deseas eliminar <strong>TODA</strong> la orden de compra con todos sus ítems?
                </p>
            </div>
            <div class="modal-footer" style="display: flex; gap: 10px; flex-wrap: wrap;">
                <button class="btn-clear" id="btn-cancel-delete">Cancelar</button>
                <button class="btn-secondary" id="btn-delete-item" style="color: #ef4444;">Eliminar Solo Ítem</button>
                <button class="btn-danger" id="btn-delete-order">Eliminar Toda la Orden</button>
            </div>
        </div>
    </div>

    <!-- Load JS as module to support Firebase SDK imports -->
    <script type="module" src="script.js"></script>
</body>
</html>
