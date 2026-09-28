<script>
	let menuPerfilAbierto = $state(false);
	let notificacionesAbiertas = $state(false);
	let busqueda = $state('');

	let notificaciones = $state([
		{
			id: 1,
			titulo: 'Nueva inscripción',
			mensaje: 'Se registró una nueva inscripción en Robótica.',
			tiempo: 'Hace 10 min',
			icono: 'bi-pencil-square',
			leida: false
		},
		{
			id: 2,
			titulo: 'Autorización pendiente',
			mensaje: 'Hay una autorización pendiente de revisión.',
			tiempo: 'Hace 25 min',
			icono: 'bi-file-earmark-check',
			leida: false
		},
		{
			id: 3,
			titulo: 'Actividad actualizada',
			mensaje: 'La actividad de Teatro fue actualizada.',
			tiempo: 'Hace 1 h',
			icono: 'bi-calendar-event',
			leida: true
		}
	]);


	let notificacionesPendientes = $derived(
		notificaciones.filter(
			(notificacion) => !notificacion.leida
		).length
	);


	function alternarPerfil() {
		menuPerfilAbierto = !menuPerfilAbierto;
		notificacionesAbiertas = false;
	}


	function alternarNotificaciones() {
		notificacionesAbiertas = !notificacionesAbiertas;
		menuPerfilAbierto = false;
	}


	function marcarComoLeida(id) {

		const notificacion =
			notificaciones.find(
				(item) => item.id === id
			);


		if (notificacion) {
			notificacion.leida = true;
		}
	}


	function marcarTodasComoLeidas() {

		notificaciones.forEach(
			(notificacion) => {
				notificacion.leida = true;
			}
		);
	}


	function limpiarBusqueda() {
		busqueda = '';
	}


	function cerrarMenus() {
		menuPerfilAbierto = false;
		notificacionesAbiertas = false;
	}


	function cerrarAlHacerClickFuera(event) {

		const elemento = event.target;


		if (
			!elemento.closest(
				'.profile-wrapper'
			) &&
			!elemento.closest(
				'.notifications-wrapper'
			)
		) {
			cerrarMenus();
		}
	}
</script>


<svelte:window
	onclick={cerrarAlHacerClickFuera}
/>


