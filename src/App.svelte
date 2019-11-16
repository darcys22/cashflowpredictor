<script>

  let transactions = [];

	const tomorrow = new Date(Date.now() + 86400000);

	let dte = [
		tomorrow.getFullYear(),
		pad(tomorrow.getMonth() + 1, 2),
		pad(tomorrow.getDate(), 2)
	].join('-');

	let amount = 100;
	let type = 'weekly';

	$: strdate = convertToDate(dte);

  function addTransaction() {
    transactions = [...transactions, {date:strdate.toDateString(), amount:amount, type:type}];

		console.log(transactions.length);
	}

	function convertToDate(str) {
		const split = str.split('-');
		return new Date(+split[0], +split[1] - 1, +split[2]);
	}

	function pad(x, len) {
		x = String(x);
		while (x.length < len) x = `0${x}`;
		return x;
	}
</script>

<style>
	select, input, button {
		display: block;
		margin: 0.5em 0;
		font-size: inherit;
	}
</style>

<select bind:value={type}>
		<option value={"daily"}>Daily</option>
		<option value={"weekly"}>Weekly</option>
		<option value={"monthly"}>Monthly</option>
		<option value={"annually"}>Annually</option>
</select>

<input type=date bind:value={dte}>
<input type=number bind:value={amount}>

<button
	on:click={addTransaction}
>Add</button>
