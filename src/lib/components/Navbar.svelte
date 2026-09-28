<script>
	import { page } from '$app/state';


	let menuAbierto = $state(false);


	// =========================================================
	// RUTAS DEL SISTEMA
	// =========================================================

	let rutas = [
		{
			nombre: 'Inicio',
			ruta: '/dashboard',
			icono: 'bi-house'
		},
		{
			nombre: 'Usuarios',
			ruta: '/usuarios',
			icono: 'bi-people'
		},
		{
			nombre: 'Actividades',
			ruta: '/actividades',
			icono: 'bi-calendar-event'
		},
		{
			nombre: 'Inscripciones',
			ruta: '/inscripciones',
			icono: 'bi-pencil-square'
		},
		{
			nombre: 'Autorizaciones',
			ruta: '/autorizaciones',
			icono: 'bi-file-earmark-check'
		},
		{
			nombre: 'Reportes',
			ruta: '/reportes',
			icono: 'bi-bar-chart'
		},
		{
			nombre: 'Configuración',
			ruta: '/configuracion',
			icono: 'bi-gear'
		}
	];


	// =========================================================
	// RUTA ACTIVA
	// =========================================================

	function esRutaActiva(ruta) {

		return page.url.pathname === ruta;
	}


	// =========================================================
	// CERRAR MENÚ
	// =========================================================

	function cerrarMenu() {

		menuAbierto = false;
	}
</script>


<nav class="main-navbar">

	<div class="container-fluid px-4">

		<div class="navbar-content">


			<!-- =================================================
			     BOTÓN MÓVIL
			     ================================================= -->

			<button
				class="mobile-toggle"
				type="button"
				aria-label="Abrir menú"
				aria-expanded={menuAbierto}
				onclick={() =>
					menuAbierto = !menuAbierto
				}
			>

				<span></span>

				<span></span>

				<span></span>

			</button>


			<!-- =================================================
			     NAVEGACIÓN
			     ================================================= -->

			<div
				class:menu-open={menuAbierto}
				class="navigation"
			>

				{#each rutas as item}

					<a
						href={item.ruta}
						class:active={
							esRutaActiva(item.ruta)
						}
						class="nav-link"
						aria-current={
							esRutaActiva(item.ruta)
								? 'page'
								: undefined
						}
						onclick={cerrarMenu}
					>

						<span class="nav-icon">

							<i
								class={`bi ${item.icono}`}
							></i>

						</span>


						<span>
							{item.nombre}
						</span>

					</a>

				{/each}

			</div>

		</div>

	</div>

</nav>


<style>

	/* =========================================================
	   BARRA
	   ========================================================= */

	.main-navbar {

		background: #ffffff;

		border-bottom:
			1px solid #edf0f2;
	}


	/* =========================================================
	   CONTENEDOR
	   ========================================================= */

	.navbar-content {

		min-height: 58px;

		display: flex;

		align-items: center;

		justify-content: center;
	}


	/* =========================================================
	   NAVEGACIÓN
	   ========================================================= */

	.navigation {

		display: flex;

		align-items: center;

		justify-content: center;

		gap: 6px;
	}


	/* =========================================================
	   ENLACES
	   ========================================================= */

	.nav-link {

		position: relative;

		display: flex;

		align-items: center;

		gap: 7px;

		padding:
			9px 14px;

		border-radius: 11px;

		color: #667085;

		background: transparent;

		text-decoration: none;

		font-size: 13px;

		font-weight: 500;

		transition:
			color 0.2s ease,
			background-color 0.2s ease,
			box-shadow 0.2s ease,
			transform 0.2s ease;
	}


	/* =========================================================
	   HOVER
	   ========================================================= */

	.nav-link:hover {

		color: #0d6efd;

		background: #f8faff;

		box-shadow:
			0 4px 12px
			rgba(
				13,
				110,
				253,
				0.08
			);

		transform:
			translateY(-1px);
	}


	/* =========================================================
	   OPCIÓN ACTIVA
	   ========================================================= */

	.nav-link.active {

		color: #0d6efd;

		background: #eef5ff;

		font-weight: 600;

		box-shadow:
			0 5px 14px
			rgba(
				13,
				110,
				253,
				0.12
			),

			0 1px 3px
			rgba(
				13,
				110,
				253,
				0.08
			);
	}


	/* =========================================================
	   DETALLE INFERIOR
	   ========================================================= */

	.nav-link.active::after {

		content: '';

		position: absolute;

		left: 18px;

		right: 18px;

		bottom: 1px;

		height: 2px;

		background: #0d6efd;

		border-radius: 10px;
	}


	/* =========================================================
	   ICONOS
	   ========================================================= */

	.nav-icon {

		width: 17px;

		display: flex;

		align-items: center;

		justify-content: center;

		color: currentColor;

		font-size: 14px;

		line-height: 1;

		opacity: 0.85;
	}


	.nav-link.active
	.nav-icon {

		opacity: 1;
	}


	/* =========================================================
	   BOTÓN MÓVIL
	   ========================================================= */

	.mobile-toggle {

		display: none;

		border:
			1px solid #e9ecef;

		background: #ffffff;

		border-radius: 9px;

		width: 40px;

		height: 38px;

		padding: 8px;

		cursor: pointer;
	}


	.mobile-toggle span {

		display: block;

		height: 2px;

		background: #495057;

		border-radius: 5px;

		margin: 4px 0;
	}


	/* =========================================================
	   HOVER BOTÓN MÓVIL
	   ========================================================= */

	.mobile-toggle:hover {

		background: #f8f9fa;

		border-color: #dfe3e8;
	}


	/* =========================================================
	   TABLET
	   ========================================================= */

	@media (max-width: 1100px) {

		.navigation {

			gap: 3px;
		}


		.nav-link {

			padding-left: 10px;

			padding-right: 10px;
		}


		.nav-icon {

			display: none;
		}

	}


	/* =========================================================
	   MÓVIL
	   ========================================================= */

	@media (max-width: 900px) {

		.navbar-content {

			position: relative;

			min-height: 56px;

			justify-content:
				flex-start;
		}


		.mobile-toggle {

			display: block;
		}


		.navigation {

			display: none;

			position: absolute;

			top: 55px;

			left: 0;

			right: 0;

			z-index: 1000;

			flex-direction: column;

			align-items: stretch;

			padding: 10px;

			background: #ffffff;

			border:
				1px solid #edf0f2;

			border-radius:
				0 0 14px 14px;

			box-shadow:
				0 12px 28px
				rgba(
					0,
					0,
					0,
					0.08
				);
		}


		.navigation.menu-open {

			display: flex;
		}


		.nav-link {

			padding:
				11px 12px;
		}


		.nav-icon {

			display: flex;

			width: 18px;

			font-size: 14px;
		}


		.nav-link.active::after {

			display: none;
		}


		.nav-link.active {

			box-shadow:
				0 4px 12px
				rgba(
					13,
					110,
					253,
					0.10
				);
		}

	}


	/* =========================================================
	   TELÉFONOS
	   ========================================================= */

	@media (max-width: 576px) {

		.container-fluid {

			padding-left:
				15px !important;

			padding-right:
				15px !important;
		}

	}

</style>