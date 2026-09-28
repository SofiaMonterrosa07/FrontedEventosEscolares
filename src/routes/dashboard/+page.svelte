<svelte:head>
	<title>Dashboard | Eventos Escolares</title>
</svelte:head>


<div class="container-fluid py-4 px-4">

	<!-- =====================================================
	     ENCABEZADO
	     ===================================================== -->

	<div
		class="d-flex flex-column flex-md-row justify-content-between align-items-md-center mb-4"
	>

		<div>

			<h1 class="fw-semibold mb-1">
				Dashboard
			</h1>

			<p class="text-muted mb-0">
				Resumen general del sistema de eventos escolares.
			</p>

		</div>


		<div class="mt-3 mt-md-0">

			<span
				class="badge rounded-pill bg-primary-subtle text-primary px-3 py-2"
			>
				<i class="bi bi-calendar3"></i>
				Septiembre 2026
			</span>

		</div>

	</div>


	<!-- =====================================================
	     INDICADORES
	     ===================================================== -->

	<div class="row g-4 mb-4">

		<!-- ACTIVIDADES -->

		<div class="col-12 col-md-6 col-xl-3">

			<div class="card border-0 shadow-sm h-100 soft-card">

				<div class="card-body p-4">

					<div
						class="d-flex justify-content-between align-items-start"
					>

						<div>

							<p class="text-muted small mb-2">
								Actividades
							</p>

							<h2 class="fw-semibold mb-1">
								20
							</h2>

							<small class="text-muted">
								Actividades registradas
							</small>

						</div>


						<div
							class="icon-soft bg-primary-subtle text-primary"
						>
							<i class="bi bi-calendar-event"></i>
						</div>

					</div>

				</div>

			</div>

		</div>


		<!-- INSCRIPCIONES -->

		<div class="col-12 col-md-6 col-xl-3">

			<div class="card border-0 shadow-sm h-100 soft-card">

				<div class="card-body p-4">

					<div
						class="d-flex justify-content-between align-items-start"
					>

						<div>

							<p class="text-muted small mb-2">
								Inscripciones
							</p>

							<h2 class="fw-semibold mb-1">
								86
							</h2>

							<small class="text-muted">
								Registros realizados
							</small>

						</div>


						<div
							class="icon-soft bg-success-subtle text-success"
						>
							<i class="bi bi-journal-check"></i>
						</div>

					</div>

				</div>

			</div>

		</div>


		<!-- ESTUDIANTES -->

		<div class="col-12 col-md-6 col-xl-3">

			<div class="card border-0 shadow-sm h-100 soft-card">

				<div class="card-body p-4">

					<div
						class="d-flex justify-content-between align-items-start"
					>

						<div>

							<p class="text-muted small mb-2">
								Estudiantes
							</p>

							<h2 class="fw-semibold mb-1">
								240
							</h2>

							<small class="text-muted">
								Estudiantes registrados
							</small>

						</div>


						<div
							class="icon-soft bg-info-subtle text-info"
						>
							<i class="bi bi-mortarboard"></i>
						</div>

					</div>

				</div>

			</div>

		</div>


		<!-- PENDIENTES -->

		<div class="col-12 col-md-6 col-xl-3">

			<div class="card border-0 shadow-sm h-100 soft-card">

				<div class="card-body p-4">

					<div
						class="d-flex justify-content-between align-items-start"
					>

						<div>

							<p class="text-muted small mb-2">
								Pendientes
							</p>

							<h2 class="fw-semibold mb-1">
								18
							</h2>

							<small class="text-muted">
								Requieren atención
							</small>

						</div>


						<div
							class="icon-soft bg-warning-subtle text-warning-emphasis"
						>
							<i class="bi bi-exclamation-triangle"></i>
						</div>

					</div>

				</div>

			</div>

		</div>

	</div>


	<!-- =====================================================
	     ACCIONES RÁPIDAS
	     ===================================================== -->

	<div class="card border-0 shadow-sm soft-card mb-4">

		<div class="card-body p-4">

			<div class="mb-3">

				<h5 class="fw-semibold mb-1">
					Acciones rápidas
				</h5>

				<small class="text-muted">
					Accede a las funciones principales del sistema
				</small>

			</div>


			<div class="row g-3">

				<!-- ACTIVIDADES -->

				<div class="col-12 col-md-6 col-lg-3">

					<a
						href="/actividades"
						class="quick-action"
					>

						<div
							class="quick-icon bg-primary-subtle text-primary"
						>
							<i class="bi bi-calendar-event"></i>
						</div>


						<div>

							<span class="fw-semibold d-block">
								Actividades
							</span>

							<small class="text-muted">
								Gestionar actividades
							</small>

						</div>

					</a>

				</div>


				<!-- INSCRIPCIONES -->

				<div class="col-12 col-md-6 col-lg-3">

					<a
						href="/inscripciones"
						class="quick-action"
					>

						<div
							class="quick-icon bg-success-subtle text-success"
						>
							<i class="bi bi-journal-check"></i>
						</div>


						<div>

							<span class="fw-semibold d-block">
								Inscripciones
							</span>

							<small class="text-muted">
								Consultar inscripciones
							</small>

						</div>

					</a>

				</div>


				<!-- AUTORIZACIONES -->

				<div class="col-12 col-md-6 col-lg-3">

					<a
						href="/autorizaciones"
						class="quick-action"
					>

						<div
							class="quick-icon bg-warning-subtle text-warning-emphasis"
						>
							<i class="bi bi-file-earmark-check"></i>
						</div>


						<div>

							<span class="fw-semibold d-block">
								Autorizaciones
							</span>

							<small class="text-muted">
								Revisar solicitudes
							</small>

						</div>

					</a>

				</div>


				<!-- REPORTES -->

				<div class="col-12 col-md-6 col-lg-3">

					<a
						href="/reportes"
						class="quick-action"
					>

						<div
							class="quick-icon bg-info-subtle text-info"
						>
							<i class="bi bi-bar-chart"></i>
						</div>


						<div>

							<span class="fw-semibold d-block">
								Reportes
							</span>

							<small class="text-muted">
								Consultar estadísticas
							</small>

						</div>

					</a>

				</div>

			</div>

		</div>

	</div>


	<!-- =====================================================
	     CONTENIDO INFERIOR
	     ===================================================== -->

	<div class="row g-4">

		<!-- =================================================
		     ACTIVIDADES PRÓXIMAS
		     ================================================= -->

		<div class="col-lg-8">

			<div class="card border-0 shadow-sm soft-card h-100">

				<div class="card-header bg-white border-0 p-4">

					<div
						class="d-flex justify-content-between align-items-center"
					>

						<div>

							<h5 class="fw-semibold mb-1">
								Actividades próximas
							</h5>

							<small class="text-muted">
								Eventos programados próximamente
							</small>

						</div>


						<a
							href="/actividades"
							class="btn btn-sm btn-outline-primary rounded-pill px-3"
						>
							Ver todas
						</a>

					</div>

				</div>


				<div class="card-body px-4 pt-0">

					<div class="table-responsive">

						<table class="table table-hover align-middle mb-0">

							<thead>

								<tr>

									<th class="border-0 text-muted small">
										Actividad
									</th>

									<th class="border-0 text-muted small">
										Fecha
									</th>

									<th class="border-0 text-muted small">
										Lugar
									</th>

									<th class="border-0 text-muted small">
										Cupo
									</th>

									<th class="border-0 text-muted small">
										Estado
									</th>

								</tr>

							</thead>


							<tbody>

								<!-- BALONCESTO -->

								<tr>

									<td>

										<div class="activity-name">

											<div class="dashboard-activity-icon">
												<i class="bi bi-dribbble"></i>
											</div>

											<div>

												<div class="fw-semibold">
													Baloncesto
												</div>

												<small class="text-muted">
													Actividad deportiva
												</small>

											</div>

										</div>

									</td>


									<td>
										20/09/2026
									</td>


									<td>
										Cancha principal
									</td>


									<td>
										20
									</td>


									<td>

										<span
											class="badge rounded-pill bg-success-subtle text-success"
										>
											Disponible
										</span>

									</td>

								</tr>


								<!-- ROBÓTICA -->

								<tr>

									<td>

										<div class="activity-name">

											<div class="dashboard-activity-icon">
												<i class="bi bi-robot"></i>
											</div>

											<div>

												<div class="fw-semibold">
													Robótica
												</div>

												<small class="text-muted">
													Actividad académica
												</small>

											</div>

										</div>

									</td>


									<td>
										22/09/2026
									</td>


									<td>
										Aula 3
									</td>


									<td>
										15
									</td>


									<td>

										<span
											class="badge rounded-pill bg-warning-subtle text-warning-emphasis"
										>
											Pocos cupos
										</span>

									</td>

								</tr>


								<!-- TEATRO -->

								<tr>

									<td>

										<div class="activity-name">

											<div class="dashboard-activity-icon">
												<i class="bi bi-mask"></i>
											</div>

											<div>

												<div class="fw-semibold">
													Teatro
												</div>

												<small class="text-muted">
													Actividad cultural
												</small>

											</div>

										</div>

									</td>


									<td>
										25/09/2026
									</td>


									<td>
										Auditorio
									</td>


									<td>
										30
									</td>


									<td>

										<span
											class="badge rounded-pill bg-success-subtle text-success"
										>
											Disponible
										</span>

									</td>

								</tr>

							</tbody>

						</table>

					</div>

				</div>

			</div>

		</div>


		<!-- =================================================
		     ESTADO DE ACTIVIDADES
		     ================================================= -->

		<div class="col-lg-4">

			<div class="card border-0 shadow-sm soft-card h-100">

				<div class="card-header bg-white border-0 p-4">

					<h5 class="fw-semibold mb-1">
						Estado de actividades
					</h5>

					<small class="text-muted">
						Distribución actual
					</small>

				</div>


				<div class="card-body px-4 pt-0">

					<!-- PRÓXIMAS -->

					<div class="activity-status-row mb-4">

						<div
							class="d-flex justify-content-between align-items-center mb-2"
						>

							<div class="status-label">

								<span class="status-dot upcoming"></span>

								<span class="small">
									Próximas
								</span>

							</div>


							<strong>
								12
							</strong>

						</div>


						<div class="progress">

							<div
								class="progress-bar"
								style="width: 60%"
							></div>

						</div>

					</div>


					<!-- EN CURSO -->

					<div class="activity-status-row mb-4">

						<div
							class="d-flex justify-content-between align-items-center mb-2"
						>

							<div class="status-label">

								<span class="status-dot ongoing"></span>

								<span class="small">
									En curso
								</span>

							</div>


							<strong>
								4
							</strong>

						</div>


						<div class="progress">

							<div
								class="progress-bar bg-success"
								style="width: 20%"
							></div>

						</div>

					</div>


					<!-- FINALIZADAS -->

					<div class="activity-status-row mb-4">

						<div
							class="d-flex justify-content-between align-items-center mb-2"
						>

							<div class="status-label">

								<span class="status-dot finished"></span>

								<span class="small">
									Finalizadas
								</span>

							</div>


							<strong>
								4
							</strong>

						</div>


						<div class="progress">

							<div
								class="progress-bar bg-secondary"
								style="width: 20%"
							></div>

						</div>

					</div>


					<hr class="my-4" />


					<div class="text-center">

						<p class="text-muted small mb-1">
							Total de actividades
						</p>

						<h3 class="fw-semibold mb-0">
							20
						</h3>

					</div>

				</div>

			</div>

		</div>

	</div>

