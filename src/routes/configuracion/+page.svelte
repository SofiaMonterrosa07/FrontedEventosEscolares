<script>
	let seccionActiva = $state('institucion');

	let mostrarGuardar = $state(false);
	let mostrarRestablecer = $state(false);

	let configuracion = $state({
		nombreColegio: 'Colegio San Miguel',
		correo: 'contacto@colegiosanmiguel.edu.co',
		telefono: '(605) 123 4567',
		direccion: 'Barranquilla, Atlántico',

		nombreAdministrador: 'Administrador',
		correoAdministrador: 'admin@colegiosanmiguel.edu.co',

		notificacionesInscripciones: true,
		notificacionesAutorizaciones: true,
		notificacionesActividades: true,
		resumenSemanal: false,

		sesionesActivas: true,
		confirmarEliminaciones: true
	});


	let roles = $state([
		{
			nombre: 'Administrador',
			descripcion: 'Acceso completo al sistema',
			usuarios: 2,
			estado: true,
			icono: 'bi-shield-check'
		},
		{
			nombre: 'Coordinación',
			descripcion: 'Gestión de actividades y registros',
			usuarios: 4,
			estado: true,
			icono: 'bi-clipboard-check'
		},
		{
			nombre: 'Padre / acudiente',
			descripcion: 'Autorizaciones y seguimiento',
			usuarios: 86,
			estado: true,
			icono: 'bi-person-heart'
		},
		{
			nombre: 'Estudiante',
			descripcion: 'Consulta e inscripción a actividades',
			usuarios: 240,
			estado: true,
			icono: 'bi-mortarboard'
		}
	]);


	function seleccionarSeccion(seccion) {
		seccionActiva = seccion;
	}


	function guardarCambios() {
		mostrarGuardar = true;

		setTimeout(() => {
			mostrarGuardar = false;
		}, 2200);
	}


	function abrirRestablecer() {
		mostrarRestablecer = true;
	}


	function cerrarRestablecer() {
		mostrarRestablecer = false;
	}


	function restablecerConfiguracion() {
		configuracion.notificacionesInscripciones = true;
		configuracion.notificacionesAutorizaciones = true;
		configuracion.notificacionesActividades = true;
		configuracion.resumenSemanal = false;
		configuracion.sesionesActivas = true;
		configuracion.confirmarEliminaciones = true;

		mostrarRestablecer = false;
	}


	function alternarRol(rol) {
		roles = roles.map((item) =>
			item.nombre === rol.nombre
				? {
						...item,
						estado: !item.estado
					}
				: item
		);
	}
</script>


<svelte:head>
	<title>Configuración | Colegio San Miguel</title>
</svelte:head>


