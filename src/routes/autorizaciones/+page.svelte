<script>
	let busqueda = $state('');
	let filtroEstado = $state('Todos');
	let filtroTipo = $state('Todos');

	let mostrarFormulario = $state(false);
	let mostrarDetalles = $state(false);

	let modoEdicion = $state(false);
	let autorizacionSeleccionada = $state(null);

	// =========================================================
	// PAGINACIÓN
	// =========================================================

	let paginaActual = $state(1);
	const autorizacionesPorPagina = 6;


	// =========================================================
	// 20 AUTORIZACIONES DE EJEMPLO
	// 12 APROBADAS + 5 PENDIENTES + 3 RECHAZADAS
	// =========================================================

	let autorizaciones = $state([
		{
			id: 1,
			estudiante: 'María Fernanda López',
			grado: '10°',
			acudiente: 'Laura López',
			actividad: 'Baloncesto',
			tipo: 'Actividad deportiva',
			icono: 'bi-dribbble',
			fechaSolicitud: '05 de septiembre de 2026',
			fechaRespuesta: '05 de septiembre de 2026',
			estado: 'Aprobada',
			observaciones: 'Autorización aprobada por el acudiente.'
		},
		{
			id: 2,
			estudiante: 'Juan Sebastián Pérez',
			grado: '9°',
			acudiente: 'Carlos Pérez',
			actividad: 'Robótica',
			tipo: 'Actividad académica',
			icono: 'bi-robot',
			fechaSolicitud: '06 de septiembre de 2026',
			fechaRespuesta: 'Pendiente',
			estado: 'Pendiente',
			observaciones: 'Se encuentra pendiente la respuesta del acudiente.'
		},
		{
			id: 3,
			estudiante: 'Valentina Rodríguez',
			grado: '11°',
			acudiente: 'Andrea Rodríguez',
			actividad: 'Teatro',
			tipo: 'Actividad artística',
			icono: 'bi-mask',
			fechaSolicitud: '06 de septiembre de 2026',
			fechaRespuesta: '06 de septiembre de 2026',
			estado: 'Aprobada',
			observaciones: 'Participación autorizada para la actividad.'
		},
		{
			id: 4,
			estudiante: 'Daniel Andrés Gómez',
			grado: '8°',
			acudiente: 'Sandra Gómez',
			actividad: 'Natación',
			tipo: 'Actividad deportiva',
			icono: 'bi-water',
			fechaSolicitud: '07 de septiembre de 2026',
			fechaRespuesta: '07 de septiembre de 2026',
			estado: 'Aprobada',
			observaciones: 'Autorización recibida correctamente.'
		},
		{
			id: 5,
			estudiante: 'Sofía Martínez',
			grado: '10°',
			acudiente: 'Jorge Martínez',
			actividad: 'Ajedrez',
			tipo: 'Actividad académica',
			icono: 'bi-grid-3x3-gap',
			fechaSolicitud: '07 de septiembre de 2026',
			fechaRespuesta: 'Pendiente',
			estado: 'Pendiente',
			observaciones: 'Pendiente de revisión por parte del acudiente.'
		},
		{
			id: 6,
			estudiante: 'Samuel Torres',
			grado: '7°',
			acudiente: 'Paola Torres',
			actividad: 'Danza',
			tipo: 'Actividad artística',
			icono: 'bi-music-note-beamed',
			fechaSolicitud: '08 de septiembre de 2026',
			fechaRespuesta: '08 de septiembre de 2026',
			estado: 'Rechazada',
			observaciones: 'El acudiente no autorizó la participación.'
		},
		{
			id: 7,
			estudiante: 'Gabriela Herrera',
			grado: '9°',
			acudiente: 'Miguel Herrera',
			actividad: 'Fútbol',
			tipo: 'Actividad deportiva',
			icono: 'bi-circle-fill',
			fechaSolicitud: '08 de septiembre de 2026',
			fechaRespuesta: 'Pendiente',
			estado: 'Pendiente',
			observaciones: 'Solicitud enviada y pendiente de respuesta.'
		},
		{
			id: 8,
			estudiante: 'Nicolás Ramírez',
			grado: '8°',
			acudiente: 'Claudia Ramírez',
			actividad: 'Programación',
			tipo: 'Actividad académica',
			icono: 'bi-code-slash',
			fechaSolicitud: '08 de septiembre de 2026',
			fechaRespuesta: '08 de septiembre de 2026',
			estado: 'Aprobada',
			observaciones: 'Autorización confirmada.'
		},
		{
			id: 9,
			estudiante: 'Laura Carolina Díaz',
			grado: '10°',
			acudiente: 'Ricardo Díaz',
			actividad: 'Pintura',
			tipo: 'Actividad artística',
			icono: 'bi-palette',
			fechaSolicitud: '09 de septiembre de 2026',
			fechaRespuesta: '09 de septiembre de 2026',
			estado: 'Aprobada',
			observaciones: 'Participación autorizada.'
		},
		{
			id: 10,
			estudiante: 'Mateo Castro',
			grado: '7°',
			acudiente: 'Diana Castro',
			actividad: 'Ciencias',
			tipo: 'Actividad académica',
			icono: 'bi-beaker',
			fechaSolicitud: '09 de septiembre de 2026',
			fechaRespuesta: 'Pendiente',
			estado: 'Pendiente',
			observaciones: 'Pendiente de respuesta del acudiente.'
		},
		{
			id: 11,
			estudiante: 'Isabella Moreno',
			grado: '11°',
			acudiente: 'Felipe Moreno',
			actividad: 'Voleibol',
			tipo: 'Actividad deportiva',
			icono: 'bi-volleyball',
			fechaSolicitud: '09 de septiembre de 2026',
			fechaRespuesta: '09 de septiembre de 2026',
			estado: 'Aprobada',
			observaciones: 'Autorización aprobada correctamente.'
		},
		{
			id: 12,
			estudiante: 'Sebastián Vargas',
			grado: '9°',
			acudiente: 'Natalia Vargas',
			actividad: 'Fotografía',
			tipo: 'Actividad artística',
			icono: 'bi-camera',
			fechaSolicitud: '10 de septiembre de 2026',
			fechaRespuesta: '10 de septiembre de 2026',
			estado: 'Aprobada',
			observaciones: 'Participación autorizada por el acudiente.'
		},
		{
			id: 13,
			estudiante: 'Camila Rojas',
			grado: '8°',
			acudiente: 'Andrés Rojas',
			actividad: 'Ciencia y Tecnología',
			tipo: 'Actividad académica',
			icono: 'bi-cpu',
			fechaSolicitud: '10 de septiembre de 2026',
			fechaRespuesta: 'Pendiente',
			estado: 'Pendiente',
			observaciones: 'Solicitud pendiente de confirmación.'
		},
		{
			id: 14,
			estudiante: 'Tomás Herrera',
			grado: '10°',
			acudiente: 'Mariana Herrera',
			actividad: 'Literatura',
			tipo: 'Actividad académica',
			icono: 'bi-book',
			fechaSolicitud: '11 de septiembre de 2026',
			fechaRespuesta: '11 de septiembre de 2026',
			estado: 'Aprobada',
			observaciones: 'Autorización aprobada.'
		},
		{
			id: 15,
			estudiante: 'Juliana Pérez',
			grado: '11°',
			acudiente: 'Fernando Pérez',
			actividad: 'Atletismo',
			tipo: 'Actividad deportiva',
			icono: 'bi-person-running',
			fechaSolicitud: '11 de septiembre de 2026',
			fechaRespuesta: '11 de septiembre de 2026',
			estado: 'Aprobada',
			observaciones: 'Autorización confirmada.'
		},
		{
			id: 16,
			estudiante: 'Alejandro Ruiz',
			grado: '9°',
			acudiente: 'Patricia Ruiz',
			actividad: 'Diseño Digital',
			tipo: 'Actividad académica',
			icono: 'bi-vector-pen',
			fechaSolicitud: '12 de septiembre de 2026',
			fechaRespuesta: '12 de septiembre de 2026',
			estado: 'Rechazada',
			observaciones: 'El acudiente no autorizó la actividad.'
		},
		{
			id: 17,
			estudiante: 'Sara González',
			grado: '8°',
			acudiente: 'Luis González',
			actividad: 'Coro Escolar',
			tipo: 'Actividad artística',
			icono: 'bi-mic',
			fechaSolicitud: '12 de septiembre de 2026',
			fechaRespuesta: '12 de septiembre de 2026',
			estado: 'Aprobada',
			observaciones: 'Autorización aprobada por el acudiente.'
		},
		{
			id: 18,
			estudiante: 'David Martínez',
			grado: '10°',
			acudiente: 'Carolina Martínez',
			actividad: 'Matemáticas Recreativas',
			tipo: 'Actividad académica',
			icono: 'bi-calculator',
			fechaSolicitud: '13 de septiembre de 2026',
			fechaRespuesta: 'Pendiente',
			estado: 'Pendiente',
			observaciones: 'Pendiente de revisión.'
		},
		{
			id: 19,
			estudiante: 'Ana María Torres',
			grado: '7°',
			acudiente: 'Julián Torres',
			actividad: 'Tenis de Mesa',
			tipo: 'Actividad deportiva',
			icono: 'bi-table',
			fechaSolicitud: '13 de septiembre de 2026',
			fechaRespuesta: '13 de septiembre de 2026',
			estado: 'Rechazada',
			observaciones: 'No se recibió autorización para la participación.'
		},
		{
			id: 20,
			estudiante: 'Emiliano Silva',
			grado: '11°',
			acudiente: 'Mónica Silva',
			actividad: 'Cine y Producción',
			tipo: 'Actividad artística',
			icono: 'bi-camera-reels',
			fechaSolicitud: '14 de septiembre de 2026',
			fechaRespuesta: '14 de septiembre de 2026',
			estado: 'Aprobada',
			observaciones: 'Participación autorizada correctamente.'
		}
	]);


	// =========================================================
	// FORMULARIO
	// =========================================================

	let formulario = $state({
		estudiante: '',
		grado: '',
		acudiente: '',
		actividad: 'Baloncesto',
		tipo: 'Actividad deportiva',
		icono: 'bi-dribbble',
		fechaSolicitud: '',
		fechaRespuesta: 'Pendiente',
		estado: 'Pendiente',
		observaciones: ''
	});


	// =========================================================
	// FILTROS
	// =========================================================

	let autorizacionesFiltradas = $derived(
		autorizaciones.filter((autorizacion) => {

			const texto = busqueda.toLowerCase();

			const coincideBusqueda =
				autorizacion.estudiante
					.toLowerCase()
					.includes(texto) ||
				autorizacion.acudiente
					.toLowerCase()
					.includes(texto) ||
				autorizacion.actividad
					.toLowerCase()
					.includes(texto);

			const coincideEstado =
				filtroEstado === 'Todos' ||
				autorizacion.estado === filtroEstado;

			const coincideTipo =
				filtroTipo === 'Todos' ||
				autorizacion.tipo === filtroTipo;

			return (
				coincideBusqueda &&
				coincideEstado &&
				coincideTipo
			);
		})
	);


	// =========================================================
	// INDICADORES
	// =========================================================

	let totalAutorizaciones = $derived(
		autorizaciones.length
	);


	let aprobadas = $derived(
		autorizaciones.filter(
			(autorizacion) =>
				autorizacion.estado === 'Aprobada'
		).length
	);


	let pendientes = $derived(
		autorizaciones.filter(
			(autorizacion) =>
				autorizacion.estado === 'Pendiente'
		).length
	);


	let rechazadas = $derived(
		autorizaciones.filter(
			(autorizacion) =>
				autorizacion.estado === 'Rechazada'
		).length
	);


	// =========================================================
	// PAGINACIÓN
	// =========================================================

	let totalPaginas = $derived(
		Math.max(
			1,
			Math.ceil(
				autorizacionesFiltradas.length /
					autorizacionesPorPagina
			)
		)
	);


	let autorizacionesPaginadas = $derived(
		autorizacionesFiltradas.slice(
			(paginaActual - 1) * autorizacionesPorPagina,
			paginaActual * autorizacionesPorPagina
		)
	);


	function irPagina(numero) {
		paginaActual = Math.max(
			1,
			Math.min(numero, totalPaginas)
		);
	}


	function paginaAnterior() {
		if (paginaActual > 1) {
			paginaActual--;
		}
	}


	function paginaSiguiente() {
		if (paginaActual < totalPaginas) {
			paginaActual++;
		}
	}


	// =========================================================
	// FORMULARIOS
	// =========================================================

	function abrirNuevaAutorizacion() {

		modoEdicion = false;
		autorizacionSeleccionada = null;

		formulario = {
			estudiante: '',
			grado: '',
			acudiente: '',
			actividad: 'Baloncesto',
			tipo: 'Actividad deportiva',
			icono: 'bi-dribbble',
			fechaSolicitud: '',
			fechaRespuesta: 'Pendiente',
			estado: 'Pendiente',
			observaciones: ''
		};

		mostrarFormulario = true;
	}


	function editarAutorizacion(autorizacion) {

		modoEdicion = true;
		autorizacionSeleccionada = autorizacion;

		formulario = {
			estudiante: autorizacion.estudiante,
			grado: autorizacion.grado,
			acudiente: autorizacion.acudiente,
			actividad: autorizacion.actividad,
			tipo: autorizacion.tipo,
			icono: autorizacion.icono,
			fechaSolicitud: autorizacion.fechaSolicitud,
			fechaRespuesta: autorizacion.fechaRespuesta,
			estado: autorizacion.estado,
			observaciones: autorizacion.observaciones
		};

		mostrarFormulario = true;
	}


	function guardarAutorizacion() {

		if (
			!formulario.estudiante.trim() ||
			!formulario.grado.trim() ||
			!formulario.acudiente.trim() ||
			!formulario.fechaSolicitud.trim()
		) {
			return;
		}


		if (modoEdicion) {

			autorizaciones = autorizaciones.map(
				(autorizacion) =>
					autorizacion.id ===
					autorizacionSeleccionada.id
						? {
								...autorizacion,
								estudiante:
									formulario.estudiante,
								grado:
									formulario.grado,
								acudiente:
									formulario.acudiente,
								actividad:
									formulario.actividad,
								tipo:
									formulario.tipo,
								icono:
									formulario.icono,
								fechaSolicitud:
									formulario.fechaSolicitud,
								fechaRespuesta:
									formulario.fechaRespuesta,
								estado:
									formulario.estado,
								observaciones:
									formulario.observaciones
							}
						: autorizacion
			);

		} else {

			const nuevaAutorizacion = {
				id: Date.now(),
				estudiante:
					formulario.estudiante,
				grado:
					formulario.grado,
				acudiente:
					formulario.acudiente,
				actividad:
					formulario.actividad,
				tipo:
					formulario.tipo,
				icono:
					formulario.icono,
				fechaSolicitud:
					formulario.fechaSolicitud,
				fechaRespuesta:
					formulario.fechaRespuesta,
				estado:
					formulario.estado,
				observaciones:
					formulario.observaciones
			};

			autorizaciones = [
				...autorizaciones,
				nuevaAutorizacion
			];
		}


		cerrarFormulario();
	}


	function eliminarAutorizacion(autorizacion) {

		const confirmar = confirm(
			`¿Deseas eliminar la autorización de "${autorizacion.estudiante}"?`
		);

		if (!confirmar) {
			return;
		}


		autorizaciones =
			autorizaciones.filter(
				(item) =>
					item.id !== autorizacion.id
			);


		if (paginaActual > totalPaginas) {
			paginaActual = totalPaginas;
		}
	}


	// =========================================================
	// ESTADOS
	// =========================================================

	function aprobarAutorizacion(autorizacion) {

		autorizaciones = autorizaciones.map(
			(item) =>
				item.id === autorizacion.id
					? {
							...item,
							estado: 'Aprobada',
							fechaRespuesta:
								'08 de septiembre de 2026',
							observaciones:
								'Autorización aprobada.'
						}
					: item
		);
	}


	function rechazarAutorizacion(autorizacion) {

		autorizaciones = autorizaciones.map(
			(item) =>
				item.id === autorizacion.id
					? {
							...item,
							estado: 'Rechazada',
							fechaRespuesta:
								'08 de septiembre de 2026',
							observaciones:
								'Autorización rechazada.'
						}
					: item
		);
	}


	// =========================================================
	// MODALES
	// =========================================================

	function verDetalles(autorizacion) {

		autorizacionSeleccionada =
			autorizacion;

		mostrarDetalles = true;
	}


	function cerrarFormulario() {

		mostrarFormulario = false;
		modoEdicion = false;
		autorizacionSeleccionada = null;
	}


	function cerrarDetalles() {

		mostrarDetalles = false;
		autorizacionSeleccionada = null;
	}


	// =========================================================
	// TIPO E ICONOS
	// =========================================================

	function actualizarTipo() {

		const tipos = {

			Baloncesto:
				'Actividad deportiva',

			Natación:
				'Actividad deportiva',

			Fútbol:
				'Actividad deportiva',

			Voleibol:
				'Actividad deportiva',

			Atletismo:
				'Actividad deportiva',

			'Tennis de Mesa':
				'Actividad deportiva',

			'Tenis de Mesa':
				'Actividad deportiva',

			Robótica:
				'Actividad académica',

			Ajedrez:
				'Actividad académica',

			Programación:
				'Actividad académica',

			Ciencias:
				'Actividad académica',

			'Literatura':
				'Actividad académica',

			'Matemáticas Recreativas':
				'Actividad académica',

			'Diseño Digital':
				'Actividad académica',

			'Teatro':
				'Actividad artística',

			Danza:
				'Actividad artística',

			Pintura:
				'Actividad artística',

			Fotografía:
				'Actividad artística',

			'Coro Escolar':
				'Actividad artística',

			'Cine y Producción':
				'Actividad artística',

			'Ciencia y Tecnología':
				'Actividad académica'
		};


		const iconos = {

			Baloncesto:
				'bi-dribbble',

			Natación:
				'bi-water',

			Fútbol:
				'bi-circle-fill',

			Voleibol:
				'bi-volleyball',

			Atletismo:
				'bi-person-running',

			'Tenis de Mesa':
				'bi-table',

			Robótica:
				'bi-robot',

			Ajedrez:
				'bi-grid-3x3-gap',

			Programación:
				'bi-code-slash',

			Ciencias:
				'bi-beaker',

			'Literatura':
				'bi-book',

			'Matemáticas Recreativas':
				'bi-calculator',

			'Ciencia y Tecnología':
				'bi-cpu',

			'Diseño Digital':
				'bi-vector-pen',

			Teatro:
				'bi-mask',

			Danza:
				'bi-music-note-beamed',

			Pintura:
				'bi-palette',

			Fotografía:
				'bi-camera',

			'Coro Escolar':
				'bi-mic',

			'Cine y Producción':
				'bi-camera-reels'
		};


		formulario.tipo =
			tipos[formulario.actividad] ||
			'Actividad deportiva';

		formulario.icono =
			iconos[formulario.actividad] ||
			'bi-calendar-event';
	}


	function claseEstado(estado) {

		if (estado === 'Aprobada') {
			return 'status-approved';
		}

		if (estado === 'Pendiente') {
			return 'status-pending';
		}

		if (estado === 'Rechazada') {
			return 'status-rejected';
		}

		return 'status-default';
	}


	function iconoEstado(estado) {

		if (estado === 'Aprobada') {
			return 'bi-check-circle';
		}

		if (estado === 'Pendiente') {
			return 'bi-clock';
		}

		if (estado === 'Rechazada') {
			return 'bi-x-circle';
		}

		return 'bi-circle';
	}
