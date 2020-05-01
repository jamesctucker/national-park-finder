
<script>
    const apiKey = process.env.NPS_API_KEY
    let parks = [];
    let selection = '';
	const fetchParks = async () => {
        const response = await fetch(`https://developer.nps.gov/api/v1/parks?stateCode=${selection}&limit=50&api_key=${apiKey}`);
        let data = await response.json();

        parks = data.data.filter(item => item.designation === 'National Park')
    }
    
    const states = [
        {name: 'Alabama', code: 'AL'},
        {name: 'Alaska', code: 'AK'},
        {name: 'Arizona', code: 'AZ'},
        {name: 'Arkansas', code: 'AR'},
        {name: 'California', code: 'CA'},
        {name: 'Colorado', code: 'CO'},
        {name: 'Delaware', code: 'DE'},
        {name: 'Florida', code: 'FL'},
        {name: 'Hawaii', code: 'HI'},
        {name: 'Idaho', code: 'ID'},
        {name: 'Illinois', code: 'IL'},
        {name: 'Iowa', code: 'IA'},
        {name: 'Kansas', code: 'KS'},
        {name: 'Kentucky', code: 'KY'},
        {name: 'Louisiana', code: 'LA'},
        {name: 'Maine', code: 'ME'},
        {name: 'Maryland', code: 'MD'},
        {name: 'Massachusetts', code: 'MA'},
        {name: 'Michigan', code: 'MI'},
        {name: 'Minnesota', code: 'MN'},
        {name: 'Mississippi', code: 'MS'},
        {name: 'Missouri', code: 'MO'},
        {name: 'Montana', code: 'MT'},
        {name: 'Nebraska', code: 'NE'},
        {name: 'Nevada', code: 'NV'},
        {name: 'New Hampshire', code: 'NH'},
        {name: 'New Jersey', code: 'NJ'},
        {name: 'New Mexico', code: 'NM'},
        {name: 'New York', code: 'NY'},
        {name: 'North Carolina', code: 'NC'},
        {name: 'North Dakota', code: 'ND'},
        {name: 'Ohio', code: 'OH'},
        {name: 'Oklahoma', code: 'OK'},
        {name: 'Oregon', code: 'OR'},
        {name: 'Pennsylvania', code: 'PA'},
        {name: 'Rhode Island', code: 'RI'},
        {name: 'South Carolina', code: 'SC'},
        {name: 'South Dakota', code: 'SD'},
        {name: 'Tennessee', code: 'TN'},
        {name: 'Texas', code: 'TX'},
        {name: 'Utah', code: 'UT'},
        {name: 'Vermont', code: 'VT'},
        {name: 'Virginia', code: 'VA'},
        {name: 'Washington', code: 'WA'},
        {name: 'West Virginia', code: 'WV'},
        {name: 'Wisconsin', code: 'WI'},
        {name: 'Wyoming', code: 'WY'},
    ]
</script>

{#if parks}
	{#each parks as park, index}
        <p>{park.fullName}</p>
    {/each}
{/if}

<select 
    name="state selector" 
    id="state-selector"
    bind:value={selection}
>
    {#each states as state, index}
        <option value={state.code}>{state.name}</option>
    {/each}
</select>

<button on:click={fetchParks}>Get Parks</button>