<div class="container-fluid px-4 py-4">

	<!-- =====================================================
	     ENCABEZADO
	     ===================================================== -->

	<div class="page-header">

		<div>
			<h2>Configuración</h2>

			<p>
				Administra las preferencias generales del sistema.
			</p>
		</div>


		<div class="header-actions">

			<button
				class="btn btn-light reset-button"
				onclick={abrirRestablecer}
			>
				<i class="bi bi-arrow-counterclockwise"></i>
				Restablecer
			</button>


			<button
				class="btn btn-primary save-button"
				onclick={guardarCambios}
			>
				<i class="bi bi-check-lg"></i>
				Guardar cambios
			</button>

		</div>

	</div>


	<!-- =====================================================
	     ESTRUCTURA PRINCIPAL
	     ===================================================== -->

	<div class="settings-layout">

		<!-- ===================================================
		     MENÚ LATERAL
		     =================================================== -->

		<aside class="soft-card settings-menu">

			<div class="menu-title">
				<span>Preferencias</span>
			</div>


			<button
				class:active={seccionActiva === 'institucion'}
				class="settings-link"
				onclick={() =>
					seleccionarSeccion('institucion')}
			>

				<span class="settings-icon">
					<i class="bi bi-building"></i>
				</span>

				<div>
					<strong>Institución</strong>
					<small>Información general</small>
				</div>

			</button>


			<button
				class:active={seccionActiva === 'perfil'}
				class="settings-link"
				onclick={() =>
					seleccionarSeccion('perfil')}
			>

				<span class="settings-icon">
					<i class="bi bi-person"></i>
				</span>

				<div>
					<strong>Perfil</strong>
					<small>Datos del usuario</small>
				</div>

			</button>


			<button
				class:active={seccionActiva === 'notificaciones'}
				class="settings-link"
				onclick={() =>
					seleccionarSeccion('notificaciones')}
			>

				<span class="settings-icon">
					<i class="bi bi-bell"></i>
				</span>

				<div>
					<strong>Notificaciones</strong>
					<small>Preferencias de avisos</small>
				</div>

			</button>


			<button
				class:active={seccionActiva === 'seguridad'}
				class="settings-link"
				onclick={() =>
					seleccionarSeccion('seguridad')}
			>

				<span class="settings-icon">
					<i class="bi bi-shield-lock"></i>
				</span>

				<div>
					<strong>Seguridad</strong>
					<small>Acceso y sesiones</small>
				</div>

			</button>


			<button
				class:active={seccionActiva === 'roles'}
				class="settings-link"
				onclick={() =>
					seleccionarSeccion('roles')}
			>

				<span class="settings-icon">
					<i class="bi bi-people"></i>
				</span>

				<div>
					<strong>Roles</strong>
					<small>Permisos de usuarios</small>
				</div>

			</button>

		</aside>


		<!-- ===================================================
		     CONTENIDO
		     =================================================== -->

		<section class="settings-content">

			<!-- =================================================
			     INSTITUCIÓN
			     ================================================= -->

			{#if seccionActiva === 'institucion'}

				<div class="soft-card settings-card">

					<div class="card-header-custom">

						<div class="heading-icon blue">
							<i class="bi bi-building"></i>
						</div>

						<div>

							<h3>
								Información institucional
							</h3>

							<p>
								Datos generales del colegio.
							</p>

						</div>

					</div>


					<div class="card-body-custom">

						<div class="row g-3">

							<div class="col-md-7">

								<label
									for="nombreColegio"
									class="form-label"
								>
									Nombre de la institución
								</label>

								<input
									id="nombreColegio"
									type="text"
									class="form-control"
									bind:value={
										configuracion.nombreColegio
									}
								/>

							</div>


							<div class="col-md-5">

								<label
									for="telefono"
									class="form-label"
								>
									Teléfono
								</label>

								<input
									id="telefono"
									type="text"
									class="form-control"
									bind:value={
										configuracion.telefono
									}
								/>

							</div>


							<div class="col-12">

								<label
									for="correo"
									class="form-label"
								>
									Correo institucional
								</label>

								<input
									id="correo"
									type="email"
									class="form-control"
									bind:value={
										configuracion.correo
									}
								/>

							</div>


							<div class="col-12">

								<label
									for="direccion"
									class="form-label"
								>
									Dirección
								</label>

								<input
									id="direccion"
									type="text"
									class="form-control"
									bind:value={
										configuracion.direccion
									}
								/>

							</div>

						</div>

					</div>

				</div>


				<div class="soft-card information-card">

					<div class="information-icon">
						<i class="bi bi-info-lg"></i>
					</div>


					<div>

						<strong>
							Información del sistema
						</strong>

						<p>
							Estos datos son utilizados para identificar
							la institución dentro de la plataforma.
						</p>

					</div>

				</div>

			{/if}


			<!-- =================================================
			     PERFIL
			     ================================================= -->

			{#if seccionActiva === 'perfil'}

				<div class="soft-card settings-card">

					<div class="card-header-custom">

						<div class="heading-icon purple">
							<i class="bi bi-person"></i>
						</div>

						<div>

							<h3>
								Perfil del usuario
							</h3>

							<p>
								Administra la información de tu cuenta.
							</p>

						</div>

					</div>


					<div class="card-body-custom">

						<div class="profile-preview">

							<div class="profile-avatar">
								AD
							</div>

							<div>

								<strong>
									{configuracion.nombreAdministrador}
								</strong>

								<span>
									Administrador
								</span>

							</div>

						</div>


						<div class="row g-3">

							<div class="col-md-6">

								<label
									for="nombreAdministrador"
									class="form-label"
								>
									Nombre
								</label>

								<input
									id="nombreAdministrador"
									type="text"
									class="form-control"
									bind:value={
										configuracion.nombreAdministrador
									}
								/>

							</div>


							<div class="col-md-6">

								<label
									for="correoAdministrador"
									class="form-label"
								>
									Correo
								</label>

								<input
									id="correoAdministrador"
									type="email"
									class="form-control"
									bind:value={
										configuracion.correoAdministrador
									}
								/>

							</div>

						</div>

					</div>

				</div>


				<div class="soft-card account-card">

					<div>

						<strong>
							Tipo de cuenta
						</strong>

						<span>
							Administrador del sistema
						</span>

					</div>


					<span class="account-badge">
						<i class="bi bi-shield-check"></i>
						Administrador
					</span>

				</div>

			{/if}


			<!-- =================================================
			     NOTIFICACIONES
			     ================================================= -->

			{#if seccionActiva === 'notificaciones'}

				<div class="soft-card settings-card">

					<div class="card-header-custom">

						<div class="heading-icon orange">
							<i class="bi bi-bell"></i>
						</div>

						<div>

							<h3>
								Notificaciones
							</h3>

							<p>
								Selecciona los avisos que deseas recibir.
							</p>

						</div>

					</div>


					<div class="card-body-custom no-padding">

						<div class="setting-row">

							<div class="setting-description">

								<strong>
									Nuevas inscripciones
								</strong>

								<span>
									Recibir avisos cuando un estudiante
									se registre en una actividad.
								</span>

							</div>


							<label class="switch">

								<input
									type="checkbox"
									bind:checked={
										configuracion.notificacionesInscripciones
									}
								/>

								<span class="slider"></span>

							</label>

						</div>


						<div class="setting-row">

							<div class="setting-description">

								<strong>
									Autorizaciones
								</strong>

								<span>
									Recibir avisos sobre nuevas
									autorizaciones de acudientes.
								</span>

							</div>


							<label class="switch">

								<input
									type="checkbox"
									bind:checked={
										configuracion.notificacionesAutorizaciones
									}
								/>

								<span class="slider"></span>

							</label>

						</div>


						<div class="setting-row">

							<div class="setting-description">

								<strong>
									Actividades
								</strong>

								<span>
									Recibir avisos relacionados con
									cambios en las actividades.
								</span>

							</div>


							<label class="switch">

								<input
									type="checkbox"
									bind:checked={
										configuracion.notificacionesActividades
									}
								/>

								<span class="slider"></span>

							</label>

						</div>


						<div class="setting-row">

							<div class="setting-description">

								<strong>
									Resumen semanal
								</strong>

								<span>
									Recibir un resumen periódico
									del comportamiento del sistema.
								</span>

							</div>


							<label class="switch">

								<input
									type="checkbox"
									bind:checked={
										configuracion.resumenSemanal
									}
								/>

								<span class="slider"></span>

							</label>

						</div>

					</div>

				</div>

			{/if}


			<!-- =================================================
			     SEGURIDAD
			     ================================================= -->

			{#if seccionActiva === 'seguridad'}

				<div class="soft-card settings-card">

					<div class="card-header-custom">

						<div class="heading-icon green">
							<i class="bi bi-shield-lock"></i>
						</div>

						<div>

							<h3>
								Seguridad
							</h3>

							<p>
								Administra las preferencias de acceso.
							</p>

						</div>

					</div>


					<div class="card-body-custom no-padding">

						<div class="setting-row">

							<div class="setting-description">

								<strong>
									Control de sesiones
								</strong>

								<span>
									Mantener seguimiento de las sesiones
									activas del sistema.
								</span>

							</div>


							<label class="switch">

								<input
									type="checkbox"
									bind:checked={
										configuracion.sesionesActivas
									}
								/>

								<span class="slider"></span>

							</label>

						</div>


						<div class="setting-row">

							<div class="setting-description">

								<strong>
									Confirmar eliminaciones
								</strong>

								<span>
									Solicitar confirmación antes de
									eliminar información.
								</span>

							</div>


							<label class="switch">

								<input
									type="checkbox"
									bind:checked={
										configuracion.confirmarEliminaciones
									}
								/>

								<span class="slider"></span>

							</label>

						</div>

					</div>

				</div>


				<div class="soft-card security-card">

					<div class="security-icon">
						<i class="bi bi-key"></i>
					</div>


					<div class="security-content">

						<strong>
							Contraseña
						</strong>

						<span>
							Actualiza periódicamente las credenciales
							de acceso de la cuenta.
						</span>

					</div>


					<button
						class="btn btn-light security-button"
						type="button"
					>
						Cambiar contraseña
					</button>

				</div>

			{/if}


			<!-- =================================================
			     ROLES
			     ================================================= -->

			{#if seccionActiva === 'roles'}

				<div class="soft-card settings-card">

					<div class="card-header-custom">

						<div class="heading-icon blue">
							<i class="bi bi-people"></i>
						</div>

						<div>

							<h3>
								Roles del sistema
							</h3>

							<p>
								Consulta y administra los roles disponibles.
							</p>

						</div>

					</div>


					<div class="roles-list">

						{#each roles as rol}

							<div class="role-row">

								<div class="role-icon">

									<i class={`bi ${rol.icono}`}></i>

								</div>


								<div class="role-info">

									<strong>
										{rol.nombre}
									</strong>

									<span>
										{rol.descripcion}
									</span>

									<small>
										{rol.usuarios} usuarios
									</small>

								</div>


								<div class="role-status">

									<span
										class:enabled={rol.estado}
										class="status-badge"
									>
										{rol.estado
											? 'Activo'
											: 'Inactivo'}
									</span>


									<button
										class="role-toggle"
										class:on={rol.estado}
										type="button"
										onclick={() =>
											alternarRol(rol)}
										aria-label="Cambiar estado del rol"
									>

										<span></span>

									</button>

								</div>

							</div>

						{/each}

					</div>

				</div>

			{/if}

		</section>

	</div>

</div>


<!-- =========================================================
     NOTIFICACIÓN GUARDADO
     ========================================================= -->

{#if mostrarGuardar}

	<div class="save-toast">

		<div class="toast-icon">
			<i class="bi bi-check-lg"></i>
		</div>


		<div>

			<strong>
				Cambios guardados
			</strong>

			<span>
				La configuración se actualizó correctamente.
			</span>

		</div>

	</div>

{/if}


<!-- =========================================================
     MODAL RESTABLECER
     ========================================================= -->

{#if mostrarRestablecer}

	<div
		class="modal-backdrop-custom"
		role="presentation"
		onclick={(event) => {

			if (
				event.target ===
				event.currentTarget
			) {
				cerrarRestablecer();
			}

		}}
	>

		<div
			class="confirm-modal"
			role="dialog"
			aria-modal="true"
		>

			<div class="confirm-icon">
				<i class="bi bi-arrow-counterclockwise"></i>
			</div>


			<h3>
				Restablecer configuración
			</h3>


			<p>
				Se restaurarán las preferencias a sus valores
				predeterminados. Los datos institucionales y
				del perfil no se modificarán.
			</p>


			<div class="confirm-actions">

				<button
					class="btn btn-light cancel-button"
					onclick={cerrarRestablecer}
				>
					Cancelar
				</button>


				<button
					class="btn btn-primary confirm-button"
					onclick={restablecerConfiguracion}
				>
					<i class="bi bi-arrow-counterclockwise"></i>
					Restablecer
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


	.header-actions {
		display: flex;
		align-items: center;
		gap: 8px;
	}


	.save-button,
	.reset-button {
		height: 40px;
		padding: 0 15px;
		border-radius: 8px;
		font-size: 12px;
		font-weight: 600;
	}


	.save-button i,
	.reset-button i {
		margin-right: 6px;
	}


	.reset-button {
		border: 1px solid #e9ecef;
		color: #6c757d;
		background: #ffffff;
	}


	.reset-button:hover {
		background: #f8f9fa;
	}


	/* =========================================================
	   ESTRUCTURA
	   ========================================================= */

	.settings-layout {
		display: grid;
		grid-template-columns: 235px minmax(0, 1fr);
		gap: 18px;
		align-items: start;
	}


	.soft-card {
		background: #ffffff;
		border: 1px solid #edf0f2;
		border-radius: 13px;
		box-shadow:
			0 3px 14px rgba(0, 0, 0, 0.035);
	}


	.settings-content {
		min-width: 0;
	}


	/* =========================================================
	   MENÚ
	   ========================================================= */

	.settings-menu {
		padding: 10px;
		position: sticky;
		top: 15px;
	}


	.menu-title {
		padding: 8px 10px 10px;
		color: #adb5bd;
		font-size: 9px;
		font-weight: 700;
		text-transform: uppercase;
		letter-spacing: 0.4px;
	}


	.settings-link {
		width: 100%;
		display: flex;
		align-items: center;
		gap: 10px;
		padding: 10px;
		margin-bottom: 3px;
		border: none;
		border-radius: 9px;
		background: transparent;
		text-align: left;
		cursor: pointer;
		transition:
			background-color 0.2s ease,
			color 0.2s ease;
	}


	.settings-link:last-child {
		margin-bottom: 0;
	}


	.settings-link:hover {
		background: #f8f9fa;
	}


	.settings-link.active {
		background: #eef5ff;
	}


	.settings-icon {
		width: 33px;
		height: 33px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 8px;
		background: #f8f9fa;
		color: #6c757d;
		font-size: 14px;
		flex-shrink: 0;
	}


	.settings-link.active .settings-icon {
		background: #ffffff;
		color: #0d6efd;
	}


	.settings-link div {
		min-width: 0;
	}


	.settings-link strong {
		display: block;
		margin-bottom: 2px;
		color: #495057;
		font-size: 11px;
		font-weight: 600;
	}


	.settings-link.active strong {
		color: #0d6efd;
	}


	.settings-link small {
		display: block;
		color: #adb5bd;
		font-size: 9px;
	}


	/* =========================================================
	   TARJETAS DE CONFIGURACIÓN
	   ========================================================= */

	.settings-card {
		overflow: hidden;
	}


	.card-header-custom {
		display: flex;
		align-items: center;
		gap: 12px;
		padding: 20px 22px;
		border-bottom: 1px solid #edf0f2;
	}


	.heading-icon {
		width: 42px;
		height: 42px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 10px;
		font-size: 18px;
		flex-shrink: 0;
	}


	.heading-icon.blue {
		background: #eaf2ff;
		color: #0d6efd;
	}


	.heading-icon.purple {
		background: #f1edff;
		color: #6f42c1;
	}


	.heading-icon.orange {
		background: #fff2e5;
		color: #d97706;
	}


	.heading-icon.green {
		background: #e9f7ef;
		color: #198754;
	}


	.card-header-custom h3 {
		margin: 0 0 3px;
		color: #343a40;
		font-size: 15px;
		font-weight: 650;
	}


	.card-header-custom p {
		margin: 0;
		color: #adb5bd;
		font-size: 10px;
	}


	.card-body-custom {
		padding: 22px;
	}


	.card-body-custom.no-padding {
		padding: 0;
	}


	.form-label {
		margin-bottom: 7px;
		color: #495057;
		font-size: 11px;
		font-weight: 600;
	}


	.form-control {
		min-height: 40px;
		border-color: #e1e5e9;
		border-radius: 8px;
		font-size: 12px;
	}


	.form-control:focus {
		border-color: #86b7fe;
		box-shadow:
			0 0 0 0.15rem
			rgba(13, 110, 253, 0.08);
	}


	/* =========================================================
	   INFORMACIÓN
	   ========================================================= */

	.information-card {
		display: flex;
		align-items: flex-start;
		gap: 10px;
		margin-top: 12px;
		padding: 14px;
	}


	.information-icon {
		width: 28px;
		height: 28px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 50%;
		background: #eaf2ff;
		color: #0d6efd;
		font-size: 13px;
		flex-shrink: 0;
	}


	.information-card strong {
		display: block;
		margin-bottom: 2px;
		color: #495057;
		font-size: 10px;
	}


	.information-card p {
		margin: 0;
		color: #adb5bd;
		font-size: 9px;
		line-height: 1.5;
	}


	/* =========================================================
	   PERFIL
	   ========================================================= */

	.profile-preview {
		display: flex;
		align-items: center;
		gap: 11px;
		padding: 13px;
		margin-bottom: 20px;
		background: #f8f9fa;
		border-radius: 10px;
	}


	.profile-avatar {
		width: 44px;
		height: 44px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 50%;
		background: #0d6efd;
		color: #ffffff;
		font-size: 12px;
		font-weight: 700;
	}


	.profile-preview strong {
		display: block;
		margin-bottom: 2px;
		color: #343a40;
		font-size: 12px;
	}


	.profile-preview span {
		color: #adb5bd;
		font-size: 9px;
	}


	.account-card {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 15px;
		margin-top: 12px;
		padding: 16px;
	}


	.account-card strong {
		display: block;
		margin-bottom: 3px;
		color: #495057;
		font-size: 10px;
	}


	.account-card > div > span {
		color: #adb5bd;
		font-size: 9px;
	}


	.account-badge {
		display: inline-flex;
		align-items: center;
		gap: 5px;
		padding: 5px 9px;
		border-radius: 20px;
		background: #eaf2ff;
		color: #0d6efd;
		font-size: 9px;
		font-weight: 600;
		white-space: nowrap;
	}


	/* =========================================================
	   INTERRUPTORES
	   ========================================================= */

	.setting-row {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 20px;
		padding: 17px 22px;
		border-bottom: 1px solid #f0f2f4;
	}


	.setting-row:last-child {
		border-bottom: none;
	}


	.setting-description {
		min-width: 0;
	}


	.setting-description strong {
		display: block;
		margin-bottom: 3px;
		color: #495057;
		font-size: 11px;
		font-weight: 600;
	}


	.setting-description span {
		display: block;
		color: #adb5bd;
		font-size: 9px;
		line-height: 1.5;
	}


	.switch {
		position: relative;
		width: 40px;
		height: 22px;
		flex-shrink: 0;
	}


	.switch input {
		width: 0;
		height: 0;
		opacity: 0;
	}


	.slider {
		position: absolute;
		inset: 0;
		background: #dee2e6;
		border-radius: 20px;
		cursor: pointer;
		transition: background-color 0.2s ease;
	}


	.slider::before {
		content: '';
		position: absolute;
		width: 16px;
		height: 16px;
		left: 3px;
		top: 3px;
		background: #ffffff;
		border-radius: 50%;
		box-shadow:
			0 1px 3px rgba(0, 0, 0, 0.15);
		transition: transform 0.2s ease;
	}


	.switch input:checked + .slider {
		background: #0d6efd;
	}


	.switch input:checked + .slider::before {
		transform: translateX(18px);
	}


	/* =========================================================
	   SEGURIDAD
	   ========================================================= */

	.security-card {
		display: flex;
		align-items: center;
		gap: 12px;
		margin-top: 12px;
		padding: 16px;
	}


	.security-icon {
		width: 38px;
		height: 38px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 9px;
		background: #f8f9fa;
		color: #495057;
		font-size: 16px;
		flex-shrink: 0;
	}


	.security-content {
		flex: 1;
		min-width: 0;
	}


	.security-content strong {
		display: block;
		margin-bottom: 2px;
		color: #495057;
		font-size: 10px;
	}


	.security-content span {
		color: #adb5bd;
		font-size: 9px;
		line-height: 1.5;
	}


	.security-button {
		height: 35px;
		padding: 0 11px;
		border: 1px solid #e9ecef;
		border-radius: 7px;
		color: #6c757d;
		font-size: 10px;
		font-weight: 600;
		white-space: nowrap;
	}


	.security-button:hover {
		background: #f8f9fa;
	}


	/* =========================================================
	   ROLES
	   ========================================================= */

	.roles-list {
		padding: 5px 22px;
	}


	.role-row {
		display: flex;
		align-items: center;
		gap: 12px;
		padding: 15px 0;
		border-bottom: 1px solid #f0f2f4;
	}


	.role-row:last-child {
		border-bottom: none;
	}


	.role-icon {
		width: 38px;
		height: 38px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 9px;
		background: #f8f9fa;
		color: #0d6efd;
		font-size: 16px;
		flex-shrink: 0;
	}


	.role-info {
		flex: 1;
		min-width: 0;
	}


	.role-info strong {
		display: block;
		margin-bottom: 2px;
		color: #495057;
		font-size: 11px;
		font-weight: 600;
	}


	.role-info span {
		display: block;
		margin-bottom: 3px;
		color: #adb5bd;
		font-size: 9px;
	}


	.role-info small {
		color: #868e96;
		font-size: 8px;
	}


	.role-status {
		display: flex;
		align-items: center;
		gap: 10px;
	}


	.status-badge {
		padding: 5px 8px;
		border-radius: 20px;
		background: #fff0f1;
		color: #dc3545;
		font-size: 8px;
		font-weight: 600;
	}


	.status-badge.enabled {
		background: #e9f7ef;
		color: #198754;
	}


	.role-toggle {
		position: relative;
		width: 35px;
		height: 20px;
		padding: 0;
		border: none;
		border-radius: 20px;
		background: #dee2e6;
		cursor: pointer;
		transition: background-color 0.2s ease;
	}


	.role-toggle span {
		position: absolute;
		width: 14px;
		height: 14px;
		top: 3px;
		left: 3px;
		border-radius: 50%;
		background: #ffffff;
		box-shadow:
			0 1px 3px rgba(0, 0, 0, 0.15);
		transition: transform 0.2s ease;
	}


	.role-toggle.on {
		background: #0d6efd;
	}


	.role-toggle.on span {
		transform: translateX(15px);
	}


	/* =========================================================
	   TOAST
	   ========================================================= */

	.save-toast {
		position: fixed;
		right: 22px;
		bottom: 22px;
		z-index: 3000;
		display: flex;
		align-items: center;
		gap: 10px;
		min-width: 280px;
		padding: 13px 15px;
		background: #ffffff;
		border: 1px solid #e1e5e9;
		border-radius: 11px;
		box-shadow:
			0 10px 35px rgba(0, 0, 0, 0.12);
		animation: toast-in 0.25s ease;
	}


	.toast-icon {
		width: 30px;
		height: 30px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 50%;
		background: #e9f7ef;
		color: #198754;
		font-size: 12px;
		font-weight: 700;
	}


	.save-toast strong {
		display: block;
		margin-bottom: 2px;
		color: #343a40;
		font-size: 10px;
	}


	.save-toast span {
		color: #adb5bd;
		font-size: 8px;
	}


	@keyframes toast-in {

		from {
			opacity: 0;
			transform: translateY(8px);
		}

		to {
			opacity: 1;
			transform: translateY(0);
		}

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
		background: rgba(33, 37, 41, 0.35);
	}


	.confirm-modal {
		width: 100%;
		max-width: 390px;
		padding: 25px;
		background: #ffffff;
		border-radius: 15px;
		box-shadow:
			0 18px 50px rgba(0, 0, 0, 0.15);
		text-align: center;
	}


	.confirm-icon {
		width: 45px;
		height: 45px;
		margin: 0 auto 13px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 50%;
		background: #eaf2ff;
		color: #0d6efd;
		font-size: 18px;
	}


	.confirm-modal h3 {
		margin: 0 0 7px;
		color: #343a40;
		font-size: 16px;
		font-weight: 700;
	}


	.confirm-modal p {
		margin: 0 auto 20px;
		max-width: 320px;
		color: #868e96;
		font-size: 10px;
		line-height: 1.6;
	}


	.confirm-actions {
		display: flex;
		justify-content: center;
		gap: 8px;
	}


	.cancel-button,
	.confirm-button {
		height: 37px;
		padding: 0 14px;
		border-radius: 8px;
		font-size: 11px;
		font-weight: 600;
	}


	.confirm-button i {
		margin-right: 5px;
	}


	/* =========================================================
	   RESPONSIVE
	   ========================================================= */

	@media (max-width: 900px) {

		.settings-layout {
			grid-template-columns: 1fr;
		}


		.settings-menu {
			position: static;
			display: flex;
			align-items: stretch;
			gap: 4px;
			overflow-x: auto;
			padding: 8px;
		}


		.menu-title {
			display: none;
		}


		.settings-link {
			min-width: 150px;
			margin: 0;
		}

	}


	@media (max-width: 700px) {

		.page-header {
			align-items: flex-start;
			flex-direction: column;
		}


		.header-actions {
			width: 100%;
		}


		.header-actions button {
			flex: 1;
		}


		.security-card {
			align-items: flex-start;
			flex-wrap: wrap;
		}


		.security-button {
			width: 100%;
		}

	}


	@media (max-width: 576px) {

		.container-fluid {
			padding-left: 15px !important;
			padding-right: 15px !important;
		}


		.card-header-custom,
		.card-body-custom {
			padding: 17px;
		}


		.setting-row {
			padding: 15px 17px;
		}


		.roles-list {
			padding: 5px 17px;
		}


		.settings-link {
			min-width: 135px;
		}


		.settings-link small {
			display: none;
		}


		.role-status {
			gap: 6px;
		}


		.status-badge {
			display: none;
		}


		.save-toast {
			left: 15px;
			right: 15px;
			bottom: 15px;
			min-width: 0;
		}


		.modal-backdrop-custom {
			padding: 10px;
		}


		.confirm-modal {
			padding: 21px;
			border-radius: 12px;
		}

	}


	@media (max-width: 380px) {

		.header-actions {
			flex-direction: column;
		}


		.header-actions button {
			width: 100%;
		}


		.settings-link {
			min-width: 120px;
		}


		.settings-link strong {
			font-size: 10px;
		}


		.role-row {
			gap: 8px;
		}


		.role-icon {
			width: 34px;
			height: 34px;
		}

	}

</style>