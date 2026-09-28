<script>
	let periodo = $state('Septiembre 2026');
	let tipoActividad = $state('Todas');
	let mostrarReporte = $state(false);


	// =========================================================
	// DATOS ESTÁTICOS
	// =========================================================

	let actividades = $state([
		{
			nombre: 'Baloncesto',
			tipo: 'Deportiva',
			icono: 'bi-dribbble',
			cupos: 30,
			inscritos: 24,
			autorizadas: 20,
			pendientes: 3,
			rechazadas: 1
		},
		{
			nombre: 'Robótica',
			tipo: 'Académica',
			icono: 'bi-robot',
			cupos: 25,
			inscritos: 19,
			autorizadas: 16,
			pendientes: 2,
			rechazadas: 1
		},
		{
			nombre: 'Teatro',
			tipo: 'Artística',
			icono: 'bi-mask',
			cupos: 20,
			inscritos: 15,
			autorizadas: 12,
			pendientes: 2,
			rechazadas: 1
		},
		{
			nombre: 'Natación',
			tipo: 'Deportiva',
			icono: 'bi-water',
			cupos: 20,
			inscritos: 14,
			autorizadas: 12,
			pendientes: 1,
			rechazadas: 1
		},
		{
			nombre: 'Ajedrez',
			tipo: 'Académica',
			icono: 'bi-grid-3x3-gap',
			cupos: 15,
			inscritos: 8,
			autorizadas: 6,
			pendientes: 2,
			rechazadas: 0
		},
		{
			nombre: 'Danza',
			tipo: 'Artística',
			icono: 'bi-music-note-beamed',
			cupos: 25,
			inscritos: 6,
			autorizadas: 5,
			pendientes: 1,
			rechazadas: 0
		}
	]);


	// =========================================================
	// FILTROS
	// =========================================================

	let actividadesFiltradas = $derived(
		tipoActividad === 'Todas'
			? actividades
			: actividades.filter(
					(actividad) =>
						actividad.tipo === tipoActividad
				)
	);


	// =========================================================
	// TOTALES
	// =========================================================

	let totalActividades = $derived(
		actividadesFiltradas.length
	);


	let totalInscritos = $derived(
		actividadesFiltradas.reduce(
			(total, actividad) =>
				total + actividad.inscritos,
			0
		)
	);


	let totalAutorizadas = $derived(
		actividadesFiltradas.reduce(
			(total, actividad) =>
				total + actividad.autorizadas,
			0
		)
	);


	let totalPendientes = $derived(
		actividadesFiltradas.reduce(
			(total, actividad) =>
				total + actividad.pendientes,
			0
		)
	);


	let totalRechazadas = $derived(
		actividadesFiltradas.reduce(
			(total, actividad) =>
				total + actividad.rechazadas,
			0
		)
	);


	let totalCupos = $derived(
		actividadesFiltradas.reduce(
			(total, actividad) =>
				total + actividad.cupos,
			0
		)
	);


	let cuposDisponibles = $derived(
		totalCupos - totalInscritos
	);


	let porcentajeAutorizacion = $derived(
		totalInscritos > 0
			? Math.round(
					(totalAutorizadas / totalInscritos) * 100
				)
			: 0
	);


	let actividadMasPopular = $derived(
		actividadesFiltradas.length > 0
			? actividadesFiltradas.reduce(
					(anterior, actual) =>
						actual.inscritos >
						anterior.inscritos
							? actual
							: anterior
				)
			: null
	);


	// =========================================================
	// FUNCIONES
	// =========================================================

	function porcentajeOcupacion(actividad) {

		if (actividad.cupos === 0) {
			return 0;
		}

		return Math.round(
			(actividad.inscritos / actividad.cupos) * 100
		);
	}


	function claseBarra(porcentaje) {

		if (porcentaje >= 85) {
			return 'bar-high';
		}

		if (porcentaje >= 60) {
			return 'bar-medium';
		}

		return 'bar-low';
	}


	function abrirReporte() {
		mostrarReporte = true;
	}


	function cerrarReporte() {
		mostrarReporte = false;
	}
