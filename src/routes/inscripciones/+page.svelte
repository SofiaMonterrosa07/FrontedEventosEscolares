<script>
	let busqueda = $state('');
	let filtroEstado = $state('Todos');
	let filtroAutorizacion = $state('Todas');

	let mostrarFormulario = $state(false);
	let mostrarDetalles = $state(false);

	let modoEdicion = $state(false);
	let inscripcionSeleccionada = $state(null);


	// =========================================================
	// INSCRIPCIONES ESTÁTICAS
	// =========================================================

	let inscripciones = $state([
		{
			id: 1,
			estudiante: 'María Fernanda López',
			grado: '10°',
			actividad: 'Baloncesto',
			categoria: 'Deportes',
			icono: 'bi-dribbble',
			fecha: '05 de septiembre de 2026',
			estado: 'Confirmada',
			autorizacion: 'Aprobada',
			acudiente: 'Laura López',
			observaciones: 'Participación confirmada.'
		},
		{
			id: 2,
			estudiante: 'Juan Sebastián Pérez',
			grado: '9°',
			actividad: 'Robótica',
			categoria: 'Tecnología',
			icono: 'bi-robot',
			fecha: '06 de septiembre de 2026',
			estado: 'Pendiente',
			autorizacion: 'Pendiente',
			acudiente: 'Carlos Pérez',
			observaciones: 'Esperando autorización del acudiente.'
		},
		{
			id: 3,
			estudiante: 'Valentina Rodríguez',
			grado: '11°',
			actividad: 'Teatro',
			categoria: 'Arte',
			icono: 'bi-mask',
			fecha: '06 de septiembre de 2026',
			estado: 'Confirmada',
			autorizacion: 'Aprobada',
			acudiente: 'Andrea Rodríguez',
			observaciones: 'Inscripción completada correctamente.'
		},
		{
			id: 4,
			estudiante: 'Daniel Andrés Gómez',
			grado: '8°',
			actividad: 'Natación',
			categoria: 'Deportes',
			icono: 'bi-water',
			fecha: '07 de septiembre de 2026',
			estado: 'Confirmada',
			autorizacion: 'Aprobada',
			acudiente: 'Sandra Gómez',
			observaciones: 'Cupo asignado.'
		},
		{
			id: 5,
			estudiante: 'Sofía Martínez',
			grado: '10°',
			actividad: 'Ajedrez',
			categoria: 'Académica',
			icono: 'bi-grid-3x3-gap',
			fecha: '07 de septiembre de 2026',
			estado: 'Pendiente',
			autorizacion: 'Pendiente',
			acudiente: 'Jorge Martínez',
			observaciones: 'Pendiente de revisión.'
		},
		{
			id: 6,
			estudiante: 'Samuel Torres',
			grado: '7°',
			actividad: 'Danza',
			categoria: 'Arte',
			icono: 'bi-music-note-beamed',
			fecha: '08 de septiembre de 2026',
			estado: 'Cancelada',
			autorizacion: 'Rechazada',
			acudiente: 'Paola Torres',
			observaciones: 'La inscripción fue cancelada.'
		},
		{
			id: 7,
			estudiante: 'Gabriela Herrera',
			grado: '9°',
			actividad: 'Baloncesto',
			categoria: 'Deportes',
			icono: 'bi-dribbble',
			fecha: '08 de septiembre de 2026',
			estado: 'Confirmada',
			autorizacion: 'Aprobada',
			acudiente: 'Miguel Herrera',
			observaciones: 'Participación confirmada.'
		},
		{
			id: 8,
			estudiante: 'Nicolás Ramírez',
			grado: '8°',
			actividad: 'Fútbol',
			categoria: 'Deportes',
			icono: 'bi-circle-fill',
			fecha: '08 de septiembre de 2026',
			estado: 'Confirmada',
			autorizacion: 'Aprobada',
			acudiente: 'Claudia Ramírez',
			observaciones: 'Inscripción confirmada.'
		},
		{
			id: 9,
			estudiante: 'Laura Carolina Díaz',
			grado: '10°',
			actividad: 'Pintura',
			categoria: 'Arte',
			icono: 'bi-palette',
			fecha: '09 de septiembre de 2026',
			estado: 'Confirmada',
			autorizacion: 'Aprobada',
			acudiente: 'Ricardo Díaz',
			observaciones: 'Participación autorizada.'
		},
		{
			id: 10,
			estudiante: 'Mateo Castro',
			grado: '7°',
			actividad: 'Ciencias',
			categoria: 'Académica',
			icono: 'bi-beaker',
			fecha: '09 de septiembre de 2026',
			estado: 'Pendiente',
			autorizacion: 'Pendiente',
			acudiente: 'Diana Castro',
			observaciones: 'Pendiente de respuesta.'
		},
		{
			id: 11,
			estudiante: 'Isabella Moreno',
			grado: '11°',
			actividad: 'Voleibol',
			categoria: 'Deportes',
			icono: 'bi-trophy',
			fecha: '09 de septiembre de 2026',
			estado: 'Confirmada',
			autorizacion: 'Aprobada',
			acudiente: 'Felipe Moreno',
			observaciones: 'Autorización confirmada.'
		},
		{
			id: 12,
			estudiante: 'Sebastián Vargas',
			grado: '9°',
			actividad: 'Fotografía',
			categoria: 'Arte',
			icono: 'bi-camera',
			fecha: '10 de septiembre de 2026',
			estado: 'Confirmada',
			autorizacion: 'Aprobada',
			acudiente: 'Natalia Vargas',
			observaciones: 'Participación confirmada.'
		}
	]);


	// =========================================================
	// FORMULARIO
	// =========================================================

	let formulario = $state({
		estudiante: '',
		grado: '',
		actividad: 'Baloncesto',
		categoria: 'Deportes',
		icono: 'bi-dribbble',
		fecha: '',
		estado: 'Pendiente',
		autorizacion: 'Pendiente',
		acudiente: '',
		observaciones: ''
	});


	// =========================================================
	// FILTROS
	// =========================================================

	let inscripcionesFiltradas = $derived(
		inscripciones.filter((inscripcion) => {

			const texto = busqueda.toLowerCase();

			const coincideBusqueda =
				inscripcion.estudiante
					.toLowerCase()
					.includes(texto) ||
				inscripcion.actividad
					.toLowerCase()
					.includes(texto);

			const coincideEstado =
				filtroEstado === 'Todos' ||
				inscripcion.estado === filtroEstado;

			const coincideAutorizacion =
				filtroAutorizacion === 'Todas' ||
				inscripcion.autorizacion === filtroAutorizacion;

			return (
				coincideBusqueda &&
				coincideEstado &&
				coincideAutorizacion
			);
		})
	);


	// =========================================================
	// INDICADORES
	// =========================================================

	let totalInscripciones = $derived(
		inscripciones.length
	);


	let confirmadas = $derived(
		inscripciones.filter(
			(inscripcion) =>
				inscripcion.estado === 'Confirmada'
		).length
	);


	let pendientes = $derived(
		inscripciones.filter(
			(inscripcion) =>
				inscripcion.estado === 'Pendiente'
		).length
	);


	let autorizacionesPendientes = $derived(
		inscripciones.filter(
			(inscripcion) =>
				inscripcion.autorizacion === 'Pendiente'
		).length
	);


	// =========================================================
	// ABRIR NUEVA INSCRIPCIÓN
	// =========================================================

	function abrirNuevaInscripcion() {

		modoEdicion = false;
		inscripcionSeleccionada = null;

		formulario = {
			estudiante: '',
			grado: '',
			actividad: 'Baloncesto',
			categoria: 'Deportes',
			icono: 'bi-dribbble',
			fecha: '',
			estado: 'Pendiente',
			autorizacion: 'Pendiente',
			acudiente: '',
			observaciones: ''
		};

		mostrarFormulario = true;
	}


	// =========================================================
	// EDITAR
	// =========================================================

	function editarInscripcion(inscripcion) {

		modoEdicion = true;
		inscripcionSeleccionada = inscripcion;

		formulario = {
			estudiante: inscripcion.estudiante,
			grado: inscripcion.grado,
			actividad: inscripcion.actividad,
			categoria: inscripcion.categoria,
			icono: inscripcion.icono,
			fecha: inscripcion.fecha,
			estado: inscripcion.estado,
			autorizacion: inscripcion.autorizacion,
			acudiente: inscripcion.acudiente,
			observaciones: inscripcion.observaciones
		};

		mostrarFormulario = true;
	}


	// =========================================================
	// GUARDAR
	// =========================================================

	function guardarInscripcion() {

		if (
			!formulario.estudiante.trim() ||
			!formulario.grado.trim() ||
			!formulario.fecha.trim() ||
			!formulario.acudiente.trim()
		) {
			return;
		}


		if (modoEdicion) {

			inscripciones = inscripciones.map(
				(inscripcion) =>
					inscripcion.id ===
					inscripcionSeleccionada.id
						? {
								...inscripcion,
								estudiante:
									formulario.estudiante,
								grado:
									formulario.grado,
								actividad:
									formulario.actividad,
								categoria:
									formulario.categoria,
								icono:
									formulario.icono,
								fecha:
									formulario.fecha,
								estado:
									formulario.estado,
								autorizacion:
									formulario.autorizacion,
								acudiente:
									formulario.acudiente,
								observaciones:
									formulario.observaciones
							}
						: inscripcion
			);

		} else {

			const nuevaInscripcion = {

				id: Date.now(),

				estudiante:
					formulario.estudiante,

				grado:
					formulario.grado,

				actividad:
					formulario.actividad,

				categoria:
					formulario.categoria,

				icono:
					formulario.icono,

				fecha:
					formulario.fecha,

				estado:
					formulario.estado,

				autorizacion:
					formulario.autorizacion,

				acudiente:
					formulario.acudiente,

				observaciones:
					formulario.observaciones
			};


			inscripciones = [
				...inscripciones,
				nuevaInscripcion
			];
		}


		cerrarFormulario();
	}


	// =========================================================
	// ELIMINAR
	// =========================================================

	function eliminarInscripcion(inscripcion) {

		const confirmar = confirm(
			`¿Deseas eliminar la inscripción de "${inscripcion.estudiante}"?`
		);


		if (!confirmar) {
			return;
		}


		inscripciones =
			inscripciones.filter(
				(item) =>
					item.id !== inscripcion.id
			);
	}


	// =========================================================
	// DETALLES
	// =========================================================

	function verDetalles(inscripcion) {

		inscripcionSeleccionada =
			inscripcion;

		mostrarDetalles = true;
	}


	function cerrarFormulario() {

		mostrarFormulario = false;

		modoEdicion = false;

		inscripcionSeleccionada = null;
	}


	function cerrarDetalles() {

		mostrarDetalles = false;

		inscripcionSeleccionada = null;
	}


	// =========================================================
	// CLASE ESTADO
	// =========================================================

	function claseEstado(estado) {

		if (estado === 'Confirmada') {
			return 'status-confirmed';
		}


		if (estado === 'Pendiente') {
			return 'status-pending';
		}


		if (estado === 'Cancelada') {
			return 'status-cancelled';
		}


		return 'status-default';
	}


	// =========================================================
	// CLASE AUTORIZACIÓN
	// =========================================================

	function claseAutorizacion(autorizacion) {

		if (autorizacion === 'Aprobada') {
			return 'authorization-approved';
		}


		if (autorizacion === 'Pendiente') {
			return 'authorization-pending';
		}


		if (autorizacion === 'Rechazada') {
			return 'authorization-rejected';
		}


		return 'authorization-default';
	}


	// =========================================================
	// CLASE CATEGORÍA
	// =========================================================

	function claseCategoria(categoria) {

		if (categoria === 'Deportes') {
			return 'category-sport';
		}


		if (categoria === 'Tecnología') {
			return 'category-tech';
		}


		if (categoria === 'Arte') {
			return 'category-art';
		}


		if (categoria === 'Académica') {
			return 'category-academic';
		}


		return 'category-default';
	}


	// =========================================================
	// ACTUALIZAR CATEGORÍA E ICONO
	// =========================================================

	function actualizarCategoria() {

		const datos = {

			Baloncesto: {
				categoria: 'Deportes',
				icono: 'bi-dribbble'
			},

			Natación: {
				categoria: 'Deportes',
				icono: 'bi-water'
			},

			Robótica: {
				categoria: 'Tecnología',
				icono: 'bi-robot'
			},

			Teatro: {
				categoria: 'Arte',
				icono: 'bi-mask'
			},

			Danza: {
				categoria: 'Arte',
				icono: 'bi-music-note-beamed'
			},

			Ajedrez: {
				categoria: 'Académica',
				icono: 'bi-grid-3x3-gap'
			},

			Fútbol: {
				categoria: 'Deportes',
				icono: 'bi-circle-fill'
			},

			Programación: {
				categoria: 'Tecnología',
				icono: 'bi-code-slash'
			},

			Pintura: {
				categoria: 'Arte',
				icono: 'bi-palette'
			},

			Ciencias: {
				categoria: 'Académica',
				icono: 'bi-beaker'
			},

			Voleibol: {
				categoria: 'Deportes',
				icono: 'bi-trophy'
			},

			Fotografía: {
				categoria: 'Arte',
				icono: 'bi-camera'
			},

			'Ciencia y Tecnología': {
				categoria: 'Tecnología',
				icono: 'bi-cpu'
			},

			Literatura: {
				categoria: 'Académica',
				icono: 'bi-book'
			},

			Atletismo: {
				categoria: 'Deportes',
				icono: 'bi-person-running'
			},

			'Diseño Digital': {
				categoria: 'Tecnología',
				icono: 'bi-vector-pen'
			},

			'Coro Escolar': {
				categoria: 'Arte',
				icono: 'bi-mic'
			},

			'Matemáticas Recreativas': {
				categoria: 'Académica',
				icono: 'bi-calculator'
			},

			'Tenis de Mesa': {
				categoria: 'Deportes',
				icono: 'bi-table'
			},

			'Cine y Producción': {
				categoria: 'Arte',
				icono: 'bi-camera-reels'
			}
		};


		const seleccionado =
			datos[formulario.actividad];


		formulario.categoria =
			seleccionado?.categoria ||
			'Deportes';


		formulario.icono =
			seleccionado?.icono ||
			'bi-calendar-event';
	}
