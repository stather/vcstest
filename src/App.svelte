<script>
	import { beforeUpdate, afterUpdate } from 'svelte';

	export let name;
	let formData;

	// 28814c132852403686cb1a5eb9ab0c22

	async function startTransaction(){
    	var myHeaders = new Headers();
    	myHeaders.append("Content-Type", "application/json; charset=utf-8");
		myHeaders.append("origin", "marketic.co.za")
		myHeaders.append("Ocp-Apim-Subscription-Key", "28814c132852403686cb1a5eb9ab0c22")
	
		var requestOptions = {
			method: 'POST',
			headers: myHeaders,
			redirect: 'follow',
			body: JSON.stringify({
				"VcsTerminalId": "9473",
				"ReferenceNumber": "12346",
				"TransactionAmount": "100",
				"DescriptionOfGoods": "some stuff",
				"SubscriptionStartDate": "2020/10/01",
				"ReturnUrl": "string",
				"CustomerId": "12345",
				"OccurrenceCount": "U",
				"Occurrencefrequency": "M",
				"OccurrenceEmailAddress": "russell.stather@outlook.com"			
			})
		};

		const res = await fetch(`https://hotspotterdev.azure-api.net/vcsapi/Payment/True`, requestOptions);
		formData = await res.text();

	}

	afterUpdate(() => {
		// ...the DOM is now in sync with the data
		let f = document.getElementsByName("subs");
		if (f !== undefined && f.length != 0){
			f[0].submit();
		}
	});
	
</script>

<main>
	<h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
	<button on:click={startTransaction} >Press Me</button>

	{@html formData}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>