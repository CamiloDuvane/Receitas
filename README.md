
<html lang="pt-br">

<head><base href="https://camiloduvane.github.io/Receitas/"><style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
}

body {
    padding: 20px;
    background: #f5f5f5;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    background: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.back-button {
    display: inline-block;
    margin-bottom: 20px;
    padding: 8px 16px;
    background: #6c757d;
    color: white;
    text-decoration: none;
    border-radius: 4px;
    transition: background 0.3s ease;
}

.back-button:hover {
    background: #5a6268;
}

.filter-section {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 15px;
    margin-bottom: 20px;
}

.input-group {
    display: flex;
    flex-direction: column;
}

label {
    margin-bottom: 5px;
    color: #666;
}

input, select {
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-size: 14px;
}

button {
    padding: 8px 16px;
    background: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background 0.3s ease;
}

button:hover {
    background: #0056b3;
}

table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
}

th, td {
    padding: 12px;
    text-align: left;
    border-bottom: 1px solid #ddd;
}

th {
    background: #f8f9fa;
    font-weight: bold;
}

tr:hover {
    background: #f5f5f5;
}

.status-pago {
    color: #28a745;
    font-weight: bold;
}

.status-pendente {
    color: #dc3545;
    font-weight: bold;
}

.total-section {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 4px;
    border: 1px solid #ddd;
}

.total-valor {
    font-size: 18px;
    font-weight: bold;
    color: #28a745;
}

@media (max-width: 768px) {
    .filter-section {
        grid-template-columns: 1fr;
    }
    
    table {
        display: block;
        overflow-x: auto;
    }
}
</style></head><body>
<div class="container">
    <a href="https://camiloduvane.github.io/DMTT/" class="back-button">← Voltar</a>
    <h1>Consulta de Receitas</h1>
    <div class="filter-section">
        <div class="input-group">
            <label for="mes">Mês</label>
            <select id="mes">
                <option value="todos">Todos os Meses</option>
                <option value="1">Janeiro</option>
                <option value="2">Fevereiro</option>
                <option value="3">Março</option>
                <option value="4">Abril</option>
                <option value="5">Maio</option>
                <option value="6">Junho</option>
                <option value="7">Julho</option>
                <option value="8">Agosto</option>
                <option value="9">Setembro</option>
                <option value="10">Outubro</option>
                <option value="11">Novembro</option>
                <option value="12">Dezembro</option>
            </select>
        </div>
        <div class="input-group">
            <label for="tipo">Tipo</label>
            <select id="tipo">
                <option value="">Todos os Tipos</option>
                <option value="Camiao">Camiao</option>
                <option value="Multa">Multa</option>
                <option value="Taxe de Mercadoria">Taxe de Mercadoria</option>
                <option value="Taxi de Passageiro">Taxi de Passageiro</option>
                <option value="Transporte Funembre">Transporte Funembre</option>
                <option value="Taxi por Aplicativo">Taxi por Aplicativo</option>
            </select>
        </div>
        <div class="input-group">
            <label for="licenca">Licença</label>
            <input type="text" id="licenca" placeholder="Digite o número da licença" oninput="buscarReceitas()">
        </div>
        <div class="input-group">
            <label>&nbsp;</label>
            <button onclick="buscarReceitas()">Buscar</button>
        </div>
    </div>

    <table>
        <thead>
            <tr>
                <th>Data</th>
                <th>Licença</th>
                <th>Tipo</th>
                <th>Valor</th>
                <th>Status</th>
            </tr>
        </thead>
        <tbody id="receitas-body">
        </tbody>
    </table>

    <div class="total-section">
        <span>Total Pago: </span>
        <span id="total-valor" class="total-valor">0,00 MZN</span>
    </div>
</div>

