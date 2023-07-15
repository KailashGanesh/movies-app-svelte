<script lang="ts">
	function handleSubmit(e:Event){
		if (e && e.target){
			e.preventDefault();
			const form = e.target as HTMLFormElement;
			console.log(form.search.value);
		}
	}
</script>

<header>
	<div class="corner">
		<a href="/">
			Movies App
		</a>
	</div>
	<form class="corner" on:submit={handleSubmit}>
		<input type="text" placeholder="Search" name="search" />
		<input type="submit" value="Search" />
	</form>
</header>

<style>
	header {
		display: flex;
		justify-content: space-between;
		width: 100%;
		padding: 0 20px;
	}
	header form{
		display: inline-block;
		padding: 0 40px 0 0;
	}

	.corner {
		width: fit-content; 
	}

	.corner a {
		width: 100%;
		height: 100%;
		font-size: 20px;
		font-weight: 700;
		font-family: lato;
		text-align: center;
	}
</style>
