<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestor de Inventario</title>
    <!-- Tailwind CSS CDN para un estilo moderno y responsivo -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
    </style>
</head>
<body class="bg-red-50 min-h-screen flex items-center justify-center p-4">

    <!-- Contenedor principal de la página -->
    <div class="max-w-xl w-full mx-auto bg-white rounded-3xl shadow-2xl p-8 md:p-10 lg:p-12 space-y-8">

        <!-- Cabecera de la página -->
        <header class="text-center">
            <h1 class="text-3xl md:text-4xl font-extrabold text-gray-800 leading-tight">
                Gestor de Inventario Simple
            </h1>
            <p class="mt-2 text-lg text-gray-600 font-medium">
                Registra tus productos, lotes, zonas y fechas
            </p>
        </header>

        <!-- Sección de contenido interactivo -->
        <section class="space-y-6">
            <h2 class="text-2xl font-bold text-gray-700">Agregar Nuevo Producto</h2>
            
            <!-- Formulario para interactuar con la página -->
            <form id="item-form" class="space-y-4">
                <input id="product-name-input" type="text" placeholder="Nombre del Producto" class="w-full p-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500 transition-shadow">
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <input id="batch-input" type="text" placeholder="Lote" class="p-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500 transition-shadow">
                    <input id="zone-input" type="text" placeholder="Zona" class="p-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500 transition-shadow">
                    <input id="date-input" type="date" class="p-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500 transition-shadow">
                    <input id="expiration-date-input" type="date" placeholder="Vencimiento" class="p-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500 transition-shadow">
                </div>
                <button type="submit" class="w-full bg-blue-600 text-white p-3 rounded-lg font-semibold hover:bg-blue-700 transition-colors shadow-lg">
                    Agregar Producto
                </button>
            </form>

            <!-- Lista donde se mostrarán los elementos agregados -->
            <ul id="item-list" class="space-y-2">
                <!-- Los elementos se agregarán aquí dinámicamente -->
            </ul>
        </section>
    </div>

    <!-- Script de JavaScript para añadir interactividad -->
    <script>
        const form = document.getElementById('item-form');
        const productNameInput = document.getElementById('product-name-input');
        const batchInput = document.getElementById('batch-input');
        const zoneInput = document.getElementById('zone-input');
        const dateInput = document.getElementById('date-input');
        const expirationDateInput = document.getElementById('expiration-date-input');
        const list = document.getElementById('item-list');

        // Escucha el envío del formulario
        form.addEventListener('submit', (e) => {
            e.preventDefault(); // Evita que la página se recargue

            const productName = productNameInput.value.trim();
            const batch = batchInput.value.trim();
            const zone = zoneInput.value.trim();
            const date = dateInput.value;
            const expirationDate = expirationDateInput.value;

            if (productName && batch && zone && date && expirationDate) {
                // Crea un nuevo elemento para la lista
                const newItem = document.createElement('li');
                newItem.className = 'bg-gray-50 p-4 rounded-lg shadow-sm text-gray-800 space-y-1 relative';
                newItem.innerHTML = `
                    <button class="delete-btn absolute top-2 right-2 text-red-500 hover:text-red-700 transition-colors">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd" />
                        </svg>
                    </button>
                    <p class="font-bold text-lg">${productName}</p>
                    <p class="text-sm">Lote: <span class="font-semibold">${batch}</span></p>
                    <p class="text-sm">Zona: <span class="font-semibold">${zone}</span></p>
                    <p class="text-sm">Fecha: <span class="font-semibold">${date}</span></p>
                    <p class="text-sm">Vencimiento: <span class="font-semibold">${expirationDate}</span></p>
                `;

                // Agrega el nuevo elemento a la lista
                list.appendChild(newItem);

                // Limpia los campos de entrada
                form.reset();
            }
        });
        
        // Delegación de eventos para manejar clics en la lista
        list.addEventListener('click', (e) => {
            const deleteButton = e.target.closest('.delete-btn');
            if (deleteButton) {
                // Encuentra el elemento <li> padre y lo elimina
                const listItem = deleteButton.closest('li');
                listItem.remove();
            }
        });
    </script>

</body>
</html>