<script>
function buscarReceitas() {
    const mes = document.getElementById('mes').value;
    const licenca = document.getElementById('licenca').value;
    const tipo = document.getElementById('tipo').value;
    
    const dadosPorMes = {
        1: [
            {data: '2024-01-15', licenca: 'ABC123', tipo: 'Camiao', valor: 150.00, status: 'Pago'},
            {data: '2024-01-10', licenca: 'XYZ789', tipo: 'Multa', valor: 293.47, status: 'Pendente'},
            {data: '2024-01-05', licenca: 'DEF456', tipo: 'Taxe de Mercadoria', valor: 85.90, status: 'Pago'}
        ],
        2: [
            {data: '2024-02-05', licenca: 'MNO345', tipo: 'Taxi por Aplicativo', valor: 180.00, status: 'Pago'},
            {data: '2024-02-12', licenca: 'PQR678', tipo: 'Taxe de Mercadoria', valor: 95.50, status: 'Pago'}
        ],
        3: [
            {data: '2024-03-03', licenca: 'YZA567', tipo: 'Taxi de Passageiro', valor: 680.00, status: 'Pago'},
            {data: '2024-03-08', licenca: 'BCD890', tipo: 'Transporte Funembre', valor: 110.00, status: 'Pago'}
        ],
        4: [
            {data: '2024-04-05', licenca: 'HIJ456', tipo: 'Multa', valor: 890.00, status: 'Pago'},
            {data: '2024-04-15', licenca: 'KLM789', tipo: 'Camiao', valor: 450.00, status: 'Pendente'}
        ],
        5: [
            {data: '2024-05-10', licenca: 'NOP012', tipo: 'Taxi por Aplicativo', valor: 320.00, status: 'Pago'},
            {data: '2024-05-20', licenca: 'QRS345', tipo: 'Transporte Funembre', valor: 550.00, status: 'Pendente'}
        ],
        6: [
            {data: '2024-06-08', licenca: 'TUV678', tipo: 'Taxe de Mercadoria', valor: 270.00, status: 'Pago'},
            {data: '2024-06-25', licenca: 'WXY901', tipo: 'Taxi de Passageiro', valor: 420.00, status: 'Pago'}
        ],
        7: [
            {data: '2024-07-12', licenca: 'ZAB234', tipo: 'Multa', valor: 150.00, status: 'Pendente'},
            {data: '2024-07-30', licenca: 'CDE567', tipo: 'Camiao', valor: 680.00, status: 'Pago'}
        ],
        8: [
            {data: '2024-08-05', licenca: 'FGH890', tipo: 'Taxi por Aplicativo', valor: 230.00, status: 'Pago'},
            {data: '2024-08-18', licenca: 'IJK123', tipo: 'Transporte Funembre', valor: 490.00, status: 'Pago'}
        ],
        9: [
            {data: '2024-09-10', licenca: 'LMN456', tipo: 'Taxe de Mercadoria', valor: 340.00, status: 'Pendente'},
            {data: '2024-09-22', licenca: 'OPQ789', tipo: 'Taxi de Passageiro', valor: 560.00, status: 'Pago'}
        ],
        10: [
            {data: '2024-10-08', licenca: 'RST012', tipo: 'Multa', valor: 420.00, status: 'Pago'},
            {data: '2024-10-25', licenca: 'UVW345', tipo: 'Camiao', valor: 730.00, status: 'Pendente'}
        ],
        11: [
            {data: '2024-11-15', licenca: 'XYZ678', tipo: 'Taxi por Aplicativo', valor: 280.00, status: 'Pago'},
            {data: '2024-11-28', licenca: 'ABC901', tipo: 'Transporte Funembre', valor: 620.00, status: 'Pago'}
        ],
        12: [
            {data: '2024-12-05', licenca: 'DEF234', tipo: 'Taxe de Mercadoria', valor: 390.00, status: 'Pendente'},
            {data: '2024-12-20', licenca: 'GHI567', tipo: 'Taxi de Passageiro', valor: 480.00, status: 'Pago'}
        ]
    };
    
    const tbody = document.getElementById('receitas-body');
    tbody.innerHTML = '';
    
    let receitasFiltradas = [];
    if (mes === 'todos') {
        Object.values(dadosPorMes).forEach(mesReceitas => {
            receitasFiltradas = receitasFiltradas.concat(mesReceitas);
        });
    } else {
        receitasFiltradas = dadosPorMes[mes] || [];
    }
    
    let receitasFinal = receitasFiltradas;
    
    if (licenca) {
        receitasFinal = receitasFinal.filter(r => r.licenca.toLowerCase().includes(licenca.toLowerCase()));
    }
    
    if (tipo) {
        receitasFinal = receitasFinal.filter(r => r.tipo === tipo);
    }
    
    let totalPago = 0;
    
    receitasFinal.forEach(receita => {
        if (receita.status === 'Pago') {
            totalPago += receita.valor;
        }
        
        const tr = document.createElement('tr');
        tr.innerHTML = `
            <td>${formatarData(receita.data)}</td>
            <td>${receita.licenca}</td>
            <td>${receita.tipo}</td>
            <td>${receita.valor.toFixed(2)} MZN</td>
            <td class="status-${receita.status.toLowerCase()}">${receita.status}</td>
        `;
        tbody.appendChild(tr);
    });
    
    document.getElementById('total-valor').textContent = `${totalPago.toFixed(2)} MZN`;
}

function formatarData(data) {
    return new Date(data).toLocaleDateString('pt-BR');
}

// Carregar dados iniciais
document.addEventListener('DOMContentLoaded', function() {
    buscarReceitas();
});
</script>
</body></html>
