<script>
    import ParkCard from './ParkCard.svelte'

    const apiKey = process.env.NPS_API_KEY
    let parks = [];
    let isLoading = false;
    let isError = false;
    let error = '';
    let selection = '';
	const fetchParks = async () => {
        isLoading = true;
        isError - false;
        try {
            const response = await fetch(`https://developer.nps.gov/api/v1/parks?stateCode=${selection}&limit=50&api_key=${apiKey}`);
            let data = await response.json();
            parks = data.data.filter(item => item.designation === 'National Park');
            isLoading = false;
        } catch(error) {
            console.error(error)
            isLoading = false;
            isError = true
            error = 'Sorry, there was an issue loading your results.'
        }
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

<section>
    <select 
        name="state selector" 
        class="state-selector"
        bind:value={selection}
    >
        {#each states as state, index}
            <option value={state.code}>{state.name}</option>
        {/each}
    </select>

    <button on:click={fetchParks} class="fetch-park-btn">Search</button>

    <div class="card-container">
        {#if isLoading} 
            <p>loading...</p>
        {:else if isError}
            <p>{error}</p>
        {:else}
            {#each parks as park, index}
                <ParkCard park={park} />
            {/each}
        {/if}
        </div>
</section>

<style>
    .card-container {
        display: flex;
        flex-flow: row;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
    }

    .state-selector {
        margin: 1.5rem 0rem;
        padding: .5rem;
        font-family: 'Lato', sans-serif;
        font-size: 1.25em;
    }

    .fetch-park-btn {
        padding: .25rem;
        min-width: 100px;
        background-color: crimson;
        color: white;
        border-radius: 3px;
        font-family: 'Lato', sans-serif;
        font-size: 1.25em;
    }

    .fetch-park-btn:hover {
        border: 1px solid crimson;
        background-color: white;
        color: crimson;
    }

</style>




