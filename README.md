
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Central de Macros Claro Empresas</title>
<style>
{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Segoe UI,sans-serif;
}
body{
background:#eef1f5;
display:flex;
min-height:100vh;
}
.sidebar{
width:280px;
background:white;
padding:20px;
border-right:1px solid #ddd;
overflow-y:auto;
}
.logo{
font-size:22px;
font-weight:bold;
color:#da291c;
margin-bottom:20px;
}
.section-title{
font-size:13px;
font-weight:700;
color:#666;
margin:15px 0 8px;
letter-spacing:.5px;
}
.input{
width:100%;
padding:12px;
border:1px solid #ddd;
border-radius:10px;
margin-bottom:10px;
font-size:14px;
}
.helper{
font-size:12px;
color:#777;
margin-bottom:20px;
}
.category{
display:flex;
justify-content:space-between;
align-items:center;
padding:12px;
border-radius:10px;
cursor:pointer;
margin-bottom:5px;
}
.category:hover{
background:#f4f4f4;
}
.category.active{
background:#da291c;
color:white;
}
.badge{
background:rgba(255,255,255,.25);
padding:2px 8px;
border-radius:20px;
font-size:12px;
}
.main{
flex:1;
padding:24px;
}
.search-bar{
display:flex;
align-items:center;
gap:15px;
margin-bottom:20px;
}
.search-input{
flex:1;
padding:14px;
border:none;
border-radius:12px;
font-size:15px;
box-shadow:0 2px 10px rgba(0,0,0,.10);
}
.counter{
font-size:14px;
color:#666;
}
.cards{
display:grid;
grid-template-columns:repeat(auto-fill,minmax(380px,1fr));
gap:18px;
}
.card{
background:white;
border-radius:16px;
padding:16px;
box-shadow:0 2px 12px rgba(0,0,0,.08);
display:flex;
flex-direction:column;
}
.card-header{
display:flex;
justify-content:space-between;
align-items:center;
margin-bottom:10px;
}
.card-title{
font-size:18px;
font-weight:700;
}
.favorite{
cursor:pointer;
font-size:22px;
color:#bbb;
}
.favorite.active{
color:#ffb400;
}
.card-category{
background:#fdeaea;
color:#da291c;
padding:5px 10px;
font-size:12px;
border-radius:6px;
font-weight:700;
display:inline-block;
margin-bottom:10px;
}
.editable-text{
width:100%;
min-height:180px;
resize:vertical;
border:1px solid #eee;
background:#f8f8f8;
border-radius:10px;
padding:14px;
line-height:1.5;
margin-bottom:15px;
font-size:14px;
font-family:Segoe UI,sans-serif;
}
.editable-text:focus{
outline:none;
border-color:#da291c;
box-shadow:0 0 0 3px rgba(218,41,28,.1);
}
.copy-btn{
background:#da291c;
color:white;
border:none;
padding:12px;
border-radius:10px;
cursor:pointer;
font-weight:600;
}
.copy-btn:hover{
background:#bc2318;
}
.info{
margin-top:10px;
font-size:12px;
color:#777;
}
@media(max-width:900px){
body{
flex-direction:column;
}
.sidebar{
width:100%;
border-right:none;
border-bottom:1px solid #ddd;
}
.cards{
grid-template-columns:1fr;
}
}
</style>
</head>
<body>
<div class="sidebar">
<div class="logo">📋 MACROS</div>
<details open>
<summary style="
font-weight:bold;
font-size:15px;
cursor:pointer;
margin-bottom:15px;
color:#da291c;
">
⚙️ Variáveis
</summary>
<div class="section-title">NOME DO CLIENTE</div>
<input id="cliente" class="input" placeholder="Digite o nome...">
<div class="section-title">NOME DO ATENDENTE</div>
<input id="nome" class="input" placeholder="Digite seu nome...">
<div class="section-title">PROTOCOLO</div>
<input id="protocolo" class="input" placeholder="Digite o protocolo...">
<div class="section-title">DATA BOLETO</div>
<input id="databoleto" class="input" placeholder="Digite a data...">
<div class="section-title">CONTRATO</div>
<input id="contrato" class="input" placeholder="Digite o contrato...">
<div class="section-title">VALOR AVULSO</div>
<input id="valorAvulso" class="input" placeholder="Digite o valor...">
<div class="section-title">VALOR MULTA</div>
<input id="valorMulta" class="input" placeholder="Digite o valor...">
<div class="section-title">DESCONTO GEVENUE (%)</div>
<input id="descontoGevenue" class="input" placeholder="Digite o desconto...">
<div class="section-title">VALOR DESCONTO GEVENUE</div>
<input id="valorDescontoGevenue" class="input" placeholder="Digite o valor...">
<div class="section-title">DESCONTO MOBILE (%)</div>
<input id="descontoMobile" class="input" placeholder="Digite o desconto...">
<div class="section-title">VALOR DESCONTO MOBILE</div>
<input id="valorDescontoMobile" class="input" placeholder="Digite o valor...">
<div class="section-title">VALOR ENTRADA</div>
<input id="valorEntrada" class="input" placeholder="Digite o valor...">
<div class="section-title">VALOR PARCELA</div>
<input id="valorParcela" class="input" placeholder="Digite o valor...">
<div class="helper">
Substitui automaticamente [CLIENTE], [NOME], [PROTOCOLO], [DATA BOLETO], [CONTRATO] e demais variáveis.
</div>
</details>
<div class="section-title">CATEGORIAS</div>
<div id="categorias"></div>
</div>
<div class="main">
<div class="search-bar">
<input
id="busca"
class="search-input"
placeholder="🔍 Buscar macro por palavra-chave...">
<div class="counter">
<span id="contador">0</span> macros encontradas
</div>
</div>
<div class="cards" id="cards"></div>
</div>
<script>
const macros = [
{
categoria:"Atendimento",
titulo:"Saudação",
texto:`Olá! Tudo bem?
Meu nome é [NOME], falo em nome da Claro Empresas.
Estou entrando em contato referente ao seu contrato Claro.
Para sua segurança, vou realizar uma breve confirmação dos dados antes de prosseguirmos, tudo bem?`
},
{
categoria:"Atendimento",
titulo:"Confirmação de Dados",
texto:`Para darmos continuidade, poderia confirmar, por favor:
CNPJ
RAZÃO SOCIAL`
},
{
categoria:"Atendimento",
titulo:"PID Confirmado",
texto:`Obrigado pela confirmação.
Agora consigo consultar sua situação e verificar as melhores possibilidades para regularização.`
},
{
categoria:"Atendimento",
titulo:"Encerramento",
texto:`A Claro agradece e espero que tenhamos conseguido ajudar na regularização da sua conta.
Tenha um ótimo dia!`
},
{
categoria:"Atendimento",
titulo:"Adimplente",
texto:`Olá! Verifiquei no sistema e constatei que os débitos em aberto já foram quitados, e as linhas estão funcionando normalmente. Posso ajudar em mais alguma coisa?
`
},
{
categoria:"Atendimento",
titulo:"Direcionamento à central",
texto:`Este canal é voltado apenas para negociações de débitos então infelizmente não temos esse acesso. Essas configurações só podem ser feitas pelo próprio cliente através do site ou aplicativo Minha Claro ou através da central de atendimento 1052.`
},
{
categoria:"Chamadas",
titulo:"Está Conectado?",
texto:`Está conectado para que possamos dar continuidade?`
},
{
categoria:"Chamadas",
titulo:"Sem Retorno",
texto:`Caso esteja disponível, por gentileza, responda esta mensagem para darmos andamento ao processo.`
},
{
categoria:"Chamadas",
titulo:"Abandono",
texto:`Como não houve retorno às nossas mensagens anteriores, informamos que este atendimento será encerrado no momento.Permanecemos à inteira disposição para qualquer assistência necessária por meio dos nosso canal official de atendimento, através do numero 1052.`
},

{
categoria:"Boletos",
titulo:"Boleto Negociação",
texto:`Segue em anexo o boleto para pagamento da fatura referente ao mês de setembro com a data atualizada para hoje [DATA BOLETO]. O boleto contém código de barras e código PIX. Lembrando apenas que é importante regularizar todos os débitos para evitar suspensões de serviços, juros ou multas. Para tirar qualquer dúvida referente ao seu contrato Claro, você pode entrar em contato através da central 1052.`
},
{
categoria:"Boletos",
titulo:"Boleto Reativação",
texto:`Segue em anexo o boleto para pagamento da fatura referente ao acordo de reativação O boleto contém código PIX que deve ser utilizado para efetuar o pagamento na data de hoje [DATA BOLETO] para que o acordo seja validado. Para tirar qualquer dúvida referente ao seu contrato Claro, você pode entrar em contato através da central 1052.`
},
{
categoria:"Reativação",
titulo:"Reativação com Sucesso",
texto:`Boa tarde [CLIENTE].
o pagamento foi recebido e as linhas foram reativadas com sucesso!
A Claro agradece e espero que tenhamos conseguido ajudar na regularização da sua conta.
Tenha um ótimo dia!`
},
{
categoria:"Reativação",
titulo:"Protocolo",
texto:`Aqui está o Protocolo Único da Solicitação Isenção de Multa - [PROTOCOLO]`
},
{
categoria:"Negociação",
titulo:"Multa Contratual",
texto:`Junto a este valor encontra-se uma multa de R$ [VALOR MULTA] por quebra de contrato. Entretanto como a linha está suspensa, seu contrato está elegível para a oferta de reativação da Claro.
Caso aceite a reativação, iniciaremos um protocolo de insenção da multa.
Para isso, basta aceitar a proposta de reativação e realizar o pagamento de R$ [VALOR AVULSO] na data de hoje via PIX.`
},
{
categoria:"Negociação",
titulo:"Desconto Gevenue",
texto:`Como sua conta está suspensa, seu contrato está elegível para a oferta de reativação. Onde é fornecido um desconto sobre o valor total caso deseje retomar suas linhas móveis.
Com o desconto de [DESCONTO GEVENUE]% o valor atualizado será de R$[VALOR DESCONTO GEVENUE]
Gostaria de fazer a reativação?`
},
{
categoria:"Negociação",
titulo:"Desconto Mobile",
texto:`Verifiquei uma possibilidade de desconto para o senhor:
Podemos aplicar [DESCONTO MOBILE]% de desconto em cima do valor total caso o pagamento seja efetuado hoje em [DATA BOLETO] via PIX.
O valor total atualizado seria de R$[VALOR DESCONTO MOBILE]`
},
{
categoria:"Negociação",
titulo:"Dívida em aberto",
texto:`Verifiquei em sistema e existe um contrato de linha móvel ([CONTRATO]) com débitos pendentes nos valores de R$ [VALOR AVULSO]
[BOLETO AVULSO]`
},
{
categoria:"Negociação",
titulo:"Conta suspensa",
texto:`Verifiquei em sistema e existe um contrato de linha móvel ([CONTRATO]) suspenso com débitos pendentes nos valores de R$ [VALOR AVULSO]
[BOLETO AVULSO]`
},
{
categoria:"Negociação",
titulo:"Parcelamento Mobile",
texto:`Outra opção seria o parcelamento em até 6 vezes sem juros com desconto de [DESCONTO MOBILE]% no valor total.
A parcela de entrada seria de R$[VALOR ENTRADA] seguidas de 5 parcelas de R$[VALOR PARCELA]`
},
{
categoria:"Negociação",
titulo:"Proposta",
texto:`Gostaria de seguir com a proposta de reativação?`
},

{
categoria:"Validação",
titulo:"Validador de Boletos",
texto:`Através do site oficial da Claro Empresas: https://minhaclaroempresas.claro.com.br O senhor pode verificar a integridade de seus boletos. Basta usar o código de barras para se assegurar de que está pagando um boleto legítimo e oficial da Claro Empresas.`
},
{
categoria:"Validação",
titulo:"Recusa-se a confirmar dados",
texto:`Por questões de segurança e em conformidade com a LGPD (Lei Geral de Proteção de Dados), não estamos autorizados a fornecer dados completos de pessoas físicas ou jurídicas.
Se não for possível confirmar ou complementar essa informação, infelizmente não poderemos prosseguir com o atendimento por este canal. Nesse caso, orientamos que entre em contato diretamente com a nossa Central de Atendimento pelo número 1052 para tratar do seu assunto com total segurança.`
},
{
categoria:"Validação",
titulo:"Desconhece a linha",
texto:`Compreendo, sentimos muito pelo inconveniente e orientamos que entre em contato com a central 1052 e informe que existem cobranças vinculadas ao seu CNPJ referentes a um contrato que o senhor desconhece. Dessa forma evitando novas faturas de serem emitidas.`
}
,

];
let categoriaAtual="Todas";
function substituir(texto){
const nome =
document.getElementById("nome").value || "[NOME]";
const cliente =
document.getElementById("cliente").value || "[CLIENTE]";
const protocolo =
document.getElementById("protocolo").value || "[PROTOCOLO]";
const databoleto =
document.getElementById("databoleto").value || "[DATA BOLETO]";
const contrato =
document.getElementById("contrato").value || "[CONTRATO]";
const valorAvulso =
document.getElementById("valorAvulso").value || "[VALOR AVULSO]";
const valorMulta =
document.getElementById("valorMulta").value || "[VALOR MULTA]";
const descontoGevenue =
document.getElementById("descontoGevenue").value || "[DESCONTO GEVENUE]";
const valorDescontoGevenue =
document.getElementById("valorDescontoGevenue").value || "[VALOR DESCONTO GEVENUE]";
const descontoMobile =
document.getElementById("descontoMobile").value || "[DESCONTO MOBILE]";
const valorDescontoMobile =
document.getElementById("valorDescontoMobile").value || "[VALOR DESCONTO MOBILE]";
const valorEntrada =
document.getElementById("valorEntrada").value || "[VALOR ENTRADA]";
const valorParcela =
document.getElementById("valorParcela").value || "[VALOR PARCELA]";
return texto
.replaceAll("[NOME]",nome)
.replaceAll("[CLIENTE]",cliente)
.replaceAll("[PROTOCOLO]",protocolo)
.replaceAll("[DATA BOLETO]",databoleto)
.replaceAll("[CONTRATO]",contrato)
.replaceAll("[VALOR AVULSO]",valorAvulso)
.replaceAll("[VALOR MULTA]",valorMulta)
.replaceAll("[DESCONTO GEVENUE]",descontoGevenue)
.replaceAll("[VALOR DESCONTO GEVENUE]",valorDescontoGevenue)
.replaceAll("[DESCONTO MOBILE]",descontoMobile)
.replaceAll("[VALOR DESCONTO MOBILE]",valorDescontoMobile)
.replaceAll("[VALOR ENTRADA]",valorEntrada)
.replaceAll("[VALOR PARCELA]",valorParcela);
}
``

