<style>
body {
    font-family: sans-serif;
}
form {
    width: 500px;
}
</style>

<script>
function getRadios(name) {
    var val;
    var radios = document.getElementsByName(name);
    for (var i = 0, length = radios.length; i < length; i++) {
        if (radios[i].checked) {
            val = radios[i].value;
            break;
        }
    }
    return val;
}

function compute(form) {
    var ehp = parseInt(form.ehp.value,10);
    var secstatus = getRadios('security');
    var correction = form.correction.checked;
    var shipsNeeded;
    var volleysNeeded;
	
    switch (getRadios('shiptype')) {
        case 't2cat':
            shipVolley = 1450; //1484 perfect skills
            shipROF = 2; // 1.93 perfect skills
            break;
        case 't1cat':
            shipVolley = 800; //830 perfect skills
            shipROF = 2; // 1.97 perfect skills
            break;
        case 't1talos':
            shipVolley = 5200; //5301 perfect skills
            shipROF = 5; // 4.15 perfect skills
            break;
        case 't2talos':
            shipVolley = 7300; //7479 perfect skills
            shipROF = 5; // 4.15 perfect skills
            break;
    }

    if (correction) {
        ehp = ehp * 1.2;
    }

    shipsNeeded = Math.ceil(ehp/(shipVolley*(Math.ceil(secstatus/shipROF))));
    volleysNeeded = Math.ceil(ehp/(shipsNeeded*shipVolley));
    alert("You will need " + shipsNeeded + " ships doing " + volleysNeeded + " volleys each to destroy the target.");
}
</script>

<form action="#" method="post" class="gankulator" id="gankulator">
<fieldset>
<center><h3><label>How many do I need to gank it?</label></h3></center>
<p>
<label><input type="text" name="ehp" /> EHP against Antimatter/Void</label><br>
<p>
<label><input type="radio" name="security" value="19" checked />0.5</label>
<label><input type="radio" name="security" value="14" />0.6</label>
<label><input type="radio" name="security" value="10" />0.7</label>
<label><input type="radio" name="security" value="7" />0.8</label>
<label><input type="radio" name="security" value="6" />0.9</label>
<label><input type="radio" name="security" value="6" />1.0</label>
<label>System security</label>
<p>
<label><input type="radio" name="shiptype" value="t1cat" checked />t1 catalysts</label>
<label><input type="radio" name="shiptype" value="t2cat"  />t2 catalysts</label>
<label><input type="radio" name="shiptype" value="t1talos" disabled />t1 taloses</label>
<label><input type="radio" name="shiptype" value="t2talos" disabled />t2 taloses</label>
<p>
<label><input type="checkbox" name="correction">Apply the Darwin correction (+20% EHP on target)</label> 
<p>
<button type="button" onclick="compute(this.form)" name="getVal">Gankulate</button>
</fieldset>
</form>

