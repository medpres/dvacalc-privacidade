<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prontuário Eletrônico - Demonstração MedPres</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
            background: #f0f2f5;
            min-height: 100vh;
            color: #1a1a2e;
        }

        /* Header */
        .header {
            background: linear-gradient(135deg, #1a5f7a 0%, #0d3b4c 100%);
            color: white;
            padding: 16px 24px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .header-left {
            display: flex;
            align-items: center;
            gap: 16px;
        }

        .hospital-logo {
            width: 48px;
            height: 48px;
            background: white;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
        }

        .hospital-info h1 {
            font-size: 1.25rem;
            font-weight: 600;
        }

        .hospital-info p {
            font-size: 0.85rem;
            opacity: 0.8;
        }

        .header-right {
            display: flex;
            align-items: center;
            gap: 24px;
            font-size: 0.9rem;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .user-avatar {
            width: 36px;
            height: 36px;
            background: rgba(255,255,255,0.2);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* Demo Banner */
        .demo-banner {
            background: linear-gradient(135deg, #ff6b6b 0%, #ee5a24 100%);
            color: white;
            text-align: center;
            padding: 12px;
            font-weight: 600;
            font-size: 0.95rem;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .demo-banner span {
            background: rgba(255,255,255,0.2);
            padding: 4px 12px;
            border-radius: 100px;
            font-size: 0.8rem;
        }

        /* Main Container */
        .main-container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 24px;
            display: grid;
            grid-template-columns: 320px 1fr;
            gap: 24px;
        }

        /* Sidebar - Patient Info */
        .sidebar {
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .card {
            background: white;
            border-radius: 12px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.06);
            overflow: hidden;
        }

        .card-header {
            background: #f8f9fa;
            padding: 14px 18px;
            border-bottom: 1px solid #e9ecef;
            font-weight: 600;
            font-size: 0.9rem;
            color: #495057;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .card-body {
            padding: 18px;
        }

        .patient-header {
            display: flex;
            align-items: center;
            gap: 14px;
            margin-bottom: 18px;
            padding-bottom: 18px;
            border-bottom: 1px solid #e9ecef;
        }

        .patient-avatar {
            width: 64px;
            height: 64px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.5rem;
            font-weight: 600;
        }

        .patient-name {
            font-size: 1.1rem;
            font-weight: 600;
            color: #1a1a2e;
        }

        .patient-id {
            font-size: 0.85rem;
            color: #6c757d;
            margin-top: 2px;
        }

        .patient-details {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .detail-row {
            display: flex;
            justify-content: space-between;
            font-size: 0.9rem;
        }

        .detail-label {
            color: #6c757d;
        }

        .detail-value {
            font-weight: 500;
            color: #1a1a2e;
        }

        .vital-signs {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
        }

        .vital-item {
            background: #f8f9fa;
            padding: 12px;
            border-radius: 8px;
            text-align: center;
        }

        .vital-value {
            font-size: 1.25rem;
            font-weight: 700;
            color: #1a5f7a;
        }

        .vital-label {
            font-size: 0.75rem;
            color: #6c757d;
            margin-top: 4px;
        }

        .vital-item.alert {
            background: #fff3cd;
        }

        .vital-item.alert .vital-value {
            color: #856404;
        }

        /* Main Content - SOAP */
        .main-content {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .soap-section {
            background: white;
            border-radius: 12px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.06);
            overflow: hidden;
        }

        .soap-header {
            padding: 16px 20px;
            border-bottom: 1px solid #e9ecef;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .soap-letter {
            width: 40px;
            height: 40px;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.25rem;
            font-weight: 700;
            color: white;
        }

        .soap-s .soap-letter { background: #4361ee; }
        .soap-o .soap-letter { background: #7209b7; }
        .soap-a .soap-letter { background: #f72585; }
        .soap-p .soap-letter { background: #4cc9f0; }

        .soap-title {
            font-weight: 600;
            font-size: 1rem;
            color: #1a1a2e;
        }

        .soap-subtitle {
            font-size: 0.8rem;
            color: #6c757d;
        }

        .soap-body {
            padding: 20px;
        }

        .soap-body textarea {
            width: 100%;
            min-height: 120px;
            border: 1px solid #dee2e6;
            border-radius: 8px;
            padding: 14px;
            font-family: inherit;
            font-size: 0.95rem;
            line-height: 1.6;
            resize: vertical;
            transition: border-color 0.2s, box-shadow 0.2s;
        }

        .soap-body textarea:focus {
            outline: none;
            border-color: #1a5f7a;
            box-shadow: 0 0 0 3px rgba(26, 95, 122, 0.1);
        }

        .soap-body textarea::placeholder {
            color: #adb5bd;
        }

        /* Prescription Section */
        .prescription-section {
            background: white;
            border-radius: 12px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.06);
            overflow: hidden;
            border: 2px solid #10b981;
        }

        .prescription-header {
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
            padding: 16px 20px;
            display: flex;
            align-items: center;
            gap: 12px;
            color: white;
        }

        .prescription-icon {
            width: 40px;
            height: 40px;
            background: rgba(255,255,255,0.2);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.25rem;
        }

        .prescription-title {
            font-weight: 600;
            font-size: 1rem;
        }

        .prescription-subtitle {
            font-size: 0.8rem;
            opacity: 0.9;
        }

        .prescription-body {
            padding: 20px;
        }

        .prescription-body textarea {
            width: 100%;
            min-height: 200px;
            border: 2px dashed #10b981;
            border-radius: 8px;
            padding: 14px;
            font-family: 'Courier New', monospace;
            font-size: 0.9rem;
            line-height: 1.7;
            resize: vertical;
            background: #f0fdf4;
            transition: border-color 0.2s, box-shadow 0.2s;
        }

        .prescription-body textarea:focus {
            outline: none;
            border-style: solid;
            box-shadow: 0 0 0 3px rgba(16, 185, 129, 0.1);
        }

        .prescription-body textarea::placeholder {
            color: #6ee7b7;
        }

        .prescription-hint {
            margin-top: 12px;
            padding: 12px;
            background: #ecfdf5;
            border-radius: 8px;
            font-size: 0.85rem;
            color: #065f46;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        /* Action Buttons */
        .action-buttons {
            display: flex;
            gap: 12px;
            justify-content: flex-end;
            padding: 20px;
            background: #f8f9fa;
            border-top: 1px solid #e9ecef;
        }

        .btn {
            padding: 12px 24px;
            border-radius: 8px;
            font-weight: 600;
            font-size: 0.9rem;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            gap: 8px;
            border: none;
        }

        .btn-secondary {
            background: white;
            color: #495057;
            border: 1px solid #dee2e6;
        }

        .btn-secondary:hover {
            background: #f8f9fa;
        }

        .btn-primary {
            background: linear-gradient(135deg, #1a5f7a 0%, #0d3b4c 100%);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(26, 95, 122, 0.3);
        }

        .btn-success {
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
            color: white;
        }

        .btn-success:hover {
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(16, 185, 129, 0.3);
        }

        /* Timestamp */
        .timestamp {
            text-align: center;
            padding: 16px;
            color: #6c757d;
            font-size: 0.85rem;
        }

        /* Responsive */
        @media (max-width: 1024px) {
            .main-container {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 768px) {
            .header {
                flex-direction: column;
                gap: 12px;
                text-align: center;
            }

            .header-right {
                flex-direction: column;
                gap: 8px;
            }

            .main-container {
                padding: 16px;
            }

            .vital-signs {
                grid-template-columns: repeat(4, 1fr);
            }
        }
    </style>
</head>
<body>
    <!-- Demo Banner -->
    <div class="demo-banner">
        ⚠️ AMBIENTE DE DEMONSTRAÇÃO — PACIENTE FICTÍCIO — <span>Apenas para demonstração do MedPres</span>
    </div>

    <!-- Header -->
    <header class="header">
        <div class="header-left">
            <div class="hospital-logo">🏥</div>
            <div class="hospital-info">
                <h1>UPA 24h Demonstração</h1>
                <p>Sistema de Prontuário Eletrônico</p>
            </div>
        </div>
        <div class="header-right">
            <div>📅 04/01/2026 - 14:32</div>
            <div class="user-info">
                <div class="user-avatar">👨‍⚕️</div>
                <div>
                    <div style="font-weight: 600;">Dr. Demonstração</div>
                    <div style="font-size: 0.8rem; opacity: 0.8;">CRM 00000-UF</div>
                </div>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <div class="main-container">
        <!-- Sidebar - Patient Info -->
        <aside class="sidebar">
            <!-- Patient Card -->
            <div class="card">
                <div class="card-header">
                    👤 Dados do Paciente
                </div>
                <div class="card-body">
                    <div class="patient-header">
                        <div class="patient-avatar">JF</div>
                        <div>
                            <div class="patient-name">João Fictício da Silva</div>
                            <div class="patient-id">Prontuário: #DEMO-2026-001</div>
                        </div>
                    </div>
                    <div class="patient-details">
                        <div class="detail-row">
                            <span class="detail-label">CPF:</span>
                            <span class="detail-value">000.000.000-00</span>
                        </div>
                        <div class="detail-row">
                            <span class="detail-label">Nascimento:</span>
                            <span class="detail-value">15/03/1985 (40 anos)</span>
                        </div>
                        <div class="detail-row">
                            <span class="detail-label">Sexo:</span>
                            <span class="detail-value">Masculino</span>
                        </div>
                        <div class="detail-row">
                            <span class="detail-label">Peso:</span>
                            <span class="detail-value">75 kg</span>
                        </div>
                        <div class="detail-row">
                            <span class="detail-label">Altura:</span>
                            <span class="detail-value">1,72 m</span>
                        </div>
                        <div class="detail-row">
                            <span class="detail-label">Alergias:</span>
                            <span class="detail-value" style="color: #dc3545;">Dipirona</span>
                        </div>
                        <div class="detail-row">
                            <span class="detail-label">Convênio:</span>
                            <span class="detail-value">SUS</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Vital Signs Card -->
            <div class="card">
                <div class="card-header">
                    💓 Sinais Vitais
                </div>
                <div class="card-body">
                    <div class="vital-signs">
                        <div class="vital-item alert">
                            <div class="vital-value">38.2°C</div>
                            <div class="vital-label">Temperatura</div>
                        </div>
                        <div class="vital-item">
                            <div class="vital-value">110/70</div>
                            <div class="vital-label">PA (mmHg)</div>
                        </div>
                        <div class="vital-item">
                            <div class="vital-value">88</div>
                            <div class="vital-label">FC (bpm)</div>
                        </div>
                        <div class="vital-item">
                            <div class="vital-value">18</div>
                            <div class="vital-label">FR (irpm)</div>
                        </div>
                        <div class="vital-item">
                            <div class="vital-value">97%</div>
                            <div class="vital-label">SpO2</div>
                        </div>
                        <div class="vital-item">
                            <div class="vital-value">96</div>
                            <div class="vital-label">Glicemia</div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Classification Card -->
            <div class="card">
                <div class="card-header">
                    🏷️ Classificação de Risco
                </div>
                <div class="card-body">
                    <div style="display: flex; align-items: center; gap: 12px;">
                        <div style="width: 48px; height: 48px; background: #ffc107; border-radius: 8px; display: flex; align-items: center; justify-content: center; font-size: 1.5rem;">⚠️</div>
                        <div>
                            <div style="font-weight: 600; color: #856404;">AMARELO</div>
                            <div style="font-size: 0.85rem; color: #6c757d;">Urgência - Pouco Urgente</div>
                        </div>
                    </div>
                    <div style="margin-top: 12px; padding-top: 12px; border-top: 1px solid #e9ecef; font-size: 0.85rem; color: #6c757d;">
                        Queixa: Febre e dor no corpo há 2 dias
                    </div>
                </div>
            </div>
        </aside>

        <!-- Main Content - SOAP -->
        <main class="main-content">
            <!-- S - Subjetivo -->
            <section class="soap-section soap-s">
                <div class="soap-header">
                    <div class="soap-letter">S</div>
                    <div>
                        <div class="soap-title">Subjetivo (Anamnese)</div>
                        <div class="soap-subtitle">Queixas e história relatada pelo paciente</div>
                    </div>
                </div>
                <div class="soap-body">
                    <textarea placeholder="Cole aqui a anamnese do MedPres..."></textarea>
                </div>
            </section>

            <!-- O - Objetivo -->
            <section class="soap-section soap-o">
                <div class="soap-header">
                    <div class="soap-letter">O</div>
                    <div>
                        <div class="soap-title">Objetivo (Exame Físico)</div>
                        <div class="soap-subtitle">Achados do exame físico e exames complementares</div>
                    </div>
                </div>
                <div class="soap-body">
                    <textarea placeholder="Cole aqui o exame físico do MedPres..."></textarea>
                </div>
            </section>

            <!-- A - Avaliação -->
            <section class="soap-section soap-a">
                <div class="soap-header">
                    <div class="soap-letter">A</div>
                    <div>
                        <div class="soap-title">Avaliação (Diagnóstico)</div>
                        <div class="soap-subtitle">Hipóteses diagnósticas e CID-10</div>
                    </div>
                </div>
                <div class="soap-body">
                    <textarea placeholder="Cole aqui o diagnóstico / CID-10..."></textarea>
                </div>
            </section>

            <!-- P - Plano -->
            <section class="soap-section soap-p">
                <div class="soap-header">
                    <div class="soap-letter">P</div>
                    <div>
                        <div class="soap-title">Plano (Conduta)</div>
                        <div class="soap-subtitle">Prescrição interna e conduta</div>
                    </div>
                </div>
                <div class="soap-body">
                    <textarea placeholder="Cole aqui a prescrição interna do MedPres..."></textarea>
                </div>
            </section>

            <!-- Receita Domiciliar -->
            <section class="prescription-section">
                <div class="prescription-header">
                    <div class="prescription-icon">📋</div>
                    <div>
                        <div class="prescription-title">Receita Domiciliar</div>
                        <div class="prescription-subtitle">Prescrição para uso em casa - Cole a receita do MedPres aqui</div>
                    </div>
                </div>
                <div class="prescription-body">
                    <textarea placeholder="Cole aqui a receita domiciliar do MedPres..."></textarea>
                    <div class="prescription-hint">
                        💡 <strong>Dica:</strong> No MedPres, clique em "Copiar Prescrição" e cole diretamente neste campo.
                    </div>
                </div>
                <div class="action-buttons">
                    <button class="btn btn-secondary">🖨️ Imprimir Receita</button>
                    <button class="btn btn-success">✅ Salvar Atendimento</button>
                </div>
            </section>

            <!-- Timestamp -->
            <div class="timestamp">
                ⚠️ Este é um ambiente de demonstração com dados fictícios para apresentação do MedPres.<br>
                Nenhum dado real de paciente está sendo utilizado.
            </div>
        </main>
    </div>
</body>
</html>
