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
        .container { max-width: 1100px; margin: 0 auto; background: var(--card); padding: 30px; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); }
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
        .morph-section { background: #eaf2f8; padding: 12px; border-radius: 8px; margin: 15px 0; }
    </style>
</head>
<body>

<div class="container">
    <h1>Guia Interativo de Parasitologia</h1>
    
    <div class="controls" id="buttons"></div>

    <div id="content" class="grid">
        <div class="info-card" id="details">
            <p style="text-align:center; color: #666;">Selecione um agente acima para ver os detalhes do ciclo biológico, morfologia e identificação.</p>
        </div>
    </div>
</div>

<script>
    const dados = [
        { 
            agente: "Leishmania sp.", 
            doenca: "Leishmaniose (Tegumentar e Visceral)", 
            vetor: "Mosquito flebotomíneo (Lutzomyia)", 
            infectante: "Promastigota", 
            evolutivas: "Promastigota / Amastigota", 
            local: "Macrófagos (pele ou vísceras)", 
            ciclo: "Heteroxenico",
            morfologia: "Promastigota: corpo alongado, flagelo livre, núcleo central, cinetoplasto anterior. </br>Amastigota: forma arredondada, sem flagelo externo, núcleo e cinetoplasto visíveis em microscopia.",
            identificacao: "Pesquisa direta de amastigotas em esfregaços de lesão ou aspirado de medula óssea; cultura (promastigotas); PCR; testes sorológicos (IFI, ELISA)."
        },
        { 
            agente: "Trypanosoma cruzi", 
            doenca: "Doença de Chagas", 
            vetor: "Barbeiro (fezes contaminadas)", 
            infectante: "Tripomastigota metacíclico", 
            evolutivas: "Tripomastigota / Amastigota / Epimastigota", 
            local: "Células (coração, músculo liso)", 
            ciclo: "Heteroxenico",
            morfologia: "Tripomastigota: formato de 'C' ou 'S', núcleo central, cinetoplasto posterior, membrana ondulante. </br>Amastigota: esférica, intracelular. Epimastigota: cinetoplasto anterior ao núcleo, encontrada no vetor.",
            identificacao: "Fase aguda: exame direto do sangue (gota espessa, esfregaço). Fase crônica: sorologia (ELISA, HAI, IFI). Xenodiagnóstico ou PCR em casos especiais."
        },
        { 
            agente: "Plasmodium sp.", 
            doenca: "Malária", 
            vetor: "Mosquito Anopheles", 
            infectante: "Esporozoíto", 
            evolutivas: "Esporozoíto / Merozoíto / Trofozoíto / Esquizonte / Gametócito", 
            local: "Fígado e hemácias", 
            ciclo: "Heteroxenico",
            morfologia: "Trofozoíto jovem: anel com citoplasma delgado e núcleo puntiforme. Trofozoíto maduro: citoplasma irregular, pigmento malárico. </br>Esquizonte: múltiplos núcleos (merozoítos). Gametócitos: formas arredondadas ou em foice (P. falciparum).",
            identificacao: "Gota espessa (padrão ouro) e esfregaço sanguíneo corados por Giemsa ou Walker. Testes rápidos (detecção de antígenos HRP2, pLDH). PCR para diferenciação de espécies."
        },
        { 
            agente: "Toxoplasma gondii", 
            doenca: "Toxoplasmose", 
            vetor: "Água, alimentos, carne, congênita", 
            infectante: "Oocisto / Bradizoíto / Taquizoíto", 
            evolutivas: "Oocisto / Esporozoíto / Taquizoíto / Bradizoíto", 
            local: "Tecidos (SNC, músculo, olho)", 
            ciclo: "Heteroxenico",
            morfologia: "Taquizoíto: formato de meia-lua, núcleo central, multiplicação rápida. Bradizoíto: semelhante, porém de multiplicação lenta dentro de cistos teciduais. </br>Oocisto: esférico, contém esporozoítos após esporulação.",
            identificacao: "Sorologia (IgG e IgM) por ELISA, IFI. Pesquisa de taquizoítos em líquor ou tecidos (imunohistoquímica). PCR em líquido amniótico para diagnóstico congênito."
        },
        { 
            agente: "Giardia lamblia", 
            doenca: "Giardíase", 
            vetor: "Água/alimento (fecal-oral)", 
            infectante: "Cisto", 
            evolutivas: "Cisto / Trofozoíto", 
            local: "Intestino delgado", 
            ciclo: "Monoxênico",
            morfologia: "Trofozoíto: formato de pera, simetria bilateral, dois núcleos, quatro pares de flagelos, disco suctorial ventral. </br>Cisto: oval ou elipsoide, parede refringente, dois a quatro núcleos no interior.",
            identificacao: "Exame parasitológico de fezes (método direto ou Faust). Pesquisa de antígenos nas fezes por ELISA. Aspirado duodenal ou biópsia em casos refratários."
        },
        { 
            agente: "Entamoeba histolytica", 
            doenca: "Amebíase", 
            vetor: "Água/alimento (fecal-oral)", 
            infectante: "Cisto", 
            evolutivas: "Cisto / Trofozoíto", 
            local: "Intestino grosso (± fígado)", 
            ciclo: "Monoxênico",
            morfologia: "Trofozoíto: pleomórfico, emite pseudópodes, núcleo com cromatina periférica regular e cariossoma central. Pode conter hemácias fagocitadas (patognomônico). </br>Cisto: esférico, 1 a 4 núcleos, corpos cromatóides em bastonete.",
            identificacao: "Exame de fezes (método de Hoffmann, Faust). Distinção de E. dispar por pesquisa de antígeno (ELISA) ou PCR. Sorologia (ELISA) útil para amebíase extraintestinal. Colonoscopia com biópsia em suspeita de colite amebiana."
        }
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
        const cicloClass = item.ciclo === "Heteroxênico" ? "hetero" : "mono";
        
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
            
            <div class="morph-section">
                <div class="detail-row"><span class="label">🔬 Morfologia</span><span class="value">${item.morfologia}</span></div>
                <div class="detail-row"><span class="label">🩺 Identificação / Diagnóstico</span><span class="value">${item.identificacao}</span></div>
            </div>
            
            <div class="cycle-box">
                <strong>Esquema do Ciclo:</strong><br>
                ${item.vetor} ➔ <em>(${item.infectante})</em> ➔ ${item.local} ➔ Replicação (${item.evolutivas})
            </div>
        `;
    }
</script>
</body>
</html>
