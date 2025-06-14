# Minuta-IA-LK
Herramienta para tomar reuniones
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestor de Minutas de Reuniones</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <style>
        body {
            font-family: 'Arial', sans-serif;
        }
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            background-color: white;
            padding: 20px;
            border-radius: 5px;
            max-width: 500px;
            width: 100%;
        }
    </style>
</head>
<body class="bg-gray-100 p-5">

    <h1 class="text-2xl font-bold mb-5">Gestor de Minutas de Reuniones</h1>

    <div>
        <h2 class="text-xl font-semibold mb-3">Registro de Reunión</h2>
        <form id="meetingForm" class="bg-white p-4 rounded shadow-md">
            <label class="block mb-2">
                Cargo:
                <input type="text" id="position" required class="mt-1 block w-full border-gray-300 rounded p-2"/>
            </label>
            <label class="block mb-2">
                Correo Electrónico:
                <input type="email" id="email" required class="mt-1 block w-full border-gray-300 rounded p-2"/>
            </label>
            <label class="block mb-2">
                Número Telefónico (opcional):
                <input type="tel" id="phone" class="mt-1 block w-full border-gray-300 rounded p-2"/>
            </label>
            <button type="submit" class="bg-blue-500 text-white p-2 rounded mt-3 w-full">Agregar Participante</button>
        </form>
    </div>

    <div id="meetingNotes" class="mt-5">
        <h2 class="text-xl font-semibold mb-3">Notas de la Reunión</h2>
        <ol id="notesList" class="list-decimal pl-5"></ol>
        <button id="sendNotes" class="mt-3 bg-green-500 text-white p-2 rounded">Enviar Minuta</button>
    </div>

    <div class="modal" id="confirmationModal">
        <div class="modal-content">
            <p>¿Estás seguro de que deseas eliminar este participante?</p>
            <button id="confirmYes" class="bg-red-500 text-white p-2 rounded">Sí</button>
            <button id="confirmNo" class="bg-gray-300 text-black p-2 rounded">No</button>
        </div>
    </div>

    <script>
        const participants = [];

        // Añadir participante
        $("#meetingForm").on("submit", function(event) {
            event.preventDefault();
            const position = $("#position").val();
            const email = $("#email").val();
            const phone = $("#phone").val() || "No proporcionado";

            if (participants.some(p => p.email === email)) {
                alert("Este correo ya está registrado.");
                return;
            }

            participants.push({ position, email, phone });
            $("#notesList").append(`<li>${position} - ${email} (${phone})</li>`);
            $("#meetingForm")[0].reset();
        });

        // Enviar minutas (simulación)
        $("#sendNotes").on("click", function() {
            alert("Minuta enviada a: " + participants.map(p => p.email).join(", "));
        });

        // Modal de confirmación para eliminar (falta implementación)
        $("#notesList").on("click", "li", function() {
            $("#confirmationModal").show();
        });
        $("#confirmYes").on("click", function() {
            $("#confirmationModal").hide();
            // Aquí debería ir la lógica para eliminar el participante
            alert("Participante eliminado.");
        });
        $("#confirmNo").on("click", function() {
            $("#confirmationModal").hide();
        });
    </script>
</body>
</html>
