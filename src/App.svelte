<script>
    import Password from './Password.svelte';
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

    function removePwd(index) {
        // this is not efficient, since it will go through the array
        // and compare the index, if it is not returning true, it won't be added to the new array.
        passwords = passwords.filter((pwd, idx) => {
            return idx != index;
        });
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

<ul>
    {#each passwords as password, index (password.pwdid)}
        <p># {index + 1}</p>
        <!--
			This is if we want to use component.
				<Password pwd={password.myPwd} />
		-->

        <!-- To pass the index to the function, we use bind. I need to look at the format of this a bit deeper.-->
        <li on:click={removePwd.bind(this, index)}>{password.myPwd}</li>
    {/each}
</ul>
