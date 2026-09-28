<script>
	let correo = $state('');
	let contrasena = $state('');
	let mostrarContrasena = $state(false);
	let recordar = $state(false);
	let mensaje = $state('');

	let whatsappAbierto = $state(false);


	// =========================================================
	// LOGIN
	// =========================================================

	function iniciarSesion() {
		mensaje = '';
		window.location.href = '/dashboard';
	}


	// =========================================================
	// WHATSAPP
	// =========================================================

	function alternarWhatsapp() {
		whatsappAbierto = !whatsappAbierto;
	}


	function cerrarWhatsapp() {
		whatsappAbierto = false;
	}


	function cerrarAlHacerClickFuera(event) {

		const elemento = event.target;

		if (!elemento.closest('.whatsapp-wrapper')) {
			cerrarWhatsapp();
		}
	}
</script>


<svelte:window onclick={cerrarAlHacerClickFuera} />


<svelte:head>

	<title>
		Iniciar sesión | Colegio San Miguel
	</title>

	<meta
		name="description"
		content="Acceso al sistema de gestión de eventos escolares del Colegio San Miguel"
	/>

</svelte:head>


<div class="login-page">


	<!-- =====================================================
	     CONTENIDO PRINCIPAL
	     ===================================================== -->

	<main class="login-main">

		<div class="login-content">


			<!-- =================================================
			     IDENTIDAD
			     ================================================= -->

			<div class="institution">

				<div class="institution-logo">

					<i class="bi bi-building"></i>

				</div>


				<h1>
					Colegio San Miguel
				</h1>


				<p>
					Gestión de Eventos Escolares
				</p>

			</div>


			<!-- =================================================
			     TARJETA LOGIN
			     ================================================= -->

			<section class="login-card">

				<div class="login-heading">

					<h2>
						Bienvenido
					</h2>


					<p>
						Ingresa tus datos para continuar
					</p>

				</div>


				<!-- =================================================
				     MENSAJE
				     ================================================= -->

				{#if mensaje}

					<div
						class="alert-message"
						role="alert"
					>

						<span class="alert-icon">

							<i class="bi bi-exclamation-lg"></i>

						</span>


						<span>
							{mensaje}
						</span>

					</div>

				{/if}


				<!-- =================================================
				     FORMULARIO
				     ================================================= -->

				<form
					onsubmit={(event) => {

						event.preventDefault();

						iniciarSesion();

					}}
				>


					<!-- =================================================
					     CORREO
					     ================================================= -->

					<div class="form-group">

						<label for="correo">
							Correo electrónico
						</label>


						<div class="input-wrapper">

							<span class="input-icon">

								<i class="bi bi-envelope"></i>

							</span>


							<input
								id="correo"
								type="email"
								bind:value={correo}
								placeholder="Ingresa tu correo"
								autocomplete="email"
								aria-label="Correo electrónico"
							/>

						</div>

					</div>


					<!-- =================================================
					     CONTRASEÑA
					     ================================================= -->

					<div class="form-group">

						<div class="label-row">

							<label for="contrasena">
								Contraseña
							</label>

						</div>


						<div class="input-wrapper">

							<span class="input-icon">

								<i class="bi bi-lock"></i>

							</span>


							<input
								id="contrasena"
								type={
									mostrarContrasena
										? 'text'
										: 'password'
								}
								bind:value={contrasena}
								placeholder="Ingresa tu contraseña"
								autocomplete="current-password"
								aria-label="Contraseña"
							/>


							<button
								type="button"
								class="password-toggle"
								aria-label={
									mostrarContrasena
										? 'Ocultar contraseña'
										: 'Mostrar contraseña'
								}
								onclick={() =>
									mostrarContrasena =
										!mostrarContrasena
								}
							>

								<i
									class={`bi ${
										mostrarContrasena
											? 'bi-eye-slash'
											: 'bi-eye'
									}`}
								></i>

							</button>

						</div>

					</div>


					<!-- =================================================
					     OPCIONES
					     ================================================= -->

					<div class="login-options">

						<label class="remember-option">

							<input
								type="checkbox"
								bind:checked={recordar}
							/>


							<span>
								Recordarme
							</span>

						</label>


						<button
							type="button"
							class="forgot-button"
							onclick={() =>
								mensaje =
									'La recuperación de contraseña estará disponible próximamente.'
							}
						>
							¿Olvidaste tu contraseña?
						</button>

					</div>


					<!-- =================================================
					     BOTÓN LOGIN
					     ================================================= -->

					<button
						type="submit"
						class="login-button"
					>

						<span>
							Iniciar sesión
						</span>


						<span class="button-arrow">

							<i class="bi bi-arrow-right"></i>

						</span>

					</button>

				</form>


				<!-- =================================================
				     INFORMACIÓN
				     ================================================= -->

				<div class="login-info">

					<span class="info-icon">

						<i class="bi bi-shield-lock"></i>

					</span>


					<span>
						Acceso seguro al sistema institucional
					</span>

				</div>

			</section>

		</div>

	</main>


	<!-- =====================================================
	     FOOTER
	     ===================================================== -->

	<footer class="school-footer">

		<div class="footer-container">

			<div class="footer-content">


				<!-- =================================================
				     IDENTIDAD
				     ================================================= -->

				<div class="footer-section brand-section">

					<div class="footer-brand">

						<div class="footer-logo">

							<i class="bi bi-building"></i>

						</div>


						<div>

							<h3>
								Colegio San Miguel
							</h3>


							<p>
								Gestión de Eventos Escolares
							</p>

						</div>

					</div>

				</div>


				<!-- =================================================
				     CONTACTO
				     ================================================= -->

				<div class="footer-section">

					<h4>
						Contacto
					</h4>


					<!-- CORREO
					     Solo texto
					-->

					<div class="contact-item">

						<span class="contact-icon">

							<i class="bi bi-envelope"></i>

						</span>


						<span>
							contacto@colegiosanmiguel.edu.co
						</span>

					</div>


					<!-- =================================================
					     WHATSAPP
					     ================================================= -->

					<div class="whatsapp-wrapper">

						<button
							type="button"
							class="contact-item contact-button"
							class:contact-active={
								whatsappAbierto
							}
							onclick={
								alternarWhatsapp
							}
							aria-label="Abrir información de WhatsApp"
							aria-expanded={
								whatsappAbierto
							}
						>

							<span class="contact-icon">

								<i class="bi bi-whatsapp"></i>

							</span>


							<span>
								+57 300 000 0000
							</span>

						</button>


						<!-- =================================================
						     VENTANA WHATSAPP
						     ================================================= -->

						{#if whatsappAbierto}

							<div
								class="whatsapp-card"
								role="dialog"
								aria-label="Información de WhatsApp"
							>


								<!-- CABECERA -->

								<div class="whatsapp-header">

									<div class="whatsapp-school-icon">

										<i class="bi bi-building"></i>

									</div>


									<div class="whatsapp-title">

										<strong>
											Colegio San Miguel
										</strong>


										<span>

											<i class="bi bi-patch-check-fill"></i>

											Cuenta de empresa

										</span>

									</div>

								</div>


								<!-- INFORMACIÓN -->

								<div class="whatsapp-info">

									<div class="whatsapp-status">

										<span class="online-dot"></span>


										<span>
											Disponible para consultas
										</span>

									</div>


									<p>

										Comunícate con nuestra institución
										a través de WhatsApp.

									</p>

								</div>


								<!-- =================================================
								     BOTÓN VISUAL
								     NO REDIRIGE
								     ================================================= -->

								<button
									type="button"
									class="whatsapp-button"
									onclick={cerrarWhatsapp}
								>

									<i class="bi bi-whatsapp"></i>


									<span>
										Enviar mensaje
									</span>

								</button>

							</div>

						{/if}

					</div>

				</div>


				<!-- =================================================
				     INSTITUCIÓN
				     ================================================= -->

				<div class="footer-section">

					<h4>
						Institución
					</h4>


					<!-- =================================================
					     UBICACIÓN
					     SOLO TEXTO
					     ================================================= -->

					<div class="contact-item">

						<span class="contact-icon">

							<i class="bi bi-geo-alt"></i>

						</span>


						<span>
							Barranquilla, Atlántico
						</span>

					</div>


					<!-- =================================================
					     HORARIO
					     ================================================= -->

					<div class="contact-item">

						<span class="contact-icon">

							<i class="bi bi-clock"></i>

						</span>


						<span>
							Lunes a viernes · 7:00 a. m. - 4:00 p. m.
						</span>

					</div>

				</div>

			</div>


			<!-- =====================================================
			     PARTE INFERIOR
			     ===================================================== -->

			<div class="footer-bottom">

				<span>
					© 2026 Colegio San Miguel
				</span>


				<div class="footer-links">

					<span>
						Privacidad
					</span>


					<span>
						·
					</span>


					<span>
						Términos
					</span>

				</div>


				<span>
					Versión 1.0
				</span>

			</div>

		</div>

	</footer>

</div>


<style>

	/* =========================================================
	   PÁGINA COMPLETA
	   ========================================================= */

	.login-page {

		min-height: 100vh;

		width: 100%;

		display: flex;

		flex-direction: column;

		background:
			linear-gradient(
				135deg,
				#f8fbff 0%,
				#ffffff 48%,
				#f5f9ff 100%
			);
	}


	/* =========================================================
	   ÁREA PRINCIPAL
	   ========================================================= */

	.login-main {

		flex: 1;

		width: 100%;

		display: flex;

		align-items: center;

		justify-content: center;

		padding:
			45px 20px 40px;
	}


	.login-content {

		width: 100%;

		max-width: 430px;

		display: flex;

		flex-direction: column;

		align-items: center;
	}


	/* =========================================================
	   INSTITUCIÓN
	   ========================================================= */

	.institution {

		display: flex;

		flex-direction: column;

		align-items: center;

		text-align: center;

		margin-bottom: 25px;
	}


	.institution-logo {

		width: 58px;

		height: 58px;

		display: flex;

		align-items: center;

		justify-content: center;

		background: #eaf2ff;

		border:
			1px solid #dce9fb;

		border-radius: 15px;

		color: #0d6efd;

		font-size: 25px;

		margin-bottom: 12px;

		box-shadow:
			0 7px 20px
			rgba(
				13,
				110,
				253,
				0.08
			);
	}


	.institution h1 {

		margin: 0;

		color: #212529;

		font-size: 22px;

		font-weight: 700;

		letter-spacing:
			-0.3px;
	}


	.institution p {

		margin:
			5px 0 0;

		color: #868e96;

		font-size: 12px;
	}


	/* =========================================================
	   LOGIN CARD
	   ========================================================= */

	.login-card {

		width: 100%;

		background: #ffffff;

		border:
			1px solid #e8edf3;

		border-radius: 17px;

		padding: 30px;

		box-shadow:
			0 12px 35px
			rgba(
				28,
				55,
				90,
				0.07
			),

			0 2px 7px
			rgba(
				28,
				55,
				90,
				0.03
			);
	}


	.login-heading {

		margin-bottom: 24px;
	}


	.login-heading h2 {

		margin:
			0 0 5px;

		color: #212529;

		font-size: 20px;

		font-weight: 650;
	}


	.login-heading p {

		margin: 0;

		color: #868e96;

		font-size: 12px;
	}


	/* =========================================================
	   ALERTA
	   ========================================================= */

	.alert-message {

		display: flex;

		align-items: center;

		gap: 9px;

		padding:
			10px 12px;

		margin-bottom: 18px;

		border:
			1px solid #f1d3d6;

		border-radius: 9px;

		background: #fff7f8;

		color: #842029;

		font-size: 11px;
	}


	.alert-icon {

		width: 19px;

		height: 19px;

		display: flex;

		align-items: center;

		justify-content: center;

		border-radius: 50%;

		background: #dc3545;

		color: #ffffff;

		font-size: 11px;

		flex-shrink: 0;
	}


	/* =========================================================
	   FORMULARIO
	   ========================================================= */

	.form-group {

		margin-bottom: 18px;
	}


	.form-group label {

		display: block;

		margin-bottom: 7px;

		color: #495057;

		font-size: 12px;

		font-weight: 600;
	}


	.label-row {

		display: flex;

		align-items: center;

		justify-content: space-between;
	}


	/* =========================================================
	   INPUTS
	   ========================================================= */

	.input-wrapper {

		position: relative;

		display: flex;

		align-items: center;

		height: 44px;

		background: #ffffff;

		border:
			1px solid #dfe4ea;

		border-radius: 10px;

		transition:
			border-color 0.2s ease,
			box-shadow 0.2s ease;
	}


	.input-wrapper:focus-within {

		border-color: #86b7fe;

		box-shadow:
			0 0 0 3px
			rgba(
				13,
				110,
				253,
				0.08
			);
	}


	.input-icon {

		width: 42px;

		display: flex;

		align-items: center;

		justify-content: center;

		color: #8c98a5;

		font-size: 14px;

		flex-shrink: 0;
	}


	.input-wrapper input {

		flex: 1;

		width: 100%;

		height: 100%;

		border: none;

		outline: none;

		background: transparent;

		padding:
			0 10px 0 0;

		color: #343a40;

		font-size: 12px;
	}


	.input-wrapper input::placeholder {

		color: #adb5bd;
	}


	.password-toggle {

		width: 38px;

		height: 100%;

		border: none;

		background: transparent;

		color: #8c98a5;

		display: flex;

		align-items: center;

		justify-content: center;

		cursor: pointer;

		font-size: 14px;

		padding: 0;

		flex-shrink: 0;
	}


	.password-toggle:hover {

		color: #0d6efd;
	}


	/* =========================================================
	   OPCIONES
	   ========================================================= */

	.login-options {

		display: flex;

		align-items: center;

		justify-content: space-between;

		gap: 10px;

		margin:
			4px 0 20px;
	}


	.remember-option {

		display: flex;

		align-items: center;

		gap: 7px;

		margin: 0;

		color: #6c757d;

		font-size: 11px;

		cursor: pointer;
	}


	.remember-option input {

		width: 14px;

		height: 14px;

		margin: 0;

		accent-color: #0d6efd;

		cursor: pointer;
	}


	.forgot-button {

		border: none;

		background: transparent;

		padding: 0;

		color: #0d6efd;

		font-size: 10px;

		cursor: pointer;
	}


	.forgot-button:hover {

		color: #0a58ca;

		text-decoration: underline;
	}


	/* =========================================================
	   BOTÓN LOGIN
	   ========================================================= */

	.login-button {

		width: 100%;

		height: 44px;

		border: none;

		border-radius: 10px;

		background: #0d6efd;

		color: #ffffff;

		display: flex;

		align-items: center;

		justify-content: center;

		gap: 8px;

		font-size: 12px;

		font-weight: 600;

		cursor: pointer;

		box-shadow:
			0 6px 15px
			rgba(
				13,
				110,
				253,
				0.16
			);

		transition:
			background-color 0.2s ease,
			box-shadow 0.2s ease,
			transform 0.2s ease;
	}


	.login-button:hover {

		background: #0b5ed7;

		box-shadow:
			0 8px 20px
			rgba(
				13,
				110,
				253,
				0.20
			);

		transform:
			translateY(-1px);
	}


	.login-button:active {

		transform:
			translateY(0);
	}


	.button-arrow {

		font-size: 15px;

		line-height: 1;
	}


	/* =========================================================
	   INFORMACIÓN
	   ========================================================= */

	.login-info {

		display: flex;

		align-items: center;

		justify-content: center;

		gap: 6px;

		margin-top: 20px;

		color: #adb5bd;

		font-size: 10px;

		text-align: center;
	}


	/* =========================================================
	   FOOTER
	   ========================================================= */

	.school-footer {

		width: 100%;

		flex-shrink: 0;

		background: #ffffff;

		border-top:
			1px solid #e9ecef;

		color: #6c757d;
	}


	.footer-container {

		width: 100%;

		padding:
			30px 40px 17px;
	}


	.footer-content {

		width: 100%;

		max-width: 1200px;

		margin:
			0 auto;

		display: grid;

		grid-template-columns:
			1.2fr 1fr 1fr;

		gap: 45px;
	}


	.footer-section {

		min-width: 0;
	}


	/* =========================================================
	   IDENTIDAD FOOTER
	   ========================================================= */

	.footer-brand {

		display: flex;

		align-items: center;

		gap: 13px;
	}


	.footer-logo {

		width: 43px;

		height: 43px;

		display: flex;

		align-items: center;

		justify-content: center;

		border-radius: 11px;

		background: #eaf2ff;

		color: #0d6efd;

		font-size: 19px;

		flex-shrink: 0;
	}


	.footer-brand h3 {

		margin:
			0 0 3px;

		color: #343a40;

		font-size: 15px;

		font-weight: 700;
	}


	.footer-brand p {

		margin: 0;

		color: #868e96;

		font-size: 11px;
	}


	/* =========================================================
	   TÍTULOS FOOTER
	   ========================================================= */

	.footer-section h4 {

		margin:
			0 0 13px;

		color: #343a40;

		font-size: 12px;

		font-weight: 600;
	}


	/* =========================================================
	   CONTACTO
	   ========================================================= */

	.contact-item {

		display: flex;

		align-items: flex-start;

		gap: 8px;

		width: fit-content;

		margin-bottom: 8px;

		color: #868e96;

		font-size: 10px;

		line-height: 1.5;

		border-radius: 7px;
	}


	.contact-icon {

		width: 17px;

		color: #0d6efd;

		font-size: 12px;

		text-align: center;

		flex-shrink: 0;
	}


	/* =========================================================
	   WHATSAPP BUTTON
	   ========================================================= */

	.contact-button {

		border: none;

		background: transparent;

		padding:
			4px 6px 4px 4px;

		cursor: pointer;

		font-family: inherit;

		text-align: left;

		border-radius: 7px;

		transition:
			background-color 0.2s ease,
			color 0.2s ease,
			box-shadow 0.2s ease;
	}


	.contact-button:hover {

		background: #f5f8ff;

		color: #0d6efd;

		box-shadow:
			0 4px 12px
			rgba(
				13,
				110,
				253,
				0.08
			);
	}


	.contact-button.contact-active {

		background: #eef5ff;

		color: #0d6efd;

		box-shadow:
			0 4px 12px
			rgba(
				13,
				110,
				253,
				0.10
			);
	}


	/* =========================================================
	   CONTENEDOR WHATSAPP
	   ========================================================= */

	.whatsapp-wrapper {

		position: relative;
	}


	/* =========================================================
	   VENTANA WHATSAPP
	   ========================================================= */

	.whatsapp-card {

		position: absolute;

		left: 0;

		bottom:
			calc(100% + 9px);

		width: 275px;

		background: #ffffff;

		border:
			1px solid #e5e7eb;

		border-radius: 13px;

		box-shadow:
			0 12px 30px
			rgba(
				0,
				0,
				0,
				0.12
			);

		padding: 12px;

		z-index: 1200;

		animation:
			whatsappAppear
			0.16s ease-out;
	}


	.whatsapp-card::after {

		content: '';

		position: absolute;

		left: 18px;

		bottom: -6px;

		width: 11px;

		height: 11px;

		background: #ffffff;

		border-right:
			1px solid #e5e7eb;

		border-bottom:
			1px solid #e5e7eb;

		transform:
			rotate(45deg);
	}


	@keyframes whatsappAppear {

		from {

			opacity: 0;

			transform:
				translateY(5px);
		}


		to {

			opacity: 1;

			transform:
				translateY(0);
		}

	}


	/* =========================================================
	   CABECERA WHATSAPP
	   ========================================================= */

	.whatsapp-header {

		display: flex;

		align-items: center;

		gap: 10px;

		padding:
			3px 2px 10px;
	}


	.whatsapp-school-icon {

		width: 38px;

		height: 38px;

		display: flex;

		align-items: center;

		justify-content: center;

		border-radius: 50%;

		background: #eaf2ff;

		color: #0d6efd;

		font-size: 16px;

		flex-shrink: 0;
	}


	.whatsapp-title {

		display: flex;

		flex-direction: column;

		min-width: 0;
	}


	.whatsapp-title strong {

		color: #343a40;

		font-size: 12px;

		font-weight: 700;
	}


	.whatsapp-title span {

		display: flex;

		align-items: center;

		gap: 4px;

		margin-top: 2px;

		color: #198754;

		font-size: 10px;

		font-weight: 500;
	}


	.whatsapp-title span i {

		font-size: 9px;
	}


	/* =========================================================
	   INFORMACIÓN WHATSAPP
	   ========================================================= */

	.whatsapp-info {

		padding:
			9px 2px;

		border-top:
			1px solid #edf0f2;

		border-bottom:
			1px solid #edf0f2;
	}


	.whatsapp-status {

		display: flex;

		align-items: center;

		gap: 6px;

		margin-bottom: 6px;

		color: #495057;

		font-size: 10px;

		font-weight: 500;
	}


	.online-dot {

		width: 6px;

		height: 6px;

		background: #198754;

		border-radius: 50%;
	}


	.whatsapp-info p {

		margin: 0;

		color: #868e96;

		font-size: 10px;

		line-height: 1.5;
	}


	/* =========================================================
	   BOTÓN VISUAL WHATSAPP
	   ========================================================= */

	.whatsapp-button {

		width: 100%;

		display: flex;

		align-items: center;

		justify-content: center;

		gap: 7px;

		margin-top: 10px;

		padding:
			8px 12px;

		border: none;

		border-radius: 8px;

		background: #198754;

		color: #ffffff;

		font-family: inherit;

		font-size: 11px;

		font-weight: 600;

		cursor: pointer;

		transition:
			background-color 0.2s ease,
			box-shadow 0.2s ease;
	}


	.whatsapp-button:hover {

		background: #157347;

		box-shadow:
			0 4px 12px
			rgba(
				25,
				135,
				84,
				0.20
			);
	}


	.whatsapp-button i {

		font-size: 13px;
	}


	/* =========================================================
	   FOOTER INFERIOR
	   ========================================================= */

	.footer-bottom {

		width: 100%;

		max-width: 1200px;

		margin:
			20px auto 0;

		padding-top: 13px;

		border-top:
			1px solid #edf0f2;

		display: flex;

		align-items: center;

		justify-content: space-between;

		gap: 15px;

		color: #adb5bd;

		font-size: 9px;
	}


	.footer-links {

		display: flex;

		align-items: center;

		gap: 7px;

		color: #868e96;
	}


	/* =========================================================
	   TABLET
	   ========================================================= */

	@media (max-width: 800px) {

		.footer-container {

			padding:
				28px 25px 16px;
		}


		.footer-content {

			grid-template-columns:
				1fr 1fr;

			gap: 30px;
		}


		.brand-section {

			grid-column:
				1 / -1;
		}

	}


	/* =========================================================
	   MÓVIL
	   ========================================================= */

	@media (max-width: 576px) {

		.login-main {

			padding:
				30px 15px 25px;
		}


		.login-card {

			padding:
				25px 21px;
		}


		.institution {

			margin-bottom: 21px;
		}


		.institution-logo {

			width: 52px;

			height: 52px;

			font-size: 23px;
		}


		.institution h1 {

			font-size: 20px;
		}


		.login-heading h2 {

			font-size: 19px;
		}


		.login-options {

			align-items:
				flex-start;

			flex-direction:
				column;

			gap: 9px;
		}


		.forgot-button {

			align-self:
				flex-end;
		}


		.footer-container {

			padding:
				25px 18px 15px;
		}


		.footer-content {

			grid-template-columns: 1fr;

			gap: 21px;
		}


		.brand-section {

			grid-column: auto;
		}


		.footer-bottom {

			flex-direction:
				column;

			text-align: center;

			gap: 7px;
		}


		.whatsapp-card {

			left: auto;

			right: -5px;

			width: 255px;
		}


		.whatsapp-card::after {

			left: auto;

			right: 18px;
		}

	}


	/* =========================================================
	   CELULAR PEQUEÑO
	   ========================================================= */

	@media (max-width: 380px) {

		.login-main {

			padding:
				25px 12px;
		}


		.login-card {

			padding:
				22px 17px;
		}


		.footer-container {

			padding:
				22px 15px 14px;
		}

	}

</style>