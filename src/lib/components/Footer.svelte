<script>
	let whatsappAbierto = $state(false);


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


		if (
			!elemento.closest(
				'.whatsapp-wrapper'
			)
		) {

			cerrarWhatsapp();

		}
	}
</script>


<svelte:window
	onclick={cerrarAlHacerClickFuera}
/>


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


				<!-- =================================================
				     CORREO
				     ================================================= -->

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

						<span
							class="contact-icon whatsapp-icon"
						>

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
							     No redirige
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
				     Ya no es un enlace
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


<style>

	/* =========================================================
	   FOOTER
	   ========================================================= */

	.school-footer {

		background: #ffffff;

		border-top:
			1px solid #e9ecef;

		color: #6c757d;
	}


	.footer-container {

		width: 100%;

		padding:
			34px 40px 18px;
	}


	/* =========================================================
	   CONTENIDO
	   ========================================================= */

	.footer-content {

		display: grid;

		grid-template-columns:
			1.2fr 1fr 1fr;

		gap: 50px;

		max-width: 1200px;

		margin: 0 auto;
	}


	.footer-section {

		min-width: 0;
	}


	/* =========================================================
	   IDENTIDAD
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

		font-size: 12px;
	}


	/* =========================================================
	   TÍTULOS
	   ========================================================= */

	.footer-section h4 {

		margin:
			0 0 14px;

		color: #343a40;

		font-size: 13px;

		font-weight: 600;
	}


	/* =========================================================
	   CONTACTO
	   ========================================================= */

	.contact-item {

		display: flex;

		align-items: flex-start;

		gap: 9px;

		width: fit-content;

		margin-bottom: 9px;

		color: #868e96;

		font-size: 12px;

		line-height: 1.5;

		border-radius: 8px;

		transition:
			background-color 0.2s ease,
			color 0.2s ease,
			box-shadow 0.2s ease;
	}


	.contact-icon {

		width: 18px;

		color: #0d6efd;

		font-size: 13px;

		text-align: center;

		flex-shrink: 0;
	}


	/* =========================================================
	   WHATSAPP
	   ========================================================= */

	.whatsapp-wrapper {

		position: relative;
	}


	.contact-button {

		border: none;

		background: transparent;

		padding:
			5px 8px 5px 5px;

		cursor: pointer;

		font-family: inherit;

		text-align: left;
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


	.whatsapp-icon i {

		font-size: 13px;
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
	   BOTÓN WHATSAPP
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
	   PARTE INFERIOR
	   ========================================================= */

	.footer-bottom {

		max-width: 1200px;

		margin:
			28px auto 0;

		padding-top: 16px;

		border-top:
			1px solid #edf0f2;

		display: flex;

		align-items: center;

		justify-content: space-between;

		gap: 15px;

		color: #adb5bd;

		font-size: 11px;
	}


	/* =========================================================
	   ENLACES INFERIORES
	   ========================================================= */

	.footer-links {

		display: flex;

		align-items: center;

		gap: 8px;

		color: #868e96;
	}


	/* =========================================================
	   TABLET
	   ========================================================= */

	@media (max-width: 800px) {

		.footer-container {

			padding:
				30px 25px 18px;
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
	   CELULAR
	   ========================================================= */

	@media (max-width: 576px) {

		.footer-container {

			padding:
				28px 20px 18px;
		}


		.footer-content {

			grid-template-columns:
				1fr;

			gap: 24px;
		}


		.brand-section {

			grid-column: auto;
		}


		.footer-bottom {

			margin-top: 24px;

			flex-direction: column;

			text-align: center;

			gap: 8px;
		}


		.whatsapp-card {

			left: auto;

			right: -5px;

			width: 265px;
		}


		.whatsapp-card::after {

			left: auto;

			right: 18px;
		}

	}

</style>