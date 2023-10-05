<form id="calculator_form">
Monday:  <br>

{% for item in calc_data.mk.monday.keys() %}
    {{ item }} : <input type="number" name="{{ item }}" />
    <input type="hidden" name="{{ item }}_data" value="{{ calc_data.mk.monday[item] }}" /> <br>
{% endfor %}
<div id="total_points">&nbsp;</div>
<input type="submit" />
</form>


<script>
class MKCalc {
    constructor() {
        // grab reference to form

        const formElem = document.querySelector("#calculator_form");

        // submit handler

        formElem.addEventListener("submit", (e) => {
        // on form submission, prevent default
            e.preventDefault();
             const formData = new FormData(formElem);
        });
        // formdata handler to retrieve data

        formElem.addEventListener("formdata", (e) => {
            const formData = e.formData;

            var total = (
                (formData.get("T1 Tome") * formData.get("T1 Tome_data"))
                + (formData.get("T2 Tome") * formData.get("T2 Tome_data"))
                + (formData.get("T3 Tome") * formData.get("T3 Tome_data"))
                + (formData.get("T4 Tome") * formData.get("T4 Tome_data"))
                + (formData.get("Master Talent") * formData.get("Master Talent_data"))
                + (formData.get("Crown of Oracle") * formData.get("Crown of Oracle_data"))
                + (formData.get("Gallery Shard") * formData.get("Gallery Shard_data"))
            );

            document.getElementById('total_points').innerHTML = total;

            for (const [key, value] of e.formData) {
                console.log(`${key} : ${value}`);
            }
        });

    }
}


const test = new MKCalc();

</script>