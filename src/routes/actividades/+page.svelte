<script>
	let busqueda = $state('');
	let filtroCategoria = $state('Todas');
	let filtroEstado = $state('Todos');

	let mostrarFormulario = $state(false);
	let mostrarDetalles = $state(false);

	let modoEdicion = $state(false);
	let actividadSeleccionada = $state(null);

	// =========================================================
	// PAGINACIÓN
	// =========================================================

	let paginaActual = $state(1);
	const actividadesPorPagina = 6;

	// =========================================================
	// 20 ACTIVIDADES DE EJEMPLO
	// 17 ACTIVAS + 3 CON CUPOS COMPLETOS
	// =========================================================

	let actividades = $state([
		{
			id: 1,
			nombre: 'Baloncesto',
			icono: 'bi-dribbble',
			categoria: 'Deportes',
			fecha: '15 de septiembre de 2026',
			hora: '3:00 p. m.',
			lugar: 'Cancha principal',
			cupos: 25,
			inscritos: 18,
			estado: 'Activa',
			descripcion:
				'Entrenamiento deportivo dirigido a estudiantes interesados en fortalecer sus habilidades de baloncesto mediante ejercicios prácticos, coordinación y trabajo en equipo.'
		},
		{
			id: 2,
			nombre: 'Robótica',
			icono: 'bi-robot',
			categoria: 'Tecnología',
			fecha: '18 de septiembre de 2026',
			hora: '2:30 p. m.',
			lugar: 'Laboratorio de tecnología',
			cupos: 20,
			inscritos: 12,
			estado: 'Activa',
			descripcion:
				'Espacio de aprendizaje donde los estudiantes desarrollan conocimientos de robótica, programación y construcción de prototipos.'
		},
		{
			id: 3,
			nombre: 'Teatro',
			icono: 'bi-mask',
			categoria: 'Arte',
			fecha: '20 de septiembre de 2026',
			hora: '4:00 p. m.',
			lugar: 'Auditorio',
			cupos: 30,
			inscritos: 24,
			estado: 'Activa',
			descripcion:
				'Actividad artística enfocada en expresión corporal, actuación, creatividad y trabajo colaborativo.'
		},
		{
			id: 4,
			nombre: 'Natación',
			icono: 'bi-water',
			categoria: 'Deportes',
			fecha: '22 de septiembre de 2026',
			hora: '2:00 p. m.',
			lugar: 'Piscina escolar',
			cupos: 15,
			inscritos: 15,
			estado: 'Cupos completos',
			descripcion:
				'Entrenamiento de natación orientado al fortalecimiento de técnicas básicas y habilidades acuáticas.'
		},
		{
			id: 5,
			nombre: 'Ajedrez',
			icono: 'bi-grid-3x3-gap',
			categoria: 'Académica',
			fecha: '25 de septiembre de 2026',
			hora: '1:30 p. m.',
			lugar: 'Biblioteca',
			cupos: 20,
			inscritos: 9,
			estado: 'Activa',
			descripcion:
				'Espacio para desarrollar pensamiento estratégico, concentración y resolución de problemas mediante el ajedrez.'
		},
		{
			id: 6,
			nombre: 'Danza',
			icono: 'bi-music-note-beamed',
			categoria: 'Arte',
			fecha: '28 de septiembre de 2026',
			hora: '3:30 p. m.',
			lugar: 'Salón cultural',
			cupos: 25,
			inscritos: 10,
			estado: 'Activa',
			descripcion:
				'Actividad de expresión artística mediante diferentes estilos de danza, movimiento y coordinación corporal.'
		},
		{
			id: 7,
			nombre: 'Fútbol',
			icono: 'bi-circle-fill',
			categoria: 'Deportes',
			fecha: '30 de septiembre de 2026',
			hora: '3:00 p. m.',
			lugar: 'Cancha auxiliar',
			cupos: 30,
			inscritos: 26,
			estado: 'Activa',
			descripcion:
				'Actividad deportiva enfocada en fundamentos del fútbol, trabajo en equipo y acondicionamiento físico.'
		},
		{
			id: 8,
			nombre: 'Programación',
			icono: 'bi-code-slash',
			categoria: 'Tecnología',
			fecha: '2 de octubre de 2026',
			hora: '2:00 p. m.',
			lugar: 'Sala de informática',
			cupos: 20,
			inscritos: 14,
			estado: 'Activa',
			descripcion:
				'Taller introductorio de programación y desarrollo de soluciones mediante pensamiento lógico y computacional.'
		},
		{
			id: 9,
			nombre: 'Pintura',
			icono: 'bi-palette',
			categoria: 'Arte',
			fecha: '5 de octubre de 2026',
			hora: '3:30 p. m.',
			lugar: 'Salón de artes',
			cupos: 18,
			inscritos: 11,
			estado: 'Activa',
			descripcion:
				'Espacio artístico para explorar técnicas de pintura, color, composición y expresión creativa.'
		},
		{
			id: 10,
			nombre: 'Ciencias',
			icono: 'bi-beaker',
			categoria: 'Académica',
			fecha: '7 de octubre de 2026',
			hora: '1:00 p. m.',
			lugar: 'Laboratorio de ciencias',
			cupos: 20,
			inscritos: 16,
			estado: 'Activa',
			descripcion:
				'Actividad experimental orientada al aprendizaje de conceptos científicos mediante prácticas y demostraciones.'
		},
		{
			id: 11,
			nombre: 'Voleibol',
			icono: 'bi-volleyball',
			categoria: 'Deportes',
			fecha: '10 de octubre de 2026',
			hora: '3:00 p. m.',
			lugar: 'Coliseo escolar',
			cupos: 24,
			inscritos: 19,
			estado: 'Activa',
			descripcion:
				'Entrenamiento de voleibol enfocado en técnicas básicas, coordinación y trabajo colectivo.'
		},
		{
			id: 12,
			nombre: 'Fotografía',
			icono: 'bi-camera',
			categoria: 'Arte',
			fecha: '12 de octubre de 2026',
			hora: '2:30 p. m.',
			lugar: 'Sala audiovisual',
			cupos: 15,
			inscritos: 15,
			estado: 'Cupos completos',
			descripcion:
				'Taller de fotografía para desarrollar composición, manejo de luz y creatividad visual.'
		},
		{
			id: 13,
			nombre: 'Ciencia y Tecnología',
			icono: 'bi-cpu',
			categoria: 'Tecnología',
			fecha: '15 de octubre de 2026',
			hora: '1:30 p. m.',
			lugar: 'Laboratorio de tecnología',
			cupos: 25,
			inscritos: 17,
			estado: 'Activa',
			descripcion:
				'Espacio de exploración tecnológica mediante proyectos prácticos y actividades de innovación.'
		},
		{
			id: 14,
			nombre: 'Literatura',
			icono: 'bi-book',
			categoria: 'Académica',
			fecha: '18 de octubre de 2026',
			hora: '2:00 p. m.',
			lugar: 'Biblioteca',
			cupos: 20,
			inscritos: 13,
			estado: 'Activa',
			descripcion:
				'Club de lectura y escritura enfocado en análisis de textos, creatividad y expresión escrita.'
		},
		{
			id: 15,
			nombre: 'Atletismo',
			icono: 'bi-person-running',
			categoria: 'Deportes',
			fecha: '20 de octubre de 2026',
			hora: '3:30 p. m.',
			lugar: 'Pista deportiva',
			cupos: 25,
			inscritos: 20,
			estado: 'Activa',
			descripcion:
				'Actividad deportiva centrada en resistencia, velocidad, coordinación y preparación física.'
		},
		{
			id: 16,
			nombre: 'Diseño Digital',
			icono: 'bi-vector-pen',
			categoria: 'Tecnología',
			fecha: '22 de octubre de 2026',
			hora: '2:30 p. m.',
			lugar: 'Sala de informática',
			cupos: 18,
			inscritos: 9,
			estado: 'Activa',
			descripcion:
				'Taller de creación de piezas digitales mediante herramientas de diseño y composición visual.'
		},
		{
			id: 17,
			nombre: 'Coro Escolar',
			icono: 'bi-mic',
			categoria: 'Arte',
			fecha: '25 de octubre de 2026',
			hora: '4:00 p. m.',
			lugar: 'Auditorio',
			cupos: 25,
			inscritos: 21,
			estado: 'Activa',
			descripcion:
				'Actividad musical orientada al canto grupal, coordinación vocal y expresión artística.'
		},
		{
			id: 18,
			nombre: 'Matemáticas Recreativas',
			icono: 'bi-calculator',
			categoria: 'Académica',
			fecha: '28 de octubre de 2026',
			hora: '1:30 p. m.',
			lugar: 'Aula 5',
			cupos: 20,
			inscritos: 8,
			estado: 'Activa',
			descripcion:
				'Actividades lúdicas para fortalecer el razonamiento lógico y la resolución de problemas matemáticos.'
		},
		{
			id: 19,
			nombre: 'Tenis de Mesa',
			icono: 'bi-table',
			categoria: 'Deportes',
			fecha: '30 de octubre de 2026',
			hora: '3:00 p. m.',
			lugar: 'Coliseo escolar',
			cupos: 16,
			inscritos: 16,
			estado: 'Cupos completos',
			descripcion:
				'Entrenamiento de tenis de mesa enfocado en coordinación, reflejos y técnicas básicas del deporte.'
		},
		{
			id: 20,
			nombre: 'Cine y Producción',
			icono: 'bi-camera-reels',
			categoria: 'Arte',
			fecha: '2 de noviembre de 2026',
			hora: '3:30 p. m.',
			lugar: 'Sala audiovisual',
			cupos: 22,
			inscritos: 14,
			estado: 'Activa',
			descripcion:
				'Espacio creativo dedicado al análisis cinematográfico y elaboración de pequeños proyectos audiovisuales.'
		}
	]);


	// =========================================================
	// FORMULARIO
	// =========================================================

	let formulario = $state({
		nombre: '',
		categoria: 'Deportes',
		fecha: '',
		hora: '',
		lugar: '',
		cupos: 20,
		descripcion: '',
		estado: 'Activa',
		icono: 'bi-calendar-event'
	});


	// =========================================================
	// FILTROS
	// =========================================================

	let actividadesFiltradas = $derived(
		actividades.filter((actividad) => {

			const coincideBusqueda =
				actividad.nombre
					.toLowerCase()
					.includes(busqueda.toLowerCase());

			const coincideCategoria =
				filtroCategoria === 'Todas' ||
				actividad.categoria === filtroCategoria;

			const coincideEstado =
				filtroEstado === 'Todos' ||
				actividad.estado === filtroEstado;

			return (
				coincideBusqueda &&
				coincideCategoria &&
				coincideEstado
			);
		})
	);


	// =========================================================
	// INDICADORES
	// =========================================================

	let totalActividades = $derived(
		actividades.length
	);

	let actividadesActivas = $derived(
		actividades.filter(
			(actividad) => actividad.estado === 'Activa'
		).length
	);

	let cuposDisponibles = $derived(
		actividades.reduce(
			(total, actividad) =>
				total +
				Math.max(
					actividad.cupos - actividad.inscritos,
					0
				),
			0
		)
	);

	let totalInscritos = $derived(
		actividades.reduce(
			(total, actividad) =>
				total + actividad.inscritos,
			0
		)
	);


	// =========================================================
	// PAGINACIÓN
	// =========================================================

	let totalPaginas = $derived(
		Math.max(
			1,
			Math.ceil(
				actividadesFiltradas.length /
				actividadesPorPagina
			)
		)
	);


	let actividadesPaginadas = $derived(
		actividadesFiltradas.slice(
			(paginaActual - 1) * actividadesPorPagina,
			paginaActual * actividadesPorPagina
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
	// FORMULARIO
	// =========================================================

	function abrirNuevaActividad() {

		modoEdicion = false;
		actividadSeleccionada = null;

		formulario = {
			nombre: '',
			categoria: 'Deportes',
			fecha: '',
			hora: '',
			lugar: '',
			cupos: 20,
			descripcion: '',
			estado: 'Activa',
			icono: 'bi-calendar-event'
		};

		mostrarFormulario = true;
	}


	function editarActividad(actividad) {

		modoEdicion = true;
		actividadSeleccionada = actividad;

		formulario = {
			nombre: actividad.nombre,
			categoria: actividad.categoria,
			fecha: actividad.fecha,
			hora: actividad.hora,
			lugar: actividad.lugar,
			cupos: actividad.cupos,
			descripcion: actividad.descripcion,
			estado: actividad.estado,
			icono: actividad.icono
		};

		mostrarFormulario = true;
	}


	function guardarActividad() {

		if (
			!formulario.nombre.trim() ||
			!formulario.fecha.trim() ||
			!formulario.lugar.trim()
		) {
			return;
		}


		if (modoEdicion) {

			actividades = actividades.map((actividad) =>
				actividad.id === actividadSeleccionada.id
					? {
							...actividad,
							nombre: formulario.nombre,
							categoria: formulario.categoria,
							fecha: formulario.fecha,
							hora: formulario.hora,
							lugar: formulario.lugar,
							cupos: Number(formulario.cupos),
							descripcion: formulario.descripcion,
							estado: formulario.estado,
							icono: formulario.icono
						}
					: actividad
			);

		} else {

			const nuevaActividad = {
				id: Date.now(),
				nombre: formulario.nombre,
				categoria: formulario.categoria,
				fecha: formulario.fecha,
				hora: formulario.hora,
				lugar: formulario.lugar,
				cupos: Number(formulario.cupos),
				inscritos: 0,
				estado: formulario.estado,
				descripcion: formulario.descripcion,
				icono: formulario.icono
			};

			actividades = [
				...actividades,
				nuevaActividad
			];
		}

		cerrarFormulario();
	}


	function eliminarActividad(actividad) {

		const confirmar = confirm(
			`¿Deseas eliminar la actividad "${actividad.nombre}"?`
		);

		if (!confirmar) {
			return;
		}

		actividades = actividades.filter(
			(item) => item.id !== actividad.id
		);

		if (paginaActual > totalPaginas) {
			paginaActual = totalPaginas;
		}
	}


	// =========================================================
	// MODALES
	// =========================================================

	function verDetalles(actividad) {

		actividadSeleccionada = actividad;
		mostrarDetalles = true;
	}


	function cerrarFormulario() {

		mostrarFormulario = false;
		modoEdicion = false;
		actividadSeleccionada = null;
	}


	function cerrarDetalles() {

		mostrarDetalles = false;
		actividadSeleccionada = null;
	}


	// =========================================================
	// FUNCIONES DE APOYO
	// =========================================================

	function porcentajeOcupacion(actividad) {

		if (actividad.cupos === 0) {
			return 0;
		}

		return Math.min(
			Math.round(
				(actividad.inscritos / actividad.cupos) * 100
			),
			100
		);
	}


	function cuposRestantes(actividad) {

		return Math.max(
			actividad.cupos - actividad.inscritos,
			0
		);
	}


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


	function claseEstado(estado) {

		if (estado === 'Activa') {
			return 'status-active';
		}

		if (estado === 'Cupos completos') {
			return 'status-full';
		}

		return 'status-inactive';
	}

</script>


<svelte:head>
	<title>Actividades | Colegio San Miguel</title>
</svelte:head>


<div class="container-fluid px-4 py-4">

	<!-- =====================================================
	     ENCABEZADO
	     ===================================================== -->

	<div class="page-header">

		<div>

			<h2>
				Actividades
			</h2>

			<p>
				Consulta y administra las actividades extracurriculares.
			</p>

		</div>


		<button
			class="btn btn-primary new-activity-button"
			onclick={abrirNuevaActividad}
		>
			<i class="bi bi-plus-lg"></i>
			Nueva actividad
		</button>

	</div>


	<!-- =====================================================
	     INDICADORES
	     ===================================================== -->

	<div class="row g-3 mb-4">

		<div class="col-md-6 col-xl-3">

			<div class="soft-card indicator-card">

				<div class="icon-soft blue">
					<i class="bi bi-calendar-event"></i>
				</div>

				<div>

					<span class="indicator-label">
						Actividades
					</span>

					<strong>
						{totalActividades}
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
						Activas
					</span>

					<strong>
						{actividadesActivas}
					</strong>

				</div>

			</div>

		</div>


		<div class="col-md-6 col-xl-3">

			<div class="soft-card indicator-card">

				<div class="icon-soft purple">
					<i class="bi bi-grid-3x3-gap"></i>
				</div>

				<div>

					<span class="indicator-label">
						Cupos disponibles
					</span>

					<strong>
						{cuposDisponibles}
					</strong>

				</div>

			</div>

		</div>


		<div class="col-md-6 col-xl-3">

			<div class="soft-card indicator-card">

				<div class="icon-soft orange">
					<i class="bi bi-people"></i>
				</div>

				<div>

					<span class="indicator-label">
						Inscritos
					</span>

					<strong>
						{totalInscritos}
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
					Actividades
				</h3>

				<span>
					{actividadesFiltradas.length} resultados
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
					placeholder="Buscar actividad..."
					bind:value={busqueda}
					oninput={() => (paginaActual = 1)}
				/>

			</div>


			<select
				class="form-select"
				bind:value={filtroCategoria}
				onchange={() => (paginaActual = 1)}
			>

				<option value="Todas">
					Todas las categorías
				</option>

				<option value="Deportes">
					Deportes
				</option>

				<option value="Tecnología">
					Tecnología
				</option>

				<option value="Arte">
					Arte
				</option>

				<option value="Académica">
					Académica
				</option>

			</select>


			<select
				class="form-select"
				bind:value={filtroEstado}
				onchange={() => (paginaActual = 1)}
			>

				<option value="Todos">
					Todos los estados
				</option>

				<option value="Activa">
					Activas
				</option>

				<option value="Cupos completos">
					Cupos completos
				</option>

			</select>

		</div>

	</div>


	<!-- =====================================================
	     TARJETAS
	     ===================================================== -->

	<div class="row g-3 mt-1">

		{#if actividadesFiltradas.length > 0}

			{#each actividadesPaginadas as actividad}

				<div class="col-md-6 col-xl-4">

					<div class="soft-card activity-card">

						<div class="activity-top">

							<div class="activity-image">

								<i class={`bi ${actividad.icono}`}></i>

							</div>


							<div class="activity-actions">

								<button
									class="action-btn"
									title="Editar"
									aria-label="Editar actividad"
									onclick={() => editarActividad(actividad)}
								>
									<i class="bi bi-pencil"></i>
								</button>


								<button
									class="action-btn delete"
									title="Eliminar"
									aria-label="Eliminar actividad"
									onclick={() => eliminarActividad(actividad)}
								>
									<i class="bi bi-trash3"></i>
								</button>

							</div>

						</div>


						<div class="activity-content">

							<div class="activity-badges">

								<span
									class={`category-badge ${claseCategoria(actividad.categoria)}`}
								>
									{actividad.categoria}
								</span>


								<span
									class={`status-badge ${claseEstado(actividad.estado)}`}
								>
									{actividad.estado}
								</span>

							</div>


							<h3>
								{actividad.nombre}
							</h3>


							<div class="activity-info">

								<div>
									<span>
										<i class="bi bi-calendar3"></i>
									</span>

									{actividad.fecha}
								</div>


								<div>
									<span>
										<i class="bi bi-geo-alt"></i>
									</span>

									{actividad.lugar}
								</div>

							</div>


							<div class="capacity-section">

								<div class="capacity-header">

									<span>
										Cupos
									</span>

									<strong>
										{cuposRestantes(actividad)} disponibles
									</strong>

								</div>


								<div class="progress">

									<div
										class="progress-bar"
										style={`width: ${porcentajeOcupacion(actividad)}%`}
									></div>

								</div>

							</div>


							<button
								class="details-button"
								onclick={() => verDetalles(actividad)}
							>
								Ver detalles
								<i class="bi bi-arrow-right"></i>
							</button>

						</div>

					</div>

				</div>

			{/each}

		{:else}

			<div class="col-12">

				<div class="soft-card empty-state">

					<div class="empty-icon">
						<i class="bi bi-search"></i>
					</div>

					<strong>
						No se encontraron actividades
					</strong>

					<span>
						Prueba con otro nombre, categoría o estado.
					</span>

				</div>

			</div>

		{/if}

	</div>


	<!-- =====================================================
	     PAGINACIÓN
	     ===================================================== -->

	{#if actividadesFiltradas.length > 0 && totalPaginas > 1}

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
						onclick={() => irPagina(index + 1)}
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
     MODAL NUEVA / EDITAR
     ========================================================= -->

{#if mostrarFormulario}

	<div
		class="modal-backdrop-custom"
		role="presentation"
		onclick={(event) => {
			if (event.target === event.currentTarget) {
				cerrarFormulario();
			}
		}}
	>

		<div
			class="activity-modal"
			role="dialog"
			aria-modal="true"
		>

			<div class="modal-header-custom">

				<div>

					<h3>
						{modoEdicion ? 'Editar actividad' : 'Nueva actividad'}
					</h3>

					<p>
						Completa la información de la actividad.
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

				<div class="mb-3">

					<label
						class="form-label"
						for="nombre"
					>
						Nombre
					</label>

					<input
						id="nombre"
						type="text"
						class="form-control"
						placeholder="Ej. Fútbol"
						bind:value={formulario.nombre}
					/>

				</div>


				<div class="row g-3 mb-3">

					<div class="col-md-6">

						<label
							class="form-label"
							for="categoria"
						>
							Categoría
						</label>

						<select
							id="categoria"
							class="form-select"
							bind:value={formulario.categoria}
						>

							<option value="Deportes">
								Deportes
							</option>

							<option value="Tecnología">
								Tecnología
							</option>

							<option value="Arte">
								Arte
							</option>

							<option value="Académica">
								Académica
							</option>

						</select>

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

							<option value="Activa">
								Activa
							</option>

							<option value="Cupos completos">
								Cupos completos
							</option>

						</select>

					</div>

				</div>


				<div class="row g-3 mb-3">

					<div class="col-md-6">

						<label
							class="form-label"
							for="fecha"
						>
							Fecha
						</label>

						<input
							id="fecha"
							type="text"
							class="form-control"
							placeholder="Ej. 30 de septiembre de 2026"
							bind:value={formulario.fecha}
						/>

					</div>


					<div class="col-md-6">

						<label
							class="form-label"
							for="hora"
						>
							Hora
						</label>

						<input
							id="hora"
							type="text"
							class="form-control"
							placeholder="Ej. 3:00 p. m."
							bind:value={formulario.hora}
						/>

					</div>

				</div>


				<div class="row g-3 mb-3">

					<div class="col-md-8">

						<label
							class="form-label"
							for="lugar"
						>
							Lugar
						</label>

						<input
							id="lugar"
							type="text"
							class="form-control"
							placeholder="Ej. Cancha principal"
							bind:value={formulario.lugar}
						/>

					</div>


					<div class="col-md-4">

						<label
							class="form-label"
							for="cupos"
						>
							Cupos
						</label>

						<input
							id="cupos"
							type="number"
							min="1"
							class="form-control"
							bind:value={formulario.cupos}
						/>

					</div>

				</div>


				<div>

					<label
						class="form-label"
						for="descripcion"
					>
						Descripción
					</label>

					<textarea
						id="descripcion"
						class="form-control"
						rows="3"
						placeholder="Describe brevemente la actividad..."
						bind:value={formulario.descripcion}
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
					onclick={guardarActividad}
				>
					<i class="bi bi-check2"></i>
					{modoEdicion ? 'Guardar cambios' : 'Crear actividad'}
				</button>

			</div>

		</div>

	</div>

{/if}


<!-- =========================================================
     MODAL DETALLES
     ========================================================= -->

{#if mostrarDetalles && actividadSeleccionada}

	<div
		class="modal-backdrop-custom"
		role="presentation"
		onclick={(event) => {
			if (event.target === event.currentTarget) {
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

			<div class="details-header">

				<div class="details-heading">

					<div class="details-icon">
						<i class={`bi ${actividadSeleccionada.icono}`}></i>
					</div>

					<div>

						<span class="details-label">
							Actividad
						</span>

						<h3 id="details-title">
							{actividadSeleccionada.nombre}
						</h3>

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


			<div class="details-body">

				<div class="activity-badges">

					<span
						class={`category-badge ${claseCategoria(actividadSeleccionada.categoria)}`}
					>
						{actividadSeleccionada.categoria}
					</span>


					<span
						class={`status-badge ${claseEstado(actividadSeleccionada.estado)}`}
					>
						{actividadSeleccionada.estado}
					</span>

				</div>


				<section class="detail-section">

					<span class="section-label">
						Descripción
					</span>

					<p class="details-description">
						{actividadSeleccionada.descripcion}
					</p>

				</section>


				<section class="detail-section">

					<span class="section-label">
						Información
					</span>


					<div class="details-grid">

						<div>

							<span>
								Fecha
							</span>

							<strong>
								{actividadSeleccionada.fecha}
							</strong>

						</div>


						<div>

							<span>
								Hora
							</span>

							<strong>
								{actividadSeleccionada.hora}
							</strong>

						</div>


						<div>

							<span>
								Lugar
							</span>

							<strong>
								{actividadSeleccionada.lugar}
							</strong>

						</div>


						<div>

							<span>
								Estado
							</span>

							<strong>
								{actividadSeleccionada.estado}
							</strong>

						</div>

					</div>

				</section>


				<section class="detail-section">

					<div class="capacity-detail-header">

						<div>

							<span class="section-label">
								Cupos
							</span>

							<strong class="capacity-number">
								{actividadSeleccionada.inscritos}
								de
								{actividadSeleccionada.cupos}
							</strong>

						</div>


						<span class="percentage">
							{porcentajeOcupacion(actividadSeleccionada)}%
						</span>

					</div>


					<div class="progress details-progress">

						<div
							class="progress-bar"
							style={`width: ${porcentajeOcupacion(actividadSeleccionada)}%`}
						></div>

					</div>


					<div class="capacity-summary">

						<span>
							Inscritos
							<strong>
								{actividadSeleccionada.inscritos}
							</strong>
						</span>

						<span>
							Disponibles
							<strong>
								{cuposRestantes(actividadSeleccionada)}
							</strong>
						</span>

					</div>

				</section>

			</div>


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
						const actividad = actividadSeleccionada;

						cerrarDetalles();

						editarActividad(actividad);
					}}
				>
					<i class="bi bi-pencil"></i>
					Editar actividad
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


	.new-activity-button {
		height: 42px;
		padding: 0 17px;
		border-radius: 9px;
		font-size: 13px;
		font-weight: 600;
	}


	.new-activity-button i {
		margin-right: 6px;
	}


	/* =========================================================
	   TARJETAS
	   ========================================================= */

	.soft-card {
		background: #ffffff;
		border: 1px solid #edf0f2;
		border-radius: 13px;
		box-shadow: 0 3px 14px rgba(0, 0, 0, 0.035);
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
	}


	.icon-soft.green {
		background: #e9f7ef;
	}


	.icon-soft.purple {
		background: #f1edff;
	}


	.icon-soft.orange {
		background: #fff2e5;
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
			0 0 0 0.15rem rgba(13, 110, 253, 0.08);
	}


	.filters .form-select {
		width: 190px;
		height: 38px;
		border-radius: 8px;
		font-size: 12px;
	}


	/* =========================================================
	   ACTIVIDADES
	   ========================================================= */

	.activity-card {
		height: 100%;
		overflow: hidden;
		transition:
			transform 0.2s ease,
			box-shadow 0.2s ease;
	}


	.activity-card:hover {
		transform: translateY(-2px);
		box-shadow: 0 8px 24px rgba(0, 0, 0, 0.07);
	}


	.activity-top {
		display: flex;
		align-items: flex-start;
		justify-content: space-between;
		padding: 16px 16px 0;
	}


	.activity-image {
		width: 52px;
		height: 52px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 13px;
		background: #f4f7fb;
		color: #0d6efd;
	}


	.activity-image i {
		font-size: 24px;
	}


	.activity-actions {
		display: flex;
		gap: 5px;
	}


	.action-btn {
		width: 31px;
		height: 31px;
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


	.activity-content {
		padding: 15px 17px 18px;
	}


	.activity-badges {
		display: flex;
		flex-wrap: wrap;
		gap: 6px;
		margin-bottom: 10px;
	}


	.category-badge,
	.status-badge {
		display: inline-flex;
		align-items: center;
		padding: 5px 9px;
		border-radius: 20px;
		font-size: 10px;
		font-weight: 600;
	}


	.category-sport {
		background: #eef5ff;
		color: #0d6efd;
	}


	.category-tech {
		background: #e9f7ef;
		color: #198754;
	}


	.category-art {
		background: #f1edff;
		color: #6f42c1;
	}


	.category-academic {
		background: #fff2e5;
		color: #d97706;
	}


	.category-default {
		background: #f1f3f5;
		color: #6c757d;
	}


	.status-active {
		background: #e9f7ef;
		color: #198754;
	}


	.status-full {
		background: #fff2e5;
		color: #d97706;
	}


	.status-inactive {
		background: #f1f3f5;
		color: #6c757d;
	}


	.activity-content h3 {
		margin: 0 0 14px;
		color: #343a40;
		font-size: 17px;
		font-weight: 700;
	}


	.activity-info {
		display: flex;
		flex-direction: column;
		gap: 8px;
		margin-bottom: 18px;
		color: #868e96;
		font-size: 11px;
	}


	.activity-info div {
		display: flex;
		align-items: center;
		gap: 8px;
	}


	.activity-info div span {
		width: 18px;
		color: #0d6efd;
		text-align: center;
	}


	/* =========================================================
	   CUPOS
	   ========================================================= */

	.capacity-section {
		padding-top: 14px;
		border-top: 1px solid #f0f2f4;
	}


	.capacity-header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-bottom: 7px;
		color: #868e96;
		font-size: 11px;
	}


	.capacity-header strong {
		color: #495057;
		font-size: 11px;
	}


	.progress {
		height: 6px;
		background: #eef1f4;
		border-radius: 10px;
		overflow: hidden;
	}


	.progress-bar {
		height: 100%;
		background: #0d6efd;
		border-radius: 10px;
	}


	.details-button {
		width: 100%;
		height: 36px;
		margin-top: 15px;
		border: 1px solid #e5e9ed;
		border-radius: 8px;
		background: #ffffff;
		color: #0d6efd;
		font-size: 11px;
		font-weight: 600;
		cursor: pointer;
		transition:
			background-color 0.2s ease,
			border-color 0.2s ease;
	}


	.details-button i {
		margin-left: 5px;
		font-size: 12px;
	}


	.details-button:hover {
		background: #eef5ff;
		border-color: #d5e5ff;
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

	.empty-state {
		min-height: 250px;
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


	.activity-modal,
	.details-modal {
		width: 100%;
		background: #ffffff;
		border-radius: 15px;
		box-shadow: 0 18px 50px rgba(0, 0, 0, 0.15);
		overflow: hidden;
	}


	.activity-modal {
		max-width: 570px;
	}


	.details-modal {
		max-width: 520px;
	}


	.modal-header-custom {
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
			0 0 0 0.15rem rgba(13, 110, 253, 0.08);
	}


	.modal-footer-custom,
	.details-footer {
		padding: 16px 23px;
		display: flex;
		justify-content: flex-end;
		gap: 8px;
		background: #fafbfc;
		border-top: 1px solid #edf0f2;
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
		padding: 21px 23px;
		display: flex;
		align-items: flex-start;
		justify-content: space-between;
		border-bottom: 1px solid #edf0f2;
	}


	.details-heading {
		display: flex;
		align-items: center;
		gap: 13px;
	}


	.details-icon {
		width: 52px;
		height: 52px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 13px;
		background: #eef5ff;
		color: #0d6efd;
		font-size: 24px;
	}


	.details-label {
		display: block;
		margin-bottom: 2px;
		color: #adb5bd;
		font-size: 10px;
	}


	.details-heading h3 {
		margin: 0;
		color: #343a40;
		font-size: 20px;
		font-weight: 700;
	}


	.details-body {
		padding: 22px 23px;
	}


	.detail-section {
		padding-top: 17px;
		margin-top: 17px;
		border-top: 1px solid #edf0f2;
	}


	.section-label {
		display: block;
		margin-bottom: 8px;
		color: #868e96;
		font-size: 10px;
		font-weight: 600;
		text-transform: uppercase;
		letter-spacing: 0.3px;
	}


	.details-description {
		margin: 0;
		color: #495057;
		font-size: 12px;
		line-height: 1.7;
	}


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
		font-size: 10px;
	}


	.details-grid strong {
		display: block;
		color: #495057;
		font-size: 11px;
		font-weight: 600;
	}


	/* =========================================================
	   CUPOS DETALLE
	   ========================================================= */

	.capacity-detail-header {
		display: flex;
		align-items: flex-end;
		justify-content: space-between;
		margin-bottom: 8px;
	}


	.capacity-number {
		color: #343a40;
		font-size: 13px;
		font-weight: 600;
	}


	.percentage {
		color: #0d6efd;
		font-size: 13px;
		font-weight: 700;
	}


	.details-progress {
		height: 8px;
	}


	.capacity-summary {
		display: flex;
		justify-content: space-between;
		margin-top: 9px;
		color: #adb5bd;
		font-size: 10px;
	}


	.capacity-summary strong {
		margin-left: 4px;
		color: #495057;
		font-weight: 600;
	}


	/* =========================================================
	   RESPONSIVE
	   ========================================================= */

	@media (max-width: 800px) {

		.page-header {
			align-items: flex-start;
			flex-direction: column;
		}


		.new-activity-button {
			width: 100%;
		}


		.filters {
			flex-direction: column;
			align-items: stretch;
		}


		.filters .form-select {
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
			padding: 12px;
		}


		.activity-modal,
		.details-modal {
			border-radius: 12px;
		}


		.modal-body-custom,
		.details-body {
			padding-left: 18px;
			padding-right: 18px;
		}


		.modal-header-custom,
		.details-header {
			padding-left: 18px;
			padding-right: 18px;
		}


		.modal-footer-custom,
		.details-footer {
			padding-left: 18px;
			padding-right: 18px;
		}


		.details-grid {
			grid-template-columns: 1fr;
		}


		.pagination-container {
			flex-wrap: wrap;
			gap: 8px;
		}


		.pagination-button {
			font-size: 10px;
			padding: 0 10px;
		}

	}

</style>