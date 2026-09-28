<script>
	let busqueda = $state('');
	let filtroRol = $state('Todos');

	let mostrarFormulario = $state(false);
	let modoEdicion = $state(false);
	let usuarioEditando = $state(null);


	// =========================================================
	// USUARIOS ESTÁTICOS
	// =========================================================

	let usuarios = $state([
		{
			id: 1,
			nombre: 'Ana Martínez',
			correo: 'ana.martinez@colegiosanmiguel.edu.co',
			rol: 'Estudiante',
			estado: 'Activo'
		},
		{
			id: 2,
			nombre: 'Carlos Rodríguez',
			correo: 'carlos.rodriguez@colegiosanmiguel.edu.co',
			rol: 'Estudiante',
			estado: 'Activo'
		},
		{
			id: 3,
			nombre: 'Laura Gómez',
			correo: 'laura.gomez@colegiosanmiguel.edu.co',
			rol: 'Padre / acudiente',
			estado: 'Activo'
		},
		{
			id: 4,
			nombre: 'María González',
			correo: 'maria.gonzalez@colegiosanmiguel.edu.co',
			rol: 'Coordinación',
			estado: 'Activo'
		},
		{
			id: 5,
			nombre: 'Andrés Pérez',
			correo: 'andres.perez@colegiosanmiguel.edu.co',
			rol: 'Estudiante',
			estado: 'Inactivo'
		}
	]);


	// =========================================================
	// FORMULARIO
	// =========================================================

	let formulario = $state({
		nombre: '',
		correo: '',
		rol: 'Estudiante',
		estado: 'Activo'
	});


	// =========================================================
	// FILTROS
	// =========================================================

	let usuariosFiltrados = $derived(
		usuarios.filter((usuario) => {

			const texto =
				busqueda.toLowerCase();

			const coincideBusqueda =
				usuario.nombre
					.toLowerCase()
					.includes(texto) ||
				usuario.correo
					.toLowerCase()
					.includes(texto);

			const coincideRol =
				filtroRol === 'Todos' ||
				usuario.rol === filtroRol;

			return (
				coincideBusqueda &&
				coincideRol
			);
		})
	);


	// =========================================================
	// INDICADORES
	// =========================================================

	let totalUsuarios = $derived(
		usuarios.length
	);


	let totalEstudiantes = $derived(
		usuarios.filter(
			(usuario) =>
				usuario.rol === 'Estudiante'
		).length
	);


	let totalPadres = $derived(
		usuarios.filter(
			(usuario) =>
				usuario.rol === 'Padre / acudiente'
		).length
	);


	let totalCoordinacion = $derived(
		usuarios.filter(
			(usuario) =>
				usuario.rol === 'Coordinación'
		).length
	);


	// =========================================================
	// NUEVO USUARIO
	// =========================================================

	function abrirNuevoUsuario() {

		modoEdicion = false;

		usuarioEditando = null;

		formulario = {
			nombre: '',
			correo: '',
			rol: 'Estudiante',
			estado: 'Activo'
		};

		mostrarFormulario = true;
	}


	// =========================================================
	// EDITAR USUARIO
	// =========================================================

	function editarUsuario(usuario) {

		modoEdicion = true;

		usuarioEditando = usuario;

		formulario = {
			nombre: usuario.nombre,
			correo: usuario.correo,
			rol: usuario.rol,
			estado: usuario.estado
		};

		mostrarFormulario = true;
	}


	// =========================================================
	// GUARDAR USUARIO
	// =========================================================

	function guardarUsuario() {

		if (
			!formulario.nombre.trim() ||
			!formulario.correo.trim()
		) {
			return;
		}


		if (modoEdicion) {

			usuarios = usuarios.map(
				(usuario) =>
					usuario.id ===
					usuarioEditando.id
						? {
								...usuario,
								nombre:
									formulario.nombre,
								correo:
									formulario.correo,
								rol:
									formulario.rol,
								estado:
									formulario.estado
							}
						: usuario
			);

		} else {

			const nuevoUsuario = {

				id: Date.now(),

				nombre:
					formulario.nombre,

				correo:
					formulario.correo,

				rol:
					formulario.rol,

				estado:
					formulario.estado
			};


			usuarios = [
				...usuarios,
				nuevoUsuario
			];
		}


		cerrarFormulario();
	}


	// =========================================================
	// ELIMINAR USUARIO
	// =========================================================

	function eliminarUsuario(usuario) {

		const confirmar = confirm(
			`¿Deseas eliminar a ${usuario.nombre}?`
		);


		if (!confirmar) {
			return;
		}


		usuarios =
			usuarios.filter(
				(item) =>
					item.id !== usuario.id
			);
	}


	// =========================================================
	// CERRAR FORMULARIO
	// =========================================================

	function cerrarFormulario() {

		mostrarFormulario = false;

		modoEdicion = false;

		usuarioEditando = null;
	}


	// =========================================================
	// INICIALES
	// =========================================================

	function obtenerIniciales(nombre) {

		return nombre
			.split(' ')
			.slice(0, 2)
			.map(
				(parte) =>
					parte.charAt(0)
			)
			.join('')
			.toUpperCase();
	}


	// =========================================================
	// CLASE DEL ROL
	// =========================================================

	function claseRol(rol) {

		if (rol === 'Estudiante') {
			return 'role-student';
		}


		if (rol === 'Padre / acudiente') {
			return 'role-parent';
		}


		if (rol === 'Coordinación') {
			return 'role-coordination';
		}


		return 'role-default';
	}


	// =========================================================
	// ICONO DEL ROL
	// =========================================================

	function iconoRol(rol) {

		if (rol === 'Estudiante') {
			return 'bi-mortarboard';
		}


		if (rol === 'Padre / acudiente') {
			return 'bi-person-heart';
		}


		if (rol === 'Coordinación') {
			return 'bi-person-workspace';
		}


		return 'bi-person';
	}


	// =========================================================
	// CLASE DEL ESTADO
	// =========================================================

	function claseEstado(estado) {

		return estado === 'Activo'
			? 'status-active'
			: 'status-inactive';
	}
