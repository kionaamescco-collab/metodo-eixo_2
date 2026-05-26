[index (2).html](https://github.com/user-attachments/files/28282131/index.2.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>EIXO — Painel da Leticia | Grupo Fhilippi</title>
<script src="https://cdn.jsdelivr.net/npm/react@18/umd/react.production.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/react-dom@18/umd/react-dom.production.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/papaparse@5.4.1/papaparse.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/recharts@2.12.0/umd/Recharts.js"></script>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet"/>
<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{
  --navy:#1e2d5a;--navy2:#2a3d72;--gold:#c9973a;--gold2:#e6b85a;
  --cream:#faf7f2;--white:#ffffff;
  --green:#1b5e20;--lgreen:#e8f5e9;--green2:#2e7d32;
  --amber:#e65100;--lamber:#fff3e0;
  --red:#b71c1c;--lred:#ffebee;
  --gray:#f5f5f5;--dgray:#64748b;--border:#e2e8f0;
  --shadow:0 4px 24px rgba(30,45,90,0.10);
}
body{font-family:'DM Sans',sans-serif;background:var(--cream);color:var(--navy);min-height:100vh}
h1,h2,h3{font-family:'Playfair Display',serif}

/* HEADER */
.header{background:var(--navy);padding:0 2rem;display:flex;align-items:center;justify-content:space-between;height:72px;position:sticky;top:0;z-index:100;box-shadow:0 2px 20px rgba(0,0,0,0.3)}
.header-brand{display:flex;align-items:center;gap:1rem}
.header-logo{font-family:'Playfair Display',serif;font-size:1.5rem;font-weight:900;color:var(--white);letter-spacing:-0.5px}
.header-logo span{color:var(--gold)}
.header-sub{font-size:0.75rem;color:#8a9cc0;letter-spacing:2px;text-transform:uppercase}
.header-badge{background:var(--gold);color:var(--navy);font-size:0.7rem;font-weight:600;padding:4px 10px;border-radius:20px;letter-spacing:1px}

/* UPLOAD ZONE */
.upload-zone{max-width:680px;margin:5rem auto;padding:0 2rem;text-align:center}
.upload-zone h2{font-size:2.2rem;color:var(--navy);margin-bottom:0.5rem}
.upload-zone p{color:var(--dgray);margin-bottom:2.5rem;font-size:1rem;line-height:1.6}
.upload-box{border:2.5px dashed var(--gold);border-radius:20px;padding:3rem 2rem;background:var(--white);cursor:pointer;transition:all 0.2s;position:relative}
.upload-box:hover{background:var(--lamber);border-color:var(--amber)}
.upload-box input{position:absolute;inset:0;opacity:0;cursor:pointer;width:100%;height:100%}
.upload-icon{font-size:3rem;margin-bottom:1rem}
.upload-box h3{font-family:'DM Sans',sans-serif;font-size:1.1rem;font-weight:600;color:var(--navy);margin-bottom:0.4rem}
.upload-box small{color:var(--dgray);font-size:0.85rem}

/* DASHBOARD */
.dashboard{max-width:1280px;margin:0 auto;padding:2rem}
.dash-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:2rem;flex-wrap:wrap;gap:1rem}
.dash-title{font-size:1.8rem;color:var(--navy)}
.dash-meta{font-size:0.85rem;color:var(--dgray)}
.btn-reset{background:transparent;border:1.5px solid var(--navy);color:var(--navy);padding:8px 18px;border-radius:8px;cursor:pointer;font-size:0.85rem;font-family:'DM Sans',sans-serif;font-weight:500;transition:all 0.2s}
.btn-reset:hover{background:var(--navy);color:var(--white)}

/* CARDS DE RESUMO */
.summary-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:1rem;margin-bottom:2rem}
.summary-card{background:var(--white);border-radius:16px;padding:1.25rem 1.5rem;box-shadow:var(--shadow);border-top:4px solid var(--gold);position:relative;overflow:hidden}
.summary-card::after{content:'';position:absolute;bottom:-20px;right:-20px;width:80px;height:80px;border-radius:50%;opacity:0.07}
.summary-card.blue::after{background:var(--navy)}
.summary-card.green::after{background:var(--green)}
.summary-card.amber::after{background:var(--amber)}
.summary-card.red::after{background:var(--red)}
.summary-card.purple::after{background:#7b1fa2}
.summary-card.teal::after{background:#004d40}
.summary-label{font-size:0.75rem;color:var(--dgray);text-transform:uppercase;letter-spacing:1px;margin-bottom:0.5rem}
.summary-value{font-family:'Playfair Display',serif;font-size:2.2rem;font-weight:700;color:var(--navy);line-height:1}
.summary-sub{font-size:0.75rem;color:var(--dgray);margin-top:0.25rem}
.summary-card.blue{border-top-color:#1565c0}
.summary-card.green{border-top-color:var(--green)}
.summary-card.amber{border-top-color:var(--amber)}
.summary-card.red{border-top-color:var(--red)}
.summary-card.purple{border-top-color:#7b1fa2}
.summary-card.teal{border-top-color:#004d40}

/* SEÇÕES */
.section{background:var(--white);border-radius:20px;padding:1.75rem;margin-bottom:1.5rem;box-shadow:var(--shadow)}
.section-header{display:flex;align-items:center;gap:0.75rem;margin-bottom:1.5rem;padding-bottom:1rem;border-bottom:1.5px solid var(--border)}
.section-icon{font-size:1.4rem}
.section-title{font-family:'Playfair Display',serif;font-size:1.2rem;color:var(--navy)}
.section-count{background:var(--gray);color:var(--dgray);font-size:0.75rem;font-weight:600;padding:3px 10px;border-radius:20px;margin-left:auto}

/* TABELAS */
.table-wrap{overflow-x:auto}
table{width:100%;border-collapse:collapse;font-size:0.875rem}
th{background:var(--navy);color:var(--white);padding:10px 14px;text-align:left;font-weight:500;font-size:0.78rem;text-transform:uppercase;letter-spacing:0.5px;white-space:nowrap}
th:first-child{border-radius:8px 0 0 0}
th:last-child{border-radius:0 8px 0 0}
td{padding:10px 14px;border-bottom:1px solid var(--border);vertical-align:top;color:var(--navy)}
tr:hover td{background:var(--gray)}
tr:last-child td{border-bottom:none}
.td-light{color:var(--dgray);font-size:0.82rem}

/* BADGES */
.badge{display:inline-block;padding:3px 10px;border-radius:20px;font-size:0.75rem;font-weight:600;white-space:nowrap}
.badge-pos{background:#e8f5e9;color:#1b5e20}
.badge-cor{background:#fff3e0;color:#e65100}
.badge-dev{background:#e3f2fd;color:#1565c0}
.badge-alerta{background:#ffebee;color:#b71c1c}
.badge-rec{background:#f3e5f5;color:#6a1b9a}

/* SEMÁFORO */
.semaforo-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:1rem}
.sem-card{border-radius:14px;padding:1.25rem;display:flex;flex-direction:column;gap:0.5rem}
.sem-card.verde{background:var(--lgreen);border-left:5px solid var(--green)}
.sem-card.amarelo{background:var(--lamber);border-left:5px solid var(--amber)}
.sem-card.vermelho{background:var(--lred);border-left:5px solid var(--red)}
.sem-gestor{font-weight:600;font-size:0.95rem}
.sem-setor{font-size:0.8rem;color:var(--dgray)}
.sem-status{font-size:1.5rem;margin-top:0.25rem}
.sem-detail{font-size:0.78rem;color:var(--dgray)}

/* AVALIAÇÃO BARRAS */
.criterio-row{display:flex;align-items:center;gap:1rem;margin-bottom:0.6rem}
.criterio-label{font-size:0.82rem;color:var(--navy);width:160px;flex-shrink:0}
.criterio-bar-wrap{flex:1;background:var(--gray);border-radius:20px;height:8px;overflow:hidden}
.criterio-bar{height:100%;border-radius:20px;transition:width 0.6s}
.criterio-val{font-size:0.82rem;font-weight:600;color:var(--navy);width:28px;text-align:right}

/* CLIMA */
.clima-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:1rem}
.clima-card{border:1.5px solid var(--border);border-radius:14px;padding:1.25rem}
.clima-nota{font-family:'Playfair Display',serif;font-size:2.5rem;font-weight:700;text-align:center;margin:0.5rem 0}
.clima-stars{text-align:center;font-size:1.2rem;margin-bottom:0.75rem}
.clima-sentimento{text-align:center;font-size:0.85rem;padding:4px 12px;border-radius:20px;display:inline-block;width:100%}

/* APOIO RH */
.rh-alert{background:var(--lred);border:1.5px solid #f48fb1;border-radius:12px;padding:1rem 1.25rem;display:flex;align-items:flex-start;gap:0.75rem;margin-bottom:0.75rem}
.rh-alert-icon{font-size:1.2rem;flex-shrink:0}
.rh-alert-body{flex:1}
.rh-alert-title{font-weight:600;font-size:0.9rem;color:var(--red)}
.rh-alert-sub{font-size:0.82rem;color:var(--dgray);margin-top:2px}

/* EMPTY */
.empty{text-align:center;padding:2.5rem;color:var(--dgray)}
.empty-icon{font-size:2.5rem;margin-bottom:0.5rem}

/* RESPONSIVO */
@media(max-width:600px){
  .header{padding:0 1rem}
  .dashboard{padding:1rem}
  .summary-grid{grid-template-columns:repeat(2,1fr)}
  .section{padding:1.25rem}
}

/* ANIMAÇÃO */
@keyframes fadeUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
.section{animation:fadeUp 0.4s ease both}
.section:nth-child(1){animation-delay:0.05s}
.section:nth-child(2){animation-delay:0.10s}
.section:nth-child(3){animation-delay:0.15s}
.section:nth-child(4){animation-delay:0.20s}
.section:nth-child(5){animation-delay:0.25s}
.section:nth-child(6){animation-delay:0.30s}
</style>
</head>
<body>
<div id="root"></div>
<script>
const {useState,useMemo,useCallback}=React;
const {BarChart,Bar,XAxis,YAxis,Tooltip,ResponsiveContainer,Cell,RadarChart,Radar,PolarGrid,PolarAngleAxis}=Recharts;

// ── MAPEAMENTO DE COLUNAS ────────────────────────────────────────────────────
const COL={
  ts:0,empresa:1,gestor:2,setor:3,data:4,modulo:5,
  // Feedback
  fb_nome:6,fb_cargo:7,fb_data:8,fb_tipo:9,fb_situacao:10,
  fb_conversado:11,fb_reacao:12,fb_proximo:13,fb_rh:14,
  // Desempenho
  ds_nome:15,ds_cargo:16,ds_setor:17,ds_gestor:18,ds_periodo:19,
  ds_assiduidade:20,ds_pontualidade:21,ds_relacionamento:22,
  ds_comunicacao:23,ds_qualidade:24,ds_erros:25,ds_proatividade:26,
  ds_aprendizado:27,ds_equipe:28,ds_emocional:29,ds_responsabilidade:30,
  ds_forte:31,ds_fraco:32,
  // Admissão
  adm_nome:33,adm_setor:34,adm_data:35,adm_aprendizado:36,
  adm_integracao:37,adm_interesse:38,adm_organizacao:39,
  adm_erros:40,adm_cultura:41,adm_recomendacao:42,
  // HE
  he_total:43,he_setor:44,he_repetidas:45,
  abs_atestados:46,abs_horas:47,abs_emocional:48,
  // Clima
  clm_mes:49,clm_nota:50,clm_sentimento:51,clm_desafios:52,
  clm_canal:53,clm_descricao:54,clm_encaminhamentos:55,
  enc_apontamento:56,enc_descricao:57
};

const CRITERIOS=[
  {key:'ds_assiduidade',label:'Assiduidade'},
  {key:'ds_pontualidade',label:'Pontualidade'},
  {key:'ds_relacionamento',label:'Relacionamento'},
  {key:'ds_comunicacao',label:'Comunicação'},
  {key:'ds_qualidade',label:'Qualidade'},
  {key:'ds_erros',label:'Erros/Retrabalho'},
  {key:'ds_proatividade',label:'Proatividade'},
  {key:'ds_aprendizado',label:'Aprendizado'},
  {key:'ds_equipe',label:'Trabalho Equipe'},
  {key:'ds_emocional',label:'Int. Emocional'},
  {key:'ds_responsabilidade',label:'Responsabilidade'},
];

const BADGE_MAP={
  'Positivo':'badge-pos','De desenvolvimento':'badge-dev',
  'Corretivo':'badge-cor','Advertencia verbal':'badge-alerta',
  'Reconhecimento Formal':'badge-rec'
};

const CORES_BARRA=['#1e2d5a','#2a3d72','#c9973a','#e6b85a','#1b5e20','#7b1fa2'];

function parseRows(csv){
  const r=Papa.parse(csv,{header:false,skipEmptyLines:true});
  return r.data.slice(1).map(row=>{
    const get=(i)=>(row[i]||'').trim();
    return {
      ts:get(COL.ts),empresa:get(COL.empresa),gestor:get(COL.gestor),
      setor:get(COL.setor),data:get(COL.data),modulo:get(COL.modulo),
      fb_nome:get(COL.fb_nome),fb_cargo:get(COL.fb_cargo),fb_data:get(COL.fb_data),
      fb_tipo:get(COL.fb_tipo),fb_situacao:get(COL.fb_situacao),
      fb_conversado:get(COL.fb_conversado),fb_reacao:get(COL.fb_reacao),
      fb_proximo:get(COL.fb_proximo),fb_rh:get(COL.fb_rh),
      ds_nome:get(COL.ds_nome),ds_cargo:get(COL.ds_cargo),ds_setor:get(COL.ds_setor),
      ds_gestor:get(COL.ds_gestor),ds_periodo:get(COL.ds_periodo),
      ds_assiduidade:parseInt(get(COL.ds_assiduidade))||0,
      ds_pontualidade:parseInt(get(COL.ds_pontualidade))||0,
      ds_relacionamento:parseInt(get(COL.ds_relacionamento))||0,
      ds_comunicacao:parseInt(get(COL.ds_comunicacao))||0,
      ds_qualidade:parseInt(get(COL.ds_qualidade))||0,
      ds_erros:parseInt(get(COL.ds_erros))||0,
      ds_proatividade:parseInt(get(COL.ds_proatividade))||0,
      ds_aprendizado:parseInt(get(COL.ds_aprendizado))||0,
      ds_equipe:parseInt(get(COL.ds_equipe))||0,
      ds_emocional:parseInt(get(COL.ds_emocional))||0,
      ds_responsabilidade:parseInt(get(COL.ds_responsabilidade))||0,
      ds_forte:get(COL.ds_forte),ds_fraco:get(COL.ds_fraco),
      adm_nome:get(COL.adm_nome),adm_setor:get(COL.adm_setor),
      adm_data:get(COL.adm_data),adm_aprendizado:get(COL.adm_aprendizado),
      adm_integracao:get(COL.adm_integracao),adm_interesse:get(COL.adm_interesse),
      adm_organizacao:get(COL.adm_organizacao),adm_erros:get(COL.adm_erros),
      adm_cultura:get(COL.adm_cultura),adm_recomendacao:get(COL.adm_recomendacao),
      he_total:get(COL.he_total),he_setor:get(COL.he_setor),he_repetidas:get(COL.he_repetidas),
      abs_atestados:get(COL.abs_atestados),abs_horas:get(COL.abs_horas),
      abs_emocional:get(COL.abs_emocional),
      clm_mes:get(COL.clm_mes),clm_nota:parseInt(get(COL.clm_nota))||0,
      clm_sentimento:get(COL.clm_sentimento),clm_desafios:get(COL.clm_desafios),
      clm_canal:get(COL.clm_canal),clm_descricao:get(COL.clm_descricao),
      clm_encaminhamentos:get(COL.clm_encaminhamentos),
      enc_apontamento:get(COL.enc_apontamento),enc_descricao:get(COL.enc_descricao),
    };
  });
}

function mediaDS(r){
  const vals=CRITERIOS.map(c=>r[c.key]).filter(v=>v>0);
  if(!vals.length)return 0;
  return vals.reduce((a,b)=>a+b,0)/vals.length;
}

function semaforoGestor(rows){
  const gestores={};
  rows.forEach(r=>{
    const k=r.gestor+'|'+r.setor;
    if(!gestores[k])gestores[k]={gestor:r.gestor,setor:r.setor,feedbacks:0,desempenhos:[],clima:0,rh:0,he:false};
    const g=gestores[k];
    if(r.modulo.includes('Feedback'))g.feedbacks++;
    if(r.modulo.includes('desempenho')&&r.ds_nome){const m=mediaDS(r);if(m>0)g.desempenhos.push(m);}
    if(r.modulo.includes('Clima')&&r.clm_nota)g.clima=r.clm_nota;
    if(r.fb_rh==='Sim')g.rh++;
    if(r.he_total&&parseInt(r.he_total)>10)g.he=true;
  });
  return Object.values(gestores).map(g=>{
    const mediaDesemp=g.desempenhos.length?g.desempenhos.reduce((a,b)=>a+b,0)/g.desempenhos.length:null;
    let score=0;
    if(g.feedbacks===0)score+=2;
    if(mediaDesemp!==null&&mediaDesemp<2.5)score+=2;
    if(g.clima>0&&g.clima<=2)score+=2;
    if(g.rh>0)score+=1;
    if(g.he)score+=1;
    const status=score>=4?'vermelho':score>=2?'amarelo':'verde';
    return {...g,mediaDesemp,status,score};
  });
}

// ── COMPONENTES ───────────────────────────────────────────────────────────────
function SummaryCard({label,value,sub,color}){
  return React.createElement('div',{className:`summary-card ${color}`},
    React.createElement('div',{className:'summary-label'},label),
    React.createElement('div',{className:'summary-value'},value),
    sub&&React.createElement('div',{className:'summary-sub'},sub)
  );
}

function Section({icon,title,count,children}){
  return React.createElement('div',{className:'section'},
    React.createElement('div',{className:'section-header'},
      React.createElement('span',{className:'section-icon'},icon),
      React.createElement('h2',{className:'section-title'},title),
      count!==undefined&&React.createElement('span',{className:'section-count'},count+' registros')
    ),
    children
  );
}

function FeedbackSection({rows}){
  const fbs=rows.filter(r=>r.modulo.includes('Feedback')&&r.fb_nome);
  if(!fbs.length)return React.createElement(Section,{icon:'💬',title:'Feedbacks',count:0},
    React.createElement('div',{className:'empty'},React.createElement('div',{className:'empty-icon'},'💬'),React.createElement('p',null,'Nenhum feedback registrado'))
  );
  return React.createElement(Section,{icon:'💬',title:'Feedbacks',count:fbs.length},
    React.createElement('div',{className:'table-wrap'},
      React.createElement('table',null,
        React.createElement('thead',null,React.createElement('tr',null,
          ['Data','Gestor','Colaborador','Cargo','Tipo','Situação','Reação','Próximo Passo','Apoio RH'].map(h=>React.createElement('th',{key:h},h))
        )),
        React.createElement('tbody',null,fbs.map((r,i)=>
          React.createElement('tr',{key:i},
            React.createElement('td',{className:'td-light'},r.fb_data||r.data),
            React.createElement('td',null,React.createElement('strong',null,r.gestor)),
            React.createElement('td',null,r.fb_nome),
            React.createElement('td',{className:'td-light'},r.fb_cargo),
            React.createElement('td',null,React.createElement('span',{className:`badge ${BADGE_MAP[r.fb_tipo]||'badge-dev'}`},r.fb_tipo||'—')),
            React.createElement('td',null,r.fb_situacao||'—'),
            React.createElement('td',{className:'td-light'},r.fb_reacao||'—'),
            React.createElement('td',{className:'td-light'},r.fb_proximo||'—'),
            React.createElement('td',null,r.fb_rh==='Sim'?React.createElement('span',{className:'badge badge-alerta'},'⚠ Sim'):React.createElement('span',{className:'badge badge-pos'},'Não'))
          )
        ))
      )
    )
  );
}

function DesempenhoSection({rows}){
  const ds=rows.filter(r=>r.modulo.includes('desempenho')&&r.ds_nome);
  if(!ds.length)return React.createElement(Section,{icon:'📊',title:'Avaliações de Desempenho',count:0},
    React.createElement('div',{className:'empty'},React.createElement('div',{className:'empty-icon'},'📊'),React.createElement('p',null,'Nenhuma avaliação registrada'))
  );
  return React.createElement(Section,{icon:'📊',title:'Avaliações de Desempenho',count:ds.length},
    ds.map((r,i)=>{
      const media=mediaDS(r);
      const cor=media>=4?'#1b5e20':media>=3?'#c9973a':'#b71c1c';
      return React.createElement('div',{key:i,style:{marginBottom:'1.5rem',paddingBottom:'1.5rem',borderBottom:i<ds.length-1?'1px solid #e2e8f0':'none'}},
        React.createElement('div',{style:{display:'flex',justifyContent:'space-between',alignItems:'flex-start',marginBottom:'1rem',flexWrap:'wrap',gap:'0.5rem'}},
          React.createElement('div',null,
            React.createElement('h3',{style:{fontSize:'1rem',fontFamily:"'DM Sans',sans-serif",fontWeight:600}},r.ds_nome),
            React.createElement('p',{style:{fontSize:'0.82rem',color:'var(--dgray)'}},r.ds_cargo,' · ',r.ds_setor,' · Gestor: ',r.ds_gestor),
            React.createElement('p',{style:{fontSize:'0.78rem',color:'var(--dgray)'}},r.ds_periodo)
          ),
          React.createElement('div',{style:{textAlign:'right'}},
            React.createElement('div',{style:{fontFamily:"'Playfair Display',serif",fontSize:'2rem',fontWeight:700,color:cor}},media.toFixed(1)),
            React.createElement('div',{style:{fontSize:'0.72rem',color:'var(--dgray)'}},'/5.0 média geral')
          )
        ),
        React.createElement('div',null,
          CRITERIOS.map(c=>{
            const v=r[c.key];
            const pct=(v/5)*100;
            const barColor=v>=4?'#1b5e20':v>=3?'#c9973a':'#b71c1c';
            return React.createElement('div',{key:c.key,className:'criterio-row'},
              React.createElement('span',{className:'criterio-label'},c.label),
              React.createElement('div',{className:'criterio-bar-wrap'},
                React.createElement('div',{className:'criterio-bar',style:{width:pct+'%',background:barColor}})
              ),
              React.createElement('span',{className:'criterio-val'},v||'—')
            );
          })
        ),
        (r.ds_forte||r.ds_fraco)&&React.createElement('div',{style:{display:'grid',gridTemplateColumns:'1fr 1fr',gap:'0.75rem',marginTop:'1rem'}},
          r.ds_forte&&React.createElement('div',{style:{background:'var(--lgreen)',borderRadius:'10px',padding:'0.75rem'}},
            React.createElement('p',{style:{fontSize:'0.72rem',color:'var(--green)',fontWeight:600,marginBottom:'2px'}},'✅ PONTO FORTE'),
            React.createElement('p',{style:{fontSize:'0.85rem',color:'var(--navy)'}},r.ds_forte)
          ),
          r.ds_fraco&&React.createElement('div',{style:{background:'var(--lred)',borderRadius:'10px',padding:'0.75rem'}},
            React.createElement('p',{style:{fontSize:'0.72rem',color:'var(--red)',fontWeight:600,marginBottom:'2px'}},'⚠ PONTO DE ATENÇÃO'),
            React.createElement('p',{style:{fontSize:'0.85rem',color:'var(--navy)'}},r.ds_fraco)
          )
        )
      );
    })
  );
}

function AdmissaoSection({rows}){
  const adm=rows.filter(r=>r.modulo.includes('admiss')&&r.adm_nome);
  if(!adm.length)return React.createElement(Section,{icon:'👶',title:'Acompanhamento de Admissão',count:0},
    React.createElement('div',{className:'empty'},React.createElement('div',{className:'empty-icon'},'👶'),React.createElement('p',null,'Nenhuma admissão registrada'))
  );
  const recBadge={'Efetivar':'badge-pos','Acompanhar com mais atencao':'badge-dev','Risco de nao dar certo':'badge-alerta'};
  return React.createElement(Section,{icon:'👶',title:'Acompanhamento de Admissão',count:adm.length},
    React.createElement('div',{className:'table-wrap'},
      React.createElement('table',null,
        React.createElement('thead',null,React.createElement('tr',null,
          ['Colaborador','Setor','Data Admissão','Aprendizado','Integração','Interesse','Organização','Cultura','Recomendação'].map(h=>React.createElement('th',{key:h},h))
        )),
        React.createElement('tbody',null,adm.map((r,i)=>
          React.createElement('tr',{key:i},
            React.createElement('td',null,React.createElement('strong',null,r.adm_nome)),
            React.createElement('td',{className:'td-light'},r.adm_setor),
            React.createElement('td',{className:'td-light'},r.adm_data),
            React.createElement('td',null,r.adm_aprendizado||'—'),
            React.createElement('td',null,r.adm_integracao||'—'),
            React.createElement('td',null,r.adm_interesse||'—'),
            React.createElement('td',null,r.adm_organizacao||'—'),
            React.createElement('td',null,r.adm_cultura||'—'),
            React.createElement('td',null,React.createElement('span',{className:`badge ${recBadge[r.adm_recomendacao]||'badge-dev'}`},r.adm_recomendacao||'—'))
          )
        ))
      )
    )
  );
}

function HESection({rows}){
  const he=rows.filter(r=>r.modulo.includes('Horas')&&(r.he_total||r.abs_atestados));
  if(!he.length)return React.createElement(Section,{icon:'⏱',title:'Horas Extras e Atestados',count:0},
    React.createElement('div',{className:'empty'},React.createElement('div',{className:'empty-icon'},'⏱'),React.createElement('p',null,'Nenhum dado de HE/atestados registrado'))
  );
  return React.createElement(Section,{icon:'⏱',title:'Horas Extras e Atestados',count:he.length},
    React.createElement('div',{className:'table-wrap'},
      React.createElement('table',null,
        React.createElement('thead',null,React.createElement('tr',null,
          ['Gestor','Setor','Total HE','Setor HE','HE Repetidas?','Atestados','Horas Falta','Emocional NR1'].map(h=>React.createElement('th',{key:h},h))
        )),
        React.createElement('tbody',null,he.map((r,i)=>
          React.createElement('tr',{key:i},
            React.createElement('td',null,React.createElement('strong',null,r.gestor)),
            React.createElement('td',{className:'td-light'},r.setor),
            React.createElement('td',null,r.he_total?React.createElement('span',{style:{fontWeight:600,color:'var(--amber)'}},r.he_total,'h'):'—'),
            React.createElement('td',{className:'td-light'},r.he_setor||'—'),
            React.createElement('td',null,r.he_repetidas==='Sim'?React.createElement('span',{className:'badge badge-alerta'},'⚠ Sim'):r.he_repetidas||'—'),
            React.createElement('td',null,r.abs_atestados||'—'),
            React.createElement('td',null,r.abs_horas||'—'),
            React.createElement('td',null,r.abs_emocional==='Sim'?React.createElement('span',{className:'badge badge-alerta'},'🔴 Sim'):r.abs_emocional||'—')
          )
        ))
      )
    )
  );
}

function ClimaSection({rows}){
  const clm=rows.filter(r=>r.modulo.includes('Clima')&&(r.clm_nota||r.clm_sentimento));
  if(!clm.length)return React.createElement(Section,{icon:'🌡',title:'Clima e Canal de Escuta',count:0},
    React.createElement('div',{className:'empty'},React.createElement('div',{className:'empty-icon'},'🌡'),React.createElement('p',null,'Nenhum registro de clima'))
  );
  const sentColor={'Alegria':'#1b5e20','Tranquilidade':'#1565c0','Ansiedade':'#e65100','Irritação':'#b71c1c','Indiferença':'#64748b'};
  const notaCor=(n)=>n>=4?'#1b5e20':n>=3?'#c9973a':'#b71c1c';
  const stars=(n)=>'★'.repeat(n)+'☆'.repeat(5-n);
  return React.createElement(Section,{icon:'🌡',title:'Clima e Canal de Escuta',count:clm.length},
    React.createElement('div',{className:'clima-grid'},
      clm.map((r,i)=>
        React.createElement('div',{key:i,className:'clima-card'},
          React.createElement('div',{style:{fontWeight:600,fontSize:'0.9rem'}},r.gestor),
          React.createElement('div',{style:{fontSize:'0.78rem',color:'var(--dgray)',marginBottom:'0.5rem'}},r.setor,' · ',r.clm_mes),
          r.clm_nota>0&&React.createElement('div',{className:'clima-nota',style:{color:notaCor(r.clm_nota)}},r.clm_nota,React.createElement('span',{style:{fontSize:'1rem',color:'var(--dgray)'}},'/5')),
          r.clm_nota>0&&React.createElement('div',{className:'clima-stars',style:{color:notaCor(r.clm_nota)}},stars(r.clm_nota)),
          r.clm_sentimento&&React.createElement('div',{className:'clima-sentimento',style:{background:sentColor[r.clm_sentimento]+'22',color:sentColor[r.clm_sentimento]||'var(--navy)'}},r.clm_sentimento),
          r.clm_desafios&&React.createElement('p',{style:{fontSize:'0.8rem',color:'var(--dgray)',marginTop:'0.75rem',lineHeight:1.5}},r.clm_desafios),
          r.clm_canal==='Sim'&&React.createElement('div',{style:{marginTop:'0.75rem',background:'var(--lred)',borderRadius:'8px',padding:'0.5rem 0.75rem',fontSize:'0.8rem',color:'var(--red)',fontWeight:600}},'⚠ Denúncias no Canal',r.clm_encaminhamentos&&React.createElement('p',{style:{fontWeight:400,color:'var(--navy)',marginTop:2}},r.clm_encaminhamentos))
        )
      )
    )
  );
}

function SemaforoSection({rows}){
  const gestores=semaforoGestor(rows);
  const emojis={verde:'🟢',amarelo:'🟡',vermelho:'🔴'};
  const labels={verde:'Sem alertas',amarelo:'Atenção',vermelho:'Ação necessária'};
  return React.createElement(Section,{icon:'🚦',title:'Semáforo por Gestor'},
    React.createElement('div',{className:'semaforo-grid'},
      gestores.map((g,i)=>
        React.createElement('div',{key:i,className:`sem-card ${g.status}`},
          React.createElement('div',{className:'sem-status'},emojis[g.status]),
          React.createElement('div',{className:'sem-gestor'},g.gestor),
          React.createElement('div',{className:'sem-setor'},g.setor),
          React.createElement('div',{className:'sem-detail'},labels[g.status]),
          React.createElement('div',{className:'sem-detail',style:{marginTop:'0.25rem'}},
            '💬 ',g.feedbacks,' feedbacks',
            g.mediaDesemp&&(' · 📊 média '+g.mediaDesemp.toFixed(1)),
            g.clm_nota&&(' · 🌡 clima '+g.clima+'/5')
          )
        )
      )
    )
  );
}

function AlertasRH({rows}){
  const alertas=rows.filter(r=>r.fb_rh==='Sim'||r.abs_emocional==='Sim');
  if(!alertas.length)return null;
  return React.createElement(Section,{icon:'🔴',title:'Alertas para o RH — Apoio Solicitado'},
    alertas.map((r,i)=>
      React.createElement('div',{key:i,className:'rh-alert'},
        React.createElement('div',{className:'rh-alert-icon'},'⚠️'),
        React.createElement('div',{className:'rh-alert-body'},
          React.createElement('div',{className:'rh-alert-title'},r.gestor,' — ',r.setor),
          React.createElement('div',{className:'rh-alert-sub'},
            r.fb_rh==='Sim'&&('Feedback requer apoio do RH: '+(r.fb_situacao||r.fb_nome||'')),
            r.abs_emocional==='Sim'&&'Afastamento por motivo emocional/NR1 registrado'
          )
        )
      )
    )
  );
}

// ── APP PRINCIPAL ─────────────────────────────────────────────────────────────
function App(){
  const [rows,setRows]=useState(null);
  const [fileName,setFileName]=useState('');

  const handleFile=useCallback((e)=>{
    const file=e.target.files[0];
    if(!file)return;
    setFileName(file.name);
    const reader=new FileReader();
    reader.onload=(ev)=>{
      const parsed=parseRows(ev.target.result);
      setRows(parsed);
    };
    reader.readAsText(file,'UTF-8');
  },[]);

  const total=rows?rows.length:0;
  const nFeedbacks=rows?rows.filter(r=>r.modulo.includes('Feedback')&&r.fb_nome).length:0;
  const nDS=rows?rows.filter(r=>r.modulo.includes('desempenho')&&r.ds_nome).length:0;
  const nAdm=rows?rows.filter(r=>r.modulo.includes('admiss')&&r.adm_nome).length:0;
  const nHE=rows?rows.filter(r=>r.modulo.includes('Horas')&&(r.he_total||r.abs_atestados)).length:0;
  const nClima=rows?rows.filter(r=>r.modulo.includes('Clima')&&(r.clm_nota||r.clm_sentimento)).length:0;
  const nAlertas=rows?rows.filter(r=>r.fb_rh==='Sim'||r.abs_emocional==='Sim').length:0;

  return React.createElement('div',null,
    // HEADER
    React.createElement('header',{className:'header'},
      React.createElement('div',{className:'header-brand'},
        React.createElement('div',null,
          React.createElement('div',{className:'header-logo'},React.createElement('span',null,'EIXO'),' · Diário do Gestor'),
          React.createElement('div',{className:'header-sub'},'Grupo Fhilippi · Método Eixo')
        )
      ),
      React.createElement('div',{className:'header-badge'},'PAINEL DA LETICIA')
    ),

    // UPLOAD ou DASHBOARD
    !rows?
      React.createElement('div',{className:'upload-zone'},
        React.createElement('h2',null,'Painel de Gestão de Pessoas'),
        React.createElement('p',null,'Faça upload do CSV exportado do Google Forms para visualizar todos os registros do mês — feedbacks, desempenho, admissões, HE e clima.'),
        React.createElement('div',{className:'upload-box'},
          React.createElement('input',{type:'file',accept:'.csv',onChange:handleFile}),
          React.createElement('div',{className:'upload-icon'},'📂'),
          React.createElement('h3',null,'Clique ou arraste o arquivo CSV aqui'),
          React.createElement('small',null,'Exporte do Google Forms → Respostas → Baixar CSV')
        )
      )
    :
      React.createElement('div',{className:'dashboard'},
        // Cabeçalho dashboard
        React.createElement('div',{className:'dash-header'},
          React.createElement('div',null,
            React.createElement('h1',{className:'dash-title'},'Painel do Mês'),
            React.createElement('p',{className:'dash-meta'},fileName,' · ',total,' registros processados')
          ),
          React.createElement('button',{className:'btn-reset',onClick:()=>{setRows(null);setFileName('')}},'↩ Carregar novo CSV')
        ),

        // Cards resumo
        React.createElement('div',{className:'summary-grid'},
          React.createElement(SummaryCard,{label:'Total de Registros',value:total,sub:'todos os módulos',color:'blue'}),
          React.createElement(SummaryCard,{label:'Feedbacks',value:nFeedbacks,sub:'registrados no período',color:'purple'}),
          React.createElement(SummaryCard,{label:'Avaliações',value:nDS,sub:'de desempenho',color:'teal'}),
          React.createElement(SummaryCard,{label:'Admissões',value:nAdm,sub:'em acompanhamento',color:'amber'}),
          React.createElement(SummaryCard,{label:'HE + Atestados',value:nHE,sub:'fechamentos do mês',color:'green'}),
          React.createElement(SummaryCard,{label:'Alertas RH',value:nAlertas,sub:'apoio solicitado',color:'red'}),
        ),

        // Alertas RH primeiro (prioridade)
        React.createElement(AlertasRH,{rows}),

        // Semáforo
        React.createElement(SemaforoSection,{rows}),

        // Módulos
        React.createElement(FeedbackSection,{rows}),
        React.createElement(DesempenhoSection,{rows}),
        React.createElement(AdmissaoSection,{rows}),
        React.createElement(HESection,{rows}),
        React.createElement(ClimaSection,{rows}),

        // Rodapé
        React.createElement('div',{style:{textAlign:'center',padding:'2rem',color:'var(--dgray)',fontSize:'0.8rem',borderTop:'1px solid var(--border)',marginTop:'1rem'}},
          'MÉTODO EIXO · Kiona Ames · CRP 04895/12 · kionaamescco@gmail.com'
        )
      )
  );
}

ReactDOM.createRoot(document.getElementById('root')).render(React.createElement(App));
</script>
</body>
</html>
