
<script>
    import { onMount } from "svelte";



onMount(() => {
    document.getElementById("login").addEventListener("submit", function(e){
        e.defaultPrevented();

    })


});

</script>

<html lang="en" >
    <form name="login" id="login">
        <label for="username">Username:</label>
        <input required type="text" name="username" id="username" />

        <label for="password">Password:</label>
        <input required type="password" name="password" id="password" />

        <button type="submit">Login</button>
    </form>
</html>

<style>
    form {
        display: grid;
			width: 60vw;
			max-width: 500px;
			min-width: 300px;
			margin: auto;
    }
</style>
