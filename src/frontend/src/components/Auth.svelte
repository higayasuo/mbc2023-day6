<script>
  import { AuthClient } from "@dfinity/auth-client";
  import { onMount } from "svelte";
  import { auth, createActor } from "../store/auth";

  /** @type {AuthClient} */
  let client;

  let whoami = $auth.actor.whoami();

  onMount(async () => {
    client = await AuthClient.create();
    if (await client.isAuthenticated()) {
      handleAuth();
    }
  });

  function handleAuth() {
    auth.update(() => ({
      loggedIn: true,
      actor: createActor({
        agentOptions: {
          identity: client.getIdentity(),
        },
      }),
    }));

    whoami = $auth.actor.whoami();
  }

  function login() {
    client.login({
      identityProvider:
        process.env.DFX_NETWORK === "ic"
          ? "https://identity.ic0.app/#authorize"
          : `http://127.0.0.1:4943/?canisterId=${process.env.INTERNET_IDENTITY_CANISTER_ID}#authorize`,
      onSuccess: handleAuth,
    });
  }

  async function logout() {
    await client.logout();
    auth.update(() => ({
      loggedIn: false,
      actor: createActor(),
    }));

    whoami = $auth.actor.whoami();
  }
</script>

<div class="container">
  {#if $auth.loggedIn}
    <div>
      <button class="authButtn" on:click={logout}>Log out</button>
    </div>
  {:else}
    <button class="authButtn" on:click={login}
      >Authenticate in with Internet Identity</button
    >
  {/if}

  <div class="principal-info">
    {#await whoami}
      Querying caller identity...
    {:then principal}
      Your principal ID is
      <code>{principal}</code>

      {#if principal.isAnonymous()}
        (anonymous)
      {/if}
    {/await}
  </div>
</div>

<style>
  .container {
    margin: 64px 0;
  }

  .principal-info {
    margin-top: 32px;
  }

  .authButtn {
    //width: 70px;
    //height: 30px;
    padding: 10px 20px;
    text-align: center;
    position: relative;
    display: inline-block;
    //padding: 0.25em 0.5em;
    text-decoration: none;
    color: #fff;
    background: #fd9535; /*背景色*/
    border-bottom: solid 2px #d27d00; /*少し濃い目の色に*/
    border-radius: 4px; /*角の丸み*/
    box-shadow: inset 0 2px 0 rgba(255, 255, 255, 0.2),
      0 2px 2px rgba(0, 0, 0, 0.19);
    font-weight: bold;
  }
  .authButtn:hover {
    background: #f3aa66;
  }
  .authButtn:active {
    font-size: larger;
  }
</style>