</script>


<svelte:head>
	<title>Usuarios | Colegio San Miguel</title>
</svelte:head>


<div class="container-fluid px-4 py-4">

	<!-- =====================================================
	     ENCABEZADO
	     ===================================================== -->

	<div class="page-header">

		<div>

			<h2>
				Usuarios
			</h2>


			<p>
				Administra los usuarios registrados en el sistema.
			</p>

		</div>


		<button
			class="btn btn-primary new-user-button"
			onclick={abrirNuevoUsuario}
		>
			<i class="bi bi-person-plus"></i>
			Nuevo usuario
		</button>

	</div>


	<!-- =====================================================
	     INDICADORES
	     ===================================================== -->

	<div class="row g-3 mb-4">

		<!-- TOTAL -->

		<div class="col-md-6 col-xl-3">

			<div class="soft-card indicator-card">

				<div class="icon-soft blue">

					<i class="bi bi-people"></i>

				</div>


				<div>

					<span class="indicator-label">
						Total
					</span>


					<strong>
						{totalUsuarios}
					</strong>

				</div>

			</div>

		</div>


		<!-- ESTUDIANTES -->

		<div class="col-md-6 col-xl-3">

			<div class="soft-card indicator-card">

				<div class="icon-soft green">

					<i class="bi bi-mortarboard"></i>

				</div>


				<div>

					<span class="indicator-label">
						Estudiantes
					</span>


					<strong>
						{totalEstudiantes}
					</strong>

				</div>

			</div>

		</div>


		<!-- PADRES -->

		<div class="col-md-6 col-xl-3">

			<div class="soft-card indicator-card">

				<div class="icon-soft purple">

					<i class="bi bi-person-heart"></i>

				</div>


				<div>

					<span class="indicator-label">
						Padres / acudientes
					</span>


					<strong>
						{totalPadres}
					</strong>

				</div>

			</div>

		</div>


		<!-- COORDINACIÓN -->

		<div class="col-md-6 col-xl-3">

			<div class="soft-card indicator-card">

				<div class="icon-soft orange">

					<i class="bi bi-person-workspace"></i>

				</div>


				<div>

					<span class="indicator-label">
						Coordinación
					</span>


					<strong>
						{totalCoordinacion}
					</strong>

				</div>

			</div>

		</div>

	</div>


	<!-- =====================================================
	     TABLA
	     ===================================================== -->

	<div class="soft-card table-card">

		<!-- BARRA DE HERRAMIENTAS -->

		<div class="table-toolbar">

			<div>

				<h3>
					Usuarios registrados
				</h3>


				<span>
					{usuariosFiltrados.length} resultados
				</span>

			</div>


			<div class="filters">

				<!-- BUSCAR -->

				<div class="search-box">

					<span>
						<i class="bi bi-search"></i>
					</span>


					<input
						type="text"
						placeholder="Buscar usuario..."
						bind:value={busqueda}
					/>

				</div>


				<!-- FILTRO ROL -->

				<select
					class="form-select role-filter"
					bind:value={filtroRol}
				>

					<option value="Todos">
						Todos los roles
					</option>


					<option value="Estudiante">
						Estudiantes
					</option>


					<option value="Padre / acudiente">
						Padres / acudientes
					</option>


					<option value="Coordinación">
						Coordinación
					</option>

				</select>

			</div>

		</div>


		<!-- =================================================
		     TABLA
		     ================================================= -->

		<div class="table-responsive">

			<table class="table users-table align-middle">

				<thead>

					<tr>

						<th>
							Usuario
						</th>


						<th>
							Rol
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

					{#if usuariosFiltrados.length > 0}

						{#each usuariosFiltrados as usuario}

							<tr>

								<!-- USUARIO -->

								<td>

									<div class="user-cell">

										<div class="avatar">

											{obtenerIniciales(
												usuario.nombre
											)}

										</div>


										<div>

											<strong>
												{usuario.nombre}
											</strong>


											<span>
												{usuario.correo}
											</span>

										</div>

									</div>

								</td>


								<!-- ROL -->

								<td>

									<span
										class={`role-badge ${claseRol(
											usuario.rol
										)}`}
									>

										<i
											class={`bi ${iconoRol(
												usuario.rol
											)}`}
										></i>

										{usuario.rol}

									</span>

								</td>


								<!-- ESTADO -->

								<td>

									<span
										class={`status-badge ${claseEstado(
											usuario.estado
										)}`}
									>

										<span></span>

										{usuario.estado}

									</span>

								</td>


								<!-- ACCIONES -->

								<td>

									<div class="actions">

										<button
											class="action-btn edit"
											title="Editar usuario"
											aria-label="Editar usuario"
											onclick={() =>
												editarUsuario(
													usuario
												)}
										>

											<i class="bi bi-pencil"></i>

										</button>


										<button
											class="action-btn delete"
											title="Eliminar usuario"
											aria-label="Eliminar usuario"
											onclick={() =>
												eliminarUsuario(
													usuario
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

							<td colspan="4">

								<div class="empty-state">

									<div class="empty-icon">

										<i class="bi bi-search"></i>

									</div>


									<strong>
										No se encontraron usuarios
									</strong>


									<span>
										Prueba con otro nombre,
										correo o rol.
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
     MODAL NUEVO / EDITAR USUARIO
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
			class="user-modal"
			role="dialog"
			aria-modal="true"
			aria-labelledby="modal-title"
		>

			<!-- CABECERA -->

			<div class="modal-header-custom">

				<div>

					<h3 id="modal-title">

						{modoEdicion
							? 'Editar usuario'
							: 'Nuevo usuario'}

					</h3>


					<p>
						Completa la información del usuario.
					</p>

				</div>


				<button
					class="close-button"
					type="button"
					aria-label="Cerrar"
					onclick={cerrarFormulario}
				>
					<i class="bi bi-x-lg"></i>
				</button>

			</div>


			<!-- FORMULARIO -->

			<div class="modal-body-custom">

				<div class="mb-3">

					<label
						class="form-label"
						for="nombre"
					>
						Nombre completo
					</label>


					<input
						id="nombre"
						type="text"
						class="form-control"
						placeholder="Ej. Juan Pérez"
						bind:value={
							formulario.nombre
						}
					/>

				</div>


				<div class="mb-3">

					<label
						class="form-label"
						for="correo"
					>
						Correo institucional
					</label>


					<input
						id="correo"
						type="email"
						class="form-control"
						placeholder="usuario@colegiosanmiguel.edu.co"
						bind:value={
							formulario.correo
						}
					/>

				</div>


				<div class="row g-3">

					<!-- ROL -->

					<div class="col-md-6">

						<label
							class="form-label"
							for="rol"
						>
							Rol
						</label>


						<select
							id="rol"
							class="form-select"
							bind:value={
								formulario.rol
							}
						>

							<option value="Estudiante">
								Estudiante
							</option>


							<option value="Padre / acudiente">
								Padre / acudiente
							</option>


							<option value="Coordinación">
								Coordinación
							</option>

						</select>

					</div>


					<!-- ESTADO -->

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
							bind:value={
								formulario.estado
							}
						>

							<option value="Activo">
								Activo
							</option>


							<option value="Inactivo">
								Inactivo
							</option>

						</select>

					</div>

				</div>

			</div>


			<!-- FOOTER -->

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
					onclick={guardarUsuario}
				>

					<i
						class={`bi ${
							modoEdicion
								? 'bi-check2'
								: 'bi-person-plus'
						}`}
					></i>


					{modoEdicion
						? 'Guardar cambios'
						: 'Crear usuario'}

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


	.new-user-button {
		height: 42px;

		padding: 0 17px;

		border-radius: 9px;

		font-size: 13px;
		font-weight: 600;
	}


	.new-user-button i {
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

		flex-shrink: 0;
	}


	.icon-soft.blue {
		background: #eaf2ff;
		color: #0d6efd;
	}


	.icon-soft.green {
		background: #e9f7ef;
		color: #198754;
	}


	.icon-soft.purple {
		background: #f1edff;
		color: #6f42c1;
	}


	.icon-soft.orange {
		background: #fff2e5;
		color: #d97706;
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
	   TABLA
	   ========================================================= */

	.table-card {
		overflow: hidden;
	}


	.table-toolbar {
		padding: 20px 22px;

		display: flex;
		align-items: center;
		justify-content: space-between;

		gap: 20px;

		border-bottom: 1px solid #edf0f2;
	}


	.table-toolbar h3 {
		margin: 0 0 3px;

		color: #343a40;

		font-size: 15px;
		font-weight: 650;
	}


	.table-toolbar > div:first-child span {
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

		width: 230px;
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

		color: #343a40;

		font-size: 12px;
	}


	.search-box input:focus {
		border-color: #86b7fe;

		box-shadow:
			0 0 0 0.15rem
			rgba(13, 110, 253, 0.08);
	}


	.role-filter {
		width: 170px;

		height: 38px;

		border-radius: 8px;

		font-size: 12px;
	}


	.users-table {
		margin: 0;
	}


	.users-table thead th {
		padding: 13px 22px;

		background: #fafbfc;

		border-bottom: 1px solid #edf0f2;

		color: #868e96;

		font-size: 11px;
		font-weight: 600;

		text-transform: uppercase;

		letter-spacing: 0.3px;
	}


	.users-table tbody td {
		padding: 14px 22px;

		border-bottom: 1px solid #f0f2f4;

		color: #495057;

		font-size: 12px;
	}


	.users-table tbody tr:last-child td {
		border-bottom: none;
	}


	.users-table tbody tr:hover {
		background: #fcfdff;
	}


	/* =========================================================
	   USUARIO
	   ========================================================= */

	.user-cell {
		display: flex;
		align-items: center;

		gap: 11px;
	}


	.avatar {
		width: 38px;
		height: 38px;

		display: flex;
		align-items: center;
		justify-content: center;

		border-radius: 50%;

		background: #eef5ff;

		color: #0d6efd;

		font-size: 11px;
		font-weight: 700;

		flex-shrink: 0;
	}


	.user-cell strong {
		display: block;

		margin-bottom: 2px;

		color: #343a40;

		font-size: 12px;
		font-weight: 600;
	}


	.user-cell span {
		display: block;

		color: #adb5bd;

		font-size: 11px;
	}


	/* =========================================================
	   ROLES
	   ========================================================= */

	.role-badge,
	.status-badge {
		display: inline-flex;
		align-items: center;

		gap: 5px;

		border-radius: 20px;

		padding: 5px 9px;

		font-size: 10px;

		font-weight: 600;
	}


	.role-student {
		background: #eef5ff;

		color: #0d6efd;
	}


	.role-parent {
		background: #f1edff;

		color: #6f42c1;
	}


	.role-coordination {
		background: #e9f7ef;

		color: #198754;
	}


	.role-default {
		background: #f1f3f5;

		color: #6c757d;
	}


	.role-badge i {
		font-size: 10px;
	}


	/* =========================================================
	   ESTADO
	   ========================================================= */

	.status-active {
		background: #e9f7ef;

		color: #198754;
	}


	.status-inactive {
		background: #f8f9fa;

		color: #868e96;
	}


	.status-badge span {
		width: 5px;
		height: 5px;

		margin-right: 1px;

		border-radius: 50%;

		background: currentColor;
	}


	/* =========================================================
	   ACCIONES
	   ========================================================= */

	.actions {
		display: flex;

		justify-content: flex-end;

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

		font-size: 12px;

		cursor: pointer;

		transition: all 0.2s ease;
	}


	.action-btn.edit {
		color: #0d6efd;
	}


	.action-btn.edit:hover {
		background: #eef5ff;

		border-color: #d5e5ff;
	}


	.action-btn.delete {
		color: #adb5bd;
	}


	.action-btn.delete:hover {
		background: #fff5f5;

		border-color: #f5d8da;

		color: #dc3545;
	}


	/* =========================================================
	   ESTADO VACÍO
	   ========================================================= */

	.empty-state {
		min-height: 230px;

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
	   MODAL
	   ========================================================= */

	.modal-backdrop-custom {
		position: fixed;

		inset: 0;

		z-index: 2000;

		display: flex;

		align-items: center;

		justify-content: center;

		padding: 20px;

		background: rgba(
			33,
			37,
			41,
			0.35
		);
	}


	.user-modal {
		width: 100%;

		max-width: 500px;

		background: #ffffff;

		border-radius: 15px;

		box-shadow:
			0 18px 50px
			rgba(0, 0, 0, 0.15);

		overflow: hidden;
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

		display: flex;

		align-items: center;

		justify-content: center;

		border: none;

		border-radius: 7px;

		background: #f8f9fa;

		color: #868e96;

		font-size: 12px;

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


	.modal-body-custom
		.form-control:focus,
	.modal-body-custom
		.form-select:focus {
		border-color: #86b7fe;

		box-shadow:
			0 0 0 0.15rem
			rgba(13, 110, 253, 0.08);
	}


	.modal-footer-custom {
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
	   RESPONSIVE
	   ========================================================= */

	@media (max-width: 800px) {

		.page-header {
			align-items: flex-start;

			flex-direction: column;
		}


		.new-user-button {
			width: 100%;
		}


		.table-toolbar {
			align-items: stretch;

			flex-direction: column;
		}


		.filters {
			width: 100%;

			flex-direction: column;
		}


		.search-box,
		.role-filter {
			width: 100%;
		}

	}


	@media (max-width: 576px) {

		.container-fluid {
			padding-left: 15px !important;

			padding-right: 15px !important;
		}


		.users-table
			thead th,
		.users-table
			tbody td {
			padding-left: 14px;

			padding-right: 14px;
		}


		.user-cell span {
			max-width: 170px;

			overflow: hidden;

			text-overflow: ellipsis;

			white-space: nowrap;
		}


		.modal-backdrop-custom {
			padding: 12px;
		}


		.user-modal {
			border-radius: 12px;
		}

	}

</style>