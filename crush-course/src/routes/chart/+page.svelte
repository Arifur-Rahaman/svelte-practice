<script lang="ts">
    import axios from "axios";
    import { onMount } from "svelte";

    interface ICountry {
        name: { common: string };
        cioc: string | null;
        flags: { alt: string; png: string };
        unMember: boolean;
        population: number;
        languages: {};
    }
    let countries: ICountry[] = [];

    const fetchCountries = async () => {
        const res = await axios.get("https://restcountries.com/v3.1/all");
        countries = res.data;
        console.log(countries)
    };

    //Function to format languages as a comma-separated string
    function formatLanguages(languages:any){
        if(languages){
            return Object.values(languages).join(", ");
        }
        return 'Not found'
    }

    onMount(() => {
        fetchCountries();
    });
</script>

<div>
    <table>
        <thead>
            <tr>
                <th>Flag</th>
                <th>Name</th>
                <th>Population</th>
                <th>CIOC</th>
                <th>UN Member Status</th>
                <th>Currencies (Key)</th>
                <th>Languages</th>
            </tr>
        </thead>
        <tbody>
            {#each countries as country}
                <tr>
                    <td><img src="flag-image-url" alt="Flag" /></td>
                    <td>{country.name.common}</td>
                    <td>{country.population}</td>
                    <td>{country.cioc}</td>
                    <td>{country.unMember ? "Yes" : "No"}</td>
                    <td>Currency Key</td>
                    <td>{formatLanguages(country.languages)}</td
                    >
                </tr>
            {/each}
        </tbody>
    </table>
</div>