</script>


<svelte:head>
	<title>Inscripciones | Colegio San Miguel</title>
</svelte:head>


<div class="container-fluid px-4 py-4">

	<!-- =====================================================
	     ENCABEZADO
	     ===================================================== -->

	<div class="page-header">

		<div>

			<h2>
				Inscripciones
			</h2>

			<p>
				Consulta y administra las inscripciones a las actividades.
			</p>

		</div>


		<button
			class="btn btn-primary new-button"
			onclick={abrirNuevaInscripcion}
		>
			<i class="bi bi-plus-lg"></i>
			Nueva inscripción
		</button>

	</div>


	<!-- =====================================================
	     INDICADORES
	     ===================================================== -->

	<div class="row g-3 mb-4">

		<div class="col-md-6 col-xl-3">

			<div class="soft-card indicator-card">

				<div class="icon-soft blue">
					<i class="bi bi-journal-check"></i>
				</div>


				<div>

					<span class="indicator-label">
						Inscripciones
					</span>

					<strong>
						{totalInscripciones}
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
						Confirmadas
					</span>

					<strong>
						{confirmadas}
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

				<div class="icon-soft purple">
					<i class="bi bi-file-earmark-check"></i>
				</div>


				<div>

					<span class="indicator-label">
						Autorizaciones pendientes
					</span>

					<strong>
						{autorizacionesPendientes}
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
					Inscripciones
				</h3>

				<span>
					{inscripcionesFiltradas.length} resultados
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
					placeholder="Buscar estudiante o actividad..."
					bind:value={busqueda}
				/>

			</div>


			<select
				class="form-select"
				bind:value={filtroEstado}
			>

				<option value="Todos">
					Todos los estados
				</option>

				<option value="Confirmada">
					Confirmadas
				</option>

				<option value="Pendiente">
					Pendientes
				</option>

				<option value="Cancelada">
					Canceladas
				</option>

			</select>


			<select
				class="form-select"
				bind:value={filtroAutorizacion}
			>

				<option value="Todas">
					Todas las autorizaciones
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
							Fecha
						</th>

						<th>
							Estado
						</th>

						<th>
							Autorización
						</th>

						<th class="text-end">
							Acciones
						</th>

					</tr>

				</thead>


				<tbody>

					{#if inscripcionesFiltradas.length > 0}

						{#each inscripcionesFiltradas as inscripcion}

							<tr>

								<!-- ESTUDIANTE -->

								<td>

									<div class="student-cell">

										<div class="student-avatar">

											{inscripcion.estudiante
												.split(' ')
												.slice(0, 2)
												.map((nombre) =>
													nombre.charAt(0)
												)
												.join('')}

										</div>


										<div>

											<strong>
												{inscripcion.estudiante}
											</strong>

											<span>
												{inscripcion.grado}
											</span>

										</div>

									</div>

								</td>


								<!-- ACTIVIDAD -->

								<td>

									<div class="activity-cell">

										<div class="activity-icon">

											<i
												class={`bi ${inscripcion.icono}`}
											></i>

										</div>


										<div>

											<strong>
												{inscripcion.actividad}
											</strong>

											<span
												class={`category-text ${claseCategoria(
													inscripcion.categoria
												)}`}
											>
												{inscripcion.categoria}
											</span>

										</div>

									</div>

								</td>


								<!-- FECHA -->

								<td>

									<span class="date-text">
										{inscripcion.fecha}
									</span>

								</td>


								<!-- ESTADO -->

								<td>

									<span
										class={`status-badge ${claseEstado(
											inscripcion.estado
										)}`}
									>

										<i
											class={`bi ${
												inscripcion.estado ===
												'Confirmada'
													? 'bi-check-circle'
													: inscripcion.estado ===
													  'Pendiente'
														? 'bi-clock'
														: 'bi-x-circle'
											}`}
										></i>

										{inscripcion.estado}

									</span>

								</td>


								<!-- AUTORIZACIÓN -->

								<td>

									<span
										class={`authorization-badge ${claseAutorizacion(
											inscripcion.autorizacion
										)}`}
									>

										<i
											class={`bi ${
												inscripcion.autorizacion ===
												'Aprobada'
													? 'bi-check-lg'
													: inscripcion.autorizacion ===
													  'Pendiente'
														? 'bi-clock'
														: 'bi-x-lg'
											}`}
										></i>

										{inscripcion.autorizacion}

									</span>

								</td>


								<!-- ACCIONES -->

								<td>

									<div class="actions">

										<button
											class="action-btn"
											title="Ver detalles"
											aria-label="Ver detalles"
											onclick={() =>
												verDetalles(
													inscripcion
												)}
										>
											<i class="bi bi-eye"></i>
										</button>


										<button
											class="action-btn"
											title="Editar"
											aria-label="Editar inscripción"
											onclick={() =>
												editarInscripcion(
													inscripcion
												)}
										>
											<i class="bi bi-pencil"></i>
										</button>


										<button
											class="action-btn delete"
											title="Eliminar"
											aria-label="Eliminar inscripción"
											onclick={() =>
												eliminarInscripcion(
													inscripcion
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
										No se encontraron inscripciones
									</strong>


									<span>
										Prueba con otro estudiante,
										actividad o filtro.
									</span>

								</div>

							</td>

						</tr>

					{/if}

				</tbody>

			</table>

		</div>

	</div>

</div>


<!-- =========================================================
     MODAL NUEVA / EDITAR
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
							? 'Editar inscripción'
							: 'Nueva inscripción'}
					</h3>


					<p>
						Completa la información de la inscripción.
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
							onchange={actualizarCategoria}
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
							for="fecha"
						>
							Fecha de inscripción
						</label>


						<input
							id="fecha"
							type="text"
							class="form-control"
							placeholder="Ej. 10 de septiembre"
							bind:value={formulario.fecha}
						/>

					</div>

				</div>


				<div class="row g-3 mb-3">

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

							<option value="Confirmada">
								Confirmada
							</option>

							<option value="Cancelada">
								Cancelada
							</option>

						</select>

					</div>


					<div class="col-md-6">

						<label
							class="form-label"
							for="autorizacion"
						>
							Autorización
						</label>


						<select
							id="autorizacion"
							class="form-select"
							bind:value={
								formulario.autorizacion
							}
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
						for="acudiente"
					>
						Padre / acudiente
					</label>


					<input
						id="acudiente"
						type="text"
						class="form-control"
						placeholder="Nombre del padre o acudiente"
						bind:value={formulario.acudiente}
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
						placeholder="Observaciones adicionales..."
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
					onclick={guardarInscripcion}
				>
					<i class="bi bi-check2"></i>

					{modoEdicion
						? 'Guardar cambios'
						: 'Crear inscripción'}

				</button>

			</div>

		</div>

	</div>

{/if}


<!-- =========================================================
     MODAL DETALLES
     ========================================================= -->

{#if mostrarDetalles && inscripcionSeleccionada}

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

						{inscripcionSeleccionada.estudiante
							.split(' ')
							.slice(0, 2)
							.map((nombre) =>
								nombre.charAt(0)
							)
							.join('')}

					</div>


					<div>

						<span class="details-label">
							Inscripción
						</span>


						<h3 id="details-title">
							{inscripcionSeleccionada.estudiante}
						</h3>


						<span class="details-grade">
							{inscripcionSeleccionada.grado}
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


			<!-- CUERPO DESLIZABLE -->

			<div class="details-body">

				<!-- ACTIVIDAD -->

				<section class="detail-section">

					<span class="section-label">
						Actividad
					</span>


					<div class="activity-detail">

						<div class="activity-icon large">

							<i
								class={`bi ${inscripcionSeleccionada.icono}`}
							></i>

						</div>


						<div>

							<strong>
								{inscripcionSeleccionada.actividad}
							</strong>


							<span>
								{inscripcionSeleccionada.categoria}
							</span>

						</div>

					</div>

				</section>


				<!-- ESTADO -->

				<section class="detail-section">

					<span class="section-label">
						Estado
					</span>


					<div class="status-row">

						<div>

							<span class="small-label">
								Inscripción
							</span>


							<span
								class={`status-badge ${claseEstado(
									inscripcionSeleccionada.estado
								)}`}
							>

								<i
									class={`bi ${
										inscripcionSeleccionada.estado ===
										'Confirmada'
											? 'bi-check-circle'
											: inscripcionSeleccionada.estado ===
											  'Pendiente'
												? 'bi-clock'
												: 'bi-x-circle'
									}`}
								></i>

								{inscripcionSeleccionada.estado}

							</span>

						</div>


						<div>

							<span class="small-label">
								Autorización
							</span>


							<span
								class={`authorization-badge ${claseAutorizacion(
									inscripcionSeleccionada.autorizacion
								)}`}
							>

								<i
									class={`bi ${
										inscripcionSeleccionada.autorizacion ===
										'Aprobada'
											? 'bi-check-lg'
											: inscripcionSeleccionada.autorizacion ===
											  'Pendiente'
												? 'bi-clock'
												: 'bi-x-lg'
									}`}
								></i>

								{inscripcionSeleccionada.autorizacion}

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
								Fecha de inscripción
							</span>


							<strong>
								{inscripcionSeleccionada.fecha}
							</strong>

						</div>


						<div>

							<span>
								Grado
							</span>


							<strong>
								{inscripcionSeleccionada.grado}
							</strong>

						</div>


						<div>

							<span>
								Padre / acudiente
							</span>


							<strong>
								{inscripcionSeleccionada.acudiente}
							</strong>

						</div>


						<div>

							<span>
								Identificador
							</span>


							<strong>
								#{inscripcionSeleccionada.id}
							</strong>

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
							{inscripcionSeleccionada.observaciones ||
								'Sin observaciones registradas.'}
						</span>

					</div>

				</section>


				<!-- SEGUIMIENTO -->

				<section class="detail-section">

					<span class="section-label">
						Seguimiento
					</span>


					<div class="tracking-box">

						<div class="tracking-item">

							<div class="tracking-icon">
								<i class="bi bi-journal-check"></i>
							</div>


							<div>

								<strong>
									Registro realizado
								</strong>


								<span>
									La inscripción fue registrada en el sistema.
								</span>

							</div>

						</div>


						<div class="tracking-item">

							<div class="tracking-icon">
								<i class="bi bi-file-earmark-check"></i>
							</div>


							<div>

								<strong>
									Autorización familiar
								</strong>


								<span>
									Estado actual:
									{inscripcionSeleccionada.autorizacion}
								</span>

							</div>

						</div>


						<div class="tracking-item">

							<div class="tracking-icon">
								<i class="bi bi-calendar-event"></i>
							</div>


							<div>

								<strong>
									Actividad seleccionada
								</strong>


								<span>
									{inscripcionSeleccionada.actividad}
								</span>

							</div>

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


				<button
					class="btn btn-primary save-button"
					onclick={() => {

						const inscripcion =
							inscripcionSeleccionada;

						cerrarDetalles();

						editarInscripcion(
							inscripcion
						);

					}}
				>
					<i class="bi bi-pencil"></i>
					Editar inscripción
				</button>

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
		font-size: 18px;
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


	.icon-soft.purple {
		background: #f1edff;
		color: #6f42c1;
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
		min-width: 160px;
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
		font-size: 15px;
		flex-shrink: 0;
	}


	.activity-icon.large {
		width: 43px;
		height: 43px;
		font-size: 20px;
	}


	.activity-cell strong {
		display: block;
		margin-bottom: 2px;
		color: #495057;
		font-size: 11px;
		font-weight: 600;
	}


	.category-text {
		display: block;
		font-size: 9px;
		font-weight: 600;
	}


	.category-sport {
		color: #0d6efd;
	}


	.category-tech {
		color: #198754;
	}


	.category-art {
		color: #6f42c1;
	}


	.category-academic {
		color: #d97706;
	}


	.category-default {
		color: #6c757d;
	}


	.date-text {
		color: #6c757d;
		font-size: 10px;
		white-space: nowrap;
	}


	/* =========================================================
	   BADGES
	   ========================================================= */

	.status-badge,
	.authorization-badge {
		display: inline-flex;
		align-items: center;
		gap: 5px;
		padding: 5px 9px;
		border-radius: 20px;
		font-size: 9px;
		font-weight: 600;
		white-space: nowrap;
	}


	.status-confirmed {
		background: #e9f7ef;
		color: #198754;
	}


	.status-pending {
		background: #fff2e5;
		color: #d97706;
	}


	.status-cancelled {
		background: #fff0f1;
		color: #dc3545;
	}


	.status-default {
		background: #f1f3f5;
		color: #6c757d;
	}


	.authorization-approved {
		background: #e9f7ef;
		color: #198754;
	}


	.authorization-pending {
		background: #fff2e5;
		color: #d97706;
	}


	.authorization-rejected {
		background: #fff0f1;
		color: #dc3545;
	}


	.authorization-default {
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


	.action-btn.delete {
		color: #adb5bd;
	}


	.action-btn.delete:hover {
		color: #dc3545;
		background: #fff5f5;
		border-color: #f5d8da;
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
	.save-button {
		height: 38px;
		padding: 0 15px;
		border-radius: 8px;
		font-size: 12px;
		font-weight: 600;
	}


	.save-button i {
		margin-right: 5px;
	}


	/* =========================================================
	   DETALLES
	   ========================================================= */

	.details-header {
		flex-shrink: 0;
	}


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
	   ESTADOS
	   ========================================================= */

	.status-row {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 10px;
	}


	.status-row > div {
		padding: 12px;
		background: #f8f9fa;
		border-radius: 9px;
	}


	.small-label {
		display: block;
		margin-bottom: 7px;
		color: #adb5bd;
		font-size: 9px;
	}


	/* =========================================================
	   DETALLE ACTIVIDAD
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
	   SEGUIMIENTO
	   ========================================================= */

	.tracking-box {
		display: flex;
		flex-direction: column;
		gap: 9px;
	}


	.tracking-item {
		display: flex;
		align-items: flex-start;
		gap: 10px;
		padding: 11px;
		background: #f8f9fa;
		border-radius: 9px;
	}


	.tracking-icon {
		width: 31px;
		height: 31px;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-shrink: 0;
		border-radius: 8px;
		background: #eef5ff;
		color: #0d6efd;
		font-size: 14px;
	}


	.tracking-item strong {
		display: block;
		margin-bottom: 3px;
		color: #495057;
		font-size: 10px;
		font-weight: 600;
	}


	.tracking-item span {
		display: block;
		color: #adb5bd;
		font-size: 9px;
		line-height: 1.5;
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


		.status-row,
		.details-grid {
			grid-template-columns: 1fr;
		}


		.details-footer {
			flex-wrap: wrap;
		}


		.cancel-button,
		.save-button {
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

	}

</style>