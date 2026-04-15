<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Estudo de Parasitologia - Ciclos Biológicos</title>
    <style>
        :root {
            --primary: #2c3e50;
            --accent: #3498db;
            --bg: #f4f7f6;
            --card: #ffffff;
            --text: #333;
        }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: var(--bg); color: var(--text); margin: 0; padding: 20px; }
        .container { max-width: 1000px; margin: 0 auto; background: var(--card); padding: 30px; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); }
        h1 { color: var(--primary); text-align: center; border-bottom: 2px solid var(--accent); padding-bottom: 10px; }
        .controls { display: flex; gap: 10px; margin-bottom: 20px; flex-wrap: wrap; justify-content: center; }
        button { padding: 10px 15px; border: none; border-radius: 5px; background: var(--primary); color: white; cursor: pointer; transition: 0.3s; }
        button:hover { background: var(--accent); }
        button.active { background: var(--accent); font-weight: bold; }
        .grid { display: grid; grid-template-columns: 1fr; gap: 20px; margin-top: 20px; }
        .info-card { border-left: 5px solid var(--accent); padding-left: 20px; background: #f9f9f9; padding: 15px; border-radius: 0 8px 8px 0; }
        .detail-row { margin-bottom: 10px; }
        .label { font-weight: bold; color: var(--primary); display: block; font-size: 0.9em; text-transform: uppercase; }
        .value { font-size: 1.1em; }
        .cycle-box { text-align: center; padding: 20px; border: 2px dashed #ccc; border-radius: 10px; margin-top: 20px; background: #fff; }
        .badge { display: inline-block; padding: 4px 8px; border-radius: 4px; font-size: 0.8em; font-weight: bold; color: white; }
        .hetero { background: #e67e22; }
        .mono { background: #27ae60; }
    </style>
</head>
<body>

<div class="container">
    <h1>Guia Interativo de Parasitologia</h1>
    
    <div class="controls" id="buttons">
        </div>

    <div id="content" class="grid">
        <div class="info-card" id="details">
            <p style="text-align:center; color: #666;">Selecione um agente acima para ver os detalhes do ciclo biológico.</p>
        </div>
    </div>
</div>

<script>
    const dados = [
        { agente: "Leishmania sp.", doenca: "Leishmaniose (Tegumentar e Visceral)", vetor: "Mosquito flebotomíneo (Lutzomyia)", infectante: "Promastigota", evolutivas: "Promastigota / Amastigota", local: "Macrófagos (pele ou vísceras)", ciclo: "Heteroxenico" },
        { agente: "Trypanosoma cruzi", doenca: "Doença de Chagas", vetor: "Barbeiro (fezes contaminadas)", infectante: "Tripomastigota metacíclico", evolutivas: "Tripomastigota / Amastigota / Epimastigota", local: "Células (coração, músculo)", ciclo: "Heteroxenico" },
        { agente: "Plasmodium sp.", doenca: "Malária", vetor: "Mosquito Anopheles", infectante: "Esporozoíto", evolutivas: "Esporozoíto / Merozoíto / Trofozoíto / Esquizonte / Gametócito", local: "Fígado e hemácias", ciclo: "Heteroxenico" },
        { agente: "Toxoplasma gondii", doenca: "Toxoplasmose", vetor: "Água, alimentos, carne, congênita", infectante: "Oocisto / Bradizoíto / Taquizoíto", evolutivas: "Oocisto / Esporozoíto / Taquizoíto / Bradizoíto", local: "Tecidos (SNC, músculo, olho)", ciclo: "Heteroxenico" },
        { agente: "Giardia lamblia", doenca: "Giardíase", vetor: "Água/alimento (fecal-oral)", infectante: "Cisto", evolutivas: "Cisto / Trofozoíto", local: "Intestino delgado", ciclo: "Monoxênico" },
        { agente: "Entamoeba histolytica", doenca: "Amebíase", vetor: "Água/alimento (fecal-oral)", infectante: "Cisto", evolutivas: "Cisto / Trofozoíto", local: "Intestino grosso (± fígado)", ciclo: "Monoxênico" }
    ];

    const buttonsDiv = document.getElementById('buttons');
    const detailsDiv = document.getElementById('details');

    dados.forEach((item, index) => {
        const btn = document.createElement('button');
        btn.innerText = item.agente;
        btn.onclick = () => showDetails(index, btn);
        buttonsDiv.appendChild(btn);
    });

    function showDetails(index, btn) {
        document.querySelectorAll('button').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
        
        const item = dados[index];
        const cicloClass = item.ciclo === "Heteroxênico" ? "heter" : "mono";
        
        detailsDiv.innerHTML = `
            <div style="display:flex; justify-content:space-between; align-items:center;">
                <h2>${item.agente}</h2>
                <span class="badge ${cicloClass}">${item.ciclo}</span>
            </div>
            <div class="detail-row"><span class="label">Doença</span><span class="value">${item.doenca}</span></div>
            <div class="detail-row"><span class="label">Vetor / Transmissão</span><span class="value">${item.vetor}</span></div>
            <div class="detail-row"><span class="label">Forma Infectante</span><span class="value">${item.infectante}</span></div>
            <div class="detail-row"><span class="label">Formas Evolutivas</span><span class="value">${item.evolutivas}</span></div>
            <div class="detail-row"><span class="label">Local Principal</span><span class="value">${item.local}</span></div>
            
            <div class="cycle-box">
                <strong>Esquema do Ciclo:</strong><br>
                ${item.vetor} ➔ <em>(${item.infectante})</em> ➔ ${item.local} ➔ Replicação (${item.evolutivas})
            </div>
        `;
    }
</script>
</body>
</html>