<header class="school-header">

	<div class="container-fluid px-4">

		<div class="header-content">


			<!-- =====================================================
			     IDENTIDAD
			     ===================================================== -->

			<div class="brand">

				<div class="brand-icon">

					<i class="bi bi-building"></i>

				</div>


				<div class="brand-text">

					<h1>
						Colegio San Miguel
					</h1>


					<span>
						Gestión escolar
					</span>

				</div>

			</div>


			<!-- =====================================================
			     BARRA DE BÚSQUEDA
			     ===================================================== -->

			<div class="search-wrapper">

				<div class="search-box">

					<span class="search-icon">

						<i class="bi bi-search"></i>

					</span>


					<input
						type="search"
						bind:value={busqueda}
						placeholder="Buscar..."
						aria-label="Buscar"
					/>


					{#if busqueda}

						<button
							type="button"
							class="clear-search"
							aria-label="Limpiar búsqueda"
							onclick={limpiarBusqueda}
						>

							<i class="bi bi-x-lg"></i>

						</button>

					{/if}

				</div>

			</div>


			<!-- =====================================================
			     NOTIFICACIONES + USUARIO
			     ===================================================== -->

			<div class="header-actions">


				<!-- =================================================
				     NOTIFICACIONES
				     ================================================= -->

				<div class="notifications-wrapper">

					<button
						type="button"
						class:active={
							notificacionesAbiertas
						}
						class="notification-button"
						aria-label="Ver notificaciones"
						aria-expanded={
							notificacionesAbiertas
						}
						onclick={
							alternarNotificaciones
						}
					>

						<span class="notification-icon">

							<i class="bi bi-bell"></i>

						</span>


						{#if notificacionesPendientes > 0}

							<span class="notification-badge">
								{notificacionesPendientes}
							</span>

						{/if}

					</button>


					{#if notificacionesAbiertas}

						<div class="notifications-menu">


							<!-- CABECERA -->

							<div class="notifications-header">

								<div>

									<strong>
										Notificaciones
									</strong>


									<span>
										{notificacionesPendientes}
										pendientes
									</span>

								</div>


								{#if notificacionesPendientes > 0}

									<button
										type="button"
										class="mark-all"
										onclick={
											marcarTodasComoLeidas
										}
									>
										Marcar todas
									</button>

								{/if}

							</div>


							<!-- LISTA -->

							<div class="notifications-list">

								{#if notificaciones.length === 0}

									<div class="empty-notifications">

										<div class="empty-icon">

											<i class="bi bi-bell-slash"></i>

										</div>


										<strong>
											No hay notificaciones
										</strong>


										<span>
											Todo está al día.
										</span>

									</div>

								{:else}

									{#each notificaciones as notificacion}

										<div
											class:unread={
												!notificacion.leida
											}
											class="notification-item"
										>


											<div class="notification-item-icon">

												<i
													class={`bi ${notificacion.icono}`}
												></i>

											</div>


											<div class="notification-content">

												<div class="notification-title-row">

													<strong>
														{notificacion.titulo}
													</strong>


													{#if !notificacion.leida}

														<span class="unread-dot"></span>

													{/if}

												</div>


												<p>
													{notificacion.mensaje}
												</p>


												<div class="notification-bottom">

													<span class="notification-time">
														{notificacion.tiempo}
													</span>


													{#if !notificacion.leida}

														<button
															type="button"
															class="read-button"
															onclick={() =>
																marcarComoLeida(
																	notificacion.id
																)}
														>
															Marcar leída
														</button>

													{/if}

												</div>

											</div>

										</div>

									{/each}

								{/if}

							</div>


							<!-- FOOTER -->

							<div class="notifications-footer">

								<a
									href="/reportes"
									onclick={cerrarMenus}
								>

									Ver todas las notificaciones

									<span>
										<i class="bi bi-arrow-right"></i>
									</span>

								</a>

							</div>

						</div>

					{/if}

				</div>


				<!-- =================================================
				     DIVISOR
				     ================================================= -->

				<div class="header-divider"></div>


				<!-- =================================================
				     USUARIO
				     ================================================= -->

				<div class="user-area">

					<div class="user-info">

						<strong>
							Administrador
						</strong>


						<span>

							<span class="status-dot"></span>

							Sesión activa

						</span>

					</div>


					<div class="profile-wrapper">

						<button
							type="button"
							class:active={
								menuPerfilAbierto
							}
							class="user-avatar"
							aria-label="Abrir información del usuario"
							aria-expanded={
								menuPerfilAbierto
							}
							onclick={
								alternarPerfil
							}
						>
							AD
						</button>


						{#if menuPerfilAbierto}

							<div class="profile-menu">


								<!-- CABECERA PERFIL -->

								<div class="profile-header">

									<div class="profile-avatar">
										AD
									</div>


									<div class="profile-name">

										<strong>
											Administrador
										</strong>


										<span>
											Administrador del sistema
										</span>

									</div>

								</div>


								<div class="menu-divider"></div>


								<!-- CORREO -->

								<div class="profile-item">

									<div class="item-icon">

										<i class="bi bi-envelope"></i>

									</div>


									<div class="item-content">

										<small>
											Correo
										</small>


										<strong>
											admin@colegiosanmiguel.edu.co
										</strong>

									</div>

								</div>


								<!-- ROL -->

								<div class="profile-item">

									<div class="item-icon">

										<i class="bi bi-shield-check"></i>

									</div>


									<div class="item-content">

										<small>
											Rol
										</small>


										<strong>
											Administrador
										</strong>

									</div>

								</div>


								<!-- ESTADO -->

								<div class="profile-item">

									<div
										class="item-icon status-icon"
									>

										<i class="bi bi-circle-fill"></i>

									</div>


									<div class="item-content">

										<small>
											Estado
										</small>


										<strong>
											Sesión activa
										</strong>

									</div>

								</div>


								<div class="menu-divider"></div>


								<!-- CERRAR SESIÓN -->

								<a
									href="/"
									class="profile-logout"
									onclick={cerrarMenus}
								>

									<i class="bi bi-box-arrow-right"></i>


									Cerrar sesión

								</a>

							</div>

						{/if}

					</div>

				</div>

			</div>

		</div>

	</div>

</header>


<style>

	/* =========================================================
	   HEADER
	   ========================================================= */

	.school-header {

		background: #ffffff;

		border-bottom:
			1px solid #edf0f2;
	}


	.header-content {

		min-height: 76px;

		display: flex;

		align-items: center;

		gap: 28px;
	}


	/* =========================================================
	   IDENTIDAD
	   ========================================================= */

	.brand {

		display: flex;

		align-items: center;

		gap: 13px;

		flex-shrink: 0;
	}


	.brand-icon {

		width: 43px;

		height: 43px;

		border-radius: 11px;

		background: #eaf2ff;

		color: #0d6efd;

		display: flex;

		align-items: center;

		justify-content: center;

		font-size: 19px;

		flex-shrink: 0;
	}


	.brand-text h1 {

		font-size: 17px;

		font-weight: 700;

		color: #212529;

		margin: 0 0 2px;

		letter-spacing: -0.2px;
	}


	.brand-text span {

		font-size: 12px;

		color: #868e96;
	}


	/* =========================================================
	   BÚSQUEDA
	   ========================================================= */

	.search-wrapper {

		flex: 1;

		display: flex;

		justify-content: center;

		min-width: 180px;
	}


	.search-box {

		width: 100%;

		max-width: 390px;

		height: 40px;

		display: flex;

		align-items: center;

		padding: 0 12px;

		background: #f8f9fb;

		border:
			1px solid #e9edf2;

		border-radius: 11px;

		transition:
			background-color 0.2s ease,
			border-color 0.2s ease,
			box-shadow 0.2s ease;
	}


	.search-box:focus-within {

		background: #ffffff;

		border-color: #b9d1f5;

		box-shadow:
			0 0 0 3px
			rgba(
				13,
				110,
				253,
				0.07
			);
	}


	.search-icon {

		color: #98a2b3;

		font-size: 14px;

		line-height: 1;

		margin-right: 9px;
	}


	.search-box input {

		flex: 1;

		min-width: 0;

		border: none;

		outline: none;

		background: transparent;

		color: #343a40;

		font-size: 13px;
	}


	.search-box input::placeholder {

		color: #adb5bd;
	}


	.clear-search {

		width: 24px;

		height: 24px;

		display: flex;

		align-items: center;

		justify-content: center;

		border: none;

		background: transparent;

		color: #98a2b3;

		border-radius: 6px;

		font-size: 11px;

		cursor: pointer;

		padding: 0;

		transition:
			background-color 0.2s ease,
			color 0.2s ease;
	}


	.clear-search:hover {

		background: #eef1f5;

		color: #495057;
	}


	/* =========================================================
	   ACCIONES DERECHA
	   ========================================================= */

	.header-actions {

		display: flex;

		align-items: center;

		gap: 13px;

		flex-shrink: 0;
	}


	/* =========================================================
	   NOTIFICACIONES
	   ========================================================= */

	.notifications-wrapper {

		position: relative;
	}


	.notification-button {

		position: relative;

		width: 38px;

		height: 38px;

		border:
			1px solid transparent;

		border-radius: 10px;

		background: transparent;

		display: flex;

		align-items: center;

		justify-content: center;

		cursor: pointer;

		transition:
			background-color 0.2s ease,
			box-shadow 0.2s ease,
			border-color 0.2s ease;
	}


	.notification-button:hover,
	.notification-button.active {

		background: #f5f8ff;

		border-color: #e8eef8;

		box-shadow:
			0 4px 12px
			rgba(
				13,
				110,
				253,
				0.08
			);
	}


	.notification-icon {

		color: #6c757d;

		font-size: 17px;

		line-height: 1;
	}


	.notification-badge {

		position: absolute;

		top: 2px;

		right: 1px;

		min-width: 16px;

		height: 16px;

		padding: 0 4px;

		border-radius: 20px;

		background: #dc3545;

		color: #ffffff;

		display: flex;

		align-items: center;

		justify-content: center;

		font-size: 9px;

		font-weight: 700;

		border: 2px solid #ffffff;
	}


	/* =========================================================
	   MENU NOTIFICACIONES
	   ========================================================= */

	.notifications-menu {

		position: absolute;

		top: calc(100% + 10px);

		right: -8px;

		width: 335px;

		background: #ffffff;

		border:
			1px solid #e7eaee;

		border-radius: 14px;

		box-shadow:
			0 14px 35px
			rgba(
				0,
				0,
				0,
				0.11
			);

		z-index: 1200;

		overflow: hidden;

		animation:
			menuAppear
			0.15s ease-out;
	}


	.notifications-menu::before {

		content: '';

		position: absolute;

		top: -6px;

		right: 20px;

		width: 11px;

		height: 11px;

		background: #ffffff;

		border-left:
			1px solid #e7eaee;

		border-top:
			1px solid #e7eaee;

		transform:
			rotate(45deg);
	}


	@keyframes menuAppear {

		from {

			opacity: 0;

			transform:
				translateY(-5px);
		}


		to {

			opacity: 1;

			transform:
				translateY(0);
		}

	}


	.notifications-header {

		display: flex;

		align-items: center;

		justify-content: space-between;

		gap: 10px;

		padding:
			13px 14px 11px;

		border-bottom:
			1px solid #edf0f2;
	}


	.notifications-header > div {

		display: flex;

		flex-direction: column;

		gap: 2px;
	}


	.notifications-header strong {

		color: #343a40;

		font-size: 13px;

		font-weight: 700;
	}


	.notifications-header span {

		color: #adb5bd;

		font-size: 10px;
	}


	.mark-all {

		border: none;

		background: transparent;

		color: #0d6efd;

		font-size: 10px;

		font-weight: 500;

		cursor: pointer;

		padding: 4px 5px;
	}


	.mark-all:hover {

		text-decoration: underline;
	}


	.notifications-list {

		max-height: 300px;

		overflow-y: auto;
	}


	.notification-item {

		display: flex;

		gap: 10px;

		padding:
			12px 14px;

		border-bottom:
			1px solid #f1f3f5;

		transition:
			background-color 0.2s ease;
	}


	.notification-item:hover {

		background: #fafbfc;
	}


	.notification-item.unread {

		background: #f8fbff;
	}


	.notification-item-icon {

		width: 34px;

		height: 34px;

		border-radius: 9px;

		background: #eef5ff;

		color: #0d6efd;

		display: flex;

		align-items: center;

		justify-content: center;

		font-size: 14px;

		flex-shrink: 0;
	}


	.notification-content {

		min-width: 0;

		flex: 1;
	}


	.notification-title-row {

		display: flex;

		align-items: center;

		gap: 5px;
	}


	.notification-title-row strong {

		color: #343a40;

		font-size: 11px;

		font-weight: 600;
	}


	.unread-dot {

		width: 5px;

		height: 5px;

		background: #0d6efd;

		border-radius: 50%;

		flex-shrink: 0;
	}


	.notification-content p {

		margin:
			3px 0 6px;

		color: #868e96;

		font-size: 10px;

		line-height: 1.45;
	}


	.notification-bottom {

		display: flex;

		align-items: center;

		justify-content: space-between;

		gap: 8px;
	}


	.notification-time {

		color: #adb5bd;

		font-size: 9px;
	}


	.read-button {

		border: none;

		background: transparent;

		color: #0d6efd;

		font-size: 9px;

		padding: 0;

		cursor: pointer;
	}


	.read-button:hover {

		text-decoration: underline;
	}


	.empty-notifications {

		padding:
			28px 15px;

		display: flex;

		align-items: center;

		flex-direction: column;

		text-align: center;
	}


	.empty-icon {

		width: 40px;

		height: 40px;

		border-radius: 50%;

		background: #f7f9fc;

		color: #adb5bd;

		display: flex;

		align-items: center;

		justify-content: center;

		font-size: 15px;

		margin-bottom: 8px;
	}


	.empty-notifications strong {

		font-size: 11px;

		color: #495057;
	}


	.empty-notifications span {

		font-size: 10px;

		color: #adb5bd;

		margin-top: 3px;
	}


	.notifications-footer {

		padding:
			10px 14px;

		border-top:
			1px solid #edf0f2;

		text-align: center;
	}


	.notifications-footer a {

		color: #0d6efd;

		font-size: 10px;

		font-weight: 500;

		text-decoration: none;
	}


	.notifications-footer a:hover {

		text-decoration: underline;
	}


	.notifications-footer a span {

		margin-left: 4px;
	}


	/* =========================================================
	   DIVISOR
	   ========================================================= */

	.header-divider {

		width: 1px;

		height: 28px;

		background: #e9ecef;
	}


	/* =========================================================
	   USUARIO
	   ========================================================= */

	.user-area {

		display: flex;

		align-items: center;

		gap: 11px;
	}


	.user-info {

		display: flex;

		flex-direction: column;

		align-items: flex-end;

		gap: 2px;
	}


	.user-info strong {

		font-size: 13px;

		font-weight: 600;

		color: #343a40;
	}


	.user-info span {

		font-size: 11px;

		color: #868e96;
	}


	.status-dot {

		display: inline-block;

		width: 6px;

		height: 6px;

		background: #198754;

		border-radius: 50%;

		margin-right: 4px;
	}


	/* =========================================================
	   PERFIL
	   ========================================================= */

	.profile-wrapper {

		position: relative;
	}


	.user-avatar {

		width: 38px;

		height: 38px;

		border-radius: 50%;

		background: #0d6efd;

		color: #ffffff;

		display: flex;

		align-items: center;

		justify-content: center;

		font-size: 12px;

		font-weight: 600;

		border: 2px solid transparent;

		cursor: pointer;

		padding: 0;

		transition:
			background-color 0.2s ease,
			box-shadow 0.2s ease;
	}


	.user-avatar:hover,
	.user-avatar.active {

		background: #0b5ed7;

		box-shadow:
			0 0 0 4px #eaf2ff;
	}


	.profile-menu {

		position: absolute;

		top: calc(100% + 10px);

		right: 0;

		width: 275px;

		background: #ffffff;

		border:
			1px solid #e9ecef;

		border-radius: 13px;

		box-shadow:
			0 12px 30px
			rgba(
				0,
				0,
				0,
				0.10
			);

		padding: 10px;

		z-index: 1100;

		animation:
			menuAppear
			0.15s ease-out;
	}


	.profile-menu::before {

		content: '';

		position: absolute;

		top: -6px;

		right: 13px;

		width: 11px;

		height: 11px;

		background: #ffffff;

		border-left:
			1px solid #e9ecef;

		border-top:
			1px solid #e9ecef;

		transform:
			rotate(45deg);
	}


	.profile-header {

		display: flex;

		align-items: center;

		gap: 10px;

		padding:
			5px 5px 9px;
	}


	.profile-avatar {

		width: 36px;

		height: 36px;

		border-radius: 50%;

		background: #eaf2ff;

		color: #0d6efd;

		display: flex;

		align-items: center;

		justify-content: center;

		font-size: 11px;

		font-weight: 700;

		flex-shrink: 0;
	}


	.profile-name {

		display: flex;

		flex-direction: column;

		min-width: 0;
	}


	.profile-name strong {

		font-size: 13px;

		font-weight: 600;

		color: #212529;
	}


	.profile-name span {

		font-size: 10px;

		color: #868e96;

		margin-top: 1px;
	}


	.menu-divider {

		height: 1px;

		background: #edf0f2;

		margin: 5px 0;
	}


	.profile-item {

		display: flex;

		align-items: center;

		gap: 10px;

		padding:
			8px 5px;
	}


	.item-icon {

		width: 30px;

		height: 30px;

		border-radius: 8px;

		background: #f7f9fc;

		color: #6c757d;

		display: flex;

		align-items: center;

		justify-content: center;

		font-size: 13px;

		flex-shrink: 0;
	}


	.status-icon {

		color: #198754;

		font-size: 9px;
	}


	.item-content {

		display: flex;

		flex-direction: column;

		min-width: 0;
	}


	.item-content small {

		font-size: 10px;

		color: #868e96;

		margin-bottom: 1px;
	}


	.item-content strong {

		font-size: 11px;

		font-weight: 600;

		color: #343a40;

		white-space: nowrap;

		overflow: hidden;

		text-overflow: ellipsis;

		max-width: 205px;
	}


	.profile-logout {

		display: flex;

		align-items: center;

		gap: 8px;

		padding:
			8px 9px;

		border-radius: 8px;

		color: #6c757d;

		text-decoration: none;

		font-size: 12px;

		font-weight: 500;

		transition:
			background-color 0.2s ease,
			color 0.2s ease;
	}


	.profile-logout i {

		font-size: 15px;
	}


	.profile-logout:hover {

		background: #fff7f7;

		color: #dc3545;
	}


	/* =========================================================
	   TABLET
	   ========================================================= */

	@media (max-width: 1000px) {

		.header-content {

			gap: 16px;
		}


		.search-box {

			max-width: 300px;
		}


		.user-info {

			display: none;
		}

	}


	/* =========================================================
	   CELULAR
	   ========================================================= */

	@media (max-width: 700px) {

		.header-content {

			min-height: 68px;

			gap: 10px;
		}


		.search-wrapper {

			display: none;
		}


		.brand-text h1 {

			font-size: 15px;
		}


		.brand-text span {

			font-size: 11px;
		}


		.header-actions {

			margin-left: auto;

			gap: 8px;
		}


		.header-divider {

			height: 25px;
		}


		.notifications-menu {

			right: -45px;

			width: 300px;
		}


		.notifications-menu::before {

			right: 55px;
		}


		.profile-menu {

			right: -5px;

			width: 260px;
		}

	}

</style>