</script>


<svelte:head>
	<title>Autorizaciones | Colegio San Miguel</title>
</svelte:head>


<div class="container-fluid px-4 py-4">

	<!-- =====================================================
	     ENCABEZADO
	     ===================================================== -->

	<div class="page-header">

		<div>

			<h2>
				Autorizaciones
			</h2>

			<p>
				Revisa y administra las autorizaciones de los acudientes.
			</p>

		</div>


		<button
			class="btn btn-primary new-button"
			onclick={abrirNuevaAutorizacion}
		>
			<i class="bi bi-plus-lg"></i>
			Nueva autorización
		</button>

	</div>


	<!-- =====================================================
	     INDICADORES
	     ===================================================== -->

	<div class="row g-3 mb-4">

		<div class="col-md-6 col-xl-3">

			<div class="soft-card indicator-card">

				<div class="icon-soft blue">
					<i class="bi bi-file-earmark-check"></i>
				</div>

				<div>

					<span class="indicator-label">
						Autorizaciones
					</span>

					<strong>
						{totalAutorizaciones}
					</strong>

				</div>

			</div>

		</div>


		<div class="col-md-6 col-xl-3">

			<div class="soft-card indicator-card">

				<div class="icon-soft green">
					<i class="bi bi-check-circle"></i>
				</div>

				<div>

					<span class="indicator-label">
						Aprobadas
					</span>

					<strong>
						{aprobadas}
					</strong>

				</div>

			</div>

		</div>


		<div class="col-md-6 col-xl-3">

			<div class="soft-card indicator-card">

				<div class="icon-soft orange">
					<i class="bi bi-clock"></i>
				</div>

				<div>

					<span class="indicator-label">
						Pendientes
					</span>

					<strong>
						{pendientes}
					</strong>

				</div>

			</div>

		</div>


		<div class="col-md-6 col-xl-3">

			<div class="soft-card indicator-card">

				<div class="icon-soft red">
					<i class="bi bi-x-circle"></i>
				</div>

				<div>

					<span class="indicator-label">
						Rechazadas
					</span>

					<strong>
						{rechazadas}
					</strong>

				</div>

			</div>

		</div>

	</div>


	<!-- =====================================================
	     FILTROS
	     ===================================================== -->

	<div class="soft-card filters-card">

		<div class="filters-header">

			<div>

				<h3>
					Autorizaciones
				</h3>

				<span>
					{autorizacionesFiltradas.length} resultados
				</span>

			</div>

		</div>


		<div class="filters">

			<div class="search-box">

				<span>
					<i class="bi bi-search"></i>
				</span>

				<input
					type="text"
					placeholder="Buscar estudiante, acudiente o actividad..."
					bind:value={busqueda}
					oninput={() => (paginaActual = 1)}
				/>

			</div>


			<select
				class="form-select"
				bind:value={filtroEstado}
				onchange={() => (paginaActual = 1)}
			>

				<option value="Todos">
					Todos los estados
				</option>

				<option value="Aprobada">
					Aprobadas
				</option>

				<option value="Pendiente">
					Pendientes
				</option>

				<option value="Rechazada">
					Rechazadas
				</option>

			</select>


			<select
				class="form-select"
				bind:value={filtroTipo}
				onchange={() => (paginaActual = 1)}
			>

				<option value="Todos">
					Todos los tipos
				</option>

				<option value="Actividad deportiva">
					Deportivas
				</option>

				<option value="Actividad académica">
					Académicas
				</option>

				<option value="Actividad artística">
					Artísticas
				</option>

			</select>

		</div>

	</div>


	<!-- =====================================================
	     TABLA
	     ===================================================== -->

	<div class="soft-card table-card">

		<div class="table-responsive">

			<table class="table align-middle">

				<thead>

					<tr>

						<th>
							Estudiante
						</th>

						<th>
							Actividad
						</th>

						<th>
							Acudiente
						</th>

						<th>
							Solicitud
						</th>

						<th>
							Estado
						</th>

						<th class="text-end">
							Acciones
						</th>

					</tr>

				</thead>


				<tbody>

					{#if autorizacionesFiltradas.length > 0}

						{#each autorizacionesPaginadas as autorizacion}

							<tr>

								<!-- ESTUDIANTE -->

								<td>

									<div class="student-cell">

										<div class="student-avatar">

											{autorizacion.estudiante
												.split(' ')
												.slice(0, 2)
												.map((nombre) =>
													nombre.charAt(0)
												)
												.join('')}

										</div>


										<div>

											<strong>
												{autorizacion.estudiante}
											</strong>

											<span>
												{autorizacion.grado}
											</span>

										</div>

									</div>

								</td>


								<!-- ACTIVIDAD -->

								<td>

									<div class="activity-cell">

										<div class="activity-icon">
											<i
												class={`bi ${autorizacion.icono}`}
											></i>
										</div>


										<div>

											<strong>
												{autorizacion.actividad}
											</strong>

											<span>
												{autorizacion.tipo}
											</span>

										</div>

									</div>

								</td>


								<!-- ACUDIENTE -->

								<td>

									<div class="guardian-cell">

										<span class="guardian-icon">
											<i class="bi bi-person"></i>
										</span>

										<span>
											{autorizacion.acudiente}
										</span>

									</div>

								</td>


								<!-- FECHA -->

								<td>

									<span class="date-text">
										{autorizacion.fechaSolicitud}
									</span>

								</td>


								<!-- ESTADO -->

								<td>

									<span
										class={`status-badge ${claseEstado(
											autorizacion.estado
										)}`}
									>

										<i
											class={`bi ${iconoEstado(
												autorizacion.estado
											)}`}
										></i>

										{autorizacion.estado}

									</span>

								</td>


								<!-- ACCIONES -->

								<td>

									<div class="actions">

										{#if autorizacion.estado === 'Pendiente'}

											<button
												class="action-btn approve"
												title="Aprobar"
												aria-label="Aprobar autorización"
												onclick={() =>
													aprobarAutorizacion(
														autorizacion
													)}
											>
												<i class="bi bi-check-lg"></i>
											</button>


											<button
												class="action-btn reject"
												title="Rechazar"
												aria-label="Rechazar autorización"
												onclick={() =>
													rechazarAutorizacion(
														autorizacion
													)}
											>
												<i class="bi bi-x-lg"></i>
											</button>

										{/if}


										<button
											class="action-btn"
											title="Ver detalles"
											aria-label="Ver detalles"
											onclick={() =>
												verDetalles(
													autorizacion
												)}
										>
											<i class="bi bi-eye"></i>
										</button>


										<button
											class="action-btn"
											title="Editar"
											aria-label="Editar autorización"
											onclick={() =>
												editarAutorizacion(
													autorizacion
												)}
										>
											<i class="bi bi-pencil"></i>
										</button>


										<button
											class="action-btn delete"
											title="Eliminar"
											aria-label="Eliminar autorización"
											onclick={() =>
												eliminarAutorizacion(
													autorizacion
												)}
										>
											<i class="bi bi-trash3"></i>
										</button>

									</div>

								</td>

							</tr>

						{/each}

					{:else}

						<tr>

							<td
								colspan="6"
								class="empty-cell"
							>

								<div class="empty-state">

									<div class="empty-icon">
										<i class="bi bi-search"></i>
									</div>

									<strong>
										No se encontraron autorizaciones
									</strong>

									<span>
										Prueba con otro estudiante,
										acudiente o filtro.
									</span>

								</div>

							</td>

						</tr>

					{/if}

				</tbody>

			</table>

		</div>

	</div>


	<!-- =====================================================
	     PAGINACIÓN
	     ===================================================== -->

	{#if autorizacionesFiltradas.length > 0 && totalPaginas > 1}

		<div class="pagination-container">

			<button
				class="pagination-button"
				disabled={paginaActual === 1}
				onclick={paginaAnterior}
			>
				<i class="bi bi-chevron-left"></i>
				Anterior
			</button>


			<div class="pagination-pages">

				{#each Array(totalPaginas) as _, index}

					<button
						class="pagination-number"
						class:active={paginaActual === index + 1}
						onclick={() =>
							irPagina(index + 1)}
					>
						{index + 1}
					</button>

				{/each}

			</div>


			<button
				class="pagination-button"
				disabled={paginaActual === totalPaginas}
				onclick={paginaSiguiente}
			>
				Siguiente
				<i class="bi bi-chevron-right"></i>
			</button>

		</div>

	{/if}

</div>


<!-- =========================================================
     MODAL NUEVA / EDITAR AUTORIZACIÓN
     ========================================================= -->

{#if mostrarFormulario}

	<div
		class="modal-backdrop-custom"
		role="presentation"
		onclick={(event) => {

			if (
				event.target ===
				event.currentTarget
			) {
				cerrarFormulario();
			}

		}}
	>

		<div
			class="form-modal"
			role="dialog"
			aria-modal="true"
		>

			<div class="modal-header-custom">

				<div>

					<h3>
						{modoEdicion
							? 'Editar autorización'
							: 'Nueva autorización'}
					</h3>

					<p>
						Registra la información correspondiente.
					</p>

				</div>


				<button
					class="close-button"
					type="button"
					onclick={cerrarFormulario}
					aria-label="Cerrar"
				>
					<i class="bi bi-x-lg"></i>
				</button>

			</div>


			<div class="modal-body-custom">

				<div class="row g-3 mb-3">

					<div class="col-md-8">

						<label
							class="form-label"
							for="estudiante"
						>
							Estudiante
						</label>

						<input
							id="estudiante"
							type="text"
							class="form-control"
							placeholder="Nombre completo"
							bind:value={formulario.estudiante}
						/>

					</div>


					<div class="col-md-4">

						<label
							class="form-label"
							for="grado"
						>
							Grado
						</label>

						<input
							id="grado"
							type="text"
							class="form-control"
							placeholder="Ej. 10°"
							bind:value={formulario.grado}
						/>

					</div>

				</div>


				<div class="mb-3">

					<label
						class="form-label"
						for="acudiente"
					>
						Padre / acudiente
					</label>

					<input
						id="acudiente"
						type="text"
						class="form-control"
						placeholder="Nombre completo del acudiente"
						bind:value={formulario.acudiente}
					/>

				</div>


				<div class="row g-3 mb-3">

					<div class="col-md-7">

						<label
							class="form-label"
							for="actividad"
						>
							Actividad
						</label>

						<select
							id="actividad"
							class="form-select"
							bind:value={formulario.actividad}
							onchange={actualizarTipo}
						>

							<option value="Baloncesto">
								Baloncesto
							</option>

							<option value="Robótica">
								Robótica
							</option>

							<option value="Teatro">
								Teatro
							</option>

							<option value="Natación">
								Natación
							</option>

							<option value="Ajedrez">
								Ajedrez
							</option>

							<option value="Danza">
								Danza
							</option>

							<option value="Fútbol">
								Fútbol
							</option>

							<option value="Programación">
								Programación
							</option>

							<option value="Pintura">
								Pintura
							</option>

							<option value="Ciencias">
								Ciencias
							</option>

							<option value="Voleibol">
								Voleibol
							</option>

							<option value="Fotografía">
								Fotografía
							</option>

							<option value="Ciencia y Tecnología">
								Ciencia y Tecnología
							</option>

							<option value="Literatura">
								Literatura
							</option>

							<option value="Atletismo">
								Atletismo
							</option>

							<option value="Diseño Digital">
								Diseño Digital
							</option>

							<option value="Coro Escolar">
								Coro Escolar
							</option>

							<option value="Matemáticas Recreativas">
								Matemáticas Recreativas
							</option>

							<option value="Tenis de Mesa">
								Tenis de Mesa
							</option>

							<option value="Cine y Producción">
								Cine y Producción
							</option>

						</select>

					</div>


					<div class="col-md-5">

						<label
							class="form-label"
							for="tipo"
						>
							Tipo
						</label>

						<select
							id="tipo"
							class="form-select"
							bind:value={formulario.tipo}
						>

							<option value="Actividad deportiva">
								Deportiva
							</option>

							<option value="Actividad académica">
								Académica
							</option>

							<option value="Actividad artística">
								Artística
							</option>

						</select>

					</div>

				</div>


				<div class="row g-3 mb-3">

					<div class="col-md-6">

						<label
							class="form-label"
							for="fechaSolicitud"
						>
							Fecha de solicitud
						</label>

						<input
							id="fechaSolicitud"
							type="text"
							class="form-control"
							placeholder="Ej. 10 de septiembre de 2026"
							bind:value={formulario.fechaSolicitud}
						/>

					</div>


					<div class="col-md-6">

						<label
							class="form-label"
							for="estado"
						>
							Estado
						</label>

						<select
							id="estado"
							class="form-select"
							bind:value={formulario.estado}
						>

							<option value="Pendiente">
								Pendiente
							</option>

							<option value="Aprobada">
								Aprobada
							</option>

							<option value="Rechazada">
								Rechazada
							</option>

						</select>

					</div>

				</div>


				<div class="mb-3">

					<label
						class="form-label"
						for="fechaRespuesta"
					>
						Fecha de respuesta
					</label>

					<input
						id="fechaRespuesta"
						type="text"
						class="form-control"
						placeholder="Ej. 10 de septiembre de 2026"
						bind:value={formulario.fechaRespuesta}
					/>

				</div>


				<div>

					<label
						class="form-label"
						for="observaciones"
					>
						Observaciones
					</label>

					<textarea
						id="observaciones"
						class="form-control"
						rows="3"
						placeholder="Observaciones..."
						bind:value={formulario.observaciones}
					></textarea>

				</div>

			</div>


			<div class="modal-footer-custom">

				<button
					type="button"
					class="btn btn-light cancel-button"
					onclick={cerrarFormulario}
				>
					Cancelar
				</button>


				<button
					type="button"
					class="btn btn-primary save-button"
					onclick={guardarAutorizacion}
				>
					<i class="bi bi-check2"></i>
					{modoEdicion
						? 'Guardar cambios'
						: 'Crear autorización'}
				</button>

			</div>

		</div>

	</div>

{/if}


<!-- =========================================================
     MODAL DETALLES
     ========================================================= -->

{#if mostrarDetalles && autorizacionSeleccionada}

	<div
		class="modal-backdrop-custom"
		role="presentation"
		onclick={(event) => {

			if (
				event.target ===
				event.currentTarget
			) {
				cerrarDetalles();
			}

		}}
	>

		<div
			class="details-modal"
			role="dialog"
			aria-modal="true"
			aria-labelledby="details-title"
		>

			<!-- CABECERA -->

			<div class="details-header">

				<div class="details-heading">

					<div class="student-avatar large">

						{autorizacionSeleccionada.estudiante
							.split(' ')
							.slice(0, 2)
							.map((nombre) =>
								nombre.charAt(0)
							)
							.join('')}

					</div>


					<div>

						<span class="details-label">
							Autorización
						</span>

						<h3 id="details-title">
							{autorizacionSeleccionada.estudiante}
						</h3>

						<span class="details-grade">
							{autorizacionSeleccionada.grado}
						</span>

					</div>

				</div>


				<button
					class="close-button"
					type="button"
					onclick={cerrarDetalles}
					aria-label="Cerrar"
				>
					<i class="bi bi-x-lg"></i>
				</button>

			</div>


			<!-- CUERPO -->

			<div class="details-body">

				<!-- ESTADO -->

				<section class="detail-section">

					<span class="section-label">
						Estado actual
					</span>


					<div class="status-large-wrapper">

						<div
							class={`status-large ${claseEstado(
								autorizacionSeleccionada.estado
							)}`}
						>

							<div class="status-large-icon">

								<i
									class={`bi ${iconoEstado(
										autorizacionSeleccionada.estado
									)}`}
								></i>

							</div>


							<div>

								<strong>
									{autorizacionSeleccionada.estado}
								</strong>

								<span>
									Estado de la autorización
								</span>

							</div>

						</div>

					</div>

				</section>


				<!-- ACTIVIDAD -->

				<section class="detail-section">

					<span class="section-label">
						Actividad
					</span>


					<div class="activity-detail">

						<div class="activity-icon large">

							<i
								class={`bi ${autorizacionSeleccionada.icono}`}
							></i>

						</div>


						<div>

							<strong>
								{autorizacionSeleccionada.actividad}
							</strong>

							<span>
								{autorizacionSeleccionada.tipo}
							</span>

						</div>

					</div>

				</section>


				<!-- INFORMACIÓN -->

				<section class="detail-section">

					<span class="section-label">
						Información
					</span>


					<div class="details-grid">

						<div>

							<span>
								Estudiante
							</span>

							<strong>
								{autorizacionSeleccionada.estudiante}
							</strong>

						</div>


						<div>

							<span>
								Grado
							</span>

							<strong>
								{autorizacionSeleccionada.grado}
							</strong>

						</div>


						<div>

							<span>
								Padre / acudiente
							</span>

							<strong>
								{autorizacionSeleccionada.acudiente}
							</strong>

						</div>


						<div>

							<span>
								Identificador
							</span>

							<strong>
								#{autorizacionSeleccionada.id}
							</strong>

						</div>

					</div>

				</section>


				<!-- FECHAS -->

				<section class="detail-section">

					<span class="section-label">
						Seguimiento de fechas
					</span>


					<div class="timeline">

						<div class="timeline-item">

							<div class="timeline-marker">

								<i class="bi bi-send"></i>

							</div>


							<div>

								<strong>
									Solicitud enviada
								</strong>

								<span>
									{autorizacionSeleccionada.fechaSolicitud}
								</span>

							</div>

						</div>


						<div class="timeline-line"></div>


						<div class="timeline-item">

							<div class="timeline-marker">

								<i
									class={`bi ${
										autorizacionSeleccionada.estado ===
										'Pendiente'
											? 'bi-clock'
											: 'bi-check2'
									}`}
								></i>

							</div>


							<div>

								<strong>
									Respuesta
								</strong>

								<span>
									{autorizacionSeleccionada.fechaRespuesta}
								</span>

							</div>

						</div>

					</div>

				</section>


				<!-- OBSERVACIONES -->

				<section class="detail-section">

					<span class="section-label">
						Observaciones
					</span>


					<div class="observation-box">

						<span>
							{autorizacionSeleccionada.observaciones ||
								'Sin observaciones registradas.'}
						</span>

					</div>

				</section>


				<!-- RESUMEN -->

				<section class="detail-section">

					<span class="section-label">
						Resumen
					</span>


					<div class="summary-box">

						<div class="summary-item">

							<span>
								Estudiante
							</span>

							<strong>
								{autorizacionSeleccionada.estudiante}
							</strong>

						</div>


						<div class="summary-item">

							<span>
								Actividad
							</span>

							<strong>
								{autorizacionSeleccionada.actividad}
							</strong>

						</div>


						<div class="summary-item">

							<span>
								Acudiente
							</span>

							<strong>
								{autorizacionSeleccionada.acudiente}
							</strong>

						</div>


						<div class="summary-item">

							<span>
								Estado
							</span>

							<strong>
								{autorizacionSeleccionada.estado}
							</strong>

						</div>

					</div>

				</section>

			</div>


			<!-- PIE -->

			<div class="details-footer">

				<button
					class="btn btn-light cancel-button"
					onclick={cerrarDetalles}
				>
					Cerrar
				</button>


				{#if autorizacionSeleccionada.estado === 'Pendiente'}

					<button
						class="btn btn-outline-danger action-footer-button"
						onclick={() => {

							const autorizacion =
								autorizacionSeleccionada;

							rechazarAutorizacion(
								autorizacion
							);

							autorizacionSeleccionada =
								{
									...autorizacion,
									estado: 'Rechazada',
									fechaRespuesta:
										'08 de septiembre de 2026',
									observaciones:
										'Autorización rechazada.'
								};

						}}
					>
						<i class="bi bi-x-lg"></i>
						Rechazar
					</button>


					<button
						class="btn btn-primary save-button"
						onclick={() => {

							const autorizacion =
								autorizacionSeleccionada;

							aprobarAutorizacion(
								autorizacion
							);

							autorizacionSeleccionada =
								{
									...autorizacion,
									estado: 'Aprobada',
									fechaRespuesta:
										'08 de septiembre de 2026',
									observaciones:
										'Autorización aprobada.'
								};

						}}
					>
						<i class="bi bi-check-lg"></i>
						Aprobar
					</button>

				{:else}

					<button
						class="btn btn-primary save-button"
						onclick={() => {

							const autorizacion =
								autorizacionSeleccionada;

							cerrarDetalles();

							editarAutorizacion(
								autorizacion
							);

						}}
					>
						<i class="bi bi-pencil"></i>
						Editar autorización
					</button>

				{/if}

			</div>

		</div>

	</div>

{/if}


<style>

	/* =========================================================
	   ENCABEZADO
	   ========================================================= */

	.page-header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 20px;
		margin-bottom: 25px;
	}


	.page-header h2 {
		margin: 0 0 5px;
		color: #212529;
		font-size: 25px;
		font-weight: 700;
	}


	.page-header p {
		margin: 0;
		color: #868e96;
		font-size: 13px;
	}


	.new-button {
		height: 42px;
		padding: 0 17px;
		border-radius: 9px;
		font-size: 13px;
		font-weight: 600;
	}


	.new-button i {
		margin-right: 6px;
	}


	/* =========================================================
	   TARJETAS
	   ========================================================= */

	.soft-card {
		background: #ffffff;
		border: 1px solid #edf0f2;
		border-radius: 13px;
		box-shadow:
			0 3px 14px rgba(0, 0, 0, 0.035);
	}


	.indicator-card {
		min-height: 90px;
		padding: 17px;
		display: flex;
		align-items: center;
		gap: 13px;
	}


	.icon-soft {
		width: 43px;
		height: 43px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 11px;
		font-size: 19px;
	}


	.icon-soft.blue {
		background: #eaf2ff;
		color: #0d6efd;
	}


	.icon-soft.green {
		background: #e9f7ef;
		color: #198754;
	}


	.icon-soft.orange {
		background: #fff2e5;
		color: #d97706;
	}


	.icon-soft.red {
		background: #fff0f1;
		color: #dc3545;
	}


	.indicator-label {
		display: block;
		margin-bottom: 2px;
		color: #868e96;
		font-size: 11px;
	}


	.indicator-card strong {
		display: block;
		color: #343a40;
		font-size: 22px;
		font-weight: 700;
	}


	/* =========================================================
	   FILTROS
	   ========================================================= */

	.filters-card {
		padding: 19px 22px;
		margin-bottom: 15px;
	}


	.filters-header {
		margin-bottom: 15px;
	}


	.filters-header h3 {
		margin: 0 0 3px;
		color: #343a40;
		font-size: 15px;
		font-weight: 650;
	}


	.filters-header span {
		color: #adb5bd;
		font-size: 11px;
	}


	.filters {
		display: flex;
		align-items: center;
		gap: 10px;
	}


	.search-box {
		position: relative;
		flex: 1;
	}


	.search-box > span {
		position: absolute;
		left: 12px;
		top: 50%;
		transform: translateY(-50%);
		color: #adb5bd;
		font-size: 14px;
	}


	.search-box input {
		width: 100%;
		height: 38px;
		padding: 0 12px 0 35px;
		border: 1px solid #e1e5e9;
		border-radius: 8px;
		outline: none;
		font-size: 12px;
	}


	.search-box input:focus {
		border-color: #86b7fe;
		box-shadow:
			0 0 0 0.15rem
			rgba(13, 110, 253, 0.08);
	}


	.filters .form-select {
		width: 205px;
		height: 38px;
		border-radius: 8px;
		font-size: 12px;
	}


	/* =========================================================
	   TABLA
	   ========================================================= */

	.table-card {
		overflow: hidden;
	}


	.table {
		margin: 0;
		font-size: 12px;
	}


	.table thead th {
		padding: 14px 16px;
		background: #fafbfc;
		border-bottom: 1px solid #edf0f2;
		color: #868e96;
		font-size: 10px;
		font-weight: 600;
		white-space: nowrap;
	}


	.table tbody td {
		padding: 14px 16px;
		border-color: #f0f2f4;
		vertical-align: middle;
	}


	.table tbody tr:last-child td {
		border-bottom: none;
	}


	.table tbody tr:hover {
		background: #fcfdff;
	}


	/* =========================================================
	   ESTUDIANTE
	   ========================================================= */

	.student-cell {
		display: flex;
		align-items: center;
		gap: 10px;
		min-width: 190px;
	}


	.student-avatar {
		width: 34px;
		height: 34px;
		flex-shrink: 0;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 50%;
		background: #eaf2ff;
		color: #0d6efd;
		font-size: 10px;
		font-weight: 700;
	}


	.student-avatar.large {
		width: 48px;
		height: 48px;
		font-size: 13px;
	}


	.student-cell strong {
		display: block;
		margin-bottom: 2px;
		color: #343a40;
		font-size: 12px;
		font-weight: 600;
	}


	.student-cell span {
		display: block;
		color: #adb5bd;
		font-size: 10px;
	}


	/* =========================================================
	   ACTIVIDAD
	   ========================================================= */

	.activity-cell {
		display: flex;
		align-items: center;
		gap: 9px;
		min-width: 170px;
	}


	.activity-icon {
		width: 34px;
		height: 34px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 9px;
		background: #f4f7fb;
		color: #0d6efd;
		font-size: 16px;
		flex-shrink: 0;
	}


	.activity-icon.large {
		width: 43px;
		height: 43px;
		font-size: 21px;
	}


	.activity-cell strong {
		display: block;
		margin-bottom: 2px;
		color: #495057;
		font-size: 11px;
		font-weight: 600;
	}


	.activity-cell span {
		display: block;
		color: #adb5bd;
		font-size: 9px;
	}


	/* =========================================================
	   ACUDIENTE
	   ========================================================= */

	.guardian-cell {
		display: flex;
		align-items: center;
		gap: 7px;
		min-width: 145px;
		color: #6c757d;
		font-size: 10px;
	}


	.guardian-icon {
		width: 25px;
		height: 25px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 7px;
		background: #f8f9fa;
		color: #6c757d;
		font-size: 12px;
	}


	.date-text {
		color: #6c757d;
		font-size: 10px;
		white-space: nowrap;
	}


	/* =========================================================
	   ESTADOS
	   ========================================================= */

	.status-badge {
		display: inline-flex;
		align-items: center;
		gap: 5px;
		padding: 5px 9px;
		border-radius: 20px;
		font-size: 9px;
		font-weight: 600;
		white-space: nowrap;
	}


	.status-approved {
		background: #e9f7ef;
		color: #198754;
	}


	.status-pending {
		background: #fff2e5;
		color: #d97706;
	}


	.status-rejected {
		background: #fff0f1;
		color: #dc3545;
	}


	.status-default {
		background: #f1f3f5;
		color: #6c757d;
	}


	/* =========================================================
	   ACCIONES
	   ========================================================= */

	.actions {
		display: flex;
		align-items: center;
		justify-content: flex-end;
		gap: 5px;
		min-width: max-content;
	}


	.action-btn {
		width: 30px;
		height: 30px;
		display: flex;
		align-items: center;
		justify-content: center;
		border: 1px solid #edf0f2;
		border-radius: 7px;
		background: #ffffff;
		color: #0d6efd;
		font-size: 12px;
		cursor: pointer;
	}


	.action-btn:hover {
		background: #eef5ff;
		border-color: #d5e5ff;
	}


	.action-btn.approve {
		color: #198754;
	}


	.action-btn.approve:hover {
		background: #e9f7ef;
		border-color: #ccebd9;
	}


	.action-btn.reject {
		color: #dc3545;
	}


	.action-btn.reject:hover {
		background: #fff0f1;
		border-color: #f1cdd1;
	}


	.action-btn.delete {
		color: #adb5bd;
	}


	.action-btn.delete:hover {
		color: #dc3545;
		background: #fff5f5;
		border-color: #f5d8da;
	}


	/* =========================================================
	   PAGINACIÓN
	   ========================================================= */

	.pagination-container {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 12px;
		margin-top: 24px;
		margin-bottom: 10px;
	}


	.pagination-pages {
		display: flex;
		align-items: center;
		gap: 6px;
	}


	.pagination-button,
	.pagination-number {
		border: 1px solid #e1e5e9;
		background: #ffffff;
		color: #495057;
		border-radius: 8px;
		cursor: pointer;
		transition:
			background-color 0.2s ease,
			border-color 0.2s ease,
			color 0.2s ease;
	}


	.pagination-button {
		height: 36px;
		padding: 0 13px;
		font-size: 11px;
		font-weight: 600;
	}


	.pagination-button i {
		font-size: 10px;
	}


	.pagination-number {
		width: 34px;
		height: 34px;
		font-size: 11px;
		font-weight: 600;
	}


	.pagination-button:hover:not(:disabled),
	.pagination-number:hover {
		background: #eef5ff;
		border-color: #cfe2ff;
		color: #0d6efd;
	}


	.pagination-number.active {
		background: #0d6efd;
		border-color: #0d6efd;
		color: #ffffff;
	}


	.pagination-button:disabled {
		opacity: 0.45;
		cursor: not-allowed;
	}


	/* =========================================================
	   VACÍO
	   ========================================================= */

	.empty-cell {
		height: 280px;
	}


	.empty-state {
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
		text-align: center;
	}


	.empty-icon {
		width: 45px;
		height: 45px;
		margin-bottom: 10px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 50%;
		background: #f8f9fa;
		color: #adb5bd;
		font-size: 18px;
	}


	.empty-state strong {
		margin-bottom: 4px;
		color: #495057;
		font-size: 13px;
	}


	.empty-state span {
		color: #adb5bd;
		font-size: 11px;
	}


	/* =========================================================
	   MODALES
	   ========================================================= */

	.modal-backdrop-custom {
		position: fixed;
		inset: 0;
		z-index: 2000;
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 20px;
		background: rgba(33, 37, 41, 0.35);
	}


	.form-modal,
	.details-modal {
		width: 100%;
		background: #ffffff;
		border-radius: 15px;
		box-shadow:
			0 18px 50px rgba(0, 0, 0, 0.15);
		overflow: hidden;
	}


	.form-modal {
		max-width: 620px;
	}


	.details-modal {
		max-width: 520px;
		max-height: calc(100vh - 40px);
		display: flex;
		flex-direction: column;
	}


	.modal-header-custom,
	.details-header {
		padding: 21px 23px;
		display: flex;
		align-items: flex-start;
		justify-content: space-between;
		border-bottom: 1px solid #edf0f2;
	}


	.modal-header-custom h3 {
		margin: 0 0 4px;
		color: #343a40;
		font-size: 17px;
		font-weight: 700;
	}


	.modal-header-custom p {
		margin: 0;
		color: #adb5bd;
		font-size: 11px;
	}


	.close-button {
		width: 31px;
		height: 31px;
		border: none;
		border-radius: 7px;
		background: #f8f9fa;
		color: #868e96;
		font-size: 13px;
		line-height: 1;
		cursor: pointer;
		flex-shrink: 0;
	}


	.close-button:hover {
		background: #f1f3f5;
		color: #495057;
	}


	.modal-body-custom {
		padding: 22px 23px;
	}


	.modal-body-custom .form-label {
		margin-bottom: 7px;
		color: #495057;
		font-size: 12px;
		font-weight: 600;
	}


	.modal-body-custom .form-control,
	.modal-body-custom .form-select {
		min-height: 40px;
		border-color: #e1e5e9;
		border-radius: 8px;
		font-size: 12px;
	}


	.modal-body-custom textarea {
		resize: vertical;
	}


	.modal-body-custom .form-control:focus,
	.modal-body-custom .form-select:focus {
		border-color: #86b7fe;
		box-shadow:
			0 0 0 0.15rem
			rgba(13, 110, 253, 0.08);
	}


	.modal-footer-custom,
	.details-footer {
		padding: 16px 23px;
		display: flex;
		justify-content: flex-end;
		gap: 8px;
		background: #fafbfc;
		border-top: 1px solid #edf0f2;
		flex-shrink: 0;
	}


	.cancel-button,
	.save-button,
	.action-footer-button {
		height: 38px;
		padding: 0 15px;
		border-radius: 8px;
		font-size: 12px;
		font-weight: 600;
	}


	.save-button i,
	.action-footer-button i {
		margin-right: 5px;
	}


	/* =========================================================
	   DETALLES
	   ========================================================= */

	.details-heading {
		display: flex;
		align-items: center;
		gap: 13px;
		min-width: 0;
	}


	.details-label {
		display: block;
		margin-bottom: 2px;
		color: #adb5bd;
		font-size: 10px;
	}


	.details-heading h3 {
		margin: 0 0 2px;
		color: #343a40;
		font-size: 18px;
		font-weight: 700;
		word-break: break-word;
	}


	.details-grade {
		color: #adb5bd;
		font-size: 10px;
	}


	.details-body {
		padding: 22px 23px;
		overflow-y: auto;
		flex: 1;
		min-height: 0;
		scroll-behavior: smooth;
		scrollbar-width: thin;
		scrollbar-color: #d9dee3 #f8f9fa;
	}


	.details-body::-webkit-scrollbar {
		width: 6px;
	}


	.details-body::-webkit-scrollbar-track {
		background: #f8f9fa;
		border-radius: 10px;
	}


	.details-body::-webkit-scrollbar-thumb {
		background: #d9dee3;
		border-radius: 10px;
	}


	.details-body::-webkit-scrollbar-thumb:hover {
		background: #c5cbd1;
	}


	.detail-section {
		padding-top: 17px;
		margin-top: 17px;
		border-top: 1px solid #edf0f2;
	}


	.detail-section:first-child {
		padding-top: 0;
		margin-top: 0;
		border-top: none;
	}


	.section-label {
		display: block;
		margin-bottom: 10px;
		color: #868e96;
		font-size: 10px;
		font-weight: 600;
		text-transform: uppercase;
		letter-spacing: 0.3px;
	}


	/* =========================================================
	   ESTADO GRANDE
	   ========================================================= */

	.status-large-wrapper {
		width: 100%;
	}


	.status-large {
		display: flex;
		align-items: center;
		gap: 11px;
		padding: 13px;
		border-radius: 10px;
	}


	.status-large-icon {
		width: 35px;
		height: 35px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 9px;
		background: rgba(255, 255, 255, 0.75);
		font-size: 16px;
	}


	.status-large strong {
		display: block;
		margin-bottom: 2px;
		font-size: 12px;
	}


	.status-large > div:last-child span {
		display: block;
		font-size: 9px;
		opacity: 0.7;
	}


	/* =========================================================
	   ACTIVIDAD
	   ========================================================= */

	.activity-detail {
		display: flex;
		align-items: center;
		gap: 11px;
	}


	.activity-detail strong {
		display: block;
		margin-bottom: 3px;
		color: #343a40;
		font-size: 13px;
	}


	.activity-detail span {
		color: #adb5bd;
		font-size: 10px;
	}


	/* =========================================================
	   GRID
	   ========================================================= */

	.details-grid {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 10px;
	}


	.details-grid div {
		padding: 12px;
		background: #f8f9fa;
		border-radius: 9px;
	}


	.details-grid span {
		display: block;
		margin-bottom: 5px;
		color: #adb5bd;
		font-size: 9px;
	}


	.details-grid strong {
		display: block;
		color: #495057;
		font-size: 11px;
		font-weight: 600;
		word-break: break-word;
	}


	/* =========================================================
	   TIMELINE
	   ========================================================= */

	.timeline {
		position: relative;
	}


	.timeline-item {
		display: flex;
		align-items: center;
		gap: 10px;
	}


	.timeline-marker {
		width: 32px;
		height: 32px;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-shrink: 0;
		border-radius: 50%;
		background: #eef5ff;
		color: #0d6efd;
		font-size: 13px;
	}


	.timeline-item strong {
		display: block;
		margin-bottom: 2px;
		color: #495057;
		font-size: 10px;
		font-weight: 600;
	}


	.timeline-item span {
		display: block;
		color: #adb5bd;
		font-size: 9px;
	}


	.timeline-line {
		width: 1px;
		height: 15px;
		margin-left: 16px;
		background: #e9ecef;
	}


	/* =========================================================
	   OBSERVACIONES
	   ========================================================= */

	.observation-box {
		padding: 13px;
		background: #f8f9fa;
		border-radius: 9px;
	}


	.observation-box span {
		color: #6c757d;
		font-size: 11px;
		line-height: 1.6;
	}


	/* =========================================================
	   RESUMEN
	   ========================================================= */

	.summary-box {
		display: flex;
		flex-direction: column;
		gap: 8px;
	}


	.summary-item {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 15px;
		padding: 10px 12px;
		background: #f8f9fa;
		border-radius: 8px;
	}


	.summary-item span {
		color: #adb5bd;
		font-size: 9px;
	}


	.summary-item strong {
		color: #495057;
		font-size: 10px;
		font-weight: 600;
		text-align: right;
		word-break: break-word;
	}


	/* =========================================================
	   RESPONSIVE
	   ========================================================= */

	@media (max-width: 900px) {

		.filters {
			flex-direction: column;
			align-items: stretch;
		}


		.filters .form-select {
			width: 100%;
		}

	}


	@media (max-width: 700px) {

		.page-header {
			align-items: flex-start;
			flex-direction: column;
		}


		.new-button {
			width: 100%;
		}

	}


	@media (max-width: 576px) {

		.container-fluid {
			padding-left: 15px !important;
			padding-right: 15px !important;
		}


		.filters-card {
			padding: 17px;
		}


		.modal-backdrop-custom {
			padding: 10px;
		}


		.form-modal,
		.details-modal {
			max-width: 100%;
			border-radius: 12px;
		}


		.details-modal {
			max-height: calc(100vh - 20px);
		}


		.modal-body-custom {
			padding: 18px;
		}


		.details-body {
			padding: 18px;
		}


		.modal-header-custom,
		.details-header {
			padding: 17px 18px;
		}


		.modal-footer-custom,
		.details-footer {
			padding: 13px 18px;
		}


		.details-heading {
			gap: 9px;
		}


		.details-heading h3 {
			font-size: 16px;
		}


		.details-grid {
			grid-template-columns: 1fr;
		}


		.details-footer {
			flex-wrap: wrap;
		}


		.details-footer .cancel-button {
			flex: 1;
		}


		.details-footer .save-button,
		.details-footer .action-footer-button {
			flex: 1;
		}


		.student-avatar.large {
			width: 44px;
			height: 44px;
			font-size: 11px;
		}

	}


	@media (max-width: 380px) {

		.details-modal {
			max-height: calc(100vh - 12px);
		}


		.details-header {
			padding: 14px;
		}


		.details-body {
			padding: 14px;
		}


		.details-footer {
			padding: 11px 14px;
		}


		.details-heading {
			gap: 8px;
		}


		.details-heading h3 {
			font-size: 15px;
		}


		.student-avatar.large {
			width: 40px;
			height: 40px;
		}


		.summary-item {
			align-items: flex-start;
			flex-direction: column;
			gap: 3px;
		}


		.summary-item strong {
			text-align: left;
		}

	}

</style>