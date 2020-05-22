<style>
form {
    width: 400px;
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
	var shipsNeeded;
	var volleysNeeded;
	
	shipVolley = 1484; //t2 null hot
	shipROF = 2; //gun cycle time
	shipsNeeded = Math.ceil(ehp/(shipVolley*(Math.ceil(secstatus/shipROF))));
	volleysNeeded = Math.ceil(ehp/(shipsNeeded*shipVolley));
	alert("You will need " + shipsNeeded + " t2 catalysts doing " + volleysNeeded + " volleys to destroy the target");
}
</script>

<form action="#" method="post" class="gankulator" id="gankulator">
<fieldset>
<label>How many t2 cats do I need to gank it?</label>
<p>
<label><input type="text" name="ehp" /> EHP against Void</label><br>
<label><input type="radio" name="security" value="19" checked />0.5</label>
<label><input type="radio" name="security" value="14" />0.6</label>
<label><input type="radio" name="security" value="10" />0.7</label>
<label><input type="radio" name="security" value="7" />0.8</label>
<label><input type="radio" name="security" value="6" />0.9</label>
<label><input type="radio" name="security" value="6" />1.0</label>
<label>Sec status</label>
</p>
<p><button type="button" onclick="compute(this.form)" name="getVal">Gankulate</button></p>
</fieldset>
</form>