</div>


<style>

	/* =========================================================
	   TARJETAS GENERALES
	   ========================================================= */

	.soft-card {
		border-radius: 14px;
	}


	.icon-soft {
		width: 46px;
		height: 46px;
		border-radius: 12px;
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 18px;
	}


	/* =========================================================
	   FECHA DEL ENCABEZADO
	   ========================================================= */

	.badge i {
		margin-right: 5px;
		font-size: 11px;
	}


	/* =========================================================
	   ACCIONES RÁPIDAS
	   ========================================================= */

	.quick-action {
		display: flex;
		align-items: center;
		gap: 12px;
		padding: 14px;
		border: 1px solid #edf0f2;
		border-radius: 12px;
		text-decoration: none;
		color: #212529;
		background: #ffffff;
		transition:
			background-color 0.2s ease,
			border-color 0.2s ease,
			transform 0.2s ease,
			box-shadow 0.2s ease;
	}


	.quick-action:hover {
		border-color: #cfe2ff;
		background: #f8fbff;
		transform: translateY(-1px);
		box-shadow:
			0 5px 15px rgba(0, 0, 0, 0.04);
	}


	.quick-icon {
		width: 40px;
		height: 40px;
		border-radius: 10px;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-shrink: 0;
		font-size: 16px;
	}


	/* =========================================================
	   TABLA
	   ========================================================= */

	.table th {
		font-weight: 500;
	}


	.table td {
		font-size: 13px;
	}


	.activity-name {
		display: flex;
		align-items: center;
		gap: 10px;
		min-width: 180px;
	}


	.dashboard-activity-icon {
		width: 36px;
		height: 36px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 9px;
		background: #f4f7fb;
		color: #0d6efd;
		font-size: 15px;
		flex-shrink: 0;
	}


	.activity-name small {
		font-size: 10px;
	}


	/* =========================================================
	   ESTADOS
	   ========================================================= */

	.progress {
		height: 7px;
		border-radius: 10px;
		background-color: #edf0f2;
		overflow: hidden;
	}


	.progress-bar {
		border-radius: 10px;
	}


	.status-label {
		display: flex;
		align-items: center;
		gap: 7px;
	}


	.status-dot {
		width: 8px;
		height: 8px;
		display: inline-block;
		border-radius: 50%;
		flex-shrink: 0;
	}


	.status-dot.upcoming {
		background: #0d6efd;
	}


	.status-dot.ongoing {
		background: #198754;
	}


	.status-dot.finished {
		background: #6c757d;
	}


	.activity-status-row strong {
		font-size: 12px;
		color: #343a40;
	}


	/* =========================================================
	   TARJETAS
	   ========================================================= */

	.card {
		overflow: hidden;
	}


	/* =========================================================
	   RESPONSIVE
	   ========================================================= */

	@media (max-width: 768px) {

		.container-fluid {
			padding-left: 15px !important;
			padding-right: 15px !important;
		}

	}


</style>