function montarCategorias(){
const categorias=["Todas",
...new Set(macros.map(m=>m.categoria))

];
document.getElementById("categorias").innerHTML=
categorias.map(cat=>`
<div
class="category ${cat===categoriaAtual?'active':''}"
onclick="mudarCategoria('${cat}')">
<span>${cat}</span>
<span class="badge">
${cat==="Todas"
? macros.length
: macros.filter(m=>m.categoria===cat).length}
</span>
</div>
`).join("");
}
function mudarCategoria(cat){
categoriaAtual=cat;
montarCategorias();
renderizar();
}
function renderizar(){
const busca =
document.getElementById("busca").value.toLowerCase();
let lista = macros.filter(m=>{
const categoriaOk =
categoriaAtual==="Todas" ||
m.categoria===categoriaAtual;
const buscaOk =
m.titulo.toLowerCase().includes(busca) ||
m.texto.toLowerCase().includes(busca);
return categoriaOk && buscaOk;
});
document.getElementById("contador").innerText =
lista.length;
document.getElementById("cards").innerHTML =
lista.map((macro,i)=>`
<div class="card">
<div class="card-header">
<div class="card-title">
#${i+1} ${macro.titulo}
</div>
<div class="favorite"
onclick="toggleFavorito(this)">
☆
</div>
</div>
<div class="card-category">
${macro.categoria}
</div>
<textarea
class="editable-text"
id="texto-${i}"
>${substituir(macro.texto)}</textarea>
<button
class="copy-btn"
onclick="copiarEditado(this,'texto-${i}')">
📋 Copiar Macro
</button>
<div class="info">
Clique para copiar para a área de transferência
</div>
</div>
`).join("");
}
function copiarEditado(botao,id){
const texto =
document.getElementById(id).value;
navigator.clipboard.writeText(texto);
const original = botao.innerHTML;
botao.innerHTML = "✅ Copiado";
setTimeout(()=>{
botao.innerHTML = original;
},1500);
}
function toggleFavorito(el){
if(el.innerHTML==="☆"){
el.innerHTML="★";
el.classList.add("active");
}
else{
el.innerHTML="☆";
el.classList.remove("active");
}
}
document.getElementById("nome")
.addEventListener("input",renderizar);
document.getElementById("cliente")
.addEventListener("input",renderizar);
document.getElementById("protocolo")
.addEventListener("input",renderizar);
document.getElementById("busca")
.addEventListener("input",renderizar);
document.getElementById("databoleto")
.addEventListener("input",renderizar);
document.getElementById("contrato")
.addEventListener("input",renderizar);
document.getElementById("valorAvulso")
.addEventListener("input",renderizar);
document.getElementById("valorMulta")
.addEventListener("input",renderizar);
document.getElementById("descontoGevenue")
.addEventListener("input",renderizar);
document.getElementById("valorDescontoGevenue")
.addEventListener("input",renderizar);
document.getElementById("descontoMobile")
.addEventListener("input",renderizar);
document.getElementById("valorDescontoMobile")
.addEventListener("input",renderizar);
document.getElementById("valorEntrada")
.addEventListener("input",renderizar);
document.getElementById("valorParcela")
.addEventListener("input",renderizar);

montarCategorias();
renderizar();
</script>
</body>
</html>
