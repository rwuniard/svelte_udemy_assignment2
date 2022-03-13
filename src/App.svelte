<script>
    let myPwd = '';
    let warning = '';
    let passwords = [];

    function checkPwd() {
        if (myPwd.length < 5) {
            warning = 'Too Short';
            console.log(warning);
        } else if (myPwd.length > 10) {
            warning = 'Too Long';
            console.log(warning);
        } else {
            warning = 'OK';
        }
    }

    function addPassword() {
        passwords = [...passwords, { pwdid: Math.random(), myPwd }];
    }

    function deletePwd() {
        passwords.slice(1);
    }

    function isButtonEnabled() {
        if (warning === 'OK') {
            return enabled;
        }
        return disabled;
    }
</script>

<h1>Assignment</h1>

<p>Solve these tasks.</p>

<ol>
    <li>Add a password input field and save the user input in a variable.</li>
    <li>Output "Too short" if the password is shorter than 5 characters and "Too long" if it's longer than 10.</li>
    <li>Output the password in a paragraph tag if it's between these boundaries.</li>
    <li>Add a button and let the user add the passwords to an array.</li>
    <li>Output the array values (= passwords) in a unordered list (ul tag).</li>
    <li>Bonus: If a password is clicked, remove it from the list.</li>
</ol>

Password
<input bind:value={myPwd} on:input={checkPwd} type="password" />

<div>
    {#if warning === 'OK'}
        <p>{myPwd}</p>
    {:else}
        <p>{warning}</p>
    {/if}
</div>
<button on:click={addPassword}>Add Password</button>

{#each passwords as password, index (password.pwdid)}
    <div>
        <p># {index + 1}</p>
        <ul>{password.myPwd}</ul>
    </div>
{/each}

<style>
</style>