</script>


<svelte:head>
	<title>Reportes | Colegio San Miguel</title>
</svelte:head>


<div class="container-fluid px-4 py-4">

	<!-- =====================================================
	     ENCABEZADO
	     ===================================================== -->

	<div class="page-header">

		<div>

			<h2>
				Reportes
			</h2>

			<p>
				Consulta el comportamiento de las actividades
				y las inscripciones.
			</p>

		</div>


		<button
			class="btn btn-primary report-button"
			onclick={abrirReporte}
		>
			<i class="bi bi-file-earmark-bar-graph"></i>
			Generar reporte
		</button>

	</div>


	<!-- =====================================================
	     FILTROS
	     ===================================================== -->

	<div class="soft-card filters-card">

		<div class="filters-title">

			<div>

				<h3>
					Filtros
				</h3>

				<span>
					Consulta la información según tus necesidades.
				</span>

			</div>

		</div>


		<div class="filters">

			<div class="filter-item">

				<label for="periodo">
					Período
				</label>


				<select
					id="periodo"
					class="form-select"
					bind:value={periodo}
				>

					<option>
						Septiembre 2026
					</option>

					<option>
						Agosto 2026
					</option>

					<option>
						Julio 2026
					</option>

					<option>
						Junio 2026
					</option>

				</select>

			</div>


			<div class="filter-item">

				<label for="tipoActividad">
					Tipo de actividad
				</label>


				<select
					id="tipoActividad"
					class="form-select"
					bind:value={tipoActividad}
				>

					<option value="Todas">
						Todas las actividades
					</option>

					<option value="Deportiva">
						Deportivas
					</option>

					<option value="Académica">
						Académicas
					</option>

					<option value="Artística">
						Artísticas
					</option>

				</select>

			</div>

		</div>

	</div>


	<!-- =====================================================
	     INDICADORES
	     ===================================================== -->

	<div class="row g-3 mb-4">

		<!-- ACTIVIDADES -->

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


					<small>
						registradas
					</small>

				</div>

			</div>

		</div>


		<!-- INSCRIPCIONES -->

		<div class="col-md-6 col-xl-3">

			<div class="soft-card indicator-card">

				<div class="icon-soft purple">
					<i class="bi bi-people"></i>
				</div>


				<div>

					<span class="indicator-label">
						Inscripciones
					</span>


					<strong>
						{totalInscritos}
					</strong>


					<small>
						estudiantes
					</small>

				</div>

			</div>

		</div>


		<!-- AUTORIZADAS -->

		<div class="col-md-6 col-xl-3">

			<div class="soft-card indicator-card">

				<div class="icon-soft green">
					<i class="bi bi-check-circle"></i>
				</div>


				<div>

					<span class="indicator-label">
						Autorizadas
					</span>


					<strong>
						{totalAutorizadas}
					</strong>


					<small>
						{porcentajeAutorizacion}% del total
					</small>

				</div>

			</div>

		</div>


		<!-- PENDIENTES -->

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
						{totalPendientes}
					</strong>


					<small>
						por revisar
					</small>

				</div>

			</div>

		</div>

	</div>


	<!-- =====================================================
	     RESUMEN SUPERIOR
	     ===================================================== -->

	<div class="row g-3 mb-4">

		<!-- GRÁFICO DE INSCRIPCIONES -->

		<div class="col-xl-8">

			<div class="soft-card chart-card">

				<div class="card-heading">

					<div>

						<h3>
							Inscripciones por actividad
						</h3>

						<span>
							Distribución de estudiantes inscritos
						</span>

					</div>


					<span class="period-badge">
						{periodo}
					</span>

				</div>


				<div class="chart-area">

					{#each actividadesFiltradas as actividad}

						<div class="chart-row">

							<div class="chart-label">

								<div class="activity-name">

									<i
										class={`bi ${actividad.icono}`}
									></i>

									<span>
										{actividad.nombre}
									</span>

								</div>


								<strong>
									{actividad.inscritos}
								</strong>

							</div>


							<div class="chart-track">

								<div
									class={`chart-bar ${claseBarra(
										porcentajeOcupacion(
											actividad
										)
									)}`}
									style={`width: ${Math.max(
										porcentajeOcupacion(
											actividad
										),
										4
									)}%`}
								></div>

							</div>


							<span class="chart-percent">
								{porcentajeOcupacion(actividad)}%
							</span>

						</div>

					{/each}

				</div>

			</div>

		</div>


		<!-- ESTADO DE AUTORIZACIONES -->

		<div class="col-xl-4">

			<div class="soft-card distribution-card">

				<div class="card-heading">

					<div>

						<h3>
							Estado de autorizaciones
						</h3>

						<span>
							Distribución actual
						</span>

					</div>

				</div>


				<div class="donut-wrapper">

					<div
						class="donut"
						style={`--approved: ${
							totalInscritos > 0
								? (totalAutorizadas /
										totalInscritos) *
									100
								: 0
						}%; --pending: ${
							totalInscritos > 0
								? (totalPendientes /
										totalInscritos) *
									100
								: 0
						}%`}
					>

						<div class="donut-center">

							<strong>
								{porcentajeAutorizacion}%
							</strong>

							<span>
								aprobadas
							</span>

						</div>

					</div>

				</div>


				<div class="legend">

					<div class="legend-item">

						<span
							class="legend-color approved"
						></span>


						<div>

							<strong>
								Aprobadas
							</strong>

							<span>
								{totalAutorizadas}
							</span>

						</div>

					</div>


					<div class="legend-item">

						<span
							class="legend-color pending"
						></span>


						<div>

							<strong>
								Pendientes
							</strong>

							<span>
								{totalPendientes}
							</span>

						</div>

					</div>


					<div class="legend-item">

						<span
							class="legend-color rejected"
						></span>


						<div>

							<strong>
								Rechazadas
							</strong>

							<span>
								{totalRechazadas}
							</span>

						</div>

					</div>

				</div>

			</div>

		</div>

	</div>


	<!-- =====================================================
	     RESUMEN DESTACADO
	     ===================================================== -->

	<div class="row g-3 mb-4">

		<!-- MÁS POPULAR -->

		<div class="col-md-6">

			<div class="soft-card highlight-card">

				<div class="highlight-icon">

					<i class="bi bi-trophy"></i>

				</div>


				<div class="highlight-content">

					<span>
						Actividad con mayor participación
					</span>


					{#if actividadMasPopular}

						<strong>
							{actividadMasPopular.nombre}
						</strong>


						<p>
							{actividadMasPopular.inscritos}
							estudiantes inscritos de
							{actividadMasPopular.cupos}
							cupos disponibles.
						</p>

					{:else}

						<strong>
							Sin información
						</strong>

					{/if}

				</div>

			</div>

		</div>


		<!-- CUPOS DISPONIBLES -->

		<div class="col-md-6">

			<div class="soft-card highlight-card">

				<div class="highlight-icon available">

					<i class="bi bi-ui-checks-grid"></i>

				</div>


				<div class="highlight-content">

					<span>
						Cupos disponibles
					</span>


					<strong>
						{cuposDisponibles}
					</strong>


					<p>
						Cupos libres entre las actividades
						seleccionadas.
					</p>

				</div>

			</div>

		</div>

	</div>


	<!-- =====================================================
	     TABLA
	     ===================================================== -->

	<div class="soft-card table-card">

		<div class="table-header">

			<div>

				<h3>
					Detalle por actividad
				</h3>


				<span>
					Información de participación y autorizaciones
				</span>

			</div>


			<span class="results-count">
				{actividadesFiltradas.length} actividades
			</span>

		</div>


		<div class="table-responsive">

			<table class="table align-middle">

				<thead>

					<tr>

						<th>
							Actividad
						</th>

						<th>
							Tipo
						</th>

						<th>
							Cupos
						</th>

						<th>
							Inscritos
						</th>

						<th>
							Ocupación
						</th>

						<th>
							Autorizaciones
						</th>

					</tr>

				</thead>


				<tbody>

					{#if actividadesFiltradas.length > 0}

						{#each actividadesFiltradas as actividad}

							<tr>

								<!-- ACTIVIDAD -->

								<td>

									<div class="activity-cell">

										<div class="activity-icon">

											<i
												class={`bi ${actividad.icono}`}
											></i>

										</div>


										<strong>
											{actividad.nombre}
										</strong>

									</div>

								</td>


								<!-- TIPO -->

								<td>

									<span class="type-badge">
										{actividad.tipo}
									</span>

								</td>


								<!-- CUPOS -->

								<td>

									<span class="number-text">
										{actividad.cupos}
									</span>

								</td>


								<!-- INSCRITOS -->

								<td>

									<strong class="number-strong">
										{actividad.inscritos}
									</strong>

								</td>


								<!-- OCUPACIÓN -->

								<td>

									<div class="occupancy">

										<div class="occupancy-top">

											<span>
												{porcentajeOcupacion(
													actividad
												)}%
											</span>

										</div>


										<div class="progress">

											<div
												class={`progress-bar ${claseBarra(
													porcentajeOcupacion(
														actividad
													)
												)}`}
												style={`width: ${porcentajeOcupacion(
													actividad
												)}%`}
											></div>

										</div>

									</div>

								</td>


								<!-- AUTORIZACIONES -->

								<td>

									<div class="authorization-summary">

										<span class="approved-number">
											{actividad.autorizadas}
										</span>


										<span>
											/
										</span>


										<span>
											{actividad.inscritos}
										</span>


										{#if actividad.pendientes > 0}

											<small>
												{actividad.pendientes}
												pendientes
											</small>

										{/if}

									</div>

								</td>

							</tr>

						{/each}

					{:else}

						<tr>

							<td colspan="6">

								<div class="empty-state">

									<div class="empty-icon">

										<i class="bi bi-search"></i>

									</div>


									<strong>
										No hay datos para mostrar
									</strong>


									<span>
										Cambia el tipo de actividad
										para consultar otros resultados.
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
     MODAL REPORTE
     ========================================================= -->

{#if mostrarReporte}

	<div
		class="modal-backdrop-custom"
		role="presentation"
		onclick={(event) => {

			if (
				event.target ===
				event.currentTarget
			) {
				cerrarReporte();
			}

		}}
	>

		<div
			class="report-modal"
			role="dialog"
			aria-modal="true"
			aria-labelledby="report-title"
		>

			<!-- CABECERA -->

			<div class="modal-header-custom">

				<div>

					<span class="modal-label">
						Reporte generado
					</span>


					<h3 id="report-title">
						Resumen de actividades
					</h3>


					<p>
						{periodo}
					</p>

				</div>


				<button
					class="close-button"
					type="button"
					onclick={cerrarReporte}
					aria-label="Cerrar"
				>
					<i class="bi bi-x-lg"></i>
				</button>

			</div>


			<!-- CUERPO -->

			<div class="report-body">

				<div class="report-summary">

					<div class="report-summary-item">

						<span>
							Actividades
						</span>

						<strong>
							{totalActividades}
						</strong>

					</div>


					<div class="report-summary-item">

						<span>
							Inscripciones
						</span>

						<strong>
							{totalInscritos}
						</strong>

					</div>


					<div class="report-summary-item">

						<span>
							Autorizadas
						</span>

						<strong>
							{totalAutorizadas}
						</strong>

					</div>


					<div class="report-summary-item">

						<span>
							Pendientes
						</span>

						<strong>
							{totalPendientes}
						</strong>

					</div>

				</div>


				<div class="report-message">

					<div class="report-message-icon">
						<i class="bi bi-check-lg"></i>
					</div>


					<div>

						<strong>
							Reporte listo para consulta
						</strong>


						<p>
							La información mostrada corresponde
							a los filtros seleccionados y puede
							ser revisada antes de exportarla.
						</p>

					</div>

				</div>


				<div class="report-detail">

					<div>

						<span>
							Período
						</span>


						<strong>
							{periodo}
						</strong>

					</div>


					<div>

						<span>
							Tipo de actividad
						</span>


						<strong>
							{tipoActividad === 'Todas'
								? 'Todas'
								: tipoActividad}
						</strong>

					</div>


					<div>

						<span>
							Cupos disponibles
						</span>


						<strong>
							{cuposDisponibles}
						</strong>

					</div>


					<div>

						<span>
							Actividades analizadas
						</span>


						<strong>
							{totalActividades}
						</strong>

					</div>

				</div>

			</div>


			<!-- PIE -->

			<div class="modal-footer-custom">

				<button
					class="btn btn-light cancel-button"
					onclick={cerrarReporte}
				>
					Cerrar
				</button>


				<button
					class="btn btn-primary save-button"
					onclick={cerrarReporte}
				>
					<i class="bi bi-check2"></i>
					Confirmar reporte
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


	.report-button {
		height: 42px;
		padding: 0 17px;
		border-radius: 9px;
		font-size: 13px;
		font-weight: 600;
	}


	.report-button i {
		margin-right: 6px;
	}


	/* =========================================================
	   TARJETA GENERAL
	   ========================================================= */

	.soft-card {
		background: #ffffff;
		border: 1px solid #edf0f2;
		border-radius: 13px;
		box-shadow:
			0 3px 14px rgba(0, 0, 0, 0.035);
	}


	/* =========================================================
	   FILTROS
	   ========================================================= */

	.filters-card {
		padding: 19px 22px;
		margin-bottom: 18px;
	}


	.filters-title {
		margin-bottom: 15px;
	}


	.filters-title h3,
	.card-heading h3,
	.table-header h3 {
		margin: 0 0 3px;
		color: #343a40;
		font-size: 15px;
		font-weight: 650;
	}


	.filters-title span,
	.card-heading span,
	.table-header span {
		color: #adb5bd;
		font-size: 11px;
	}


	.filters {
		display: flex;
		gap: 12px;
	}


	.filter-item {
		width: 240px;
	}


	.filter-item label {
		display: block;
		margin-bottom: 7px;
		color: #495057;
		font-size: 11px;
		font-weight: 600;
	}


	.filter-item .form-select {
		height: 39px;
		border-color: #e1e5e9;
		border-radius: 8px;
		font-size: 12px;
	}


	.filter-item .form-select:focus {
		border-color: #86b7fe;
		box-shadow:
			0 0 0 0.15rem
			rgba(13, 110, 253, 0.08);
	}


	/* =========================================================
	   INDICADORES
	   ========================================================= */

	.indicator-card {
		min-height: 92px;
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


	.icon-soft.purple {
		background: #f1edff;
		color: #6f42c1;
	}


	.icon-soft.green {
		background: #e9f7ef;
		color: #198754;
	}


	.icon-soft.orange {
		background: #fff2e5;
		color: #d97706;
	}


	.indicator-label {
		display: block;
		margin-bottom: 1px;
		color: #868e96;
		font-size: 10px;
	}


	.indicator-card strong {
		display: inline-block;
		margin-right: 5px;
		color: #343a40;
		font-size: 21px;
		font-weight: 700;
	}


	.indicator-card small {
		color: #adb5bd;
		font-size: 9px;
	}


	/* =========================================================
	   GRÁFICO
	   ========================================================= */

	.chart-card,
	.distribution-card {
		min-height: 335px;
		padding: 20px;
	}


	.card-heading {
		display: flex;
		align-items: flex-start;
		justify-content: space-between;
		gap: 15px;
		margin-bottom: 27px;
	}


	.period-badge {
		padding: 5px 9px;
		border-radius: 20px;
		background: #f4f7fb;
		color: #6c757d !important;
		font-size: 9px !important;
		white-space: nowrap;
	}


	.chart-area {
		display: flex;
		flex-direction: column;
		gap: 19px;
	}


	.chart-row {
		display: grid;
		grid-template-columns: 150px 1fr 38px;
		align-items: center;
		gap: 12px;
	}


	.chart-label {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 8px;
	}


	.activity-name {
		display: flex;
		align-items: center;
		gap: 7px;
		color: #495057;
		font-size: 10px;
		font-weight: 500;
		white-space: nowrap;
	}


	.activity-name i {
		width: 16px;
		color: #0d6efd;
		font-size: 12px;
		text-align: center;
	}


	.chart-label strong {
		color: #343a40;
		font-size: 10px;
	}


	.chart-track {
		height: 9px;
		background: #f1f3f5;
		border-radius: 10px;
		overflow: hidden;
	}


	.chart-bar {
		height: 100%;
		border-radius: 10px;
		min-width: 4px;
	}


	.bar-high {
		background: #0d6efd;
	}


	.bar-medium {
		background: #6ea8fe;
	}


	.bar-low {
		background: #b9d4fb;
	}


	.chart-percent {
		color: #868e96;
		font-size: 9px;
		text-align: right;
	}


	/* =========================================================
	   DONA
	   ========================================================= */

	.donut-wrapper {
		display: flex;
		justify-content: center;
		margin-bottom: 24px;
	}


	.donut {
		position: relative;
		width: 145px;
		height: 145px;
		border-radius: 50%;

		background:
			conic-gradient(
				#198754 0 var(--approved),
				#f59e0b var(--approved)
					calc(
						var(--approved) +
						var(--pending)
					),
				#dc3545
					calc(
						var(--approved) +
						var(--pending)
					)
					100%
			);

		display: flex;
		align-items: center;
		justify-content: center;
	}


	.donut::before {
		content: '';
		position: absolute;
		width: 105px;
		height: 105px;
		background: #ffffff;
		border-radius: 50%;
	}


	.donut-center {
		position: relative;
		z-index: 1;
		display: flex;
		align-items: center;
		flex-direction: column;
	}


	.donut-center strong {
		color: #343a40;
		font-size: 24px;
		font-weight: 700;
	}


	.donut-center span {
		color: #adb5bd;
		font-size: 9px;
	}


	.legend {
		display: flex;
		flex-direction: column;
		gap: 10px;
	}


	.legend-item {
		display: flex;
		align-items: center;
		gap: 9px;
	}


	.legend-color {
		width: 8px;
		height: 8px;
		border-radius: 50%;
		flex-shrink: 0;
	}


	.legend-color.approved {
		background: #198754;
	}


	.legend-color.pending {
		background: #f59e0b;
	}


	.legend-color.rejected {
		background: #dc3545;
	}


	.legend-item div {
		flex: 1;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}


	.legend-item strong {
		color: #6c757d;
		font-size: 10px;
		font-weight: 500;
	}


	.legend-item div span {
		color: #343a40;
		font-size: 10px;
		font-weight: 600;
	}


	/* =========================================================
	   DESTACADOS
	   ========================================================= */

	.highlight-card {
		min-height: 100px;
		padding: 18px;
		display: flex;
		align-items: center;
		gap: 14px;
	}


	.highlight-icon {
		width: 44px;
		height: 44px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 11px;
		background: #fff7df;
		color: #d97706;
		font-size: 18px;
		flex-shrink: 0;
	}


	.highlight-icon.available {
		background: #eaf2ff;
		color: #0d6efd;
	}


	.highlight-content span {
		display: block;
		margin-bottom: 3px;
		color: #adb5bd;
		font-size: 10px;
	}


	.highlight-content strong {
		display: block;
		margin-bottom: 2px;
		color: #343a40;
		font-size: 14px;
		font-weight: 650;
	}


	.highlight-content p {
		margin: 0;
		color: #868e96;
		font-size: 10px;
		line-height: 1.5;
	}


	/* =========================================================
	   TABLA
	   ========================================================= */

	.table-card {
		overflow: hidden;
	}


	.table-header {
		padding: 18px 21px;
		display: flex;
		align-items: center;
		justify-content: space-between;
		border-bottom: 1px solid #edf0f2;
	}


	.results-count {
		padding: 5px 9px;
		border-radius: 20px;
		background: #f8f9fa;
		white-space: nowrap;
	}


	.table {
		margin: 0;
		font-size: 11px;
	}


	.table thead th {
		padding: 13px 16px;
		background: #fafbfc;
		border-bottom: 1px solid #edf0f2;
		color: #868e96;
		font-size: 9px;
		font-weight: 600;
		white-space: nowrap;
	}


	.table tbody td {
		padding: 13px 16px;
		border-color: #f0f2f4;
	}


	.table tbody tr:last-child td {
		border-bottom: none;
	}


	.table tbody tr:hover {
		background: #fcfdff;
	}


	.activity-cell {
		display: flex;
		align-items: center;
		gap: 9px;
		min-width: 145px;
	}


	.activity-icon {
		width: 32px;
		height: 32px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 8px;
		background: #f4f7fb;
		color: #0d6efd;
		font-size: 14px;
		flex-shrink: 0;
	}


	.activity-cell strong {
		color: #495057;
		font-size: 11px;
		font-weight: 600;
	}


	.type-badge {
		padding: 5px 8px;
		border-radius: 20px;
		background: #f8f9fa;
		color: #6c757d;
		font-size: 9px;
		white-space: nowrap;
	}


	.number-text {
		color: #6c757d;
		font-size: 10px;
	}


	.number-strong {
		color: #343a40;
		font-size: 11px;
	}


	.occupancy {
		min-width: 115px;
	}


	.occupancy-top {
		margin-bottom: 4px;
		color: #6c757d;
		font-size: 9px;
		text-align: right;
	}


	.progress {
		height: 6px;
		background: #f1f3f5;
		border-radius: 10px;
	}


	.progress-bar {
		border-radius: 10px;
	}


	.authorization-summary {
		display: flex;
		align-items: center;
		gap: 4px;
		color: #adb5bd;
		font-size: 10px;
		white-space: nowrap;
	}


	.approved-number {
		color: #198754;
		font-weight: 700;
	}


	.authorization-summary small {
		margin-left: 5px;
		padding: 3px 5px;
		border-radius: 10px;
		background: #fff2e5;
		color: #d97706;
		font-size: 8px;
	}


	/* =========================================================
	   ESTADO VACÍO
	   ========================================================= */

	.empty-state {
		min-height: 220px;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
		text-align: center;
	}


	.empty-icon {
		width: 44px;
		height: 44px;
		margin-bottom: 9px;
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
		font-size: 12px;
	}


	.empty-state span {
		color: #adb5bd;
		font-size: 10px;
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


	.report-modal {
		width: 100%;
		max-width: 540px;
		max-height: calc(100vh - 40px);
		display: flex;
		flex-direction: column;
		background: #ffffff;
		border-radius: 15px;
		overflow: hidden;
		box-shadow:
			0 18px 50px rgba(0, 0, 0, 0.15);
	}


	.modal-header-custom {
		padding: 21px 23px;
		display: flex;
		align-items: flex-start;
		justify-content: space-between;
		border-bottom: 1px solid #edf0f2;
		flex-shrink: 0;
	}


	.modal-label {
		display: block;
		margin-bottom: 3px;
		color: #0d6efd;
		font-size: 9px;
		font-weight: 600;
		text-transform: uppercase;
		letter-spacing: 0.4px;
	}


	.modal-header-custom h3 {
		margin: 0 0 3px;
		color: #343a40;
		font-size: 17px;
		font-weight: 700;
	}


	.modal-header-custom p {
		margin: 0;
		color: #adb5bd;
		font-size: 10px;
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


	.report-body {
		padding: 22px 23px;
		overflow-y: auto;
		flex: 1;
		min-height: 0;
		scrollbar-width: thin;
		scrollbar-color: #d9dee3 #f8f9fa;
	}


	.report-body::-webkit-scrollbar {
		width: 6px;
	}


	.report-body::-webkit-scrollbar-track {
		background: #f8f9fa;
	}


	.report-body::-webkit-scrollbar-thumb {
		background: #d9dee3;
		border-radius: 10px;
	}


	.report-summary {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 9px;
		margin-bottom: 18px;
	}


	.report-summary-item {
		padding: 12px;
		background: #f8f9fa;
		border-radius: 9px;
	}


	.report-summary-item span {
		display: block;
		margin-bottom: 3px;
		color: #adb5bd;
		font-size: 9px;
	}


	.report-summary-item strong {
		color: #343a40;
		font-size: 17px;
		font-weight: 700;
	}


	.report-message {
		display: flex;
		gap: 10px;
		padding: 13px;
		margin-bottom: 18px;
		background: #e9f7ef;
		border-radius: 9px;
	}


	.report-message-icon {
		width: 28px;
		height: 28px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 50%;
		background: #ffffff;
		color: #198754;
		font-size: 12px;
		font-weight: 700;
		flex-shrink: 0;
	}


	.report-message strong {
		display: block;
		margin-bottom: 3px;
		color: #198754;
		font-size: 11px;
	}


	.report-message p {
		margin: 0;
		color: #6c757d;
		font-size: 9px;
		line-height: 1.5;
	}


	.report-detail {
		display: flex;
		flex-direction: column;
		gap: 8px;
	}


	.report-detail div {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 15px;
		padding: 10px 12px;
		background: #f8f9fa;
		border-radius: 8px;
	}


	.report-detail span {
		color: #adb5bd;
		font-size: 9px;
	}


	.report-detail strong {
		color: #495057;
		font-size: 10px;
		font-weight: 600;
		text-align: right;
	}


	.modal-footer-custom {
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
	   RESPONSIVE
	   ========================================================= */

	@media (max-width: 900px) {

		.filters {
			flex-direction: column;
		}


		.filter-item {
			width: 100%;
		}

	}


	@media (max-width: 700px) {

		.page-header {
			align-items: flex-start;
			flex-direction: column;
		}


		.report-button {
			width: 100%;
		}


		.chart-row {
			grid-template-columns: 125px 1fr 35px;
		}

	}


	@media (max-width: 576px) {

		.container-fluid {
			padding-left: 15px !important;
			padding-right: 15px !important;
		}


		.chart-card,
		.distribution-card {
			padding: 17px;
		}


		.chart-row {
			grid-template-columns: 105px 1fr 32px;
			gap: 8px;
		}


		.activity-name {
			font-size: 9px;
		}


		.highlight-card {
			padding: 16px;
		}


		.modal-backdrop-custom {
			padding: 10px;
		}


		.report-modal {
			max-width: 100%;
			max-height: calc(100vh - 20px);
			border-radius: 12px;
		}


		.modal-header-custom {
			padding: 17px 18px;
		}


		.report-body {
			padding: 18px;
		}


		.modal-footer-custom {
			padding: 13px 18px;
		}


		.modal-footer-custom .cancel-button,
		.modal-footer-custom .save-button {
			flex: 1;
		}

	}


	@media (max-width: 380px) {

		.chart-row {
			grid-template-columns: 90px 1fr 30px;
		}


		.activity-name {
			font-size: 8px;
		}


		.chart-percent {
			font-size: 8px;
		}


		.report-summary {
			grid-template-columns: 1fr;
		}


		.report-detail div {
			align-items: flex-start;
			flex-direction: column;
			gap: 3px;
		}


		.report-detail strong {
			text-align: left;
		}

	}

</style>